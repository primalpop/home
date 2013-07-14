---
layout: post
title: "Parsing JSON in Android"
categories: Android
share: y
disqus: y
---

As part of the college mini project,  I along with my group, developed a
micro-blogging platform for Android. One of the biggest hurdles I had to face
was of choosing the proper data format for receiving responses from the web
service. I needed something that was fast as well as easy to understand and
parse.  I first chose XML as it was easy to read and mostly because I knew no
other alternatives. But parsing XML certainly wasnt easy. With the variety of
tags in the responses from the server and the heaviness of XML format, it just
became impossible to use it.

That's when [JSON](http://www.json.org/fatfree.html)(JavaScript Object Notation) came up as an alternative to XML. I was circumspect about using JSON at first as I had doubts about its readability and ease of deserialization. But those doubts were not much more than just superstitions. JSON is smaller and easier to parse, than it's XML equivalent. Many say its less readable than XML, but considering it was used for data interchange, readability was not important.

The easiest way to parse JSON and convert to POJO (Plain Old Java Objects) in Android is to use the Google's GSON library.


### Download GSON

Download the latest Google GSON library from [here](http://code.google.com/p/google-gson/). Add this library into your Android Project as an external by right clicking on the desired project and do the following

> Properties -> Java Build Path -> Libraries -> Add External JARs and point to the downloaded gson library.


The following is an array of JSON Objects.  You have to develop a class structure in accordance with the structure of the JSON response received.  For the above example I had the class structure based on the following logic.

{% highlight java %}

{ "posts":
  [
     { "post": 
       {
       "username": "John",
       "message": "I'm back",
       "time": "2010-5-6 7:00:34"
       }},
     { "post":
       {
       "username": "Smith",
       "message": "I've been waiting",
       "time": "2010-4-6 10:30:26"
       }}]}

{% endhighlight %}

The "posts" data structure contain multiple posts, each of which contains an "post" type. In order to match this structure, I need to have 3 classes namely PostList, PostContainer and Posts. The PostList class should have an ArrayList of objects of type PostContainer. PostContainer needs just one field which is an object of type Posts. Posts classes must have  3 fields namely username, message and time

{% highlight java %}

public class PostList {

private List<PostContainer> posts = new ArrayList<PostContainer>();
public List<PostContainer> getPostContainterList() {
return posts;
}
}

class PostContainer{
Posts post;
public Posts getPost(){
return post;
}
}

public class Posts {
String message;
String time;
String username;
}

{% endhighlight %}

### Deserialization Part


Now let's get into the real business of Deserialization. Using GSON this can be done very easily.

First, import the Google gson library into the class in which JSON String is to be deserialized

{% highlight java %}

import com.google.gson.Gson;

{% endhighlight %}

I am initializing an ArrayList which contains objects of type Posts

{% highlight java %}

private List<Posts> mObjectList = new ArrayList<Posts>() ;

{% endhighlight %}

This can be latter on used for adding the Posts objects after deserialization is done.

{% highlight java %}

String jsonString = "Insert your JSON Data here"

{% endhighlight %}

Instantiate an Object of type PostList

{% highlight java %}

PostList list = null;
list = getPostList(jsonString);

{% endhighlight %}

The following function deserializes JSON response to an Object of type PostList and returns it.

{% highlight java %}

protected PostList getPostList (String jsonString){
PostList pl = null;
Gson gson = new GSON;
pl = gson.fromJson(jsonString, PostList.class);
return pl;
}

{% endhighlight %}
What the function getPostList does is, it creates an object of type GSON and deserialize the JSON String to POJO using that object(gson).

{% highlight java %}

gson.fromJson(jsonString, PostList.class)

{% endhighlight %}
The first parameter to the function is the JSON String and second parameter is the name of the class to which it should be deserialized. Two important things have to be taken care of while using GSON to parse JSON
	
 1. Tags in JSON String and name of fields of the respective classes should match exactly.
	
 2. Object hierarchy should be built correctly.

Failure to comply to the both conditions above would result in some or all of the fields of the classes being left null.

Having parsed the JSON string to POJO, we can get various Posts objects separately and add it to the ArrayList which we created earlier as follows.

{% highlight java %}
List <PostContainer> post_list = list.getPostContainterList();
PostContainer pc;
for (int i = 0; i < post_list.size(); i++) {
    pc = post_list.get(i);
    mObjectList.add(pc.getPost()); 
{% endhighlight %}

This ArrayList can be used to populate a custom list view. If you have any doubts regarding this post, feel free to ask through comments. In the next post, I will post an tutorial on how to build a custom listview which looks the twitter timeline efficiently.


