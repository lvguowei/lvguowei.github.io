---
layout: post
title:  "Dependency Injection Explained(I)"
date:   2015-10-25
categories: programming, design pattern
---

Dependency Injection frameworks has been out there for a long time, people find them useful especially in large applications.
But learning how to use such framework sometimes feels flaky.

In this series of blogs I will discuss how to use [Dagger2](http://google.github.io/dagger/) in Android development.

In the first blog (which is this one) I will discuss what is DI.

In the second blog, I will discuss the basics of Dagger2.

In the third blog, I will discuss how to apply Dagger2 in Android development.

First of all, what is dependency?

Let's take a look at the following example:

{% highlight java %}
public interface Heater {
    void on();
    void off();
}
{% endhighlight %}

{% highlight java %}
public class MyHeater implements Heater {

    void on() {
        // turn on
    }

    void off() {
        // turn off
    }
}
{% endhighlight %}

{% highlight java %}
public class Pump {

    private Heater heater;

    public Pump() {
        heater = new MyHeater();
    }
}
{% endhighlight %}

The idea is very clear, a `Pump` contains a `MyHeater`. Well, in other words, we can say that class
`Pump` depends on class `MyHeater`. Thus, `MyHeater` becomes a dependency of `Pump`. Without `MyHeater`
, `Pump` cannot work.

Now, you may already know that such dependency is rather bad. Why? Say, we want to use `FancyHeater` someday with `Pump`,
then we have to modify the `Pump` class, even though they `Pump` should have nothing to do with `Heater`.

Wouldn't it be nice that the class `Pump` only knows **how to use a `Heater`**, but has no knowledge of what kind of `Heater` it actually is using.
DI can help to solve this problem.

In short, **DI is a mechamism to separate the creation of objects from the entities that use such objects**. The DI framework knows how to create objects,
and our application code only knows how to use them. The DI will inject the created objects into application code.

For convinience of discussion, let's define 3 roles in DI:

* **service**: object to be injected
* **client**: object that service being injected into
* **injector**: object responsible of creating services and inject them into client

*(To be continued...)*
