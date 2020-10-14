# Simplicity Matters

* **Speaker: Rich Hickey**
* **Meeting: [Rails Conf 2012](https://www.youtube.com/playlist?list=PLF16D2F3A8469021E) - April 2012**
* **Video: [https://www.youtube.com/watch?v=rI8tNMsozo0](https://www.youtube.com/watch?v=rI8tNMsozo0)**

[First 50 seconds of video is Rails Conf 2012 title, and a brief promotion]

[Time 0:00:50]

Hi.  Thanks very much for inviting me.  I was told they always like to
have somebody who is really way outside of the community.  So that
would be me, apparently.  My phone booth is parked outside.

[Time 0:01:07]

```
slide title:

Simplicity Matters

Rich Hickey
```

But I am here to talk about something that I think ...

[Time 0:01:11]

```
slide title:

Simplicity is prerequisite for reliability

                      Edsger W. Dijkstra
```

... readily crosses languages, which is simplicity.  It is something I
think is super important.  And I would like you to try to imagine a
different word as the first word in this sentence.  I do not think
anything fits better than the word simplicity.


[Time 0:01:32]

```
slide title: Word Origins

+ Simple               + Easy

  sim- plex              ease < aise < adjacens

  one fold / braid       lie near

  vs. complex            vs hard
```

So we are going to talk quickly about two words, mostly because they
get conflated, and we need to stop doing that.  So the first word is
simple.  And what it means is one fold, or one braid, or twist.

And you can contrast it with complex, which means to combine many
things, or to braid together things.

And we distinguish that from easy, which in the derivation I like
means to lie near.  If you think back, when it was hard to travel,
having something nearby made it a lot easier to get, use, whatever,
than if you had to travel or expend effort to get it

So these are very different things.


[Time 0:02:22]

```
slide title: Simple

+ One fold / braid     + But not
  + One role             + One instance
  + One task             + One operation
  + One concept
  + One dimension      + About lack of
                         interleaving, not
                         cardinality

                       + Objective
```

When we talk about one fold or braid, we have to move away from
folding, because we do not actually fold our software.  And we can
look at it in terms of, maybe a piece of software, or component in
your software, fulfills one role, it has one specific task, it is
about a concept like security or scalability or access or
authorization or calculation.  Or it has a dimension.

But in particular, I want to avoid getting a fixation on the word
"one".  Because it does not mean that you only have one thing.  It
does not mean that you should have interfaces or classes, or whatever,
with only one operation, or you should only have singletons.  It is
really about the interleaving, not the cardinality.

And the main thing that distinguishes simplicity from easiness, or
simple from easy, is the fact that simple is objective.  We are going
to be able to look, and we are are going to look later in this talk at
very specific things we do in software, and think about how they may
be twisted together.  And it is something that you can go and look at,
but there is nothing subjective about it.

[Time 0:03:35]

```
slide title: Easy

+ Near, at hand                + Near our capabilities

  + on our hard drive, in      + Easy is _relative_
    our tool set, IDE, apt
    get, gem install ...

+ Near to our
  understanding / skill set

  + familiar
```

And we have easy.  And again we have to make this translation.  What
does it mean to be near?  It does not mean this library is easy
because I do not have to hop on my horse in order to get it.  So we
can talk about nearness in the same sort of physical sense, and that
means is it a part of my tool kit?  Do I normally have it installed?
Is it part of the tool kits of people that I work with?  In general,
is it at hand?

And then there is this other notion of being nearby, which is: is it
familiar to me?  Is this something that I already know?  Or does it
look similar to something that I already know?  Is it just a slight
variation on something that I already know?  That makes it easy,
because I can say: "Oh, I get that.  It is just like what I know, plus
one little difference."  And so that makes it easy.

There is a third characteristic of something being nearby in this kind
of sense, which is actually much harder to make happen, and much more
important, which is that the thing that you are doing is near your
capabilities.

You can have something installed.  I could install something really
complex, and not understand it, but it is nearby.  It may even look
exactly like something I know, but it may do something completely
different.  Again, that is going to make it hard.

But most difficult are things that are complex, which means they are
going to tax our brains in trying to manipulate them.  In other words,
it is outside of our mental capacity.  And we never talk about this,
because it is embarrassing to us.  We are in the mental work field.
The work we do is about thinking.  And so we hate to say: "Ooh.  This
is too hard for me to think about."

But it ends up we are all sort of in the same boat in terms of how
much complexity we can take on.  And we need to be frank about the
fact that there is a limit to that.  But if it is actually far away
from our capabilities, it is never going to become easy.  And yet it
may be something that we have to accomplish.  So what are we going to
do about that?

And the other thing about easiness, and the big difference between it
and simplicity, is that it is relative.  Something is hard for me
because of where I come from or what I already know.  Something is
familiar to you because of where you come from or what you already
know.  There is always going to be a relative aspect to something
being easy.  Things that are hard for me may be easy for someone else.


[Time 0:06:04]

```
slide title: Limits

+ We can only hope to
  make reliable those things
  we can understand

+ We can only consider a       [ animation of stick
  few things at a time           figure person
                                 juggling three balls ]
+ Intertwined things must be
  considered together

+ Complexity undermines
  understanding
```

So we get back to this notion of that third part: what makes something
hard for us to understand?  And we start with basic limits.  Everybody
has heard of the seven plus or minus two limit of the number of things
that you can keep in your head.  And it is actually quite analogous to
juggling limits, in terms of the actual count of things you can
manipulate.

Although of course I said when I gave a similar talk to this once I
said our max is twelve, somebody said: "I saw Cirque du Soleil and
somebody could juggle 21 balls."  Of course if he can code, you should
hire him.  That is awesome.

But we really can only think about a couple of things at a time.  And
the main problem we have with things that are not simple -- we are
going to say they are complex, they have been twisted together -- is
that as soon as you have twisted something together, when it comes
time for you to think about it, if I either have to enhance this part
of my system, I have to combine it with something else, I have to fix
a problem in it, if I pull on that thing I am trying to change, and I
get this knot of other stuff that is connected to it, I have to load
all of that stuff up in order to think about it, in order to try to
solve my problem, or enhance my software, because I have to consider
all of those things together.

So complexity, this tying of things together, is going to
fundamentally undermine our ability to understand things.  And if we
do not understand them, how can we really effectively change them or
fix them?  Or make them better?


[Time 0:07:31]

```
slide title: Change

+ Do more.  Do it differently.  Do it better

+ Changes to software require analysis and decision

+ Your ability to reason about your program is critical

  + More than tests, types, tools, process
```

So change is really the operative word.  I think we all start our
projects, maybe they are mostly startups, or green field, or whatever.
It is a beautiful day.  We have got our first stand-up.  We have got
our methodologies, or our manifestos, or practices we want to use.  We
have a great idea.  We have got the client involved.  Everything is
great the first week.  And then the second week, third week, fourth
week.

And as we keep working, what happens is: there is a new participant in
our stand-up.  It is growing in the corner of the room.  It is this
elephant.  It is called "the software we have already written".  The
elephant of the software we have already written is actually going to
completely dominate what we do.

So we are asked to do more, right?  We started, we had "do something".
OK.  That first iteration is a breeze.  We can do something.  But as
we move forward, we have to take what we already have and make it,
that elephant, do more, make it do it differently, make it do things
better.

And as we try to take on manipulating our software in order to have it
do new things, we are going to be challenged to understand it in order
to make that happen.

And I will contend that we are going to be completely dominated at
this point -- once your software is of a certain size -- you will be
dominated by complexity.  I do not care what processes you are using.
I do not care how well you test, or anything else.  Complexity, that
elephant, is going to dominate what you can do.

And you want to try to reduce the complexity of the software that you
have so you can do more.  All of those other techniques and processes
are all great, and they are important.  But this dominates.  And even
people with the best practices will talk about sort of running into a
concrete wall in terms of what they could accomplish each week, or
each iteration.  And it is this that is really stopping them from
either innovating, or changing.


[Time 0:09:33]

```
slide title: Simplicity = Opportunity

+ Architectural Agility wins

  + else - push the elephant

+ Design is about pulling things apart

+ Repurpose, substitute, move, combine, extend
```

But I do not want to characterize simplicity as only sort of a
defensive mechanism, something that you only use in order to stave off
the complexity elephant.  I believe that simplicity really buys you
opportunity in your designs.  And in fact, I will contend that
architectural agility, that is to say, the agility you get from having
built a system that is fundamentally simple, dominates all other kind
of agility.

It does not matter what kind of process you have.  If you have got the
complexity elephant over there, you are applying the process to push
an elephant.  I mean, how good can you get at it?  Only so good.

But if you built a simpler system, what you will find is that you are
going to be able to make it do different things.  The word
"architecture" is sort of like: "Ewww.  We don't do that any more.
That was like the 90s when we did architecture."  But if you do not do
this, you are wasting an enormous amount of time.

And I think it is because we have sort of demonized design, and I am
not talking about the way things look.  I am talking about the way
things work.  Because we tend to think of design as making grand plans
for how everything is going to go.  That is not actually what good
design is about.  Good design is about taking things apart.

Most of what a good designer does is say: Ugh!  That is like, too much
is going on in that.  Let us pull that into two separate things.  A
good designer intuitively does that.  Design is about taking things
apart.

Once you have done this, I think it brings genuine opportunities for
change.  If you have taken everything apart, and you have got simple
components, if you want to use them in another context, that is
easier, because you do not have to drag something else along with it.

If you want to take something you were doing and say: "I would rather
do it a different way" that is also easy, right?  Again, simplicity is
about buying us easiness.  It is buying us ease.  It is buying us
agility.  If we have made a simple system, it will be straightforward
to substitute another part.

It will be straightforward to take part of our system and say: "You
know what?  We should run that on a different box."  Or a different
set of boxes.  Or a different hosting service.  Or just completely
change the location characteristics of the software we make.  Because
we can.  Because we are not trying to drag an elephant around.

Ditto with combining different parts for different problems.  We have
built all of these different parts.  Now we have a new problem.  Oh!
Two of those parts and one new thing solves that problem.  This is
what happens for you when you have simplicity based designs.

So I would say pursuing simplicity is really about pursuing
opportunities.


[Time 0:12:23]

```
slide title:


LISP programmers know the value of
everything and the cost of nothing.

                       Alan Perlis
```

This is an old dig.  I do not really need to explain it, because I
would like to modernize it.  It has nothing to do with LISP.  It is
really this.


[Time 0:12:33]

```
slide title:

Programmers know the benefits of
everything and the tradeoffs of
nothing.
```

We are so fixated with ourselves, and our own ease of development,
like I want to sit here, and I want to push a button, and everything
just happens.  And then this thing comes down from the Internet.  And
I am in a comfy chair, and I have got a 3D visor on.

And then we look at technologies, or libraries, or tools that we want
to adopt, and again it is like: ooohh!  Cool!  A benefit.  I could do
this ten seconds faster if I use this.  Somebody says this has this
great characteristic.  We do not really look at what we are getting
along with that.

So I think we are very self focused.  We have like a culture culture
now.  We have meta culture.  We are like so infatuated with ourselves.
But we really should be thinking about our software, because that is
what we actually do.

[Time 0:13:23]

```
slide title:

[ photo of members of the band Foo Fighters ]
```

So take the Foo Fighters.  Imagine if the Foo Fighters were really
mostly concerned about how hard it was for themselves.  They are like:
"Aawww!  I don't want to learn the drums.  Or the guitar.  The
strings, they hurt my fingers!  I want something that is easy.  That
is not really far from what I know, because I do not know how to play
guitar yet."  And so instead of the Foo Fighters, they became the
Kazoo Fighters.

So there are two problems with this, right?  One: who wants to listen
to that?  It is like the Easy Bake Oven.  This is not going to produce
a good result.  The other thing which is more a question to ask
yourselves: who wants to be in that band?  Who wants to be in the band
that consistently chooses the easiest possible thing?  Do you want to
be in this band?  I don't.


[Time 0:14:21]

```
slide title: Programmers vs Programs

+ We focus on ourselves

  + programmer convenience

  + programmer replaceability

+ Rather than the programs

  + software quality, correctness

  + maintenance, change

+ _gem install hairball_
```

So there is a certain conflict between programmers and programs.
There need not be, but there is.  Currently I think we focus on
ourselves.  We focus on our own convenience.  We do this actually to
our own tremendous detriment, because our employers leverage the fact
that we love homogeneity, and we love familiarity.  And we are all
trying to be in the same room, doing the same thing, in the same
culture, just vibing on our similarity.  Because that means they can
replace us easily.

They do not want a plethora of programming languages, and all kinds of
different techniques and tools, and ways of thinking about things.
They want one.  Because if they have one, they can replace you.  So be
careful what you wish for.

Versus the programs.  What should we really be focusing on?  We should
be focusing on what we are making.  Why are we making it if we are not
going to focus on it?  We could all be happy doing other things, like
drinking margaritas by the pool.  That is not a job.  That is not
being a productive member of society.  We make things.  We should care
about what we are making, and how they come out.

So we should focus instead on the quality of the software, its
correctness, our ability to change it, maintain it, and things like
that.  And we should be careful when we are choosing things that we
want to do, that we are not looking at things and saying: "I like this
because it is good for me personally, right now."

Because some things are really easy.  Gem install some hairball.  It
is just that far away.  The complexity is so simple to get.  Just grab
something off the Internet, and you are good for the moment.  But what
is going to happen later with your program?


[Time 0:16:10]

```
slide title: Complect

[ image of different kinds of braided cords, probably from a book. ]

+ To interleave, entwine, braid

+ Don't do it!

  + Complecting things is the
    source of complexity

  + Best to avoid in the first place
```

So I think hairball is a really good analogy, because what is a
hairball?  It is all mangled together.  It really does touch this
fundamental notion, which this great word "complect" labels.  It means
to interleave, or entwine, or braid.  I love this word.  We should say
to other people when they are ruining our software with a bad design
decision: "You are complecting things right now."

Because braiding: "You are braiding."  It is kind of ... it does not
really work.  But complecting works, because you know it is bad.  It
just sounds bad.  They complected my thing.  I went on vacation.  I
came back, and it was all complected with this other thing.

So you do not want to do this.  This is where complexity comes from.
The word comes from this.  The result comes from this activity.
Taking more than one thing and tying them together in a little knot,
however easy it may have made something -- or maybe you did not do it
really thinking, you just did not think about simplicity.  You just
ended up with this -- is where complexity comes from.

And the more you do of it, the more difficult it will be for you to
make good software that is reliable, and software that you can change
and enhance.  So this is really what you are trying to avoid.  And in
order to avoid it, you have to develop sensibilities about how to
detect when it is going on.


[Time 0:17:35]

```
slide title: Making Things Easy

+ Bring to hand by installing

  + getting approved for use

+ Become familiar by learning, trying

+ But mental capability?

  + not going to move very far

+ Make challenges easy by _simplifying_ them
```

So how do we make things easy?  Because I am not saying easy is bad.
I am saying two parts of easy are really straightforward.  If you you
wanted to make something near, like in your tool kit, just choose to
use it.  You want to start using a new thing that is novel?  I mean
you do have to get over the fact that it may not be something you have
used before.  It may not be in your tool set.  It may not be what your
friends use, or what your company has approved for use yet.  But you
can do that.  You can get it.

The other thing you can do is you can become familiar with it.  You
can learn about new things.  You can read books.  If you want
everything to be familiar, you will never learn anything new.  You
have to break out of that.  But you can do that.  That is all in your
own control.

But what about this last one?  What if you really have a hard thing to
tackle?  Can you get smarter?  Is there a "Get Smarter for Dummies"?
"Get Smarter in 24 Days"?  "Get Smarter in 24 Hours"?  Two weeks?  No.
We cannot really get a whole lot smarter.  And we are not really much
smarter or dumber than each other.  We are all smart.

So if we are going tackle something more complex, either because we
want to do something that is more sophisticated for users, or you want
to write some more interesting software, solve harder problems, we
need to move them towards us.  They have the inherent complexity that
they have.  We need to move them closer to us by making sure our
implementation of them is as simple as possible.

And that is the key.  I really do want things to be easy.  But I want
them to be easy in all three senses.  If you only focus on the first
two, you are going to end up with complexity because you are going to
have that third one coming from the side.


[Time 0:19:19]

```
slide title:

  We can be creating the exact
     same programs out of
significantly simpler components
```

So this is the basic fact of this talk.  We can make the same exact
software we are making today with dramatically simpler stuff.
Dramatically simpler languages, tools, techniques, approaches.  Like
really radically simpler.  Radically simpler than Ruby, which seems
really simple.  Why aren't we?


[Time 0:19:49]

```
slide title: What's in _your_ Toolkit?

     Complexity            Simplicity
--------------------    ----------------------------

  State, Objects             Values

      Methods            Functions, Namespaces

     
     variables             Managed refs

Inheritance, switch,     Polymorphism a la carte
     matching

      Syntax                  Data

Imperative loops, fold     Set functions

      Actors                 Queues

       ORM               Declarative data manipulation

   Conditionals              Rules

  Inconsistency            Consistency
```

So let us look at some of these things.  I am not in this talk going
to break all of these down.

So we have a bunch of choices that we make.  We can write stateful
programs that are based around objects, when instead we could have
written a program that mostly manipulates values, and occasionally has
state.  We should.

We use stateful methods when we could just have an ordinary function.
An ordinary function is much much simpler in the sense that I am
talking about than a method.  And it is therefore easier to test,
easier to understand, easier to maintain, easier to combine with other
things.

Variables are things that are very complex and should be avoided as
much as possible.  You may or may not have choices in the languages
that you use.

Every time you inherit.  Every time you write an involved switch
statement, or use pattern matching, instead of a polymorphism
construct, you are adding complexity to your system.

This one is particularly interesting: syntax.  Syntax is inherently
complex, because the word "syntax" means associating meaning with
order, with position.  That is what it means to have a syntax.  So
when we write DSLs and things like that, we have to think about the
fact that we are adding complexity.  We might choose to, We should
know that is what we are doing.

Looping we know is a form of complexity, because it is complecting a
variable with the work to do.  And it is nice, like in Ruby you have
"foreach", which is a higher level construct.  It gets you out of the
looping game.

I am not going to talk about these.

ORM is one of the most complex things you can ever touch.  And we
choose it over and over and over again, without thinking at all,
because everybody is doing it.  It is really complex.  You waste an
inordinate amount of your time on this.  And you need to look at it.

Conditionals are things we might be able to replace with rules.

And then you can look at some of the cool new database technologies
that has eventual consistency.  Eventual consistency is incredibly
complex.  It is very very difficult to think about.  So do not choose
it unless you really have to.


[Time 0:22:02]

```
slide title:

Simplicity -- the art of
maximizing the amount
of work not done -- is essential.

    http://agilemanifesto.org/principles.html
```

I really do not know what to say about this.  This is wrong.  We know
this is wrong.  Why?  Because it says: simplicity is about you.  But
we know simplicity is not about you.  Simplicity is about how twisted
up is the thing that you are making?  It has nothing to do with you.

And reducing the amount of work to be done: "gem install hairball"
reduces the amount of work to be done, for the moment.  I did not have
to write whatever the hairball does.  I now have a hairball that does
it for me.

But I do not think -- I know you guys invent gems pretty quickly --
but I don't think there is a gem, oh my god, please take all these
instances out of my project, what were we thinking?  Although I don't
know.  There are a lot of gems out there.  I know some of them are
really powerful.

So it is really wrong, and it is terrible advice.  Absolutely terrible
advice.  Simplicity is not about you.  And simplicity is hard work.
It is actually work to do the job of simplifying things.  But there is
a huge payoff.  The person who has a genuinely simpler system, a
system made out of genuinely simple parts, is going to be able to
effect the greatest change with the least work.  He is going to kick
your ass.  He is never going to gem install hairball.  He is going to
spend more time simplifying things up front.  And in the long haul he
is going to wipe the plate with you.  He or she.  Because they will
have that ability to change things when you are struggling to push
elephants around.


[Time 0:23:42]

```
slide title:

Simplicity is not an objective in
art, but one achieves simplicity
despite one's self by entering
into the real sense of things

              Constantin Brancusi
```

This is a much nicer thought about simplicity.  It is not an
objective, necessarily.  It falls out of trying to pull things apart
into their essential natures.  what does it mean to be an essential
thing?

So I want to end this talk with two examples ...


[Time 0:23:59]

```
slide title: Lists and Order

+ A sequence of things

+ Does order matter?

  + [first-thing second-thing third-thing ...]

  + [depth width height]

+ set[x y z]

  + order clearly doesn't matter
```

... of the way to think about simplicity in context, because I think
this way.

So one is lists and order.  The list and order problem.  Is there a
problem?  We know what lists are, right?  They are a sequence of
things.

But when you see a list of things, you are automatically confronted
with a question: does the order in this list matter?  Is it a list of
things that are all semantically the same, or is it a list that is
acting as sort of a tuple of three different things?

The first one here, they are all sort of homogeneous, and the second
one it is depth, width, height, it is sort of performing a little
structure with semantics.  And the problem is if you start to use that
in another part of your program, you will be like: What was first?
Was it width?  width, depth, height, or ...

You see this problem, right?  If order matters, complexity has been
introduced into the system.

And of course if you have something like sets in your language, you
can properly call out the fact: order does not matter.  And, by the
way, there are no duplicates.  So prefer that if you can.


[Time 0:24:59]

```
slide title: Why Care about Order?

+ Complects each thing with the next

+ Infects usage points

+ Inhibits change

  + [name email] -> [name phone email]

+ "We don't do that"
```

Why should you care about order?  It is a source of complexity, right?
It complects each thing with the next.  When do you see the negative
aspects of that?  Any time you use it.  Every usage point that you do
will be infected this way, because you see this when you try to change
your program.

Imagine if you said: we are going to write this part of our program,
and we are going to pass a list with name and email around.  And you
wrote a whole bunch of software that leveraged that fact.  And then
you said: aaahhh!  We need to enhance the software.  We need to put a
phone in there.  I want to stick phone in the middle.  You know what
happens.  I don't care how fancy your IDEs are, or refactoring, or
whatever.  This is a source of bugs and problems.  It is really
difficult to do because it is essentially complex.

And of course everybody I think is sitting here saying: "We don't do
that."  We have associative data structures.  We would never do that.
It is actually a language feature of some languages to make tuples
like that.  They are called product types.  It does not seem like a
feature to me.

But even if you do not do this, this fundamental problem of order, it
is there.

[Time 0:26:05]

```
slide title: Order in the Wild


```

It is all over what we do.  Because as a concept, you can lift it out
of this context and see where it comes up.

For instance, positional arguments to functions are an example of this
problem.  If you wanted to add a different argument in the middle, you
would have the same problem everywhere.  And there is a way to avoid
that.  You could use named arguments, or a map.  Now I am not saying
every language should have keyword based parameter calling.  Clojure
has positional arguments.  But you have to know when you are choosing
something like that, that you are accepting some complexity here.
Hopefully you are making a tradeoff there for some concision.

Syntax I talked about being essentially complex.  If you can use
ordinary data structures to describe what you want to convey, you are
much better off than introducing syntax.  So again, you have to think
about it.

Those other things were product types.  We know we could use maps or
hashes to do that.

Any kind of imperative program will be trumped by a declarative
program in terms of being simpler, and not having order problems.
Take an imperative program that says: set this thing to that, set that
to this, take that other thing, and now do this, and change the order
of the statements.  It is now broken.  Take a SQL program and change
the order.  It is not broken.  Of course it may be slower, and that is
a different problem.

Prolog has this problem versus Datalog.

Another interesting thing that we see in our programs all of the time.
Just calls that are chained together.  A calls B, calls C, calls D.
That is an ordered list where the order matters.  That system is going
to be harder to change than one that says: A takes whatever it
created, and puts it in a queue, and B reads from that queue.  Because
if I want to change that program, I have an easy time of it.  I do not
need to touch A.  I can make somebody else start consuming that queue.
A is unaffected.

It does not mean you have to put queues between everybody, but as an
architectural concept that reduces complexity, queues are really
important.

XML is a great example of this.  XML was designed to support text
files, where order does matter.  You cannot change the order of
sentences and have them mean the same thing.  But is that what we
should be using for our data?  Are the parsers that work for XML
really good for data?  No, they are terrible.  And I think that is
why.

Everybody says JSON, because it is simpler.  It does not have angle
brackets, because they are edgy, or ugly, or something.  It is not.  I
think intuitively people are choosing things like JSON or Clojure
literals over XML because when they have a map, it is a map!  It says
it is a map.  It is inherently a map when you read it into your
program.  It is not going to be like: eewww, did the order matter?
Would there be more than one?  All this questioning.  Because on the
tin it says what it is.  These are maps.  These are lists.  It is
data.  It is a data describing protocol.  It does not have any order
stuff in it.  That means the parsers are simpler and everything else.

And there is more.  So look for the order problem in your own
programs.


[Time 0:29:05]

```
slide title: Maps (aka hashes), Dammit!


```

How do you solve this?  Just use maps.  Or you call them hashes.  Use
them all of the time.  Just choose to use them.  First class
associative data structure rule.

You want to use a language that has idiomatic support for them.  And I
am preaching to the crowd here.  We all have this.  But people that do
not really suffer.

You want to leverage the fact that you can do generic manipulation of
these things.  So choose and use this data structure often.


[Time 0:29:34]

```
slide title: Information _is_ Simple

+ Don't ruin it

+ By hiding it behind a micro-language

  + i.e. a class with information-specific methods

  + thwarts generic data composition

  + ties logic to representation du jour

+ Represent data as data
```

All right, the second problem I want to take on.  The information
problem.  Actually it is the information non-problem.  Information is
simple.  This is a problem we create for ourselves, because we ruin
it.  We wrap it up in stupid classes that accomplish nothing.  You
would be much better off, 90% of the time you use classes to do data
things, to just use a hash instead.  You would be much, much better
off.  Your system would be simpler.  You could write generic data
processing utilities because it did not have to know about your class,
or what you called your get-whatever thingy.  You could just use it
like it is.  It actually is an associative piece of information.  I
have a name, and I have an address.  It is actually just a simple
piece of information.  Do not put stuff on top of it.

When you do that, you end up with a bunch of problems: tying yourself
to representation things, losing the ability to manipulate things
generically, marrying your representation and class names du jour
instead of saying: I know how to process maps or hashes, and that is
what I will do.


[Time 0:00:00]

```
slide title: Encapsulation

+ Is for implementation details

+ Information doesn't have implementation

  + Unless _you_ added it - why?

+ Information _will_ have representation

  + have to pick one
```

One of the reasons why people choose this, frequently, or an excuse
is: I want to encapsulate things.  Encapsulation is for implementation
details, and information does not have implementation.  Until you add
some verbs or some gook to a piece of information, it does not have
any implementation.  There was nothing to hide.

Because you are not going to change this aspect of it: all information
that anybody is actually going to touch or use has to have some
representation.  I do not care if it is directly accessible through
the map, or return values to your arguments and accessors, you are
going to have to expose some representation.  So you are not actually
getting out of that by "encapsulating".  You are not actually doing
any encapsulation.


[Time 0:31:20]

```
slide title: Wrapping Information


+ The information class:

  + IPersonInfo {

        getName();

        ... verbs and other awfulness ... }
	
  + A service based upon it:

    + IService {

          doSomethingUseful(IPersonInfo); ... }
```

So what happens when we wrap information?  This is an example from a
language that has semicolons.  But you create this class that has the
information in it, and some verbs.  And then you write services that
consume it.  What happened to you?


[Time 0:31:35]

```
slide title: Can You Move It?

+ Litmus test - can you move your subsystems?

  + out of proc, different language, different thread?

+ Without changing much

  + Not seeking transparency here
```

Well how can you tell?  Again, we want to see what kind of problems
did this create for me?  You can answer that problem by looking and
asking this question: can you move it?  Can I take this thing that I
was doing this way, can I move it?  Make it a service that something
could call?  Can you take this subsystem and move it around?

I saw somebody who was advocating people start designing their systems
as systems of systems right from the get-go.  Like make it six
services in the very first iteration.  And I said to that person: Wow!
That seems like a lot of forethought.  Why can't people morph from a
system of components to a system of systems.  And he said: because of
their languages and the way they use them.  And it was a really
telling thought.

It is the case that we fail to do this because we send these
verb-oriented things around.


[Time 0:32:31]

```
slide title: Subsystems Must Have

+ Well-defined boundaries

+ Abstracted operational interface (verbs)

+ General error handling

+ Take/return _data_

  + IPersonInfo - oops!

+ Again, maps (hashes)
```

What do we want out of something that is going to become a subsystem?
We want it to have a well defined boundary.  We want to abstract away
the operation, so the service has the verbs.  And we have to do
something about error handling.  But the biggest point is: we want to
take and return data.  We don't have this same problem.  We build
these objecty-verby things in our programs, but as soon as somebody
says: it should be on another server, we immediately stop doing that
style of programming.

Why do we do that?  We immediately say: it is going to be RESTful.  It
is going to pass data.  It is going to return data structures.  We are
going to use JSON.  All these great ideas are good over here.  Why are
they not good inside of your program?

In fact, they _are_ good inside of your program.  You are not doing
them because of conventions that you have absorbed from doing object
orientation.  This is really better.  And if you took this approach
here, moving this to there would be straightforward, because you would
have been programming with data all along.

So again, of those problems we saw before, most of them would be
solved by just using maps or hashes up front.


[Time 0:33:36]

```
slide title: Simplicity is a Choice

+ Requires vigilance, sensibilities and care

+ Equating simplicity with ease and familiarity is wrong

  + Develop sensibilities around _entanglement_

+ Your 'reliability' tools (testing, refactoring, type systems) don't
  care if program is simple or not

+ Choose simple constructs
```

So to wrap up, simplicity is definitely a choice.  This is not
something that will ever fall out of tooling, or practice, or anything
else.  You really need to do this work.  This is the most important
work that we do, because doing this work makes everything else that we
do substantially and deeply easier.

You have to get some sensibilities around it, and thinking about
things like the order problem, or "am I wrapping information?", are
the ways you get good at simplifying things.  You have to separate
simplicity and ease.

Get some sensibilities around entanglement.  Try to find entanglement.
Try to have conversations about entanglement.  Try to take part of
your stand-up and say: did we entangle anything?  Did we complect
anything yesterday?  Is this next thing we are trying to do
complecting what we already have?  Take a _moment_ to have that
conversation, and now I hope you have some language to use for that.

Do not lean on your tools.  They do not actually do this part of the
job.  They have other attributes, but they do not do this.  They do
not do this.  They do not care.

So you need to choose simple things up front.  There are a lot of not
simple things in your language.  You need to not choose them, unless
there is really a good reason.


[Time 0:34:56]

```
slide title: Simplicity _Matters_

+ Complexity inhibits understanding

  + and therefore robustness

+ Simplicity enables change

  + It is the primary source of true agility

+ Simplicity = Opportunity

+ Go make (simple) things
```

So I think this really matters.  I think it solves two fundamental
problems that we all encounter every day.  The first is: we need to
deal with complexity.  We need to keep it at a minimum.  And the only
way to do that is by making things simpler.  That is sort of obvious.

The other thing, though, is this opportunity part.  Simplicity enables
change.  I think it is the primary source of real agility.  Agility
means to do something.  It does not mean to do it over.  It does not
mean to redo it.  It does not mean to undo it.  It means to do it.  It
means that I am here, and I am going to go there.  I am not going to
go take everything apart, or throw it away, and then do this next
thing.  I am going to move from here to there.  I am going to directly
do.  That is agility.  And if you are dragging an elephant around, you
are never going to be agile.

So that is it.  Please go make some simple things.

[Audience applause]

[Time 0:35:58]

[Last 55 seconds of video is Rails Conf 2012 credits, sponsors, etc. ]
