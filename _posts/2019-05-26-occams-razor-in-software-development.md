---
title: Occam's Razor in Software Development
layout: post
---

Recently we were in a meeting with multiple stakeholders from business side. When asked how one of our features work, I started explaining them the details of the features and how it is implemented. After the meeting a senior engineer told me that eventhough I explained every single detail of the feature, there is going to be a follow up meeting to discuss this. He told me this was because I had told them too much details which probably confused them. That is when I understood the principle of Occam's Razor.
# What is Occam's Razor?
Quoted from Wikipedia 
> Occam's razor (also Ockham's razor or Ocham's razor,  further known as the law of parsimony  is the problem-solving principle that essentially states that "simpler solutions are more likely to be correct than complex ones." When presented with competing hypotheses to solve a problem, one should select the solution with the fewest assumptions. The idea is attributed to English Franciscan friar William of Ockham (c. 1287–1347), a scholastic philosopher and theologian.

We have all heard the famous quote by Sherlock Holmes
> Once you eliminate the impossible, whatever remains, no matter how improbable, must be the truth.

This follows directly from Occam's Razor. This principle states that given two explanations of a situation, the one in which there is the least number of variables(simpler) however improbable is the most likely explanation. This principle is very helpful and it can be used in a wide variety of situations but it is especially powerful in the hands of software professional.

# How is it applied in Software
There are many areas of Sofware development which can benefit from this principle. A few of them are:
## Coding

The first and foremost area is coding. As developers we make hundreds of decisions on a day to day basis that directly affects the health of the codebase as well as the business. The common mistakes we make include adding unwanted abstractions, designing for the future, making it "extensible"(whatever that means).  These code with unwanted additional complexity slowly rots over time and becomes "that" part of the code that no one knows what is happening and nobody is willing to touch. These are the things we do either knowingly or unknowingly which can take a dent on our code base in the long-run.

To overcome this it would be prudent for us to think in terms of Occam's Razor. Always do the simplest thing possible at any point in time. Principles like YAGNI and KISS are examples of Occam's Razor in coding.  If you want to combine 3 design patters to accomodate a feature request you expect in the future, restrain your primal instincts and stick with a single class for now. Using Occam's razor during the development process would keep the codebase simple and readable and your future peers will really thank you.

A word of caution here is, this principle should not be used as an excuse to write bad code or take shortcuts. If there is a real need to add complexity by all means you should do that. This gives a framework for you to step back and think for a moment and it should be used as such.

## Debugging
Another intersting application of this principle is while debugging. The hard part about debugging is nobody knows the answer especially when you work in a legacy code base with business critical functionalities.  Bigger the codebase, more complex the debugging process and thus Occam's Razor comes in really handy.  All good software developers will trace the root cause of a bug by using this principle even without realizing it.

Lets say there is a program displaying a few stats in the dashboard. You observe that the each time the dashboard is updated you get 2x instead of x for a particular stat. What would be your first instict? Where is the issue? Is it an double counting issue or some thread level race condition? I am guessing most of you with go with the former. This is Occam's Razor in action. You picked the choice which provides the simplest explanation for the issue intutively.

This is not to say that always the simplest explanation is the right one. Instead you start from the simplest one and eliminate one by one by theory or experiment until you arrive at the actual root cause for the problem. This provides a framework for you to tackle problems methodically. 

## Communication
One of the most under-rated function of a software developer is communication. Be it with peers/ managers/ stakeholders, communication is as important as coding for any developer. As developers we are the closest to any given problem and it is natural for people to rely on us for understanding the whole picuture of a product/feature. This makes what you communicate and  how you communicate extremely crucial from a business standpoint. 

As we are closest to a problem, we will have a lot of  technical and domain knowledge around it. But it is extremely important to communicate the right things to the right people. Assume you are in a mail thread with Sr. engineer, PM, Manager and a Business development executive, you need to provide just the right amount of detail so that the Engineer can get the technical challenges and the others can also understand the complexity technically as well as the business justification. You need to achieve the right amount of balance in the technical/business mixture for the audience to understand and not lose interest. This is where Occam's razor comes in. You need to provide the least level of detail in the mail and schedule a follow up for the people who needs to understand more. 

Take this as an example "we did a POC  on x and we were able to achieve y.  Eventhough we discussed about A in the previous mail, we could not achieve A due to the complexities in an library that we were using. There were a lot of assumptions in the threading model in the library and thus it prevented us from achieving A".

Now what do you think the different stakeholders will understand?
1. Engineer - Yes I get the issue.
2. PM- So basically we cant achieve A.  And what is threading model?
3. Manager - Did he try enough to acheive A?

Instead if we write "we did a POC on x and were able to achieve y. A was targetted but not achieved. I'll schedule a meeting to demo the POC and go into details on the blocker for A." After that you have all the time in the world to explain in detail the blockers for the right audience and acheive a consensus.

Now what is the thought process after the demo.
1. Engineer - Makes sense. 
2. PM - The POC is good for now. I guess we can drop A for now and proceed without it.
3. Manager - He has done an indepth analysis and knows what he is doing.

## Conclusion
Occam's Razor can be employed in a wide variety of scenarios and these are just a few examples. Developers use this principle intutively without knowing it. But knowing it and using it deliberately in various situations will greatly improve you as a software developer. If you can think of any other area of Software where this principle is being used feel free to leave your thoughts in comments.