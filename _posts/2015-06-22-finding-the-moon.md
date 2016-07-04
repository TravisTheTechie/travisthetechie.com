---
layout: post
title: Finding the moon
categories:
  - Science
tags:
  - Python
description: >
  I have a young son who likes looking at the moon when it's in the sky. I'm happy to let him do so
  &ndash; who doesn't like looking up at the sky? &ndash; but it's hard for me to know when I can
  point outside and we can see the moon. I thought there might be a simple answer for this...
---

I have a young son who likes looking at the moon when it's in the sky. I'm happy to let him do so
&ndash; who doesn't like looking up at the sky? &ndash; but it's hard for me to know when I can
point outside and we can see the moon. I thought there might be a simple answer for this...

The problem seems simple enough; for a given location:

* The moon should be full or near full
* The moon should be above the horizon
* The sun should be below the horizon or far enough away from the moon it's easy to look at (early
  or late in day being best)
* The weather should be partly cloudy or clear

As a software developer, thinking about this is a bit overwhelming, but I do plenty of merging of
data together to get a result.

## Lunar phases

Okay, this one is simple enough; all I need is a full moon and the frequency between full moons. Add
a slight range around this one and we're good to go. The latest full moon was `2015-06-02 16:19 UTC`
(via the [U.S. Naval Observatory][moon-phases]). The lunar month is $29.530588853$ days (on average).
I got this one.

## Lunar location

Having a background in slightly different [orbital mechanics], I assumed we could do some
trig with a correction factor and be ready to the find the location of the moon. From there it's
easy enough to figure out if it's visible from your location with even more trig work.

Turns out, the moon is a lot more complex to nail down in location. There's an article, [Low
percision formulae for planetary positions][ads-article], that describes how to find the position
for a given body. The moon has noticeable [libration] &mdash; making the
moon appear larger or smaller at different times, leading to a cycle of [full moons].

I found [PyEphem], meaning I don't have to solve this. As with other software, I'm leaning on
others who have helped pave the way.

{% highlight bash %}
pip install pyephem
{% endhighlight %}

And then I can start with the easy thing &mdash; verifying my data above.

{% highlight python %}
>>> import ephem
>>> ephem.next_full_moon('2015/06')
2015/6/2 16:19:01
{% endhighlight %}

Hey, that aligns with the U.S. Naval Observatory. Awesome! Playing with the [REPL], let's see how
close I can get to my desired outcome using PyEphem.

{% highlight python %}
>>> import datetime
>>> import ephem
# create a Observer, where on Earth we are looking up at the sky from
>>> me = ephem.Observer()
# using Washington, DC
>>> me.lat = 38.9047
>>> me.long = 77.0164
# I'm interested in dates around the next full moon
# .datetime() is so it's in Python's datetime format and not PyEphem's
>>> date_helix = ephem.next_full_moon(datetime.datetime.now()).datetime()
# create a range of dates around the full moon
>>> date_range = [date_helix + datetime.timedelta(days=-2),
date_helix + datetime.timedelta(days=-1),
date_helix,
date_helix + datetime.timedelta(days=1),
date_helix + datetime.timedelta(days=2)]

# and a function to map those dates to nearest moon rise/set times
>>> def moon_times(date):
  me.date = date
  moon = ephem.Moon()
  return [me.next_rising(moon), me.next_setting(moon)]

# and map away
>>> map(moon_times, date_range)
[[2015/6/30 14:30:09, 2015/6/30 18:38:47],
 [2015/7/1 15:30:11, 2015/7/1 19:34:53],
 [2015/7/2 16:04:32, 2015/7/2 20:59:00],
 [2015/7/3 16:22:13, 2015/7/3 22:39:29],
 [2015/7/4 16:31:46, 2015/7/5 00:25:45]]
{% endhighlight %}

Woo, look at that. I get rising and setting times for the moon. I'm not there yet, but this gets
me started down the right path. Thinking about what happens if the date is after a rise, but before
a set, I could see a set happening before a rise.

## What's next?

Next I'll try and convert this to local time, match against
reasonable hours I'm interested in viewing, and merge that with weather data if it's within the next
week. This has not been as easy as I had hoped, but not nearly as bad as I feared it could be once
I started doing some research. Python wouldn't have been my first choice to do this, but having the
calculations I need already implemented makes it worth it.


[moon-phases]: http://aa.usno.navy.mil/cgi-bin/aa_phases.pl?year=2015&month=6&day=2&nump=50&format=p
[ads-article]: http://articles.adsabs.harvard.edu/full/1979ApJS...41..391V
[libration]: https://en.wikipedia.org/wiki/Libration
[full moons]: https://en.wikipedia.org/wiki/Full_moon_cycle
[PyEphem]: http://rhodesmill.org/pyephem/
[orbital mechanics]: https://en.wikipedia.org/?title=Atomic_orbital
[REPL]: https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop
