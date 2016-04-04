# Design notebook for week ending April 3, 2016

## Last week's critique


Last week's critique was incredibly useful. Andrew completely figured out the main issue with my project, which was that the scope was so broad it wouldn't be useful at all. He mentioned that I needed to focus on one aspect of the game - that it was impossible to reliably simulate all aspects of DOTA 2. 

As a result of this, we had a conversation where we both pretty much agreed that I should focus on carry heroes that mostly attack. To explain to anyone unfamiliar with the term "carry", one important role in DOTA 2 (and all games of the genre) is the carry, a hero whose role is to spend as much time as possible "farming" or getting money in order to buy a lot of items that help it do as well as possible in the late stages of the game (typically after 30 minutes). Thus, these heroes tend to use their main attack a lot, buying lots of items that help them survive, and tend to have the most money of any hero on their team. For this reason, their builds are not only more simple than builds on other heroes, but also arguably more important, as they are the heroes that their team relies on to carry them through the late game. This makes it the perfect area of focus for this dsl, as the carry player can test multiple different items against the other heroes' builds, and make decisions on what to buy as a result. Additionally, most other roles in the game buy a lot of utility items, which are very, very, very hard (namely, impossible) to model analytically (consider Force Staff, an item that lets you push yourself or any other hero in the game a short distance forward. Modeling the utility of this item is insanely difficult, as it has tons of uses).

This feedback, and our resulting discussion helped me focus my project into this one domain, and thus come up with much more specific things the DSL can do, like produce graphs of item effficiency over time, damage over time, damage simulations against other heroes, etc.  


## Description

**TODO:** Fill in this part with information about your work this week:
important design decisions, changes to previous decisions, open questions,
exciting milestones, preliminary results, etc. Feel free to include images
(e.g., a sketch of the design or a screenshot of a running program), links to
code, and any other resources that you think will help clearly convey your
design process.

I spend my time this week in two main partitions. First, I spent some time looking for usable data for the in-game data I need. I found data for heroes very quickly, but it was really hard to find usable data for items, and impossible to find any data at all for hero's skills. I eventually made the decision that finding nicely formatted data for items and skills would be impossible given the time constraints, and so I'd just fake it for the purposes of the project. I can hard-code some of the interesting items and skills to show that the idea is possible. 

Second, I spent the majority of my time working on the internal representation of heroe's builds. This is in the IR folder in my code repository. I have a working IR for letting any hero use a specific set of items (currently only two), and getting stats for that hero (both basic stats and more complex ones that I calculate). The reasoning for doing this first is that its the core of the project. If I can define a build sucessfully, I can do any sort of simulation I want, and make any decisions I want regarding the features I want to add to my language. I then started writing code for doing combat simulations, and it worked perfectly (see combat.py in the IR folder), which was exactly what I wanted. With this, basically half of the backend for the project is done. All I need to do is come up with a reasonable way to calculate build efficiency, which is doable with the data storage that I have, and I'll have the entire backend for the MVP complete, at which point I just need to optimize for usability.

## Questions

**What is the most pressing issue for your project? What design decision do
you need to make, what implementation issue are you trying to solve, or how
are you evaluating your design and implementation?**

I think the biggest issue for the project is what I can allow users to do that will be both useful and accurate to the game. One of my initial ideas was to let people only carry out combat once between heroes, which never actually happened in the context of a game - there are too many other factors involved. Instead, I went with doing simulations to determine generally what would happen between two fighting heroes. The other thing I talked about was analyzing build efficiency, but other than that, and simple data queries I'm not sure what things users would care about.

Lastly, I want to keep making sure that my syntax is usable to non-programmers. To that end, I'm continuing to message people that I play the game with (who are for the most part not programmers) to make sure this seems useful to them. 

**What questions do you have for your critique partners? How can they best help
you?**

My main question for both critique partners is what things they would care about this DSL being able to do. Since Andrew is an experience DOTA player, and Josh is familiar with LoL, I think both partners can probably give some ideas that would be useful to a wide variety of players. 

**How much time did you spend on the project this week? If you're working in a
team, how did you share the labor?**

I spent about 3 hours looking for data, which was an unfortunate waste of time. In class on Wednesday, I spent the time figuring out what I wanted to focus the DSL on. Then, I spent a few hours figuring out the optimal way to store the data and access it. I then spent probably about 8 hours writing code for the project. It took this long to write not that much code mostly because I was alternating between figuring out how I want to model the in-game engine as simply as possible, and actually writing the code. I'm happy with the result. 


