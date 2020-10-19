# Sherlock Holmes, Consulting Developer

* **Speaker: Stuart Halloway**
* **Conference: [Clojure/conj](http://2019.clojure-conj.org/) - November 2019**
* **Video: [https://www.youtube.com/watch?v=OUZZKtypink](https://www.youtube.com/watch?v=OUZZKtypink)**

[Time 0:00:00]

```
slide title:
```

All right.  It is such a pleasure to be back in Durham for Conj, and
to be finishing the day with so many friends, old and new.  And ...


[Time 0:00:11]

```
slide title:

     Your Code as a                   "criminal investigators
       Crime Scene                     ask many of the same
                                       open-ended questions
                                       programmers ask while
            Use Forensic Techniques    working through a
to Arrest Defects, Bottlenecks, and    codebase"
        Bad Design in Your Programs

[ image of book cover ]

https://pragprog.com/book/atcrime/your-code-as-a-crime-scene
```

I want to start by talking about a 2015 book by Adam Tornhill, "Your
Code as a Crime Scene".  And he says that: criminal investigators ask
many of the same open-ended questions that programmers ask while they
are working through a codebase.

And this is spot on.  And I would take it a step further and say that,
in fact ...


[Time 0:00:36]

```
slide title: Sherlock Holmes:
           Consulting Developer

[ drawing of Sherlock Holmes ]

https://en.wikipedia.org/wiki/Sherlock_Holmes
```

... Sherlock Holmes is the O.G. software developer.

[ O.G. here refers to this meaning of the term:

https://www.dictionary.com/e/slang/og/

Quoting the definition there:

OG is a slang term for someone who's incredibly exceptional,
authentic, or "old-school."  It can be earnestly used for a legend
like Michael Jordan or more ironically, like for that friend who can
unwrap a Starburst with their mouth. ]

And this talk is going to be making this point, starting with the
obligatory definition slide.

[Time 0:00:49]

```
the Canon:

the 56 short stories and 4 novels
about Sherlock Holmes written by
Sir Arthur Conan Doyle

https://en.wikipedia.org/wiki/Canon_of_Sherlock_Holmes
```

So today's definition is the canon.  The canon is the 56 short stories
and 4 novels about Sherlock Holmes that were written by Sir Arthur
Conan Doyle.

There is a lot of other stuff about Sherlock Holmes.  How many people
have seen a movie with Sherlock Holmes in it?  Or a TV show with
Sherlock Holmes in it?  So we are not going to be talking about those
today.  We are going to be talking about the books.  And we are
talking about what we can learn from Sherlock Holmes about how we do
software development, and how we could do it better.


[Time 0:01:21]

```
"Crime is common.
 Logic is rare."

The Adventure of the Copper Beeches
```

Throughout the talk, I am going to be quoting from the canon.  And all
of the slides that quote from the canon look the same, for your easy
reference.  They have a quote in big font in the middle of the slide,
and at the bottom is the name of the story in a font so small that you
cannot read it, and therefore have no way to actually fact check me.

However, after the talk today I will post the slides on line, so if
you want to go back and read the original stories behind these ideas,
you will be able to do so.

And you can see this quote from The Adventure of the Copper Beeches:
"Crime is common.  Logic is rare."  That sounds almost like something
you could hear said in a software meeting, or a stand-up, or a
retrospective.  People are mostly criminals, and programs are mostly
bad.


[Time 0:02:16]

```
slide title: PROBLEMS

[ xkcd web comic.

Panel #1: A person sitting at a table with food on a plate in front of
them.  They say "Can you pass the salt?"

Panel #2: Same scene, person eating.

Panel #3: Same scene.  Dialogue:

Original person: "I said --"

Outside-of-image speaker: "I know! I'm developing a system to pass you
arbitrary condiments."

Original person: "It's been 20 minutes!"

Outside-of-image speaker: "It'll save time in the long run!" ]


https://xkcd.com/974/
```

So I want to start with problem solving.  Programming is problem
solving, and this is an idea that Rich has done a great job of
communicating to us in the Clojure ecosystem.

And so it is a regular idea, and I have actually seen this.  This
happens at Cognitect.  It happens on the product team with Datomic.
But I have seen this percolate through in other companies.  So I have
been in meetings at other companies where someone starts to do
something very movie software-ish, like whipping out a keyboard.  And
someone else just puts a hand on their shoulder and says: "Whoa,
there!  What is the problem statement?"

And the thing about it is that it is an easy idea, but it is tough to
master.  So I can say: you should not proceed without a good problem
statement.  But how does one go about getting one?


[Time 0:03:11]

```
"It will be of use to me
 to hear the succession
   of events _again_"


The Stock-Broker's Clerk
```

And the way Holmes approaches it is iteratively.  One of the things
that Sherlock Holmes does is insist on having other people verbalize,
multiple times, the information that he is going to use to come up
with a problem statement.

So he says in The Stock-Broker's Clerk: Please tell me the succession
of events again.


[Time 0:03:31]

```
"I should be none the worse
for hearing the sequence of
    events _once more_"


The Adventure of Black Peter
```

And in The Adventure of Black Peter he says: I would be none the worse
if I could hear that sequence of events one more time.


[Time 0:03:38]

```
 "I shall enumerate them
   to you, for nothing
clears up a case so much
as _stating it to another
         person_"


Silver Blaze
```

Every once in a while, he even bestirs himself to state the events for
somebody else to listen to a second time.


[Time 0:03:46]

```
Now, _I'll state the case
clearly and concisely to
 you, Watson_, and maybe
you can see a spark where
    all is dark to me.


The Man with the Twisted Lip
```

And he clearly is the father of pair programming, and cardboard cutout
programming.  He says: you know what?  I do not understand this right
now, so I am going to say it you, Watson, and by the time I am done
saying it, I will have gained at least some measure of additional
insight.


[Time 0:04:03]

```
[ Photo of Benedict Cumberbatch and Martin Freeman in costume as
Sherlock Holmes and John Watson. ]

https://www.merriam-webster.com/words-at-play/10-sherlock-holmes-words
```

So great.  Holmes and Watson invented pair programming, and all you
have to do to be a good software developer is find a friend, get a
cool Victorian wardrobe, optional goofy mustache, and boom.


[Time 0:04:18]

```
   Most problem
statements are bad.
```

The problem, though, is that most problem statements are bad.  And
they are bad in particular ways.


[Time 0:04:28]

```
Stating the problem is
an _iterative_ process.
```

And so getting a problem statement right is an iterative process for
most people.  Now Rich is particularly good at this, so if you play
this game with him, he has this skill, which is: not talking until he
has done his thinking, which is really unfair.  Because I am totally
the opposite.  I definitely talk by way of thinking, and I say
progressively less stupid things until I get to something somewhat
reasonable.

But Rich has this trick where he just sits there [nods and looks
around].  And the look says: those things you other people are saying
seem kind of stupid.  And then eventually he will be like: OK, here is
the problem.

But you actually see this process play out.  Rich is not the original
here.  Sherlock Holmes is the original.  You see this process play out
in the stories.  And one of the important things that you want to do
is separate.  Usually bad problem statements are complected.

[ pauses and looks around at audience ]

I was going to say: everybody has to drink right now.  So.

[takes a drink]

That is water, by the way.  Yeah, water.  You can do what you want.  I
am still on the clock.

So what Holmes does is takes apart problem statements that seem like
simple statements, but are actually compounds.


[Time 0:05:46]

```
"There were no footmarks."

"Meaning that _you saw none_?"


The Adventure of Black Peter
```

And sometimes that is about teasing apart assumptions.  So there were
no footmarks.  Oh, meaning that _you_ saw no footmarks.  So he has
taken what seemed like an idea and broken it into two ideas, which is
that there was somebody looking for footmarks, and they failed to find
any, is an entirely different point than "there were no footmarks".

And this is incredibly important because when we are making problem
statements we often bake in the analysis of the problem, not the
problem itself.  So we say something that combines what the problem
is, with our beginning analysis of the problem, or our presumptions.
Or worst of all, we bake in common sense, which is a terrible enemy of
doing good work.

And a great example of this ...


[Time 0:06:34]

```
 "Yes, but how can we
 get at the criminal's
pocket before we catch
    the criminal?"


The Reigate Squires
```

... is in the story The Reigate Squires, where a policeman says to
Holmes: how can we get at the criminal's pocket before we catch the
criminal?  And the way they actually catch the criminal in this story
is that Holmes says: you know what?  We do not have the criminal, and
we do not know who the criminal is, _but_ if we had the criminal's
pocket we would have the information we need to capture the criminal.

Now everybody else is not capable of using that as a problem statement
because their common sense cuts in.  And what does your common sense
tell you in that situation?  If I do not know who the criminal is, and
I do not have the criminal, there is no possible way I could have the
criminal's pocket.

But Holmes teases those things apart, and once he does that, it turns
out that there is a way in the story -- and you can go read it -- to
acquire this criminal's pocket without acquiring the criminal.  Which
is what they go about doing.

And so it is an iterative exercise, and you need to tease apart the
problem from your assumptions.


[Time 0:07:36]

```
1. State the problem.
```

So the first trick to being a good software developer is to state the
problem.  That is probably unremarkable in a Clojure room.


[Time 0:07:45]

```
slide title: TOOLS

[ Image of cartoon character Inspector Gadget, with many of his
attached tools extending out from his hat and ready to use. ]

https://web.archive.org/web/20190729160619/https://denofgeek.com/us/movies/inspector-gadget/246469/new-inspector-gadget-movie-coming
```

Now the second important thing is that you need tools.  You need lots
of tools.  They need to be super shiny.  You need IDEs and build tools
and debuggers and frameworks.  That is what we all do around here:
tool driven development.


[Time 0:08:03]

```
[ Image from a film with Basil Rathbone playing Sherlock Holmes,
inspecting something through a hand held magnifying glass. ]

https://www.smithsonianmag.com/arts-culture/sherlock-holmes-and-the-tools-of-deduction-10556242
```

Well, and this is in fact supported a little bit in the canon to this
extent.  Holmes is a tool user.  And he is a very good tool user.  And
in fact -- and I did not know this until I was researching the talk --
that Holmes is the first character in fiction to use the magnifying
glass as an investigative tool.

So, but that being said, the magnifying glass kind of gives you a
little bit of insight into the sorts of tools that Holmes goes for.
He is not looking for something big or fancy or shiny or complicated
or enterprisey.  He is looking for something lean and general purpose.
And so even though Holmes does use tools, and he uses other tools as
well, the thing that stands out about him is not that he has more or
better tools than the police, but that he has a small set of tools,
and he uses them extremely well.


[Time 0:08:57]

```
You have evidently seen
more in these rooms
than was visible to me.

No, but I fancy that I
may have deduced a
little more.


The Adventure of the Speckled Band
```

And his best tool is, in fact, his eyes.  And so there is story after
story, poor Watson will say: you seem to have seen something I did not
see.  And Holmes will say: well we both looked at the same thing, but
I did in fact deduce a little bit more.


[Time 0:09:14]

```
 Problems may be solved
 in the study which have
  baffled all those who
have sought a solution by
 the aid of their senses.


The Five Orange Pips
```

Or problems may be solved in the study that have baffled those who
sought a solution by the aid of their senses.  So Holmes would rather
sit and think before even pulling out a tool to begin with.


[Time 0:09:27]

```
the toolset is the least
important part.

the algorithms ... are
fairly simple

that simplicity is a
strength ...


https://pragprog.com/book/atcrime/your-code-as-a-crime-scene
```

And then the toolset is the least important part.  Algorithms are
fairly simple.  And that simplicity is a strength.

OK, that is actually not a quote from the canon.  That is actually
back to the Adam Tornhill book.  But it is in fact the same idea.


[Time 0:09:44]

```
2. Use simple tools.
```

So the second point that I would make is: use simple tools.  And I do
not need to elaborate on this, because there are entire talks in the
Clojure world about simplicity, but I would make the point that these
tools are likely to be small relative to the power that they deliver,
they are likely to be general purpose and to work in a generic way
with data.

Now the next piece of advice I am going to give you has proved
controversial with test audiences.


[Time 0:10:15]

```
slide title: SMOKE!

[ Photo of an actor, I believe Jeremy Brett, playing Sherlock Holmes
lighting up a smoking pipe. ]

https://www.quora.com/What-kinds-of-pipes-did-Sherlock-Holmes-smoke-according-to-Sir-Arthur-Conan-Doyles-writings
```

The third thing you need to do to be a good software developer is
smoke.  And unfortunately, when I say smoke I do not mean smoke a
little bit, or smoke once, or don't inhale.


[Time 0:10:33]

```
 Having gathered these
facts, Watson, I _smoked
several pipes_ over them,
trying to separate those
which were crucial from
   others which were
   merely incidental


The Crooked Man
```

I actually mean smoke a lot.  So when you have a problem, you need to
smoke several pipes.  Cigarettes are OK, too.  But pipes are good.


[Time 0:10:47]

```
    For a whole day my
   companion had rambled
  about the room with his
chin upon his chest and his
 brows knitted, _charging
 and recharging his pipe_
 with the strongest black
         tobacco.


Silver Blaze
```

And this is the kind of thing that you could do all day.  You could

[walks around stage gesturing as if smoking]


[Time 0:10:56]

```
3. Smoke.  A lot.
```

So without further ado, or explanation, or justification, I am just
going to say that you need to smoke a lot.

Now happily, for the most part, Rich is a shifty character who is just
trading on Sherlock Holmes's fame in building Clojure and Datomic and
things like that, but this is an area where Rich actually provided a
healthful innovation, ...


[Time 0:11:20]

```
[ Photo of trees all around, looking up from the ground towards the
sky. ]


                                             Hammock-Driven Development
```

... which is instead of smoking, you can use hammock time.  So hammock
time is a non cancer causing substitute for smoking.  But it actually
accomplishes the same purposes.  It gives you the opportunity to let
the stuff that you have loaded into your background mind percolate and
develop ideas.

And once you realize that smoking was the one that Holmes liked, ...

[Time 0:11:47]

```
nicotine time [with strike through line]
hammock time
```

... and that hammock time is the one that Hickey liked, one thing you
might conclude is that your name actually has to start with H to be
good at this game, ...


[Time 0:11:57]

```
[ Photo of a river with grass and trees on both banks, and a grassy
path along one side. ]


                                      Trail-Run-Driven Development
```

... which is why Halloway actually prefers trail run driven
development.  So the thing that really works for me ...


[Time 0:12:03]

```
nicotine time [with strike through line]
hammock time [with strike through line]
trail run time
```

... is going out on a trail and taking a three mile run, or five mile
run.  I wish my legs would let me do longer than that, because it is
actually where the work gets done.  So as I become more aerobically
fit, I write better software, which is sort of a win-win.

But the idea is to give your mind the freedom to work.  And Rich has
given an entire talk about this, Hammock Driven Development.

[ https://github.com/matthiasn/talk-transcripts/blob/master/Hickey_Rich/HammockDrivenDev-mostly-text.md ]

The one point I would bring up from that talk, to remind you of here ...


[Time 0:12:30]

```
  One should always look
for a possible alternative
  and provide against it.


The Adventure of Black Peter
```

... because Holmes thinks about it a lot, is that when you are doing
this work you need to consider multiple alternatives.  One of the
things that vanishes in implementation, and in a lot of architecture
diagrams and other kinds of artifacts and documentation, is the
consideration of alternatives.  And when you have a theory about a
crime, you need to have your second best theory, and you need to know
why your first best theory is better than your second best theory.

When you have a plan for software that you are going to build, you
need to have a plan that says: if I were forbidden to use this plan,
what would my next plan be, and what would its characteristics be, and
why do I like my first best plan better?

But as a code word for these ideas, just remember: smoke a lot.


[Time 0:13:15]

```
slide title: TRIFLES

[ Drawing of Holmes and Watson sitting on chairs near each other,
perhaps engaged in some conversation. ]

https://www.theguardian.com/books/2013/jan/04/mastermind-maria-konnikova-review
```

Whether your problem is a crime or a program, your reasoning must
account for everything.  In particular, the word that Holmes likes to
use is "trifles".  You must account for trifles that initially seem
unconnected to the problem.  And when you are reading the Holmes
stories, the word trifle is a literary tip that Holmes is about to
out-perform everybody else.


[Time 0:13:42]

```
   "The incident however,
was _too trivial_ to relate
  and can have no possible
   bearing upon the case.


The Adventure of the Noble Bachelor
```

Whenever a witness says: well, I almost did not think this was worth
mentioning, because it cannot possibly be related to the case.  It was
just too trivial.  You can rest assured that that is going to be a
lynch pin in actually solving the problem.


[Time 0:13:58]

```
 "there is nothing so
important as _trifles_"


The Man with the Twisted Lip
```

And Holmes says it again and again.  There is nothing so important as
trifles.


[Time 0:14:04]

```
 "You know my method.  It
   is founded upon the
_observation of trifles_."


The Boscombe Valley Mystery
```

You know my method.  It is founded upon the observation of trifles.

And ...


[Time 0:14:09]

```
"Does your explanation
  cover every point?"


The Adventure of Black Peter
```

Does your explanation cover every point?  This is a thing that
software developers mess up over and over again.  You have ten pieces
of information at your fingertips about a problem, and you have a
theory that is supported by nine of those pieces of information, but
outright contradicted by the tenth piece of information, which
admittedly is the least important most minor detail of all of that
information.

So choice A, you are like: well hey, 90 per cent.  That is a B plus or
an A minus.  We should just proceed forward.  Or choice B, you have to
think longer.  And in my work in support I can tell you that anybody
who has ever worked in support, what do people do?  They are like:
well, there was a problem, and I did not know what was going on, so I
did stuff.


[Time 0:15:05]

```
4. Account for details.
```

So the fourth thing to remember is: account for details.  You have to
account for all the trifles.  And it is often the case that our biases
have us want to look at the information that is most exciting, that is
most emotionally charged.  The pool of blood on the floor is a lot
more interesting than the little trail of dust on the window sill.
But when you are doing problem solving, it is not about the thing that
is biggest, it is about how the things all relate together.  And they
_all_ have to work.  They cannot mostly work.


[Time 0:15:47]

```
[ Photo of Benedict Cumberbatch as Sherlock Holmes. ]

MIND PALACE, ANYONE?
```

So this is great, but there is a problem.  You can make your problem
statements.  You can have good tools.  You can use them carefully.
You can smoke a lot.  And you can account for all the trifles.

But deep down where you do not want to look, you are just afraid that
Sherlock Holmes is smarter than you are.  And that the actual reason
that Sherlock Holmes can solve these cases, and the actual reason that
the top performing developers can write software is: they have an
enormous mind palace that you simply do not have, and it is a gift
from nature that you cannot get.


[Time 0:16:30]

```
"I can distinguish at a
 glance the ash of any
 known brand, either of
  cigar or of tobacco"


A Study in Scarlet
```

And the canon supports this idea.  Holmes has things that in
individual citation do not seem like super powers when you start
listing them.  So here is one: I can distinguish at a glance the ash
of any brand of cigar or tobacco.  And in a culture where everybody is
smoking, this is pretty useful in identifying crimes.


[Time 0:16:54]

```
"It would be a poor
expert who could not
 give the date of a
 document within a
    decade or so"


The Hound of the Baskervilles
```

Or: It would be a poor expert who could not give the date of a
document.  And by this the power I am describing is: I could look out
into the room and tell how old pieces of paper were that were in your
hands.  That one is 15 years old.  That one is 35 years old.


[Time 0:17:10]

```
"has shown me splashes
upon his trousers, and
told me by their colour
and consistence in what
 part of London he had
    received them"


A Study in Scarlet
```

Or my personal favorite, Sherlock Holmes was the world's leading
expert in his time in a little known field: trouser splash
geolocation.  And so the way this works is you look at somebody's
trousers from across the room, and you have a complete Google maps
story in your head of where they have been.

And the stories enumerate these unusual skills again and again.


[Time 0:17:37]

```
[ Another photo of Benedict Cumberbatch as Sherlock Holmes. ]

PROBABLY SMARTER THAN YOU
```

And so the bottom line is: there are a few people who are superhuman,
and they are gifted, and they can do this stuff, and the rest of us
cannot.

But that is not where the canon stops.  And in fact, mind palace is
probably the most insidious phrase to work its way into pop culture
from the Sherlock Holmes stories, because that is _not_ what Sherlock
Holmes calls his head.


[Time 0:18:01]

```
I say now, as I said then, that
a man should keep his _little_
 brain-attic stocked with all
the furniture that he is likely
  to use, and the rest he can
  put away in the lumber-room
 of his library, where he can
     get it if he wants it.


The Five Orange Pips
```

He calls it a little brain-attic.  A little teeny weeny brain attic.
And the point that Holmes makes about his brain attic, when he is
asked, not only: it is not large, it is small.  But his superpower is
in _not_ putting things in there.  His super power is not in putting
things in there.  It is _avoiding_ putting things in there.  It is
avoiding exposure to information that will waste the very tiny space
in his mind palace.

This is the Victorian equivalent of stay off Facebook and Fox News.

But in fact it goes further than that.  Not only does he avoid
exposing himself to information that is not going to help him solve
crimes, he even avoids perfectly useful information that might be
distracting.

At one point, Watson finds out that Holmes does not know if the Earth
goes around the sun, or if the sun goes around the Earth.  And he is
appalled, because all smart Victorians of course know the facts of
this case.  And Holmes says: "Not only do I not know that, I am going
to endeavor to forget it."  Because he does not perceive that that is
going to be useful in solving crimes.

Now, OK, so he has a tiny mind-attic, not an enormous mind palace.
And he has chosen to furnish it with the things that are important for
his job.  That is a good lesson.  But the other thing that he does --
and I think that it is quite clear in the canon, but a little hard to
see in TV and movies, is ...


[Time 0:19:36]

```
"Kindly look her up in
  _my index_, Doctor"


A Scandal in Bohemia
```

... he writes things down.  Holmes is an inveterate logger and keeper
of information.  He maintains an index of every past case.  He will
not talk about cases that are not the current case unless he is first
given time to go and read the index, and ponder it, and reload the
context.  Anybody who has had to work on software that they wrote
three years ago knows exactly what we are talking about here.


[Time 0:20:04]

```
"You will find parallel
     cases, if you
   _consult my index_"


A Case of Identity
```

So he is constantly suggesting not: I have encyclopedic memory of every
case that I have ever worked on, but: I have written things down.


[Time 0:20:13]

<img src="SherlockHolmesConsultingDeveloper/Map-from-The-Adventure-of-the-Priory-School.png" alt="Drawing of a map of an area investigated by Holmes for a case.">
```
The Adventure of the Priory School
```

Holmes likes to draw maps, and he likes to use maps.


[Time 0:20:18]

```
   Holmes had _taken
several notes_ during Mr.
   Harding's evidence


The Adventure of the Six Napoleons
```

And he likes to take notes while he is interviewing witnesses and
suspects.  And perhaps the best single indicator of Holmes as a normal
person accomplishing extraordinary things ...


[Time 0:20:33]

<img src="SherlockHolmesConsultingDeveloper/Encrypted-Message-from-The-Adventure-of-the-Dancing-Men.png" alt="Drawing of stick figures of men in different positions, like dancing.">
```
The Adventure of the Dancing Men
```

... comes in The Adventure of the Dancing Men, when he has to
cryptanalyze the messages of the dancing men.  If Holmes were the kind
of savant that we cannot approach, he would stare at these dancing
men, and there would be some weird camera effects, and some cool
soundtrack music by a hip composer, after which the answer would just
appear to him.

But that is not at all what happens in the story.  What Holmes
actually does is what you or I or anybody else might do: he sits for
hours and fills a wastebasket with scrap paper, as he works out on
paper the frequency analysis.  I am going to start by guessing the
most common character is E and see where that takes me.  And then I am
going to go down this road.  He does what an ordinary person who is
careful and methodical would do.


[Time 0:21:24]

```
[ Photo of Dustin Hoffman playing his character in the movie Rain Man,
standing next to Tom Cruise as his brother.  There is a big red X over
the whole photo. ]

https://www.empireonline.com/movies/reviews/rain-man-review/
```

So Holmes is not at all Rain Man.  And in fact, the character in
fiction, or in TV and movies, that he most reminds me of ...


[Time 0:21:34]

```
[ Photo of Arnold Schwarzenegger as the T800 in the movie Terminator
2. ]

I HAVE DETAILED FILES

https://imgur.com/gallery/1oaCIOu
```

... is the T800.  He maintains detailed files.  Maintaining detailed
files is not a savant like super power.  You can do that, too.


[Time 0:21:46]

```
5. Write things down!
```

So my fifth piece of advice to you is to write things down.

It is stunning to me ... I know this sounds trite, and I get up once a
year in front of an overlapping group of people and keep telling
people to write things down.  When you do not write things down, you
are basically saying: I can outperform other people who are writing
things down while juggling chain saws in my head.  And developers do
this all of the time.  They wrestle with problems, and they do not
just write things down.  So I cannot underscore this point enough.


[Time 0:22:19]

```
[ Photo of Robert Downey, Jr. as Sherlock Holmes ]

SHERLOCK HOLMES, ACTION HERO

https://www.comingsoon.net/movies/news/944053-sherlock-holmes-3-release-date-set-for-christmas-2020
```

Now you have stated a problem.  You have iterated on it.  You have
used your universal tool kit to collect some information.  You have
arisen from your hammock empowered with new ideas.  You have written
down a careful plan, including multiple alternatives.  Now is time to
kick some ass.

And this in fact is a thing that Holmes does, and it is totally
supported in the canon.  He is a decent shot with a pistol and a
rifle, although that is not something that comes up that often,
because Watson is a crack shot.  So Watson usually gets that job.  But
he is also a very good stick fighter and boxer.


[Time 0:22:56]

```
"It was a straight left against
a slogging ruffian.  I emerged
 as you see me.  _Mr. Woodley
     went home in a cart_."


The Adventure of the Solitary Cyclist
```

And not only is he good at those things, he positively enjoys them.
He is flushed with delight as he tells Watson how he beat the crap out
of a ruffian.

And so what are we to make of this?  Well first off, yay!  That is
cool.  Action movie time.  I think the modern analog to this ...


[Time 0:23:16]

```
[ Amazon logo ]

Bias for Action

Speed matters in business.  Many decisions and
actions are reversible and do not need extensive
study.  We value calculated risk taking.

https://www.amazon.jobs/en/principles
```

... might be Amazon's bias for action.  I am not sure if any of you
have ever interviewed for a job at Amazon, but one of the things that
Amazon tells you -- they actually have a web site and you can go read
this -- is: speed matters in business.  Decisions and actions are
reversible.  We do not need a lot of study.  We need action.  Action,
action, action.  Gunshots.  Stick fights.  Beating up ruffians.

[ Big red X appears over the slide. ]

This is a terrible idea.  Amazon is completely wrong about this, which
is why Jeff Bezos is where he is, and where I am.  Hmmm.

[Audience laughter]

He just got lucky.  He is still wrong.  Act a little less.  Think a
little more.


[Time 0:24:03]

```
  "the art of the reasoner
  should be used rather for
the _sifting of details_ than
  for the acquiring of fresh
          evidence"


Silver Blaze
```

Holmes swings into action, but he thinks first.  He sifts the details.


[Time 0:24:10]

```
  "... how dangerous it
always is to _reason from
    insufficient data_"


The Adventure of the Speckled Band
```

And in fact, Holmes stops working entirely when he does not have good
information.  When he does not have good information, he puts it on
the shelf.  Alex Miller I am sure remembers how long the ideas that
became spec sat on the shelf in people's heads until they came
together as something that actually became code.  It was a period of
years.


[Time 0:24:30]

```
"we can do nothing until
  the answers to those
letters come, so we may
_put our little problem
upon the shelf_ for the
        interim"


A Case of Identity
```

Holmes says: you know what?  We are going to put the problem on the
shelf, and he goes and does something fun.  He says: I do not have
what I need to solve this problem right now.


[Time 0:24:38]

```
   One of the most remarkable
characteristics of Sherlock Holmes
  was his power of throwing his
brain out of action and _switching_
  all his thoughts on _to lighter
 things_ whenever he had convinced
  himself that he could no longer
         work to advantage


The Adventure of the Bruce-Partington Plans
```

And Watson, in fact, calls attention to this quite explicitly.  He
says: Sherlock Holmes just puts his brain into neutral and goes and
does something fun when he does not have the information he needs to
move forward.

Conversely, who in the Holmes stories has a bias for action?  It is
not Holmes.


[Time 0:24:59]

```
[ Photo of actor Rupert Graves as Inspector Lestrade. ]

https://www.youtube.com/watch?v=2yMJ498FEH0
```

It is poor Lestrade.  Lestrade is always moping about.


[Time 0:25:04]

```
[ Photo of actor Eddie Marsan as Inspector Lestrade. ]

https://bakerstreet.fandom.com/wiki/Inspector_Lestrade_(Marsan)
```

All of his different fictional incarnations, swinging into action.
And Holmes characterizes that action ...


[Time 0:25:11]

```
  Oh, how simple it would
  all have been had I been
    here before they came
like a _herd of buffalo_ and
   _wallowed_ all over it.


The Boscombe Valley Mystery
```

... as a herd of buffalo wallowing all over the evidence and ruining
it.

So yes, you are going to act.  Eventually if you are writing software,
some fraction of the time you are going to be presented with a problem
and say: you know what?  This problem actually could benefit from some
software that does not exist that I know how to write.  But when it
comes time ...


[Time 0:25:32]

```
6. Act with precision.
```

... act with precision.


[Time 0:25:34]

```
slide title: Program Like Holmes

1. State the problem.

2. Use simple tools.

3. Smoke (A lot).

4. Account for the trifles.

5. Write things down.

6. Act with precision.
```

So that is it!  If you want to code like Holmes, come up with a good
problem statement, prefer simple tools, smoke a lot, account for
trifles, write things down, and act with precision.

Awesome.


[Time 0:25:52]

```
slide title: PERSONAL HABITS?

[ Photo of Robert Downey, Jr as Sherlock Holmes ]

[ The following URL does not work as of 2020-Oct, but I do not know if
the material was taken down since the talk was prepared, or if I have
a different URL than given in the talk. ]
https://www.youtube.com/watch?v=PzqnDMIhKyw
```

It is possible, though, that something about this combination of
things leads you to be a very oddball person.  And the movies
certainly give Holmes a comically manic personality.  He pursues both
criminal cases and his other avocations with feverish energy.  And the
canon supports this.  When Holmes is working on a case ...


[Time 0:26:16]

```
I have had nothing since
breakfast.

Nothing?

Not a bite.  I had no time to
think of it.


The Five Orange Pips
```

... he does things like forget to eat breakfast.


[Time 0:26:20]

```
  he had never worked less
 than fifteen hours a day ...
and kept to his task for five
      days at a stretch


The Reigate Squires
```

He does things like work fifteen hours a day for five days at a
stretch.  That is what we in the agile community call a sprint.

But that is only part of the story.  Holmes activates like that when
he knows there is a moment in time when you have to move quickly
because the facts and the criminals are getting away.  And then when
that is not the time, he chills.


[Time 0:26:53]

```
I think that I shall have
 a whisky and soda and a
  cigar after all this
   cross-questioning


The Adventure of the Noble Bachelor
```

And he says: you know what?  I think we should have a whisky and soda.
Interrogating this witness has gotten me kind of tired.


[Time 0:27:00]

```
  we shall have horrors
enough before the night is
 over; for goodness' sake
 let us have a quiet pipe
 and turn our minds for a
  few hours to something
      more cheerful.


The Adventure of the Speckled Band
```

Or: we are going to have to go out and catch the bad guys tonight.  We
should just sit around and smoke -- there is the smoking again -- and
just turn our minds to something more cheerful.


[Time 0:27:10]

```
 Let us walk in these
   beautiful woods,
Watson, and give a few
hours to the birds and
     the flowers.


The Adventure of Black Peter
```

Or: bird watching.  Not the Holmes you think of if you are watching
the movies.  We are going to stop in the middle of the case.  We are
going to do a little bird watching and take a hike.  So in addition to
all of these other things ...


[Time 0:27:22]

```
slide title: ENJOY YOUR LIFE

[ Photo of woods next to a body of water. ]
```

... you need to enjoy your life.  It is fine to work hard part of the
time, but then you should play hard, and then you should chill the F
out.  Go outdoors.  Be still.  Be quiet.

The other thing besides the workaholic idea that is associated with
Holmes is that both he and Mycroft ...


[Time 0:27:49]

```
slide title: PEOPLE SKILLS?

[ Photo of Stephen Fry as Mycroft Holmes, and Kelly Reilly as Mary
Watson, in a scene from one of the movies where Robert Downey,
Jr. plays Sherlock Holmes, where Stephen Fry is naked and speaking to
her as if nothing is out of the ordinary. ]

https://emmabauer.wordpress.com/2012/06/24/naked-in-the-locker-room/
```

... are lacking in people skills.  Now if you remember this is
actually Mycroft, not Sherlock.  That was the best picture.  This is a
scene from one of the movies that underscores the fact that the Holmes
brothers are not entirely aware of what is appropriate attire.

And so there is an idea, and of course this goes with the whole savant
genius thing, right?  If you are really good at something, then you
must also have a low social IQ.  You spent all of your, like -- it is
like a role playing game -- you spent all of your resource allocation
points on being incredibly awesome at this one skill, and you had
nothing left over for social IQ.


[Time 0:28:26]

```
It was one of my friend's
  most obvious weaknesses
that he was impatient with
 less alert intelligences
       than his own.


The Adventure of the Bruce-Partington Plans
```

And you see that in the canon.  Watson complains that Holmes is not
patient with dummies.  When people have dumb ideas he is not patient
at all.  And Holmes says mean things to people ...


[Time 0:28:40]

```
 I am disappointed in
Stanley Hopkins.  I had
hoped for better things
 from him.  One should
   always look for a
possible alternative and
   provide against it.


The Adventure of Black Peter
```

... when they have dumb ideas.  I am so disappointed in Stanley
Hopkins.  I had hoped for better things from him.  One should look for
a possible alternative and provide against it.

Now actually, in Holmes's defense, he did not say that to Hopkins's
face.  So he was actually complaining privately to Watson, which shows
social IQ, right?  He is not venting to the person he is upset with.
He is actually turning to Watson and saying that in a side bar.  That
would make you feel better until you see what he actually ...


[Time 0:29:09]

```
 I understand, however,
 from the inquest that
there were some objects
  which you failed to
       overlook?


The Adventure of Black Peter
```

... said to Stanley Hopkins's face, which is: I understand, however,
that there were some objects which you failed to overlook?  Which you
scratch your head for a second, and then realize that you are being
insulted.

But there is an important point here, which is that Holmes, when he is
demonstrating low social IQ, if you want to call it that, 100% of the
time as far as I can tell in the stories, his anger is directed at
poor work and incompetence by other people who are doing the job he is
doing.  Other people who are trying and not doing a very good job, and
causing people to come to harm because they are not tracking down
crimes.

Holmes has a perfectly high social IQ when he is talking to victims or
witnesses.


[Time 0:29:57]

```
    Sherlock Holmes
 welcomed her with the
easy courtesy for which
   he was remarkable


A Case of Identity
```

And so you see Watson saying things like: Holmes welcomed her with
easy courtesy ...


[Time 0:30:02]

```
  Sherlock Holmes sat
down beside him on the
 couch and patted him
kindly on the shoulder.


A Case of Identity
```

... or: he sat down on the couch and patted him kindly on the
shoulder.


[Time 0:30:07]

```
  Sherlock Holmes was a
past-master in the art of
    putting a humble
     witness at ease


The Adventure of the Missing Three-Quarter
```

Or even: He is a past-master in the art of putting the witness at
ease.

So now here I think we should part ways with Holmes.  I think it is OK
to be nice to your coworkers as well as your stakeholders, but the
point that I want to make is that Holmes has a social IQ.  He has a
set of social skills, and he is making choices about when to use them.
All of the other things that have to do with being an excellent
detective or an excellent programmer are really orthogonal to these
social skills.

And so you could, as Holmes does to victims and even to criminals ...


[Time 0:30:46]

```
slide title: BE NICE

[ Photo of a sign on a wooden post next to a trail with some kind of
drawing of a hiker on it. ]
```

... you could be nice.  And you should be nice.


[Time 0:31:00]

```
[ Photo of actor Jeremy Brett playing the part of Sherlock Holmes. ]

Favorite Programming Language?

https://falconmovies.files.wordpress.com/2014/07/jeremy1.jpg
```

Since this is a software conference, you are probably wondering: what
is Sherlock's favorite language for programming?


[Time 0:31:13]

```

 From Holmes ...  |  ... to Clojure Community Talk
------------------+----------------------------------------
state the problem |      Hammock-Driven Development
   simple tools   | Simple Made Easy, Running With Scissors
   hammock time   |      Hammock-Driven Development
      trifles     |  Debugging with the Scientific Method
write things down |  Debugging with the Scientific Method
bias for planning |      Hammock-Driven Development
work/life balance |      Stewardship Made Practical
```

And I think it is pretty clear that Holmes spent a lot of his time
laying groundwork for the Clojure ecosystem.  That all of the ideas
that I have stated today about problems, and simple tools, and hammock
time, and trifles, and writing things down, and work/life balance, all
of these things are ideas that have traction in the Clojure community
because we as a group have worked hard to make that the case.


[Time 0:31:45]

```
[ Photo of actor Jeremy Brett playing the part of Sherlock Holmes. ]

Sherlock Holmes: Clojurian

https://falconmovies.files.wordpress.com/2014/07/jeremy1.jpg
```

And so I would like to be the first to welcome Sherlock Holmes into
our community as the O.G. Clojurian.


[Time 0:32:02]

```
[ A different photo of actor Jeremy Brett playing the part of Sherlock
Holmes. ]

Favorite Database?
```
[ https://niklasblog.com/?p=20073 ]

That said, you are probably wondering what his favorite database is.
Well we have less evidence about this, but ...


[Time 0:32:12]

```
 "He had a _horror of
destroying documents_,
especially those which
were connected with his
      past cases.


The Musgrave Ritual
```

... he has a horror of destroying documents, especially those that
were connected with past cases.  So it is pretty clear that Holmes
would only have ever worked with an immutable database that kept a log
...


[Time 0:32:29]

```
[ Datomic logo ]

Datomic
```

... and then provided an index where you could get back to your
information.


[Time 0:32:35]

```
slide title: You don't have to

+ be a genius

+ or a jerk

+ or work 15-hour days

+ in solitude
```

So you do not have to be a genius or a jerk, or work 15-hour days in
solitude to be a good programmer, or a great programmer.


[Time 0:32:44]

```
slide title: But you should

+ have an objective

+ seek simplicity
                        + enjoy your life
+ take hammock time
                        + be nice
+ master the trifles

+ write things down

+ act with precision
```

But you should have an objective.  Know what you are doing.  Say it
out loud.  Have a plan.  Find a problem that you care about and work
on it.  You should seek simplicity in your tools and in your approach
to the problem.  You should take nicotine time or hammock time or run
in the woods time, or whatever works for you.

You should master the trifles.  Good design has to account for all of
the pieces, not just some of the pieces.  You should write things
down.  And when you have done all of those things and you choose to
act, you should act with precision.

And you should balance that with enjoying your life and being nice.


[Time 0:33:22]

```
[ Photo of woods by a body of water. ]


                 Brumley Nature Preserve
```
[ Brumley Nature Preserve is in North Carolina in the USA, between
Durham and Hillsborough. ]


Enjoy the rest of the evening.  Thank you.

[Audience applause]

[Time 0:33:28]
