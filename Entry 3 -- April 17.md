# Design notebook for week ending April 17, 2016

## Last week's critique


Last week's critique was really really detailed and helpful for a lot of the specific things I need to work on. While much of it was code-related improvements (which were definitely important, I've been writing code rather quickly without as much thought to making sure the style is good), he gave me a lot of very specific feedback on how to improve the syntax to make the language more usable, with specific syntax suggestions (like "->" to add things to lists, and delineating list elements wiht "," rather than "and"), that won't be too hard for non-programmers to pick up, but make my job a lot easier. My plan with respect to this week's critique is to start by finishing up the remaining language elements, then clean up the code on the backend, and then just add features and functionality.

With respect to the last part of the critique, it seems we both agree that hero skill data is going to be pretty hard. I like his idea for putting specific skills into those buckets, with values for each skill, but the issue there is that many of those don't really effect the simulations that I'll be doing, and overall there just isn't a nicely formatted set of data, so I'll have to fake the skill data somehow. I think the way to go here would be to get a list of the skills that directly effect carry heroes, so skills that have attack buffs or buff the hero's stats in some way. 

Finally, I'm putting some thought into having a testing system, but I don't know exactly how I want to implement that yet, or how high a priority it is given the timeline we have for this project.

## Description

This is going to be rather short. Unfortunately, I got completely destroyed this week by a day-before-code-freeze-clinic-disaster scenario, and I basically couldn't get anything else done. However, before and after that, I essentially finished what I started last week. 

First, I reworked the grammar so that variable names didn't get confused with keywords, and allowed for multiple-word hero and item names. This was actually a hell of a lot harder than it should have been. Parcon (the parser I'm using) made this really tough by using an eager parsing strategy, and I was hours away from switching to pypeg and having to restart all of last week's progress. However, I found a way to get around the issue, in a way that literally makes no sense (I'm now telling parcon to not parse entiree keywords into hero names and item names instead of just not parsing the ":" thats at the end of the keyword. Despite the fact that both of these should fail at parsing the string: "and:", it seemed like parcon happily parses the "and" into the name, and then calls it a successful parse, and then sees the ":" and errors.) Regardless, now, I can run the program:

```
build1 = level: 22 Dragon Knight with: (Daedalus, Butterfly, Monkey King Bar)
build2 = level: 16 Lion
get: damage of: build1
get: hp of: build1
get: attacks of: build1 vs: build2
build3 = level: 20 Morphling with: (Crystalys, Yasha)
get: damage of: build3
get: attacks of: build3 vs: build1
items = (Daedalus, Butterfly, Yasha, Sange)
build4 = level: 16 Lina with: items
get: damage of: level: 16 Lina with: items
```
And it runs successfully (I also manually verified that the results make sense. The next thing I did (and am still in the process of doing) is adding other syntax elements. In sample_future.dota, I Have a bunch of additional syntax features as a goal. As of now, for loops work, but the optimize and max/min commands do not. I have the basics for starting these though, and will finish this as soon as possible.

## Questions

**What is the most pressing issue for your project? What design decision do
you need to make, what implementation issue are you trying to solve, or how
are you evaluating your design and implementation?**

honestly, right now, I don't really have many additional issues from last week. I wasn't able to fully finish my plan of having all of the syntax elements done, so thats the thing that I absolutely need to do. Its also probably the most relevant from a DSLs class point of view, since its the language-design part of this project, so its highest priotity. 

The other thing I need to do, once I have this first step done, is send the project to some of my friends who are not programmers, but play a lot of dota. Since they are exactly my target audience, and also able to give me honest feedback, their input should be really helpful. 

**What questions do you have for your critique partners? How can they best help
you?**

As I said, I wasn't able to fully finish my goals for the week. However, I have a list of TODOs in the readme for this project. If you want to look at those and estimate vaguely which seem the most useful to do first, that would be awesome. As of now, I've put them very loosely into the order that I think makes the most sense to implement in, but that's not strictly what's important, I should probably focus on what people think would be useful. 

**How much time did you spend on the project this week? If you're working in a
team, how did you share the labor?**

I was only able to spend about 6 hours working on this project this week (hopefully having worked much more than that last week balanced things out a little :( ). Most of it was spent figuring out how to rework the grammar, and then the rest was implementing more grammar elements. The bright side of this is now that I have a working parser that I understand how to work with, Adding the rest of the grammar elements won't be too hard. 
