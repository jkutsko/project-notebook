# Design notebook for week ending April 10, 2016

## Last week's critique

Joshua's feedback this week was really helpfully specific. He mentioned that, now that I had decided on an area of focus for the project (specifically, Carry hero builds in dota), most of the backend implementation was very feasible, and so I should expand the features of the language now that its reasonable to do so. Specifically, he mentioned adding an "optimize" command that lets the user specify a function and a build, and the engine will produce the optimal next item for that build based on the function. I thought about that for a while, because one of the things that I had briefly talked about with Andrew last week was that just having a flat "optimizer" with no user input would almost always output the same build (probably moon shard, heart of tarrasque x2, divine rapier x2, and crystalys x2), which is not only totally unreasonable for an actual build in the game, as all of the items are extremely expensive, but is terrible because divine rapiers drop on death, so giving this as a suggestion to players is awful in terms of safety and efficiency. However, I also was hesitant about letting the user define functions, as one of my major design decisions was to make this 100% accessible to people who have absolutely no programming experience. So, I settled on an idea that I'd been mulling over for a while: basically let people optimize a build by giving arbitrary numbers next to the stats they want to optimize:
'''
optimize build1 for:
	damage vs build2: 10
	attack speed: 5
	efficiency: 7
'''

and then I'd normalize their priorities and have an easy to input function. This was great in terms of fleshing out the features of the language, as it opens up tons of possibilities for testing builds within loops to really get the maximum ability to test things with my language.

Additionally, on Monday, with the help of my critique partners, I was able to get item data downloaded in a nice format, so I wrote a converted to get it from .csv to .json, and then slightly modified my item code to handle the new json tags, so item data now works completely! I tested everything in IRTesting.py in the IR folder of the code repo, and was pleased with the backend working as intended. The graphs I displayed are definitely useful to someone wanting to know, for example, if they can kill the enemy support lion in the time it takes for a teammates stun to wear off before the lion stuns you and gets away.

## Description

**TODO:** Fill in this part with information about your work this week:
important design decisions, changes to previous decisions, open questions,
exciting milestones, preliminary results, etc. Feel free to include images
(e.g., a sketch of the design or a screenshot of a running program), links to
code, and any other resources that you think will help clearly convey your
design process.

This week, I worked on two main things. First, I finalized my designs for the language features. Part of this was due to the specific decision that I talked about above, which helped me figure out exactly what I needed the language to be able to do to be useful. The rest of this process basically consisted of figuring out the most succinct way to get all of the functionality I wanted in as few commands as possible. This was a priority since again, I want the language to be accessible to total non-programmers.

The next step in this process was getting the actual syntax down. To do this, I made a grammar.txt file thats in the Code repo in the "Parsing" folder. This essentially describes all of the available commands and ways to write them, and I'm happy with how short it ended up being, while still maintaining the definition, query, optimization, and control flow. It currently doesn't have the function definition that I described above, since I don't have the backend support for that yet. This week was mostly focused on the user-facing side and getting that ready and parsed, whereas the next 2-3 weeks will be basically just adding features when I think of them.

Finally, with this done, I focused on actually implementing the parser and evaluator for the language. This was a large question mark for me in the project, ever since I switched from scala to python. From what research I had done, there were python parser combinators that existed, but none of them were really any good. Luckily, I happen to know Matt Valentine, who had also done his DSL last year in python, and is generally an expert in all things in the intersection of esoteric knowledge and programming. I asked him what he did, and he mentioned the python package Parcon. I looked into it, and while it also looked confusing to learn, it did the things I needed. So, I spent some time learning the syntax for this, and then wrote up the parser using my grammar.txt file as a reference. I also wrote the abstract syntax tree classes, which are not nearly as nice in python as scala, but it works. 

The parsing looks basically like this:
'''
build_assignment = (
	("level: " + number[int] + hero_name + "with:" + items_definition)[lambda x: Build_Assignment_Items(x[0],x[1],x[2])]\
	| ("level: " + number[int] + hero_name + "with:" + var_name)[lambda x: Build_Assignment_Value(x[0,x[1],x[2]])]\
	| ("level: " + number[int] + hero_name )[lambda x: Build_Assignment_NoItems(x[0],x[1])])
'''

The actual return type of the parcon parsers took a bit to infer, but eventually everything makes sense, all the parsers return lists of significant tokens that you apply functions to to get the abstract syntax tree result.

With that done, I focused then on the evaluator This is actually where I currently am. This part isn't hard, but in terms of design, I'm focusing primarily on getting build definitions, item definitions, and queries (both basic stat queries and combat queries) done for the demo. The process isn't finished yet, and as of writing this notebook, it might not be before midnight. I'm going to commit this version, and then commit additionally once I'm actually done, if that ends up being after the midnight deadline. 

## Questions

**What is the most pressing issue for your project? What design decision do
you need to make, what implementation issue are you trying to solve, or how
are you evaluating your design and implementation?**

The most pressing issue right now is basically making sure that the language is usable. All of my design decisions are focused on this, now that I have a concrete idea of what backend functionality I want to support, and that this will be useful to people.


**What questions do you have for your critique partners? How can they best help
you?**

With respect to the previous point, I basically want suggestions for syntax elements to have in the language that would make it easy for people to get the info they want as quickly as possible with as few programming terms as possible. For example, one such element that I don't currently support is being able to add things to lists, for example:

'''
add build1 to carry_builds
'''
Other such simple statements that might be convenient to the user are what I'm looking for right now.

**How much time did you spend on the project this week? If you're working in a
team, how did you share the labor?**

I think overall, I probably spent somewhere between 15 and 20 hours on the project this week. A lot of this was spent planning the language elements and getting the grammar working. I don't have a concrete time estimate here, as I spent a lot of time just thinking, not looking at the clock. I then probably spent 3-4 hours learning the parcon syntax, another ~5-8 writing the parser and abstract syntax tree and testing it, and then another ~3 on the evaluator.
