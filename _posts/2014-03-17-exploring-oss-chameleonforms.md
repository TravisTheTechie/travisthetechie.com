---
layout: post
title: Exploring OSS - ChameleonForms
description: I had the chance to check out ChameleonForms for ASP.NET MVC form creation and it's a nice library.
tags: [OSS]
categories: [code]
---

I had the chance to check out
[ChameleonForms](https://github.com/MRCollective/ChameleonForms)
for ASP.NET MVC form creation and it's a nice library. You can get it from the
[NuGet package](http://www.nuget.org/packages/ChameleonForms/).

ChameleonForms allows you to fluently build and configure forms.

{% highlight csharp %}
@using (var f = Html.BeginChameleonForm()) {
    using (var s = f.BeginSection("A form")) {
        @s.FieldFor(m => m.RequiredString).Label("Some string")
        @s.FieldFor(m => m.SomeEnum)
        @s.FieldFor(m => m.Phone).Placeholder("+1 (XXX) XXX-XXXX")
        @s.FieldFor(m => m.SomeCheckbox).InlineLabel("Are you sure?")
    }
    using (var n = f.BeginNavigation()) {
        @n.Submit("Submit")
    }
}
{% endhighlight %}

So that's not super complicated. Just apply some methods in a chain to the field and have at it.
There is an [example app](https://github.com/MRCollective/ChameleonForms/tree/master/ChameleonForms.Example)
that is maintained that includes pretty extensive and complicated forms to use as a base to get started.  

Interestingly enough, most of the configuration revolves around a pretty simple idea when you dig into the code.
`FieldConfiguration` keeps an `Attributes` collection which contains most of the configuration you can apply
to the form field. Want to set `Rows` on a textarea, the `IFieldConfiguration.Rows(int)` method just adds
it the internal attributes collection.

{% highlight csharp %}
public IFieldConfiguration Rows(int numRows)
{
    Attr("rows", numRows);
    return this;
}

That's pretty simple. Then there's a `FieldGenerator` that collects all this configuration and
{% endhighlight %}
passes it off to built in MVC generators in the proper format.

So I'd suggest checking it out if you ever want a new way to generate your forms in ASP.NET MVC.
