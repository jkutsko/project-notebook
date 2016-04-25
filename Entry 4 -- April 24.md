# Design notebook for week ending April 24, 2016

## Last week's critique

This week's critique was entirely focused on answering questions I had about my list of features to add. Joshua answered in pretty good detail which things he considered most useful for my project. I think this was a really important area to get feedback in, since I had essentially been considering my todo list in terms of the things that seemed most logical from an implementation standpoint. At this point, I wasn't really in the stage of development where I had a lot of important decisions that strongly effect the outcome of the language, but I definitely had a lot of small decisions to make that will influence its overal quality and usability when the final result is due.

Specifically, Joshua emphasized quite a lot that accuracy is key. As of right now, there are several missed edge cases, and innaccuracies involved in the backend, so it wouldn't be all that useful to a user as it stands. Thus, Joshua's feedback convinced me to put off adding more nice syntax elements, obscure queries, and making specifying hero names smarter for future work, and instead focus on getting the optimization and combat simulation working better. So, my goals this week were basically to get all the frontend stuff working on a basic level so that I was ready for the presentation, while simultaneously planning and beginning implementing features to the backend that will make the language give more accurate results.

## Description

Like I said, the first thing I did this week was to finish implementing the grammar for loops that I meant to finish last week. Not much to say here, I just fixed the bugs and tested everything, and it works now.

The next step was to spend some time reorganizing my task list based on feedback. I decided that I still wanted to keep my overall goal system of having the language completely working by the presentation, so the last thing I needed to add was the optimize command. This involved both backend computation, and adding the syntax to the AST/Grammar system. Nothing really went wrong here, I'm pretty good with parcon's intricacies at this point, so it all worked as planned. 

In terms of future goals though, I reorganized the task list in the readme.md file of the code directory that I've been using as a checklist. Essentially, my next few goals are to fake ability data and add that to querying and combat simulation, and to generally fix up some aspects of combat. Fishberg mentioned last week that HP regeneration is an important part of combat (certain heroes/items have quite a bit of hp regen that is very significant in fights). Additionally, like Joshua mentioned, having hero ability data will help highlight the items that have the most synergy with heroes. For example, if I add data for Phantom Assassin, who has a built-in critical hit ability, my system will prioritize giving that hero more damage items, so she hits harder with her crits. I spent some time planning where this would go. Luckily, my project is organized fairly well, as this data can just go in the build class for that hero, and all of this will be pretty easy to add, and won't change how any of the backend works. This was one of Joshua's main concerns, so I spent some time addressing it.

Finally, now that I have a DSL that has all the features that I want (albeit not super accurate), I've started to show it to some of my high school friends that play DOTA, to get feedback on both how useful this is, and how easy it is to use for non-programmers. This is much harder than I would like, because the program as it is necessitates people to have python installed, and be familiar enough with programming to enter the file name of the thing that they write into a line of the program. This isn't ideal, but making a standalone app in python that has the packages that I need is much more annoying than I would like. However, I do have two friends that are willing to play around with it, so hopefully I'll get their feedback soon. Unfortunately, one of them is familar with programming, and the other is most likely at least a little bit familiar with it, so they're not the ideal audience. I'm not sure what I can do about this at the moment. 


## Questions

**What is the most pressing issue for your project? What design decision do
you need to make, what implementation issue are you trying to solve, or how
are you evaluating your design and implementation?**

At the moment, I don't think I have any questions related to what I want to actually do with my language. I've gotten enough of the implementation and design done concurrently to know what I want to do, and that its possible to implement with my architecture. Right now, the most pressing issue is really just how much more accurate I can make my project. I have a good idea of what I'm focusing on, and what I need to implement for it to work, its just a matter of doing as much as I can before the deadline. And, honestly, I'm almost certainly going to keep working on this after the deadline, because I think it could be incredibly convenient to have and to use while in a game, or after a game to think about what I did wrong. 

**What questions do you have for your critique partners? How can they best help
you?**

I think the biggest question I have is how I can make this project easier for total non-programmers to use. I don't have any experience making standalone apps in python, so if you happen to, any tips for how to make this usable would be awesome. Essentially, what I want people to be able to do is run this program in the command line like:

```
DOTABuilder program1.dota
```

Ideally without having to install anything besides python (and possible other packages, but I'd love it it not). 

**How much time did you spend on the project this week? If you're working in a
team, how did you share the labor?**

I probably spent about 10 hrs on this project this week. I spent a few doing recovery work from last week, then a few planning, and lastly I spent about 6 hours actually doing the implementing work and documenting/making the presentation for this week.


