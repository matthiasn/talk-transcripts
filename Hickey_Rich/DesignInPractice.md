# Design In Practice

* **Speaker: Rich Hickey**
* **Conference: [Clojure Conj 2023](todo) - April 2023**
* **Video: [https://www.youtube.com/watch?v=fTtnx1AAJ-c&list=PLZdCLR02grLpIQQkyGLgIyt0eHE56aJqd](https://www.youtube.com/watch?v=fTtnx1AAJ-c&list=PLZdCLR02grLpIQQkyGLgIyt0eHE56aJqd)**
* **Slides: [https://download.clojure.org/presentations/DesignInPractice.pdf](https://download.clojure.org/presentations/DesignInPractice.pdf)**


[Time 0:00:00]

```
slide title: Design in Practice

Rich Hickey
```

Thanks everyone for coming.  It is so great to see all the old
friends, and all the new friends, and especially all the very cool
things everyone is doing.  I want to doubly thank Alex for scheduling
a talk before mine that was so full of amazing graphics that no one
would possibly be able to bear any more, and I could I could leave
them out of my talk.

[Time 0:00:26]

```
slide title: Objective - Demystify Design

            not (just) going to the hammock
                 practice - 'what you do'

concrete techniques with tangible outputs
demonstrate _progress_ 'walk forward'
activities you can make PM stories out of

  thus make time for, throughout the dev process

  not pleading for 2 weeks of nebulous 'hammock time' up front

valuable artifacts that make the effort evident

tips and techniques, not a formal method or anything highfalutin
```

So this is Design In Practice, and the objective here is to demystify
design somewhat.  I think I have given a few talks in the past that
were about a lot of the ideas in design, but left the concrete
practice of it sort of underspecified.  And it has led to maybe a
certain imagined magicness to design that I want to dispel.  I think
design is something that you can learn to do.  I think it is something
that has concrete activities, practices, or things that we do.

Oh, by the way, if you are playing word definition Bingo, you are
going to wish you had more than one card today.

And to try to talk you through some of what I think are kind of
lightweight things that we do, actually really do, in trying to do
design as a team on Clojure and Datomic as we work.  So we are talking
about concrete things.

Another thing I want to do is talk about things that you can make into
activities.  I think a lot of people struggle when they say, "well, we
want to do more design in our shop, but we can never get it
justified."  We are saying nebulous things like, "I want to take two
weeks off and think about the problem before we start."  And even if
you get that, two weeks at the beginning is not necessarily what you
are going to need.

So one of the things that is good about reifying activities is that
they can become things that go into your project management system as
stories that you are going to do that will have outputs.

The other thing I want to talk about today is progress.  A lot of
times people say, "I know what design is.  I have seen people doing
planning sheets, or diagrams, or things like that.  But I do not
really have a sense of: Did I write the right diagram?  Am I
accomplishing something?"  When we make software, we see it accrete,
and we see it do more and more stuff every day.  And when we design,
what does it mean to move forward?  Do we know we are moving forward,
or just spinning around?

So this is not any kind of method.  I do not want to adopt that.  I am
not trying to rain on proper methods.  And there are there are plenty
of really cool design methodologies out there.

[Time 0:02:39]

```
slide title: Design

              design - Latin for 'waiting to code'

_coding happens throughout_

performing experiments

answering interim questions

why you want a language that supports exploratory programming
without being in a project building context
```

So we all know, I am just reminding you, Latin for "design" means "not
being allowed to code".

[Audience laughter]

I do not actually think that is true.  In fact, I think that as we
will see as we go through the talk that you do coding throughout the
design process.  Not necessarily starting to write your system, but
exploring what your system might become, learning about the things
that are going to be parts of your system, answering questions, and
things like that.  And it is one of the reasons why I think it is
important to work in a language where that kind of work has zero
project-y kind of overhead.  That you do not need to have started your
thing, or be in a project context to start doing exploratory
programming.  You open up your editor and you go.

[Time 0:03:28]

```
slide title: Design (cont.)

                'mark out, a plan'

the emphasis in this talk is about supporting your (team's) reasoning _process_,
      not just the end-product blueprint-like design

_writing down_ your thoughts helps you form them

       _techniques can guide your thinking and decision-making_

  reified/refined/shared concepts

  onboarding/resumption

  validation

  eventually, documentation
```

No.  So really "design", the word means to "mark out a plan for doing
something", or at least the meaning that we are going to use in this
talk.  I am going to expand that idea to be the entire set of steps
that get you from a sense that something should happen in the world,
to the ability to mark out that plan, the marking out of the plan, and
then hopefully the subsequent development of it.

And this marking out is something I think is going to be super
critical.  We are going to be writing all the time.  We are going to
be putting text in front of our faces and in front of the faces of our
teammates so we can see what we are thinking about.  And I think this
is something that is very important for helping you think in the first
place.

This is not an archival activity.  This is not about capturing things
for posterity.  It is not about creating documentation as you go or
anything like that.

This is about writing as part of thinking.  Putting something down on
paper makes it a thing.  It is something that you can then look at and
now it becomes an input to you, even though it started in your own
head.  It also helps you pick things up when you have left them around
for a while, or allows people to join you in your work.  And then
maybe eventually you will turn it into something that you will use to
document what happened in the end.

[Time 0:04:48]

```
slide title: Words

           Choose good words, _all the time_
     not about bikeshedding or premature marketing

precision in naming == precision in thinking 'before + cut'

          _eschew nicknames, superheroes etc._
               not semantic/meaningful
               give cover to fuzziness
            don't track evolving thinking

_be succinct_ 'gird/gather up'
brief, clear and complete
not just concise 'cut off', or merely hinted at
```

So we are going to be writing.  We are going to be talking, but
especially writing words down, hopefully, and we can write diagrams
down, too.  And I think that choosing good words is super critical.
It is something you should do all the time.  And I am not talking
about picking the right name for your product or anything like that,
or doing something that is about marketing.

It is about choosing words that have the meaning that you intend and
that help everybody come to a shared understanding of what you mean
when you say something.  This idea of precision and cutting is going
to come up all the time.  That "cis" part is about cutting.  It is the
same part of "decide".

So we we need to be precise when we are saying things so we know what
is the thing we are saying, and what is not the thing we are saying.

So I do not like nicknames.  No superheroes or anything like that.
One of the most horrifying things was arriving at a project and
finding a diagram of the project that was: nickname in a box, nickname
in a box, nickname in a box, with unlabeled arrows pointing from one
to the other.  You are not helping anyone else, and you are not
helping yourself.  These names are not semantic.

And in particular by not being a meaningful name, it means that it
does not have to change when you change your mind.  I called it
"Kryptonite" or something, "The Flash", and if I change what I am
doing it could still be called "The Flash".  It will be fine.  So you
want to use precise words.

And the other thing you are going to need to be able to do often is
say something rather involved in not much space.  And I think that is
another critical skill.  You are going to see me say "succinct" over
and over and over again in this talk, and it is important to sort of
understand what that means.  Which I did not know what it meant you
know from an etymology standpoint, so I looked it up.  It means to
gather up your toga before battle.  To gird or gather up.

And the important thing is that what you are gathering up when you are
trying to be succinct is the entirety of things.  It is not about
being concise.  It is not about being: I have only got six words to
say here, so I have got to leave out the critical details because I
need to get it done in six words.  So we are going to gather up our
thoughts.

[Time 0:07:08]

```
slide title: More Words

      _use the dictionary_ (not just good for writing keynotes)
                      _go right to the origins_
                  - most useful/abstract semantics
              - discover the composition within words

a good word later becoming 'wrong' could mean:

  you've changed your mind w/o acknowledging it

  you are drifting from your intentions

    _your thinking will evolve and your words (story titles etc) should also_
```

The other thing is this dictionary thing.  It is not just good for
writing talks.  It is good every day.  We do actually use the
dictionary while we work.  We get to a point where we need to name
something and we will take out the dictionary.  Everybody is racing
through the thesaurus and trying to find the right word.  And a good
word -- I cannot state how wonderful I think that is and I encourage
everybody to go do it.

And especially to get down to the origins where they break apart,
because origins will always show you that most of the words that we
use are composite and that prepositional prefix part is full of really
interesting things.  Like: Is it towards something?  Is it away from
something?  Is it moving stuff together?  Is it cutting it apart?

I think that doing this fires up the process of abstraction.  You
start thinking about things in a way that is not tied to the details,
but more about bigger ideas.

The other advantage of using precise words is that you could be
looking at this word and trying to communicate something, and it
becomes evident that that word is the wrong word.  It might have been
a good word.  And it might be that, in a perfectly fine way, you have
changed your mind.  You have evolved your thinking.  You have got some
new information and you are doing something different.  But the great
thing is if you have been using precise words, they will seem wrong
and you can pause and pick a better word.

[Time 0:08:38]

```
slide title: Technique: Glossary

        _terms are inevitable in tech_
             valuable shorthand

don't presume a shared understanding

  define, in one place

  use uniformly and consistently

helps non-tech folks trying to follow along

_when terms break, fix or abandon_
```

All right.  So we are going to have our first technique.  The first
technique is: add a glossary to your set of stuff that you are
building while you are working.  We are going to have all kinds of
terms and technology that is going to happen.  It is amazing even
amongst technologists, we will say a word, and everybody in the room
will have a different idea in their head, even though they have heard
it and used it over and over and over again.  So do not presume that
everybody understands what you are saying.

You want a place where you define things, one place where you define
things, and then after you have defined it you want to use it
consistently.  Do not use words to mean two different things.  Do not
be lax about that.

This is hard to do, I think, in general, so it is an objective.  No
one does it perfectly.  This is stuff to aspire to.

And then the other thing is if something breaks, fix it or drop it.
So some of these artifacts and some of these techniques are things
that are ephemeral.  You are going to do them and and you are going to
move on.  But this is one that you have to maintain.

[Time 0:09:39]

```
slide title: Example: Glossary

Term         Meaning

locality     A property of data: It is a measure of the distribution
             of datoms you need to find, across segments as seen from
             the perspective of one of the indexes.

affinity     A strategy for assigning partitions, where you say that
             things are related and should be in the same partition,
             and thus grouped together in storage

             (could be coaligned with another entity, with time, with
             a value, with a batch)

partition    See https://docs.datomic.com/on-prem/schema/schema.html#partitions
             Partitions group data together (in storage), providing
             locality of reference when executing queries across a
             collection of entities.
             Entities in the same partition to sort and be stored
             together in E-leading indexes, i.e. EAVT and AEVT.
             Partitions are associated with entity ids, and are named
             by keywords, or referred to by index in a space.
             Encoded as hi bits in entity ids.
             Partition entity ids are suitable as arguments to
             d/terpid, d/entid-at, and :db/force-partition

explicit partition
             partition associated with an explicitly-created, named
             partition entity
              datomic comes with 3 explicit partitions: :db.part/db
             :db.part/user and :db.part/tx

implicit partition
             a partition that can be referred to by its index in a
             range of integers 0<=x<524288.  These partitions have
             entity ids, and they require no explicit installation.
             Their entity ids consist of: part=index with the 20th bit
             set, eidx=0

             In larger applications, you may want to spread data
             across a larger number of partitions.  Implicit
             partitions provide a mechanism for this.
             Implicit partitions provides a way to manage a large
             number of partitions numerically and algorithmically.

             old ref to partition sharding

primary      the owning side of affinity, use to choose partition for
             related (e.g. the customer)

related      the "owned" side of affinity, gets partition from primary
             (e.g. some activity entities related to a particular
             customer)
```

So this is an example glossary.  You probably cannot see that.  I
think I worked on how I can make you be able to see a little more.
But this is a real one talking about a feature.  We have a bunch of
very specific words that we are using to talk about locality,
affinity, and partitions in Datomic.  And so this is a thing that we
have, and that we maintained through a project that lasted eight
months or so.  So I encourage you to do this.

[Time 0:10:09]

```
slide title: Questions

          _a most powerful thinking tool_

to formulate a question is to reify what you seek

getting questions right is half the battle

_questions provoke_, often novel thinking

  logic (just) helps us rule out some of it
```

All right.  So the other thing we are going to be doing as part of an
overarching sense of skills is asking questions.

This is a very powerful tool: asking questions.  And it is an old
tool.  And one of the beautiful things about asking a question, and
formulating a question, is: you have made clear that you are looking
for something.  That there is a thing that you want.

And I think that we state things all the time.  And when you state
things, your intentions are not evident.  When you ask things, not
only do you want to try to get an answer, but what you need becomes
evident.

So I think asking good questions is a skill.  It is another one of
these things that if you do it more often you will get better at it.
The other thing I think is an aspect of questions is that they are
provocative.  They poke you.  And of course when you ask a question of
someone else, they feel like they have been poked.  So you have to get
good at asking, and being asked, and being comfortable with the
questioning process of something.  That is a positive thing.

Logic is an important part of making decisions and solving problems,
but it is mostly a negative thing.  I mean, we use logic to say: no,
this does not hold.  This is inconsistent.  If this is true, that
cannot be true.  It is mostly a way we use to rule things out.

[Time 0:11:36]

```
slide title: Technique: The Socratic Method

              _interrogate 'ask together'_
            examine an idea dispassionately
   questioning its underlying assumptions, consistency

Dispassionate 'without suffering'

  you are not your idea

  you are a source of ideas, some better than others

_We don't define/opine the truth, we discover it_

'The Socratic Method: A Practitioner's Handbook' - Farnsworth
```

So another technique I recommend is to discover, read about, and
utilize the Socratic method.  This is a proper thing with a lot of
history behind it, obviously, and some good organized descriptions.

It is an activity you do together.  It is not like a leader torturing
people with questions, although my teammates will disagree with that
statement.  But it means to sort of work together on trying to find
the truth by asking and answering questions.  By taking an answer to a
question and exposing that answer to further examination, eventually
trying to get to the truth.

And I talked before about questions being provocative.  It is supposed
to be a dispassionate examination of ideas.  And that means not
suffering.  And I think that it is a big challenge as you try to do
Socratic method with teams, this is not common, and I think socially
this kind of dialogue has fallen away, and its use as a skilled
practice amongst people who are cooperating has fallen away.  So it
just seems like a form of argument or attack or hostility or something
like that.  That is not what it is.

So one of the things I recommend is you try to detach yourself from
your own ideas.  Even when you do this by yourself, you should be
thinking about your ideas as things you are going to pose and shoot
down.  And do that over and over and over again and not get attached
to your ideas, not co-identify with your ideas.  And the whole idea
here is that there is some objective truth and we are trying to find
out what it is.  We are not inventing it.  It is not coming out of our
heads.  We are discovering it.

If you want to learn more about the Socratic method I recommend this
book.  It is really fantastic.  There is a bunch of history maybe at
the beginning you would skip, but I think it is great.

[Time 0:13:33]

```
slide title: Father Watson's Questions

Where are you at?

Where are you going?

What do you know?

What do you need to know?


Devs are good at the first two, but those miss 'why?'
```

So some of the the biggest Socratic wizards in the universe are the
Jesuits.  And I was lucky enough to study with the Jesuits back in
high school.  And my homeroom teacher was father Watson, a Jesuit.
And he would always be asking us these four questions.  And he would
ask us these questions in physics class and in algebra class as a way
to do the work, do the problem.

This stuff makes sense when you are looking at a problem.  What have
you got?  I have got X, and I know Y, and I am trying to find X and
the stuff's over here.

Where are you going?  I am going to try to discover what X is.  I know
X.  I need to know Y.  What are you going to do?  I am going to try to
isolate Y by moving stuff over to the other side.  And that was all
fine.

But he also asked us these questions in homeroom as life questions
Where are you at?  Where are you going?  What do you know?  What do
you need to know?  And I think that as developers this "Where you are
at?" "Where you are going?"  This is what we do we are good at.  This
is stand up.  What did you make yesterday?  I made a bread box.  What
are you making today?  I am making a toaster.

And then checking stuff off.  And you are busy doing things, but you
are not often talking about why you are doing the things.  And the
important part of these latter two questions is that you are now
talking about why you are doing things from the perspective of moving
your knowledge forward.

[Time 0:14:59]

```
slide title: Technique: Reflective Inquiry

                            Understanding            Activity
----------------------------------------------------------------------
Status 'to stand'       What do you know?          Where are you at?
----------------------------------------------------------------------
Agenda 'to be done'     What do you need to know?  Where are you going?


this is a framework that can be applied throughout the design process

       _note the importance of thinking about your thinking_
                         reflect - 'bend back'

  inquiry - advancing knowledge, is the driver
```

So we are going to break down these four questions into two axes and
two stages.  One is the understanding axis.  What is happening to our
understanding?  How is our understanding moving forward?  We
understood this much.  Now we are going to understand some more.  I
talked about when we are dev-ing, we know when we are getting progress
because we are creating more code, and maybe more features and the
software can do more things.

When we are designing, what are we creating?  I am going to say one
way to think about design is that you are creating understanding.  You
are expanding your understanding.  The driver for activity should be
expanding your understanding.

You are going to take the two questions in each thing and say one is a
status question.  Right?  What do we know right now?  What have we got
in hand, for both axes?

And then the other is: what do we want to do next?  And we are going
to drive what we do next -- that activity side -- from what we want to
know next, what we want to understand next.

And I think what is cool about this is that this framing -- I mean,
Father Watson asked us these questions all the time, over and over and
over again.  This is a frame you can take out on any day and say:
Where am I at?  What do I know?  What do I need to know?  What do I
want to do about it?  And as we talk about the different phases of
design, we will talk about the fact that this framing can be used over
and over.

The other thing I want to talk about here just briefly is: look at how
this is reflective.  You are thinking about your thinking.  This is
super important.  Being aware of what you are thinking about helps you
think.  It also helps agenda-ize your background thinking.  So that is
where it becomes reflective.  So we will call this reflective inquiry.

[Time 0:16:42]

```
slide title: Technique: PM Top Story/ticket

    Several design techniques contribute to your 'top' story in PM

Looking to always create structured stories with sections for:

  Title

  Description

  Problem Statement

  Approach

_Design stories_ contribute to _building a 'top' story_
```

I just want to talk a little briefly here before we dig into the steps
that I will be talking about contributing to this top ticket.  One of
the challenges I find people have is they have these project
management systems, and they are like, "We are going to make a thing."
And they start writing tickets.  And it is like, "You have no idea
what you are doing yet.  How could you write a ticket?  And how could
you even know what your tickets are supposed to be?"

And you need to have a ticket for what your tickets are going to be.
You need to have a ticket that says, "This is what the overarching
plan is."  And the thing is that ticket, it is neither the first
ticket, nor is it the last ticket.  It is sort of an early ticket, the
top story, that says, "With a good understanding of what is going on,
this is our agenda."

Before that ticket, though, you should be doing some design work that
contributes to the initial story to saying: We have a mission.  We
understand the problem.  We are going to take it on.  This is the
approach we are going to take, and this is how we are going to do it.

I think all stories should have these four sections.  I will talk more
in detail about them in a second.  A title.  A description of the
situation.  A problem statement, which we will talk about more.  And
then eventually, after you have done some design, the approach you are
going to take to doing it.

So when I talk about stories contributing to the top story, I am
talking about early design stories, right?  We said we want to
agendaize design activity.  But we are going to have early stories
that are about doing design.  They are going to contribute to a top
story, which will be sort of your lead story to move forward.

[Time 0:18:12]

```
slide title: Example: Story

Support Java Streams in Clojure's seq function

Description

As Java Streams become more pervasive, users struggle with being
unable to process them using Clojure's standard library, which does
not accept them.

Problem

Java Streams are not seqs, nor do they implement any interfaces to
which Clojure already bridges, thus are not accessible to Clojure's
functional operations.  Furthermore, they are stateful and not
functional, and require special handling.

Approach

Java streams are stateful (like iterators) but we need the ability to
seq (like `iterator-seq` which caches from stateful iteration),
reduce, and into from a stream.  Once we have that, we can leverage
existing Clojure seq/transducer tech to manipulate stream.

Create:

+ Reduce support via `Stream.reduce`, needs BinaryOperator (see
  functional interfaces story)

+ `stream-seq!` similar to `iterator-seq` - creates a seq as it reads
  stream

+ `into` support via new `stream-into!` - implemented with Collector,
  and utilizing transients etc.  Note these will be 'terminal'
  functions on the Stream.

Planning Sheet: https://docs.google.com/spreadsheets/d/1gmVNHCa6
[portion redacted] 3dy_-TcE/edit#gid=1073327933
```

All right.  So this is an example -- sorry, this is not an example top
story.  It is just an example of a story with a decent shape.  There
is this thing people are talking about.  I wish I could use Java
streams in Clojure seq functions.

The description, which is about the situation in the world, without
necessarily talking about what is wrong.

The problem, which is talking about what the challenge or obstacle is
to that.

And then the approach.

This talk is going to dig into the details of all these things.  But
that is what a story is.  And the top story will look like this, but
it will be about the overarching objective.

[Time 0:18:48]

```
slide title: Design Progress

          _measured by increasing understanding_
                of the truth of the world
            and your opportunities within it

decisions made _and why_

  not checking off some process/method or design artifact list

  or making a plan from your first idea
```

All right.  So I sort of talked about this already.  Design progress,
we are going to measure in terms of increasing our understanding, and
tracking the decisions we made, but importantly why.

What is important is that this is not a checklist kind of thing.  I am
not going to say that any of the activities I am enumerating are
necessary, or that you should put them in a list when you get home and
then say, "we are going to do Rich Hickey design by checking off these
things."

That is not it.  You are going to do whatever of these things make
sense in order to move your own understanding forward.

[Time 0:19:23]

```
slide title: Design Phases

    _not everything with any linearity is a 'waterfall'_
           nor do you want 'iterative development'
               iterate == Latin for 'do-over'
              better: incremental - 'grow into'

more like a hike up the (understanding) mountain, not always up, but trending up

being able to name phase 'appearance' helps with 'where are you at?'
not monotonic - ok!  _stay open-minded_

  this is when change is cheapest

_be explicit about backtracking_
```

So I do think that this moving forward, this linearity, of design is a
real thing.  There is this tremendous pushback, or there was a
tremendous pushback, against waterfall development.  This idea that
you analyze your design, you spec, you code the thing, and then you
deliver.  And isn't that horrible?  Isn't that awful?

And it was awful, because I think there were organizational structures
put in place that had one person doing this part, and then dumping on
the next person who did this part, and then dumped on the next person.
So I get handed this thing that was like: do you realize all these
things about what you did were not right?

But we have replaced that with a non-idea, which is this idea of
iterative programming.  And this Latin for "do-over" is not a joke.
That is what iterative means: "do over".  And I do not think do-over
programming is a thing.  I do not think that is a way to make anything
that is really good.  Incremental is probably a better word.

So we are going to try to move forward and increase our understanding.
It is not monotonic.  We will think something is a good idea.  We will
learn some more stuff, and we will say: "Nope!  That was not a good
idea."  And we will we will try another route up.

But the the cool thing about the word "phase" is that it means
appearance, like phases of the moon.  Like you you did something, and
then you saw the next thing, you saw the next step.  It is not like
you programmed it into your nav and it said, "Here is everything that
is going to happen in your future."  There is no nav for software
development.

So it is OK.  It is not monotonic.  You want to stay open-minded.  You
will backtrack.  The one thing I will say is: if you are backtracking,
_say so_.  So like say: Look, we thought we had an approach that
worked.  We started to look at some of the implementation details.  We
found another problem, or we found that we did not really understand
the problem, or we cannot do what we intended.  And now we are going
back to a prior phase, where we are going to try to find a different
approach, because there were obstacles in our way.

[Time 0:21:30]

```
slide title: Phases

"these are words with a D this time"

Describe (situation)
Diagnose (possible problems)
Delimit (the problem you are going to solve)
Direction (strategy, approach)
Design (tactics, implementation plan)
Dev (build it)

at any time:

  Decide (to do, or not)
```

So extra points for the King Crimson reference.  Did anybody get the
King Crimson reference?  All right.  That was a low that was a low
probability.

[The band "King Crimson" has a song "Elephant Talk" where one of the
lines is "These are words with a D this time"]

All right.  So I am not going to break these down now, because this
talk breaks down all these things: describing, diagnosing, delimiting
the problem, choosing a direction at a high level, choosing
particulars as implementation details, and then doing it.

The one thing is that I do think that these are phases that kind of
lead into one another.  But on an overarching level, there will always
be the potential to do "deciding".  And in this case, when I am saying
"deciding" I am talking about scoping.

You may encounter a problem, and you have required some level of
understanding of it and said, "We are not doing anything about that."
Or you have gone through and seen what the various approaches are, and
found that no approach will cover more than 80 per cent of the
problem.  And you are going to say, "That other 20 per cent we are not
going to do."  Or somebody is going to tell you there is no money for
your project, and you will say, "All right.  Well, that is that!"

So this deciding does not have a spot in the order.  You are going to
be ready to make decisions, hopefully, at any time.

[Time 0:22:46]

```
slide title: Phase: Describe

                     _the situation_
                   bug/failure reports
      feature requests, external and internal (backlog)
                         context

_What do you know?_ something seems wrong/obstructive in the world
_What do you need to know?_ the extent of it

_Where are you at?_ observing, listening
_Where are you going?_
- initial story title
- _write down_ a Description in top story
```

So "describing" literally just means to write things down.  And the
very first phase of design is just to write down what you are hearing.
Users are complaining about whatever.  People in Slack want X.
Everybody says Clojure sucks because blah.  Whatever it is.  You are
hearing things, and you just want to capture that.  Maybe you have
seen failures in the system.  Maybe what the thing that you are trying
to take on now has to do with a bug.  So you have a bug report.  So
you have exception stack traces or you have logs from production
systems.

It does not matter.  What you are going to be doing here is just
writing it all down.  Maybe having more logs gathered.  Maybe having
more conversations with people to get the information.

So what do you know?  Something seems wrong with the world.

What do you need to know?  You need to know: how big a problem is
that?  Where is it?  What are its impacts?  Things like that.

What you are doing?  You are observing and you are listening.

And where are you going?  You are trying to produce two things out of
this: an initial story, that top story, the title for that.  And also
the description paragraph for that.

[Time 0:23:55]

```
slide title: Technique: Description

                  _one paragraph summary_
                     situation/context
               symptoms/reports/observations
                          requests

_don't_:

  say what the problem is

  accept as facts assertions that imply what the problem is

    instead: X says Y
```

So description paragraph.  It should just be a paragraph.  It should
be the situation you find yourself in, the symptoms, or those problem
reports.  All those things.  You just want to capture the high level
view of what they are.  You can point to the details.

The very important thing about this is that you are not saying right
now what the problem is.  This is, "I have a headache."  You are not
saying, "Because I have a brain tumor", because you could have a brain
tumor, or you could have not had enough water today, or your eyeglass
prescription could be wrong.

That is not what you are saying.  You are saying, "patient has a
headache."  So you just do not say what the problem is.  You say what
the symptoms are, what the complaints are, and things like that.

If somebody has a complaint that seems to incorporate the problem, do
not accept that as a fact.  Just say: somebody said they think this is
the problem.

OK.  And we are going to write that down in our top story.

[Time 0:24:51]

```
slide title: Phase: Diagnose

         'know across' possible problem(s), of two kinds

1 - bugs/defects
- yes bugfixes need design (or revisions of a design)
- lest you just play symptom/code whack-a-mole
2 - features

_What do you know?_ the symptoms/context
_What do you need to know?_ the cause(s)

_Where are you at?_ have good description, evidence
_Where are you going?_
- applying logic and experimentation
- to explicate 'unfold'
```

The next phase is to diagnose the problem.  And "diagnosis", another
great word.  It is not Latin.  It is Greek, and it means "to know
across".  That across is the "dia" part, like "diagonal" or
"diameter".  Same root.  "nose" is "to know".  Again, I just looked it
up, and it was super cool that this is what it meant, because I do
think that this is a crossing.  This is a movement from one possible
set of knowing to another set of knowing.

And there is two kinds of problems.  I am going to say that we are
talking about design for both of these.  One kind of problem, though,
is: your thing is broken and you are trying to fix it.

Another kind of problem is that people want a feature, or you want a
feature, or somebody talked about some feature.  And hopefully that
feature is about a problem.  So you need to go from the feature to the
problem.

So what do you know?  You know the symptoms and the context.  That is
what you just did.

What do you need to know?  You need to know the cause.  So now we are
going to go and say, "All right.  Well, you have a headache.  Here is
five reasons why you might have a headache."

So you have a good description.  That is what you did before.  And you
have the evidence that you collected before.

And where you are going is: you are going to try to figure out what
the problem is.

[Time 0:26:14]

```
slide title: Diagnose: Bugs

         symptom -> possible problems -> (likely) problem

hypotheses (more than one)

pick one (how?)

  use logic first (to rule out)

  'most likely' (intuition)

  makes the problem space smallest (divide and conquer)

Use the scientific method
```

So I will take these in two different parts.  Diagnosing bugs is a
knowing across from a symptom to maybe multiple possible problems, and
finally down to what is actually wrong.  It is: your eyeglass
prescription is off.  You need better glasses.  That is why you are
getting headaches all the time.

So you will have hopefully more than one hypothesis.  This "more than
one", it is going to come up all the time.  Design is not thinking of
one thing and then writing it out.  That is not designing.  Designing
is about thinking of more than one thing.  That is like the first
skill you should have is: if you think it is one thing, just think of
a second thing.  Think of a second possible reason.  If you are on a
team, have everybody try to think of a reason.  Of course, if you are
playing that game you do not want to go last, so ...

And then you are going to need to address them.  And the one thing I
would say here is: address them one at a time.  In other words,
explore these things one at a time.  People will get a bunch of ideas
about what is wrong and they are like, "I think the system is falling
down.  We are getting this exception.  I think it is either: We have a
bug in our code.  There is a bug in the library code.  There is a bug
in the JVM.  Solar flares."  And then they will be in the code, or
running something looking for all these possible things.

Just do not do that.  You need to pick one.

Now logic helps you here.  Sometimes you can look at the possibilities
and say, "You know, it cannot be that.  You do not wear glasses, so
...  Although, maybe you should."  So we can use logic to rule stuff
out.

And then there is a bunch of things.  I am not really going to dig
into any of these too deeply, because every one of them would take an
hour.  But you will have a thing that may be most likely, either due
to your intuition, or it is the thing for which you have the most
evidence.  It seems like this.  All the evidence seems to be pointing
at that, from our intuition standpoint.

I think one of the most powerful tools you have here is to make the
problem space smaller.  If one of your hypotheses makes the problem
space smaller, that is often a good thing to explore early.  I am
often telling programmers that I work with, "Get that into a smaller
context."

You see a problem in your system.  Well your production system is this
big hairy monster.  Can you reproduce this problem with just this tiny
piece of code?  Can you reproduce it not using your code at all?  If
you think it might be a library.  You think it might just be an
algorithmic snafu.  Can you just write a little piece of Clojure code
on the side and reproduce it there?

[Time 0:28:48]

```
slide title: Technique: Scientific Method

               _out of scope for this talk_

formulate a supporting/refuting conjecture

design an experiment

_write result template first_
- "If this sheet were filled in we'd know X"

code it, conduct it

apply conjecture logic, repeat
```

And a great technique here is the scientific method.  Stu's given a
good talk about this, and I am not going to do that here.

[ Stuart Halloway, "Debugging with the Scientific Method", November
2015
https://github.com/matthiasn/talk-transcripts/blob/master/Halloway_Stuart/DebuggingWithTheScientificMethod.md
]

But for each hypothesis you take on, formulate a conjecture that you
are going to try to prove or disprove.  You are going to design an
experiment, which is going to be some code you get to write.

The one tip I would give you here is that frequently people will say,
"I am trying to figure out this thing", and then they will go and run
some tests.  And then they will need to summarize what they ran.  And
then you will look at the summary and be like, "I do not think you
have got any information that helps us prove or disprove this
conjecture."

So the tip I would give you is that if you are going to go and run an
experiment, the very next thing you should do, before you write the
code that tests the experiment, is to write this spreadsheet or the
template that says, "This is how we are going to display the results.
This is where we are going to put the results."  We are going to have
a column for this, a column for that, and rows for these things.  And
you want to look at that template and say, "Yeah, you know what?  If
we filled this out, we would know everything we need to know to do
this conjecture."

And then write a program that can provide the values for that
template.  Do not exploratory code and then wonder why you did not get
the answers that you need to do it.

[Time 0:30:00]

```
slide title: Diagnose: Feature Requests

               _feature: factura: 'making', of an answer_
                          _not_ the problem

'we don't have feature X' is never a valid problem statement

  recognize and kill all such statements

_feature -> problem(s)_ for what that feature is (one possible) answer

  what is the user's intention/objective? (not how)

  what is in the way?
```

OK.  Much trickier, and much more common, and much much more commonly
needed, and much less frequently exercised, is the "knowing across"
from a feature request to the actual problem.  So people ask for
features always, "I wish you had this.  I wish I had that."  You do
also, right?  You have your own internal feature requests, your
backlog, and things you thought might be good features.

"We do not have feature X" is never a valid problem statement.  If you
need proof of this you only need to look at a modern car which has a
touch screen where no one said, "I need to slide my finger on some
random piece of glass to a precise point to set my blower in my car
while I am driving."  No one has ever said that, right?

But somebody did say, "We need touch screens because young people will
never buy our cars."  This is what happens when you are not talking
about the problem.

So we are trying to get from a feature request, to a problem for which
that feature is one possible answer.  So there is two things that
happen here that were magical.  One was: you went from feature to
problem.  The other is: you went from one answer, to maybe an open set
of answers.  That is where you get the flexibility to do design.  If
somebody's just going to cram down "it is time to make the toaster",
well you may not be solving a problem.

So here are the exercises to say take the feature request, or your own
feature idea, and say: what is your intention here?  And then, what is
in your way?

[Time 0:31:36]

```
slide title: Phase: Delimit

                  _the problem you are going to solve_
  you might discover multiple problems or bigger problems during diagnosis

_What do you know?_ what the problem is
_What do you need to know?_
- how to state it succinctly
- its scope

_Where are you at?_ have diagnosis
_Where are you going?_

  making the problem statement
```

OK.  So now you have got these feature requests turned into problems.
And you have just one more step, I think, before you have a problem
statement, which is to try to delimit it.  As you have done this
thing, you may have a notion of the problem.  You may have had
conversations about the problem.

Delimiting the problem is really just a matter of saying: what is the
short, concise, precise way we are going to talk about the problem
that we are going to take on, making software to solve.

So you know what the problem is.  You sort of did that in the
diagnosis thing.  All you are trying to do now is state it succinctly,
and give it some scope.

[Time 0:32:16]

```
slide title: Technique: Problem Statement

        _Succinct statement of unmet user objectives and cause(s)_
                    not symptoms/anecdotes/desires
         not remedy/solution/feature - challenge is to filter out

modify your top story title from symptom -> problem
add Problem after the Description in the top story - link to diagnosis work

_subject to refinement_
- as your understanding increases
- don't let your problems statements get stale

            This is the most important artifact you will have.
   if you don't relentlessly focus on a problem you may make something
                 that doesn't solve any problem
```

So a problem statement is this succinct statement of unmet objectives.
We are talking about what is the user's intention, and the cause.  It
is not the symptoms any more.  We did that in the Describe phase.  And
it is not the remedy.  That is still in front of us: what to do about
it.  So if that still exists, if any sort of, "what we are going to do
about it" is still present here, you want to get rid of that.

At the point you have got a problem statement, you are going to be
able to do two things with your top story.  You are going to be able
to modify ...  The initial story title was probably something like, "I
think a toaster might be a good idea."  And now it is, "The user likes
caramelized bread."  And there is maybe more than one way to deliver
that.

So you are going to modify the title of your top story here to try to
make it about the problem.  We have given somebody a way to accomplish
X.  It is the objective now that is the name of your story.

This is great.  When you work in a project management system that is
not like, "Build toaster.  Build bread box.  Build whatever."  But it
is like, "Solve this problem.  Solve that problem.  Solve that
problem."  And you look at what you have done, that ladder list is way
more satisfying than the one that is just: feature, feature, feature,
feature.

So the other thing you are going to do is you are going to now add
another thing to that top story.  You had the title description.  Now
you are going to have that problem statement.  This is not forever and
ever and ever.  You are going to refine this.  You may have gotten it
wrong.  You may have a missed subtlety you will discover later.  So
this is another thing that needs maintenance.  But it should be short.
It should be a paragraph that says what the problem is.

This is super important.  If you do not have this, and if you do not
relentlessly focus on it, you run, I think, a very high risk of asking
somebody to slide their finger around on a touchscreen while they are
driving in order to turn up the radio.

[Time 0:34:20]

```
slide title: Phase: Direction

                        _strategy, approach_
                   User's intentions and objectives
                  High-level approaches to addressing
   e.g. in-proc/out, lib/app, buy/build, modify/add, automatic/manual etc

_What do you know?_ what the problem is
_What do you need to know?_
- the user objectives in more detail
- the possible approaches
- the best of these
- what matters in deciding (criteria)
```

So now I am going to talk about two things: the sort of direction, and
like strategy and tactics.  And I am not trying to imply that you will
always have this differentiation, or your thing will be layered like
this, but certainly if it is a bigger thing you will likely have two
phases here.

You will have a direction setting moment, and then you will have many
implementation decision moments where you are going to be doing
similar things, just at a different level, about a different level of
detail.

So at the direction stage it is about strategy.  Strategy means to be
a general, or to lead, and fundamentally it means about where are you
going?  We are all going to follow you that way.

The things you want to capture here is you want to capture those
intentions and objectives of the user -- not how, but what they are
trying to do.  And you are then going to start thinking about what are
the ways that you could possibly address it.  We are going to call
them approaches.  And these are high level, and I am not trying to
enumerate them all here.

But a very basic one would, for instance, be: are we going to try to
provide an automated solution to make this happen for the user?  Or
are we going to provide a tool for the user to do it for themselves?
That is a kind of directional decision that you want to make.  So you
know what the problem is.

What do you need to know?  You need to know about the user objectives
in more detail.  You are going to dig down a level on the user
objectives.  You are going to enumerate a bunch of possible
approaches.  You are going to try to decide which one is best.  So
this is a big phase.  And along the way you are going to have to have
reflected about what matters to you in making this decision.

[Time 0:34:20]

```
slide title: Phase: Direction (cont.)

_Where are you at?_ Have description and problem statement
_Where are you going?_

  Enumerating use cases

  Making a strategy DM

    criteria, approaches and tradeoffs

  determining scope

  entering Approach secion on top story
```

And then what are you going to do about it?  Here have already got the
description, the problem statement.  You are going to want to walk out
of this phase with enumerated use cases.  You want to walk out of this
phase with what I will call a strategy decision matrix.  I will show
you that in a second, but it incorporates the criteria for deciding
the approaches you might take, and the trade-offs of each.

You will also be doing the high level scoping thing, which could
include, "We are not taking this on right now."  But it may include,
"We are not going to provide an automated solution because that is
going to be too big.  We already have that sense.  But we may provide
a tool for the users to help themselves do this thing."

And eventually you are going to get something to write in your top
story that is the approach you are taking.

[Time 0:36:53]

```
slide title: Technique: Use Cases

                 _user's intentions and objectives_
             in terms of _what_ the user could accomplish
                       were the problem solved
                           _not how_ (yet)
                 make a blank 'how' column for later

should not start with
"the user will push an orange oval button and music will play"

_later_ you will fill in the 'how' column with that kind of recipe for
using the solution you've designed
```

So use cases.  I think everybody thinks they know how to do use cases.
And that is usually not what I want to see in a use case, because I
think again there is two phases.  The best first phase for use cases
is to talk about only what people intend to accomplish.  What they
would like to be different about the world.  What they wish they could
do, not how.

So you are going to make a little tiny sheet that says intention,
intention, intention.  It has got a "how" column that is blank.

I do not believe in this, "Make a card that says the user should put a
push a button.  It is going to be this color, and it will do this
thing."  I mean if you want to do that, that is great.  That is not
what this talk is about.

Later, you will have a strategy that you have chosen, and you will go
back -- actually you will know a little bit more about how you are
going to implement it, and you are going to go back and say, "You know
what we are actually going to do?  We are going to give the user a
freaking knob for the volume, please."

[Time 0:37:51]

```
slide title: Template: Use Cases

problem this sheet is about      | How (given solution design)  | Notes
---------------------------------+------------------------------+-----
user intention/objective         |                              |
another user intention/objective |                              |
another user intention/objective |                              |
```

So here we go.  This is what a template for a use case should be.  It
is not very sophisticated, right?  But always put your problem in A1
[cell A1, top left corner of a spreadsheet].  Just remind yourselves,
"this is what we are thinking about".  Now if you leave that off, I do
not know what this sheet is about.  You are going to fill in column A:
objective, objective, objective.  I wish the radio was louder.  I wish
I could make the radio louder.  I wish I could turn it off.  I wish I
could mute it while my phone call came in.

Not how.  These are just things I would like to be able to do, and
then how, you will do later.

[Time 0:38:25]

```
slide title: Example: Use Cases

[todo: put slide image here - lots of text]
```

So this is real.  Again, we really do this.  Everybody heard about
Morse today, maybe?  REBL's successor?  This is a lot of things you
could do with Morse.  A lot of context in which you could use Morse,
and a lot of ways you might want to connect Morse to your stuff.

And we were just sort of brainstorming.  And this is not a giant
thing.  We sat and talked for 40 minutes, and this is what we did
while we were talking.  We made this sheet.  We filled it out, and we
talked about what was what.  But in this use case phase we would only
do A, right?  This is a completed story that shows column B, the how,
as well.

[Time 0:39:08]

```
slide title:  Technique: Decision Matrix (DM)

              _a (google or other live-editing) sheet_

    A:1 what decision are you trying to make, for which problem?

_Approaches_ - Columns (but first labels rows)
_Criteria_ - Rows (but first labels columns)
_Aspects_ - Cells

sheets > docs

  prose docs create a linearization that makes contrast difficult
```

So the other big technique in this phase is the decision matrix.  And
this is the heart of the talk, is to talk about decision matrix.  I
used to do this when I was mostly designing by myself in Org mode [an
editing mode in Emacs https://orgmode.org ], but I am a complete
convert that the best way to do this kind of design, in this phase of
design, and this work, is in a spreadsheet.  And in particular, it is
in a spreadsheet that is a live editing spreadsheet.  So we use Google
Sheets for this thing [ https://www.google.com/sheets/about ].

So what is a decision matrix?  It is a spreadsheet.  It is a
spreadsheet that more than one person can see at the same time, and
edit at the same time.  I do not know if somebody else ... I am sure
Microsoft has one.

A1 will be: what decision are you trying to make?  What problem are
you working on?  Always A1.  If I come up to your project and you want
some design mentoring, and A1 is not filled in, guess what we are
going to be working on?  A1.  Have a good problem statement.

You can copy your problem statement right in here.  Often, though,
this is more of a specific decision.  But it should be related to
that.  Keeping your problem in your face is super important.  It
should just be always like this problem is just haunting me.

And I am seeing it, which means I am forced to think about it as an
external stimulus.  That is also critical.

All right.  So what are you going to have?  You are going to have
different approaches to solving the problem.  These will be your
columns.  The first of the columns will label the rows, but the other
columns will be your various possible approaches.

You will have criteria: how are you going to make this decision?
These will be the rows, except the very first row, or two, labels the
columns.

And finally, you have the interior cells, which is the aspects of a
particular approach from the perspective of that criteria.  That is
what goes in the inner cell.  I do strongly recommend sheets over docs
here.  Docs are linear, and they do not support contrast, which I will
talk about in a second.

[Time 0:41:05]

```
slide title: Template: DM

TODO: add template here
```

So this is a template for a DM.  I do not think I have to zoom this
one in.  This is not real.  This is just a template.  The upper left
corner, A1: what problem are you working on?

[Columns] B C D E are the approaches you want to take.  If you are
modifying a system that already kind of does this, or has a lacking in
this area, make that the first approach.  The first approach is: do
nothing.  Where are we at?  What does our system do right now?
Usually, there will be something not great in that column.  And then
you will have other approaches.  I will talk in detail about that in a
second.

And then down the rows are criterion, criterion, criterion.  And then
inside we have the aspects, where we are going to talk about how the
approach deals with criterion.

[Time 0:41:50]

```
slide title: DM Columns: Approaches

first row or two describe approach
- must give you shorthand for talking, yet make clear what about
- _succinct description_ of approach, use row 2 if needed
- freeze the approach title/description rows

  if you are modifying something, the first 'approach' should be the status quo

  columns for what others have done in same situation

  and your initial ideas

A DM is about _creating_ a great approach, not merely shopping

         _the answer is often an approach you don't begin with_
```

So the approach is we are going to label them in the top.  Again, you
need to be succinct, but do not take goofy names.  Do not do super
shorthands.  If somebody walked up to your thing and they read just
the first box of column C, would they understand what columns C was
really about, or did you shorthand the meaning of it away.  If you
cannot get it done in something that is more like a title, like in row
one, take a second row and put in a sentence length thing.

You need for what you are talking about to be super clear.  I have
seen a lot of people just struggle here because they have columns and
it is not actually clear what this column is about.  What strategy or
what approach this is about.  Put enough detail in there so you can
distinguish the two.

And then freeze those rows.  I already talked about using the first
column, first approach, to be like what you do right now.

You want to think about what other people do.  This is stuff from
"Hammock-driven Development".

[ Rich Hickey, "Step Away from the Computer, or Hammock-driven
Development", October, 2010
https://github.com/matthiasn/talk-transcripts/blob/master/Hickey_Rich/HammockDrivenDev-mostly-text.md
]

And then you are going to have your own first ideas about possibly
good approaches.

The main thing I want to do here is, I want to emphasize, this is not
a shopping exercise.  This is not just like: well, I have got what we
do, what other people do, and my first idea, and we are going to pick
one.  That is not what it is about.  It is about going through the
exercise of examining how they differ from each other, what their
qualities are, and hopefully driving the birth of one or more new
columns, new approaches.  This is a place where you can innovate.  So
it is not it is not shopping.

[Time 0:43:23]

```
slide title: DM Rows: Criteria

                    'means of judging/deciding'

First column - _succinct descriptions_ of criteria (freeze this column)
Include criterion iff salient or relevant, sort by importance, distinction

will usually include rows for

  fitness for solving the problem (from use cases)

  various '-ilities'

  costs (time, dev effort, $), risks

  compatibility, complexity

  etc - purpose built for problem (reflective)
```

All right.  Criteria.  This word is very important.  It is not
characteristic.  It is criteria.  Criteria.  It is a means of judging,
deciding.  Critic.  Critical.  All those words are about making a
decision, and about saying positive and negative things about things
so that you can judge.

But what is the basis for that judgment?  Well that is something that
has got to be reflective.  It is not in the problem.  It is in how you
feel about addressing the problem.  I mean that some of it is driven
by the problem.  If your approach does not solve the problem at all,
if it does not make the headache go away, well it is not really an
approach to getting rid of somebody's headache.

So you will have some rows for solving the problem, but you will have
a bunch of other rows, potentially, that are about meta
characteristics of this approach.  How much development time does it
take?  Is it compatible with what we have done before?  Is it going to
possibly break things?  How much does it cost?  How much will it cost
to operate?  Is it allowed by some regulatory thing?

You are going to have a bunch of things that are candidates for rows,
but you should never fully enumerate them in advance.  Every time you
take on a problem, you are going to need to be selective about what
matters, and only put in what matters.  So you want things that are
salient or relevant.  Salient means it is an aspect of this thing that
sticks out, and relevant means that it is an aspect of this thing that
matters to our problem.

If you have one of your columns is a live bunny, and another one of
your columns is a tank in a bunny suit, you are not going to have a
row that is "what color is the fur?" or "how soft is it?"  You are
going to have a row that says "how much lettuce does it eat?" and "can
it crush a truck?" and "what kind of ammunition does it need?"  The
things that really distinguish these two things.  I do not know how
much does a tank weigh?  We do not want a really, really, heavy bunny.
All right.  So it is not characteristics, it is criteria.

[Time 0:45:31]

```
slide title: DM Cells: Aspects

                     _of approach per criterion_
   _succinct description_ of how approach handles criterion (or doesn't)
          avoid y/n/true/false/numeric-rank criteria, and in cells

_avoid judgement in text_, instead use (unsaturated!) cell background color

  Neutral - clear

  Some challenge or negative - yellow

  Seems blocking or failing to address problem - red

  Seems particularly desirable/better - green
```

And then we are going to have the aspects.  This is, again, a succinct
description that goes in the inner cell.  You really want to write
some words here.  You really want to help people understand: when you
think about this approach from this perspective, or when you look at
this approach from the perspective of this criteria -- that is what
aspect means: look at something.  When you look at it from that, this
is what you see.

It should be words here, not yes, no, true, false, that kind of stuff.
Try to say: if it does it, say _how_ it does it, not that yes it does
it.  Say how it does it, because you are going to have two different
answers that both have a "yes", but how they do it differs.  Write
down how they are doing it, not just yes they do it.  Yes, they have
it.  Do they have a backup strategy?  Yes, yes.  Well, one may use
floppy disks, and one may use replication.  So say that.

The other thing you want to do here is: you want to avoid subjective
judgment in your text.  Do not do that.  Just write what the facts
are.  When we look at this from this perspective, this is what it has.
Or maybe, it does not have this.

And then what I would advocate, and what we do, is we use colors,
which you saw before, some colors on the sheet to show subjectivity.
This is the _only_ place that we use subjectivity on the sheet.  If
something is just OK for this, we leave it neutral, clear.  If there
is some challenge or negative characteristic to the way that this
approach deals with this criterion, then we will color it yellow.  If
the way it does it seems completely blocking -- it is prohibitive to
us, prohibitive to the user, failing to answer the problem, we will
color it red.  So it is kind of blocking.  And if it is particularly
nice, desirable or better than the others, we will color it green.

You can, as a shorthand, just start with pros and cons rows.  Here is
my approaches.  Here is the pros of this, and here is the cons of
this.  But the thing is, maybe you are picking between two libraries,
and one of the libraries says "I have really low latency" and the
other one says "I really have high throughput".  And these are their
features.  Well okay, that is two pros.

But you have not looked at the high throughput one on the basis of
what is its latency, and you have not looked at the low latency one
from the perspective of how is its throughput.  So until you have
broken up these things so that every criterion gets its own row, you
are not going to have the ability to contrast.

What we are trying to do is to get things next to each other that are
different.  That is what makes our mind go.  We love edges.  We love
seeing edges.  You need to create edges in your ideas.  That is what
is going to trigger your thinking.

[Time 0:48:22]

```
slide title: Example: DM

[todo: put slide image here - lots of text]
```

This is a real DM here we are thinking about.  This is not something
we are shipping yet.

How do we deal with functional interfaces in Clojure?  There is a lot
of ways to do it.  This sheet goes, goes over there [as he is
scrolling to the right up to column G at least].

But there is a concise problem statement in A1: You cannot use Java
methods to take Java functional interfaces without using an adapter or
reify today.  Column B is what we have today.  People are writing
reify a lot.  They need to know the types that they are trying to
target.  It is a lot of redundant stuff.  That column is kind of a lot
of orange, which is between yellow and red, and yellow.  And then
there are other approaches which are good.  It is rare that something
is totally amazing.

[Time 0:49:14]

```
slide title: DM: Tips

Avoid
_the all-green column_ - are you rationalizing?
_undistinguished columns_ - find the differences that matter
_exhaustive or template rowsets_ - s.b. specific criteria, not just characteristics
_links as primary cell content_ - ok as supplement to summary text in cell
_hidden comments/popups etc_ - keep things in view
_phrasing criteria as questions_ - clash with inline questions

include questions as soon as they arise!

  put '?' anywhere (approach/criterion/aspect)

    - if you are unsure of importance

    - or the info is unknown
```

So some tips about doing a good DM.  Avoid the all green column.  That
is very unlikely.  That is a sign you might be rationalizing.  Nothing
is totally wonderful.

Avoid undistinguished columns.  If you go through in those two columns
and they are not different in any way, you are probably missing a row.
You are probably missing some criteria that distinguishes them, and
you want to find it.

I talked before, you do not want an exhaustive row set.  You do not
want a predefined row set, and you do not want every characteristic of
every possible approach.  You just want the ones that matter.

And relentlessly move up.  The other nice thing about a spreadsheet
is: you can move rows up.  You just drag them and they go up.  So keep
pushing up on your spreadsheet on the things that most distinguish
your different approaches.  No one cares about pages and pages of
everything's the same on this from this perspective.

Avoid links or references out as your primary cell content.  Write
something there.  The key here from a thinking standpoint is: you are
seeing the stuff that matters.  If it is a link, you are seeing
nothing.  You have got to go break your concentration and go follow
the link then.  You can have links as supplements.

Do not use the features of these things that allow comments.  I see a
little triangle in the corner.  What is that?  I have got to hover or
click and now it is over here.  If you have a question about
something, or you think it is bad or whatever, just write it on the
cell next to it, or in the notes.  You will see a lot of these things
have "Notes" columns.  Just write it in the notes so it is in
someone's face.  Now they do not have to opt into seeing what you
think.  You said what you think, and you put it in their way.

And then avoid phrasing the criteria as questions.  This is because
you want to be able to write questions in your sheet, and you want to
be able to search for them.  As you were going you are like, "I wonder
if this can do this?  I wonder if this will be fast enough?  I wonder
if we should be thinking about this thing?"  If you phrase your
criteria as, "Does it have this question mark.  Does it have that
question mark," then you cannot search for question mark and find your
questions.

[Time 0:51:19]

```
slide title: DM: Outputs

a succinct _description of the problem/decision_ being taken on
a set of _several approaches_, succinctly described
an explicit and clear expression of _what matters in making the decision_
_detailed aspects_ for all of the approaches per criterion
- aligned for contrast

at-a-glance, fine-grained _subjective assessment_
- subjectivity all in one place (cell color)

  a set of questions for follow up

                _clear benefits + tradeoffs_
```

All right, so what do you get when you do this?  You are going to have
a good description of the problem.  You are going to have a bunch of
approaches with good descriptions of those.  You will have made
decisions about what matters.  You will have done that introspection,
so it is reflective.  You will have details about how everything
approaches it.

And you will have an at-a-glance subjective assessment, so if I am
coming into your thing and you have done this, I can quickly see what
you think is good or bad, or where you think the trade-offs lie.  And
all the subjectivity is in one dimension.  If I do not agree with you,
I can take your sheet, dupe it, and change all the colors to blank,
and I will be dealing with something with no subjectivity left.

[Time 0:52:02]

```
slide title: DM: Benefits

come back later/arrive late - (re)load context

live group thinking tool - make everything visible as text
- vs voice + independent notes

promotes shared understanding
- call out ambiguity, inconsistency etc
- raise and capture questions and ideas immediately

_birthplace of abstraction_

               _provocation for background thought_
                        hammock, sleep
           where new columns and best answers are born
```

All right, so what are the benefits of having done this?

Well certainly you get to come back later and resume your work.
Somebody else can join you in the thought process, and arrive late and
catch up.  While more than one person is working on this, you all can
be looking at the sheet.  This is so much better than just gabbing on
Zoom and having everybody take independent notes, and then maybe
trying to reconcile those notes.  We _always_ make a sheet and stick
it in our face and type into it while we are talking.

And it means that you are going to have shared understanding.  You are
going to be able to say, "I do not think you are saying that right.  I
do not think that that is the case."  That is good.  That is the
Socratic method, questioning: Is that really true?

The other thing I think happens as you have done this sort of cutting
up, and pick the criteria, is: you are starting to do abstraction.
You are trying to see, well I had five possible choices, but only two
ways to do this.  You are learning the physics of the problem.  There
is only two ways to do this.  There is only one way to do that.
Everybody does it the same way.  Maybe there should be another way.
You could ask the question.

And you are finding characteristics that maybe you want to lift later,
as abstraction.  And then this is the kind of thing, if you do this
during the day, I promise you, you are going to get new ideas when you
hit the hammock or the bed.

[Time 0:53:18]

```
slide title: Phase: Design

               _tactics, implementation plan_
                  the blueprint-like design

_What do you know?_ the problem and the direction we are taking to solve
_What do you need to know?_
- the possible implementation approaches
- the best of these
- what matters in deciding
- how the users will use your solution
```

All right, and then the next phase of design is design.  And I
purposely made design a phase of design because this design is about
"mark out a plan for doing it".  This is the actual traditional notion
of design.  By putting the context of what is design -- because you
actually cannot start here.  You cannot just say, "I am doing design.
This is the first thing I am going to do.  I am going to start
figuring about how I am going to make something.  You see now, you
will have skipped over all this other stuff that is valuable.

So now you will actually be down to: all right, we have an approach
chosen to take.  We think it is the eyeglass thing.  Now we are going
to go and try to figure out how to make it.  Or maybe we figured out
we are going to want a knob, and we have to figure out where to put
it.  And should it be grippy, or should it be slidy?  Hint: it should
be grippy.  Should it be detented or not.  Yes, it should be detented.
You know.  This kind of stuff.

All right.  So what do we know?  We know the problem and the direction
already.  And you see this.  You are gaining power.  You are gaining
velocity.  You are gaining confidence.  You know the direction you are
going to take.

What do you need to know?  Well you you have got maybe an approach you
are going to take, but not exactly how you are going to implement it.
Right now is where you would be talking about like, "What is the API
going to look like?"  We have decided to make an API.  Or, we have
decided to make a library for people to use to do it on their own.  We
are not going to automate it.  But now you would be talking about
like, "What is that API going to look like?  What is the signatures
going to be?"

The same thing is going to happen.  Hopefully, you are going to create
more than one idea.  Then you are going to try to pick the best.  You
are going to use the same techniques to decide.  Criteria.

The other thing that is new here and different is before with approach
we wanted to know in detail what are the user's intentions.  Now we
get to talk about: as we make implementation decisions, we can go back
to that use cases sheet and say, "this is how they will accomplish
their intention, given the solution that we are intending to make."
And the implementation decisions we are choosing right now.

[Time 0:55:25]

```
slide title: Phase: Design (cont.)

_Where are you at?_ Have use cases and strategy/direction DM
_Where are you going?_

  implementation approach DM(s)

  design (plan) diagrams

  implementation decisions

  add detail to Approach section of top story

  fill in 'How' column in Use Cases

    how user can accomplish using feature/API etc

    _possible scope adjustment or backtracking if impl poses new challenges_
```

So what do you got?  You have the use cases and you have this DM.  You
are going to have more DMS.  These can be very light 15-minute
exercises.  We need to make this choice.  We need to do something
here.  What are our choices?  Boom.  What is the trade-offs of these
things?  This, that, or the other.  It can be very lightweight.  I am
not talking about suffering over every decision.  I am talking about
just trying to be considerate, as often as you can.

This is when you may do diagramming.  You are certainly going to, as
an outcome of doing these DMS, you are going to make implementation
decisions.  You are going to go back to that part of the story which
is the approach, and which has the direction in it right now, and you
are going to add the details.

I do not know if you remember back to the other thing, but we said
like what are we going to do about this problem?  We are going to have
these three APIs.  And you are going to be able to do this.

And then you are going to go back to your use cases and fill in the
"How?"  column.  It is certainly possible that in doing -- I talked
about this before -- in doing the implementation details, you may
actually need to go back and alter your scope.  We thought we were
going to do this, and we did not find a way to implement it that was
not going to be too much work, or too possibly risky in altering code
that we already had.  And we do not want to take on the risk of that
much change.  And then you are going to back up.

[Time 0:56:48]

```
slide title: Example: Impl DM

[todo: put slide image here - lots of text]
```

This is a real implementation DM for something we did already ship.
We had this problem.  Newcomers to Clojure do not know Java.  They do
not know there is a Java math thing, and they do not know how to do
cosine.  And it is just this hurdle for people.

But there is a lot of different things you could do about it.  You
could do nothing, and say, "All right, we will give you a better way
to find the Java doc."  So we have these characteristics.  The same
thing.  We could do static imports.  We could have a program that gens
the thing from the Java, which is what we ended up doing.  Or we could
hand code and we were looking at these trade-offs.  So that is how we
do that.

[Time 0:57:35]

```
slide title: Technique: Diagrams

              _details out of scope for this talk_

important complement for tables and prose, better for:

  architecture

  flows

  relationships

  representations/layouts

  UI

        _diagram your problems, not just your solutions_
```

Diagrams are out of scope.  Again, I could talk for an hour about
this.  But you you want to use this when prose and tables are
inadequate.  A lot of times when you are talking about flow,
relationships between things, visual representations are super
important.  So you want to do that.

The one tip I would give you here is: this is not just about
diagramming what you are going to do.  You should diagram what is
wrong.  If you do not know how things are going to flow.  If you have
this problem of: I only know this here, and in our intention we need
to know it over there, well, draw the diagram that shows: I have a
question mark about how this gets over there.  Because we presume that
this knowledge would be here, or would be in this database, and we
have not decided yet how it gets there.  So diagramming your problem
before you diagram your solution is a good technique.

[Time 0:58:24]

```
slide title: Phase: Dev

                            build it

You _understand_ why you are making the thing - solving this problem
You _know how_ to make it - few or no unknowns
You are _confident it will work_
- lots of supportive material
- keeps you on track
- facilitates adding others to team

the solutions will be _smaller_ and _more general_ due to having designed it

Have at, with you dev toolkit and techniques

  but don't build something on the same day you think of it
```

And finally, finally you have done all this design.  You have got this
top level story that has what is wrong.  What is the context?  What is
actually the cause?  What is the strategy you are going to take?  What
are the details of the implementation choices you are going to make?
You know why you are doing things.  You know how you are going to
build it.  You should have a very high confidence that what you are
going to build is going to work.  You have a ton of supportive
material.

This will help you do it.  When you are trying to do it, you do not
have to remember.  You will look at the work you did before.  If you
need to grow the team or hand it off to someone else, you have a lot
of stuff to give them.

And then the contention I will make in this talk is that: I believe
very strongly that if you take this kind of rigorous approach to doing
design, the thing you will make in the end will be smaller and more
general.  A lot of times people say, "We like this about Clojure.  We
like that about Clojure."  And it comes from this kind of a thing.  It
is just like you keep cutting it down and cutting it across, and you
end up with small things that are more composable and more general due
to having done the design.

So obviously there is a million talks about how to do dev.  I think
people have strategies for CI whatever.  This is not that talk.  The
one tip I would give you is: do not build something on the same day
you think of it.  Why not?

You have not slept on it.  I promise you, if you do this kind of work
during the day, and you start coding in the afternoon, the next
morning you are going to be like: "That?  No.  We should not have done
that."  So just do not even bother.  Go out for coffee, or talk about
something else.  But give it a day.

[Time 1:00:07]

```
slide title: Thanks!

Dan (for all the notes), Stu, Alex and my other Socratic victims
[strikethrough on "victims"] friends on the Clojure and Datomic teams.
```

So, thanks.  I want to thank especially Dan.  He is not here, but he
has been tracking me, doing a lot of mentorship of design and taking a
lot of notes, which really helped me build this talk.  And Stu and
Alex and all the people I work with on the Clojure and Datomic teams.
We do this.  I think it is hard to do, and I think it is hard to
learn.  But I think you can do it.  You can learn it.  And with
practice ...

[Time 1:00:45]

```
slide title: 

Inspiration exists, but it has to find you working

                                 -- Pablo Picasso
```

... you can accomplish things.  So thank you very much.

[Applause]
