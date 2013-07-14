---
layout: post
title: "Summer of 11: Story of my Google Summer of Code application"
category: projects
share: y
disqus: y
---

It is that time of the year
[again](http://google-opensource.blogspot.in/2012/02/google-summer-of-code-2012-is-on.html), when students all around the world are given an unique opportunity by Google to contribute to an Open Source Project over
the summer. Initially I thought of writing a **How to apply for Google Summer
of Code(GSoC)** guide at this time
but Internet has too
[many](http://www.sarathlakshman.com/2011/03/28/how-to-apply-for-google-summer-of-code-a-byte-of-note/)
of [them](http://www.vaidikkapoor.info/2011/12/gsoc-2012/) already. Hence I settled upon writing this story of
my GSoC application during 2011 hoping to share my memorable experience.

###Genesis

Doing Google Summer of code had been 
a long cherished dream from when I first knew about it in undergraduate studies. But when the 
program was announced in early February of 2011, I was in my usual
**busy-doing-nothing** mode to notice it. Time flew by, it was mid march and I
was in a very bad and desperate mood owing to end of college days nearing(final year student at that time)
when the list of selected organizations for GSoC 2011 came out. Realizing that
it was my last chance at glory, I made up my mind to apply to at least one
project even though time was not on my side.

The most painful process of finding out a suitable project, ensued. After days of reading through [organization
and project
pages](http://www.google-melange.com/gsoc/accepted_orgs/google/gsoc2011), I filtered out some projects based on the intersection of
skills on my resume and requirements of the project. Having done a [decent mini
project](http://primalpop.wordpress.com/2010/09/21/cygnus-microblogging-platform-for-android/) in Android in the previous year, I looked out for projects which
sported that keyword in particular. 

###Exodus

Hanging around in the [IRC](http://en.wikipedia.org/wiki/Internet_Relay_Chat) channels of the chosen organizations was my next
logical move. Even though, I hardly said anything in these channels during this
time, it helped me to figure out the already set pool of applicants and evaluate my chances of making the
cut for that project. Owing to extreme delay(march-end) in my start of proceedings, some of the
projects already had a large number of prospective applicants. After few days
of reading, I settled upon [Indoor Geocaching game project by Komodo Open
Lab](http://wiki.komodoopenlab.com/index.php/Main/GSoC2011#toc6)
for applying.  

After being the silent observer in various IRC channels previously, I decided to get into action
straightaway in the IRC channel for this project. Blurting out the details of
my interest in the project, I waited for a response. After a few minutes of
silence, [Jorge Silva](http://www.youtube.com/watch?v=Czn0Cn3OmPo&lr=1)(my future mentor) asked whether we could talk over skype the details of
project. For someone who was expecting only a minimal text response, this was a 
jackpot. He talked to me in length about the project idea and encouraged me to
apply asap.


###Chronicles

Until that moment, GSoC was feeling like a distant dream but now I was in
with a chance. This motivated me to go on full throttle. After working for a
continous stretch of 9 hours I was up with what can be called a beta version of the
project proposal and mailed to Jorge. This happened before the real application
process began in April and gave me some much needed leverage.

Having almost completed the application left me with nothing to do until April
end when results would be announced. I started brainstorming for further ideas to be
implemented on the application and documenting them in the
[Wiki](http://wiki.mobile-accessibility.idrc.ocad.ca/w/User_talk:Primalpop). I took it up
as a challenge to have something new to show on the wiki on at least every alternate
day. Nights were spent in IRC discussing the brainwaves I had earlier
in the day(if any). Being the wonderful guy he is, Jorge
always listened to my ideas patiently and pointed out the flaws and fine points
in them. Over this period the abstract ideas were refined out and this also aided
in improving my application. When I was without ideas, I asked plainly what
could I do for the project.

###Judgement

I submitted my [final
application](http://www.google-melange.com/gsoc/proposal/review/google/gsoc2011/primalpop/1) one week before the deadline and was pretty
satisfied about it. Just after the deadline, upon my inquiry Jorge told in IRC
that there were 3 slots and 17 applicants for them that year. This
was a wake up call for me and I realized a good application can take me only so
far. I needed something to distuinguish myself from others. The solution was
staring down at me from the alpha version of the application source code Jorge
had pushed to Launchpad earlier in the day.

Next weekend was spent in reading the source code and understanding how the
application worked. Not having a phone handicapped me from testing the
app and [Mr. Pramode C E](http://pramode.net), my FOSS guru, was kind enough to lent me his phone for
the purpose. But testing involved a lot of repetitive work which could be
automated and I sat down to code a [Logger for the
app](https://code.launchpad.net/~primal007/tagin/tagin-inplace) which would esentially
run the app in an infinite loop and store the various readings in CSV format. 
Few days before the results were announced I pushed the code into a seperate
branch of launchpad and thus I had that something powerful and substantial to aid my application.

The day of results arrived and by this time I had fallen in love with the project
and had made up my mind to contribute irrespective of whether I was selected for
GSoC or not.  As I had no idea of how the results would be announced, I was
lingering around in IRC channels chatting to other applicants who had already become my
friends over the one month period. At 12 in midnight, Carol posted in gsoc irc channel
that results had been sent out to applicants. I waited nervously with seconds 
feeling like hours. Finally at 12.30 I received a mail in my inbox which read like this

>Dear Primal,
>
>Congratulations! Your proposal "Indoor Geocaching game" as submitted to Komodo
> OpenLab Inc. has been accepted for Google Summer of Code 2011. 
>

I went numb with happyness. The month long ordeal had paid its
dividends in full. Thus began the open source adventure and wonderful summer of
coding, which taught me so many things that it wouldnt be an exaggeration if I said it was life
changing because it really was. :-)

###Epilogue

The completion of Google Summer of Code convinced me that higher education
was the way to go and only research would satiate my urge to know more. Dropping other job offers, I joined IIT Bombay as a Research
Assistant in FOSSEE project with a plan to apply for higher studies in the next
fall. I was also chosen to speak at [First
International Android Conference in India](http://droidcon.in/2011/), which
happened at Bangalore, on [Indoor Location Tagging Engine](http://funnel.hasgeek.com/droidcon/70-indoor-location-tagging-engine). 
Also, my name was mentioned in the coveted [Google Open
Source Blog](http://google-opensource.blogspot.in/2011/07/whos-new-in-google-summer-of-code-part_22.html)
as part of introducing Komodo Open Lab to GSoC 2011. Now thats something, isnt
it? 


*P.S*: My contributions(through code) to the FOSS world was very minimal
while applying. A couple of personal projects and a decent
stackoverflow reputation were the mention worthy items in my resume at that
time. 

*P.P.S*: Due to frequent nighouts and infrequent eating, I had lost nearly 6
kilograms of weight with no excercise at all during the application period. 


