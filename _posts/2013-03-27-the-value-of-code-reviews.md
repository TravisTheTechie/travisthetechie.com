---
layout: post
title: The Value of Code Reviews
categories: [code]
tags: [Reviews]
description: What should you get out of code reviews?
---

I've been having a lot of discussion lately about the real value of doing code reviews. 
The discussions really haven't been any argument about if they are valuable. It has been 
around exactly how they are valuable. I want to share some of the themes.

<h2>Correctness</h2>

Something that everyone seems to strive for when doing code reviews is asserting correctness 
of the code they are reviewing. I think striving for getting things right and assuring that
by having a third party (outside of who did primary development, maybe not a party outside 
your development group) look over it is great. However, I have rarely found a code review 
to locate something that is incorrect. It does happen, so I won't completely discount it. 
It seems that having all the needed domain knowledge about the feature you are reviewing 
to ensure the feature has been coded correctly is hard. Can you be sure that branch logic 
is exactly what it needs to be per spec? Do you want to even spend the time going over each 
line making sure that's the case? I feel like there's better use of code reviews than 
holding onto "correctness" being the primary objective.
 
<h2>Sharing Understanding</h2>
 
There's some sense of sharing. Especially if you see something you didn't know would work
and learn something new. I think like correctness you might not learn everything about a 
set of code just by looking it over rather quickly.
 
<h2>Standards</h2>
 
Assuring that team members are following coding standards are an excellent use of code 
reviews. Teams really shouldn't have a lot of feedback around this if people are on 
board with the standards. "Hey you forgot x," and call it a day.
 
<h2>Clarity</h2>
 
When it comes down to it, I feel that clarity is the most important part of a code review. 
You are looking over someone's changes to make sure if you had to make changes to the code 
you could understand it tomorrow or next year to effectively make changes in the code. Most 
clean and maintainable code standards/suggestions converge around making code as readable 
and understandable as possible. One of the most important thing in a long term development 
effort.
 
<h2>In Summary</h2>
 
In the end, clarity is the most important thing you are checking for when reviewing code. 
I think standards review and knowledge sharing are also important. While you can do other 
things while code reviewing, I don't think it's worth the effort to really focus on those 
things.
