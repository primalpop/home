---
layout: post
title: "AWS RDS:  'MySQL server has gone away error' starring Flask-SQLAlchemy and MYSQLdb"
category: devops
share: y
disqus: y
---

After a week long week of coding/testing we(myself and [Ani](https://twitter.com/aniv)) finally deployed the website on a Friday evening. Fast-forward a relaxing 
weekend and website has acting weird on Monday morning. Looking at the logs it said something which sounded very 
philosophical at first.

> OperationalError: (2006, 'MySQL server has gone away')

I carefully copied the error and start googling to see what the usual suspects are. I quickly see that this is one of the
expected issues and [MySQL had a full page documentation on it](http://dev.mysql.com/doc/refman/5.0/en/gone-away.html).
Here's the briefing of what was happening.

> By default, the server closes the connection after eight hours if nothing has happened. You can change the time 
> limit by setting the wait_timeout variable.

Now we were using Flask-SQLAlchemy and MYSQLdb for making connections to the database. So I started reading into the
configuration keys for Flask-SQLAlchemy and [found out](http://stackoverflow.com/a/6473271/323404) that by setting *SQLALCHEMY_POOL_RECYCLE* to a lower value than default(8 hours) I could force it to recycle connections by default. 

With MySQLdb, the solution wasn't as easy as that. I could use the [mysql_ping function](http://oxygene.sk/2009/11/mysql-server-has-gone-away/) for checking if database connection was alive before making a query. But this could result in lot of extra
overhead for the database. This [SO answer and related blog post](http://stackoverflow.com/a/3104681/323404) tells that *upto 73% of the load on that instance of MySQL was caused by applications checking if the DB was up*. 

Then I came across [this question](http://stackoverflow.com/questions/567622/is-there-a-pythonic-way-to-try-something-up-to-a-maximum-number-of-times) in SO and the answer was the perfect candidate for what I was looking for. By encapsulating the code
in a try-catch statement and pinging the server only when exception was raised, there was no 
unnecessary overload on the server. Also by trying 3 times before giving up, the exceptions related to the initial server latency
can be avoided.

### Bonus Points: Testing it on the RDS instance

At [Picwell](http://picwell.com/) we love AWS and for databases we use Amazon RDS for MySQL. Waiting 8 hours after making
changes to the code, to see if the error has been resolved was not a practical solution. So I decided to set the wait_timeout
variable to something lower than it's default value of 28800 seconds(8 hours). But I couldn't change in globally on RDS
as it was throwing the crazy *Access privileges* error.

The next day, [Ani](https://twitter.com/aniv) shared this article on [RDS DB Parameter Group](http://aws.amazon.com/articles/2935_)  deployment from AWS articles. From there I learned about the awesome [Amazon RDS Command Line Toolkit](http://aws.amazon.com/developertools/2928) which is something everyone should use for managing RDS instances. The [document on
installation](http://docs.aws.amazon.com/AmazonRDS/latest/CommandLineReference/StartCLI.html) was very elaborate so I wouldn't focus on that. 

Later on after following steps from original article, I created a temporary database for testing purposes which is a copy of
the original database. I used the following command to change the 'wait_timeout' variable 

{% highlight bash %}
rds-modify-db-parameter-group twin-test --parameters="name=wait_timeout, value=300, method=immediate"
{% endhighlight %}

I logged into the db instance to verify if the changes have been made correctly but surprisingly was greeted by the 
default parameters. 

{% highlight sql %}
mysql> show variables like "%wait_timeout";
+--------------------------+----------+
| Variable_name            | Value    |
+--------------------------+----------+
| innodb_lock_wait_timeout | 50       |
| lock_wait_timeout        | 31536000 |
| wait_timeout             | 28800    |
+--------------------------+----------+
3 rows in set (0.02 sec)

{% endhighlight %}

After a short break of screaming at my laptop screen, I started seeing if anyone else on the Internet faced the same problem. Of course,
there is always [someone](https://forums.aws.amazon.com/message.jspa?messageID=248879)(at least in database related things). One of the answers had the explaination of what was happening. 

>The wait time_timeout parameter only applies to non-interactive sessions, such as would normally be established 
> when accessing your RDS instances via code. When using the mysql command line client, an interactive session 
> is established, and so the parameter interactive_timeout is applied.

So I decided to check the global variables this time through mysql client.

{% highlight sql %}
mysql> show global variables like "%wait_timeout%";
+--------------------------+----------+
| Variable_name            | Value    |
+--------------------------+----------+
| innodb_lock_wait_timeout | 50       |
| lock_wait_timeout        | 31536000 |
| wait_timeout             | 300      |
+--------------------------+----------+
3 rows in set (0.02 sec)
{% endhighlight %}

Voila, there it was. 'wait_timeout' variable was set to 300 seconds. 

I wasted a lot of time while trying to debug this error and getting all the details.  I hope this post will save some dev
hours while trying to debug this error but I am sure I haven't covered all the possible issues w.r.t this specific error. 
Let me know in comments if you had resolved this problem differently or any related problems you had faced. 

