# Maybe Not

* **Speaker: Rich Hickey**
* **Meeting: [Clojure/conj 2018](http://2018.clojure-conj.org) - November 2018**
* **Video: [https://www.youtube.com/watch?v=YR5WdGrpoug](https://www.youtube.com/watch?v=YR5WdGrpoug)**

[Time 0:00:00]
```
slide title: Maybe Not

Rich Hickey
```

Thank you.  Hi.  Everybody can hear me?  All right.

Once again, it is wonderful to see everybody here.  A lot of friends.
How many people have been here every time?  How many people it is the
first time?  Nice.  How many newlyweds?  Yes.  Oh, two!  Woo!  Yeah.
That is awesome.

Before I get started, there has been a lot of controversy about what
we are working on, and how much we are working on it, and road maps.
I hope it is evident to everyone this week what we have been working
on.  It is our fashion sense.

[Audience laughter]

And I am happy to announce tonight, with the caveat that things can
change, and also that this is completely up to me, but the five year
road map for Clojure is going to be stripes [touches his shirt],
because I know you have seen enough of my purple shirt.

And if we get enough time to work on it -- and again, no guarantees --
we have done some experimental work already -- but we may work on
scarves.

[Audience laughter]

OK.  Actually we have been working on a ton of stuff, and it is mostly
getting spoken about at the conj, but the thing we did not quite get
out in time for conj was 1.10.  But it represents a ton of work.  And
in particular, it represents a ton of work by someone who is not
getting to speak, who you just heard speak, but I would really like to
hear a super recognition for the work of Alex Miller.

[Audience applause]

All right.  Maybe not.

[Time 0:02:27]
```
slide title: $N Mistakes

+ "I call it my billion-dollar mistake.  It was the
  invention of the null reference in 1965"

                   -- Tony Hoare
```

So yeah.  It is tricky working at the bottom of everybody else's
stuff.  Being a language designer, and working on languages.  And it
is something that anyone who does it takes very seriously.  And it is
super stressful, because you just do not want to make mistakes.

But they happen.  So let us talk about N dollar mistakes.  So I am
going to start with this quote from Tony Hoare, who said that null
references were his billion dollar mistake.  And they led to all kind
of expoits in languages like C, and things like that down the line.
And of course they still exist.  And we still have nulls, although we
have Java's memory system, which makes them not necessarily exploit
vectors, but certainly still things that we are not happy to see at
run time, null pointer errors or whatnot.


[Time 0:03:25]
```
slide title: Where are nulls / options used?

+ optional requirements (args)
  + variadics and kw-args mitigate in Clojure
+ conditional provision (returns)
+ managing partial information (aggregates)
  + not idiomatic in Clojure
```

And there are many reasons why you might have put null references in a
language back when he did that had nothing to do with design
intention, or user intention.  Things like: it was easy to implement,
or it is efficient to implement, or he did not have another idea.

And in this talk, what I want to talk about is the fact that we still
use things like this.  We still have the desire to say that something
is optional, and whether we use nulls or some other thing in our
programming languages, this is still an idea.  This idea of maybe not
needing information in a certain context.

So when do we do it, and why?  Well the first is that we might
optionally require something.  So you could give me this, or not.  If
you give it to me, maybe I will have an extended set of features I
provide, but I do not need it.  So this is an argument to my function
I might not need.  And of course if you have no variadic args, and you
have a fixed number of slots and some have to be optional, you are
going to have to put your optional thing as one of the types of args.
Or if you are using something like spec, you are going to have to say
that there.

Now we do that less often in Clojure, because we have a couple of
other ways to accomodate optionality.  For instance, we have
variadics.  You can just not pass me those extra args.  I will put
them on the end, and I will have different overloads of arity, and
that is how you can get them.

Or you can say the optional args are keyword args.  And that is
another way to do that that does not have you having a nominal thing
which is a nilable, nullable, optional, maybe kind of thing in there.
But that is a place, certainly, argument lists are kind of product
types.  They have places in them.  The first argument, the second
argument, and whatnot.  If you have places, you have to put things in
places.

[Time 0:05:25]

Another place where we use optionality is in returns.  I am going to
try to find that thing for you, and if I find it I will return it, and
if I cannot find it I will return null, did not find it, some other
kind of thing.  So I might or might not provide something to you.
That is in the return value spot.

And pretty much there we do the null thing.  And we have nil punning
and everything else, because we are still having the nil party in
Lisps.

And then the core of this talk is going to be about the third context,
which I think is particularly interesting, and very challenging, which
is: how do you manage partial information in aggregates?  So I am
going to give you a collection of stuff, or a bunch of things that
have a name associated with the bunch, and then names within the
bunch.  And maybe in certain contexts I want to, or need to, see them
coming towards me, or I will or will not give you them as a provision.

We do not, in Clojure, tend to do this using nulls, right?  We do not
put a key in our map, and put nil in as the value there.  And I am
going to talk about the differences there.

So this is the context.  How do we represent optionality in programs?


[Time 0:06:51]
```
slide title: FTFY ?

Haskell

  data Maybe a = Just a | Nothing

Scala

  abstract class Any

  abstract final class Nothing extends Any

  sealed abstract class Option[+A]

  object None extends Option[Nothing]

  final case class

    Some[+A](value: A) extends Option[A]
```

So of course nils were bad, so other people fixed them for us, and we
are philistines for not yet using this.  And there are many floating
around.  This is not like: there is one answer.  There are many
answers, so probably they are not all the best.

So in Haskell there is a type called Maybe.  It is a parameterized
type, Maybe of some type a.  And it has two constructors.  You can
have just an A, or you can have nothing, which is our nil.

And then Scala uses a lot of things to make that same kind of thing
ish, somewhat.  So I think we will stick with the Haskell version
moving forward.


[Time 0:07:43]
```
slide title: Making an arg optional

+ Yesterday

  foo :: x -> y

+ Today

  foo :: Maybe x -> y

+ compiler will force foo to check - win!

+ existing callers - break :(
```

And you will hear this said: this is the way to do this.  This fixes
the problem.  What is great about it is: it forces you to check.  And
of course that is the most important thing in programming: that
somebody is watching you and making sure you are checking for nils, no
matter what the cost.  And the problem is: no one can articulate the
costs.  No one ever mentions costs.  It is all benefit.

But it is not.  So when do you see the cost of Maybe?  You see them in
program maintenance.

So yesterday I had a function.  It took an X, and returned a Y.
People wrote code to that function.

Today, I am like: you know what?  I was asking too much of you.  I
actually can get by without that X.  I am now making it optional.
This is an easing of requirements.  An easing of requirements should
be a compatible change, I think.

So we make this change.  We say foo now takes a Maybe X.  This is the
way you write optionality.  And returns a Y.  And the compiler, inside
foo, will make sure that the code in foo does not accidentally fail to
consider nothing.  Woo!  That is all win.

Except what?  This breaks existing callers.  This is a breaking
change.  It should be a compatible change, but it is a breaking
change.


[Time 0:09:20]
```
slide title: Providing a stronger return promise

+ Yesterday

  foo :: x -> Maybe y

+ Today

  foo :: x -> y

+ future callers getter stronger guarantee

+ existing callers - break :(
```

Let us talk about providing a stronger return type.  So yesterday, I
was not sure I could do the job in all cases.  I was not sure I could
provide a meaningful return value.  So I took an X, and returned a
Maybe Y.

But today, I figured out how I could give you an answer in all cases.
And so because when I was giving you that Maybe Y you had to deal with
it, I want future callers to have more certainty about what they are
getting.  So I want to make a compatible change of strengthening my
promise.

So relaxing a requirement should be a compatible change.
Strengthening a promise should be a compatible change.  So I do this.
I say: I am definitely going to give you a Y.  Guess what happened?  I
broke all of my callers again.  I broke my callers.  Because now they
have code that deals with Maybe, and they are not getting a Maybe any
more.


[Time 0:10:22]
```
slide title: What's happening?

+ Maybe/Either are not type system's 'or/union' type
  + rather, evidence of _lack_ of first-class union types
+ 'Either' is -malarkey- [strikethrough] misnomer
  + not associative / commutative / composable / symmetric
```

So what is happening here?  What is happening is that Maybe and
Either, in spite of their names, and the play on language in English,
are not actually type systems "or", no matter how many blog posts from
people that just learned Scala you read, and Haskell that you read.
This is not "or".

This is evidence of a type system that does not have "or" for types,
does not have union types, and you are trying to fix it in the user
space.  And guess what?  You cannot fix it in the user space.

Either, in particular, wow.  It is just not a beautiful thing.  It
does not mean "or".  It has got a left and a right.  It should have
been called "left right thingy", because then you would have a better
sense of the true semantics.  There are no semantics, except what you
superimpose on top of it.  And using English words to try to give you
some impression is not good, especially in this case where you are so
failing to come close to "or".

It has none of the mathematical properties.  It is not associative.
It is not commutative.  And it is not symmetric.  Actually, better
than "left right thingy" would be "sinister dexter thingy", because at
least you would have some sense of how it treats "left".  It is: quite
poorly.


[Time 0:11:53]
```
slide title: Need not be this way

Kotlin - Nullable and Non-Null types:

  var a: String = "abc"

  a = null  // compilation error

  var b: String? = "abc"

  b = null  // ok

Dotty:

  "Union types are dual of intersection types.  Values of type A | B
  are all values of type A and all values of type B.

  | is commutative: A | B is the same type as B | A."
```

So I have a reputation for bashing type systems, and I am not.  I am
bashing Maybe and Either.  But other type systems have other answers
to the same questions.

Here is Kotlin.  Kotlin has nullable and non-null types.  So if you
say "String", it is assignable from a string.  That is pretty good.
But if you try to assign null to it, it is a compilation error.  So
they have strengthened the reference types in Kotlin.  They have said:
you know what?  Null is not an OK value of all reference types, even
though the Java JVM allows you to have null as the value of a string,
we are not going to allow it in the surface language of Kotlin, even
though it compiles to byte code.

But you can have string question mark ["String?"], and question mark
is the way you add nullability to a type.  And it creates a proper
union -- all of the strings and null -- as a type.  Because types are
sets.  So it is all of the strings -- that set -- and one more thing.
And then it is assignable from both.  You can assign it from "abc" and
you can assign it from null.

If you made the changes I just described in Kotlin, you would not
break callers.  Subject to how Kotlin links, and I do not know how
Kotlin links.

Dotty, the successor to Scala that the Odersky team is working on, has
union types in their plan.  And it says of union types: union types
are the dual of intersection types.  Values of type A -- I am going to
say "or" because I think it matches -- values of type A or B are _all_
values of type A, and _all_ values of type B.  That set.  It is a set
union.  "or" is commutative.  "A or B" is the same type as "B or A".

I think this is awesome.  I have never used a type system where I have
not desperately wanted this.  So it can be different.  Do not get
lectured to by people about Maybe and Either.  They are not the best
answers in the type system world.


[Time 0:14:00]
```
slide title: What about Clojure?

+ spec/nilable
+ spec/or
```

So let us get to the harder problems.  First of all, let us talk about
Clojure's versions of those things.  Obviously we are dynamically
typed, so we do not get into the "are you doing the right thing?" game
until you add spec.  But once we add spec, we are exactly in the same
place.  We are trying to enforce, in testing, the same kinds of
things.  Are you making sure you are dealing with what you expect?
Are people passing you what you expect?  Are you returning what they
expect?  Are you providing and requiring?

So we have spec/nilable, which is an analogy to the Kotlin nullable,
and we have spec/or, which is straight "or".  Of course, our types are
just sort of predicative sets.  You have a predicate.  Things that
satisfy the predicate constitute a set.  And "or" is unions of those
sets.  And it has all of the same properties you want for "or".  That
is why we are allowed to call it "or".


[Time 0:15:01]
```
slide title: Partial information

+ when requiring / providing aggregates
+ aggregate
  from ad- "to" + gregare "flock / herd"
+ information that travels together
```

So let us talk about the hard problem.  The hard problem is this
partial information problem.  So here we are talking about providing
or supplying aggregates.  So in Clojure, we would be talking about
sending around maps.  In object oriented languages you would be
talking about sending around objects, instances of classes.  You might
have a language that has record types.  It could be that.  Or it could
be Haskell style types.

Of course we have our definition: aggregate.  And the thing that is
cool -- more secrets of giving talks -- is that it seems like I know
all of this Latin stuff.  But what happens is: I look it up, and I see
this great definition, and I am like: "oh my goodness!"  I mean, we
have known it all along.  Like our languages embed essential concepts.

And so when I looked up "aggregate", I discovered that "gregare",
which is the same root as "gregarious", it means "flock" or "herd".
And flocks or herds mean animals that travel together.  This is a
beautiful notion.  It is exactly the right notion that I need for this
talk, which is that we are trying to talk about information flow in
programs.  And we are trying to say: we are creating these sort of ad
hoc, willy nilly aggregations for the purpose of a particular
communication.  We are gathering a set of fields, sets of information,
things we know, and we are passing them around.  It is going to travel
together.

So the notion of aggregates is I think super important, and the notion
of an aggregate being a herd is really beautiful.  So we want to stick
to that.  No matter how you make aggregations in your programs, you
are doing the same thing.  You are trying to name your herds, your
flocks.


[Time 0:17:04]
```
slide title: Sets vs Slots

[ Left picture is a herd of sheep grazing near each other in an open
grassy field.  Right picture shows a collection of small square pens
bounded by short walls, with one sheep inside each pen. ]
```

So now we get to sort of a fundamental difference in how you model
this.  It is sets versus slots.

In Clojure we use maps.  That is fundamentally sets of keys, and the
things to which they are associated.  In languages with records and
whatnot, you are dealing with slots.

Of course, you can already tell which one is better.

[Audience laughter]


[Time 0:17:39]
```
slide title: Maps vs Records / Fields

+ maps are (mathematical) functions!
+ simplest functions in programming
  + keyset -> vals
  + no code, no categories
+ in Clojure, we can directly write, and invoke

  ({:a 1 :b 2} :b)  =>  2
```

So let us talk about maps.  I find it really interesting, because
people look at maps, and our use of maps, and they are like: it is
just you being lazy, blah, blah, blah.

But you know what?  The thing is ...  Russ Olsen just gave a talk, and
he was trying to talk about functional programming to people who were
just trying it.  And he talked about mathematical functions, and the
fact that they are essentially mappings, but they are essentially
abstract.  And in programming, we only get mappings via code.

That is not true, actually.  We have an even more primitive way to get
from a mapping from one set to another.  And it is the literal map.
It is saying: if you give me this, I will give you that.  If you give
me this other thing, I will give you that other thing.  And if you
give me this third thing, I will give you this third thing.  I am
saying specifically, declaratively, with no executable code, no
functions being run, nothing, a definition of a function.  A
mathematical function.  A mapping between a set and another set.  It
is a concrete thing.

It is the best function in programming, because it is the easiest one
to understand.  It should be a function.  It should be something that
you can call, if it is a function.  And we can call the keys, right?
We do this all day long.  Maps are the most fundamental functions in
programming.  They should not be denigrated.  They should be exalted.
This is the first place to start.  This is the simplest thing you can
do.

There is no code associated with it.  There are no categorical
statements that need to be made about it.  It is not like: something
of this, mapping to something of that, and binding between two ...  It
is like: no, it is this set, and that set.  An enumerated set is the
simplest possible thing.  A categoric set, or predicative set, is a
bigger notion.

So we can directly write these, and we can directly invoke them.  And
everyone knows, who works in Clojure, the feeling of this.  This is a
big deal.


[Time 0:19:57]
```
slide title: Records / Fields / Product Types

+ Place-oriented programming (PLOP)
+ Even when named fields
  + names not usually first-class indices
  + thus are not functions
+ Product types complect meaning and place

  data Person = Person String String Int Float String String
```

All right.  Records, fields, product types, blugh!  The stuff you did
before you did maps.  I will contend: even if they are immutable, this
is still place oriented programming.  There is a place for the name.
There is a place for the address.  There is a place for the other
thing.  This is not a function any more.  And in general, because even
when the fields are named, and sometimes they are not, if you just
have raw product types you have got no names.  But even when the
fields are named, so for instance a Java class, you have got names for
your fields, they are still not first class.  You cannot say: give me
this object, give me this name, give me the thing.  Obviously, you can
use Java reflection and make six function calls to get the same
effect, but it is not an invokable entity.  So they are not functions.
You do not get to use your information as a functional mapping.

And a straight product type just completely complects the meanig of
things with their position in a list.  Now I know Haskell has a record
syntax, and I am going to show that.  So I am not trying to say they
do not have a way to put names on these things.  But the fact is you
have to know the second string is different from the first because, I
do not know what.  It is not in the types.

So this is place oriented programming.

And it matters, right?  Because what is the challenge of having a
place?  There always has to be something in the place, right?  There
is this big difference between having places, and therefore spaces,
and not.


[Time 0:21:50]
```
slide title: But ...

+ At least records enumerate what's possible
+ maps completely open, no guidance
```

But -- and of course this is another thing we have to be defensive
about -- at least these records, classes, whatever, they enumerate
what is possible.  We are passing maps around, it is the wild West.
It could be anything.  How do you know what it is?  All I am going to
do is debug this thing forever.  Maps are too open.  There is no
guidance.  There is no delimiting thing.  There is nothing that
enumerates the possible herd.


[Time 0:22:20]
```
slide title: spec/keys

+ independent, reusable attributes, RDF-style

  (spec/def ::make string?)

  (spec/def ::model string?)

  (spec/def ::year (spec/and int? #(>= % 1885)))

+ aggregate to form _schema_

  + information about cars that travels together

  (spec/def ::car (spec/keys :req [::make ::model ::year]))
```

But of course that is true until you add spec.  The idea is that spec
is an orthoganal way to add that kind of communication, expression,
validation, testing, around statements you would make about your
aggregates.

And then we have similar kind of stuff.  Of course, it is not the same
at all.  What we have is RDF-style, independent, reusable attributes,
especially when they are namespaced keywords.  And we connect them to
their range specifications.  And they are all by themselves, until we
go, in a second step, and we aggregate them when we say: let us take a
set of those and name that.  And that is our little herd or flock.  We
are going to group some of them together.

And I would like to call those aggregations schemas.  They sort of
imply a shape.  And we will talk a little bit more about that shape
being not always a list, in a second.

So that is how we can say: this is information about cars that travels
together.  Car is a spec, or names a spec, which is a keys spec, which
means it is just sort of describes the keys that can be present in a
map.  And there is make, model, and year.  So this gives us the same
kind of ability to say there is a name for the herd, and there are
names for the things that could be part of the information that
travels together.  So we are sort of drawing a circle around a
particular kind of shape.  Or we are drawing a shape around the
particular set of information.


[Time 0:24:05]
```
slide title: Optionality and aggregates

+ When something is missing from a set
  + _leave it out!_
+ When something can be missing from a slot
  + make a billion dollar mistake?
  + Maybe sheep?
```

So now we are at the core question.  What do we do when some of the
stuff can be missing in a particular usage context?  We sort of talked
about this before.  We are dealing with maps in Clojure, what do we do
if we do not have the street address for some user?  What am I going
to do?  I am just going to leave the key out.  I am going to leave it
out of the set.

And there is a tremendous benefit from that, because the thing is that
in addition to the maps being functions, maps are also self
descriptive.  You can call "keys" on a map, unlike a function.  If you
want to know: "what mapping does a function make between X and Y?",
the categoric descriptions of it: "takes a string and returns a
string", that actually does not really help you understand: "if I gave
you this string, what string would I get?"  Categoric descriptions do
not really tell you what is happening in the function.

But maps as functions, you can do that.  You can say: "exactly what
things can you take?"  "keys" tells you.  Exactly what things can you
return?  "vals" tells you.  So this enumerability is super important,
which is why you do not want junk empty keys in your maps.  You want
to leave it out.  That way the map can tell you: I do not _know_ the
last name, or the address.  I do not know that.  The maps know what
they know.  That sheep is missing today.  It was sick.  It stayed in
the barn, not out in the field.  I do not have to worry about it.  It
is not like: where is Fred sheepy?  Just "not present" does not help
me.  Now I am anxious, right?  Should I have Fred sheepy?

What about slots?  Now you have a problem.  You have those boxes.  We
saw those sheep in the boxes.  If you have places, you have to have
something in the place.  These languages pride themselves on not
having uninitialized memory.  Because in the old C days, you could
just do nothing, and have at it.  When you try to touch it, it will
definitely blow up, spectacularly.

But in the area of no uninitialized memory, then you have to have
something to put there.  Which means, what are you going to put?  You
have a couple of choices.  You have billion dollar mistakes, which
they do not love.  Maybe sheep.

So that is the thing.  When you say maybe sheep, you know that that is
not really a thing.


[Time 0:26:48]
```
slide title: Context

+ RDF-style attributes are context-free
+ make it clear that Maybe things aren't real
+ e.g. either you know the ::model or not
  + in some context
+ nothing is inherently a Maybe string

  (spec/def ::model (spec/nilable string?))  [strikethrough line through that line]
```

So how do we know it is not a thing?  How do we get to: "it is not a
thing"?  Well I do think that the RDF people who are information
representation experts, who have been working on that problem for a
long time, really have good ideas.  And I think their ideas about
properties being independent, and about making declarations about
properties, about ranges, that are independent of how you might ever
put them together with other properties to form any kind of aggregate,
is a completely sound one.

And when you do that, you realize that you would never say "maybe
anything".  Because when you are talking about something in isolation,
destined to be combined in myriad ways in many different aggregates,
to be part of many different herds, who knows that it is maybe?  That
you might not need it, or will need it, definitely will need it?  You
cannot decide then, because you know this is a building block.  And
that is how you know maybe is not a good idea, maybe types.  And Ido
not care what they are, they are not really a great idea.  Especially
maybe types now in slots.

Because the thing is, there is no such thing as a maybe thing.  If
names are strings, names are always strings.  You either know the
name, or you do not know the name.  That is an orthoganal idea from
"what is a name?"  A name is a string.  Knowing a name is a different
idea.  If type systems make you jam those two things together, they
are wrong, because they are separate ideas.  We would like to keep
them separate.  We are trying to use our programs to model the world
and communicate with each other, and when we communictate with each
other you never say "I have got six maybe sheep in my truck".  Never
ever.  Nothing is inherently a maybe string.

So we do not want to do this.  And this is actually sort of usage
guidance.  We do not want to say that a thing is a nilable whatever.
Because we do not know where it is going to be used.  We would like
that to be something that happens later.  And it is part of the talk
just to talk about this.


[Time 0:29:03]
```
slide title: Optionality in aggregate schemas

  data Car = Car {make :: String,
      model :: Maybe String, year :: Maybe Int}

  (spec/def ::car (spec/keys :req [::make]
                             :opt [::model ::year]))

+ model and year are optional ...
```

Let us talk about how we do this, then.  I want to contrast these two
things.  So we have these ideas in both spaces.  If you were doing it
in Haskell -- and this now shows the record syntax, because they do
have names possible.  It is just sugar over that product type I showed
you before.  But we have the same idea.  A make is a string.  We have
a car.  It has a make, a model, and a year.  And we are saying maybe
it has a model, and maybe it has a year.

And in spec we can say the same kind of thing.  We have keys, and we
say we require the make, and that the model and the year are optional.

There is this word in your head.  It is like [sound effect].  It is
like The Telltale Heart.


[Time 0:29:52]
```
slide title: Optional when?!

+ mistake
+ unlike args/returns, there is no usage context here
+ wrong place for optionality
+ _I made this mistake too in spec_ :(
```

"When?"  When?  When?  When?  When?  When?

We do not know the model and the year.  _When_ don't we know the model
and the year?  We do not give you the model and the year.  _When_
don't we give you the model and the year?  We do not require the model
and the year.  _When_ don't we require the model and the year?  Who
knows when?

[ jump back to previous slide ]

When does this say when?  This does not say when.  This says forever
and ever and ever: cars maybe have years and models.  There are a lot
of times when they do have years and models, and there are other times
when I do not care about the years and models.  Or I only care about
the make and the model, but not the year.  Show me everything about
Ford Mustangs.

[ jump back forward a slide ]

So this is a mistake.  It is a mistake to put optionality in aggregate
definitions.  There is no usage context.  At least when you look at
function arguments and returns, you are in a usage context.  You are
saying "of function foo, it requires these arguments, and it provides
this return value".  There is like a baked in context in the fact that
you are talking about foo's arguments, and foo's return.  The context
is: when calling foo, this is required and that is not.  Making an
aggregate definition that you are going to use all over the place --
it may be an argument sometimes.  It may be a return sometimes.  It
may be arguments to five different functions that do different jobs.

It is the wrong place for optionality.  And I made the same mistake,
right?

[ jump back to previous slide ]

I just showed you this.  This is not better.  This is the same
problem.  This is not Clojure being better than Haskell, or Kotlin, or
Scala, when you put maybe in the definition of a struct or record.
This is the same problem.  There is no context here, and optionality
is context dependent.

[ jump back forward a slide ]

So I know people are wondering: oh, where is spec?  When is it going
to be finished, or whatever?  It is going to be finished when I figure
this out.  So last year I had a pang.  I saw this.  I had seen some
people using it.  I had done more thinking about it, and I realized
that this was not right.  And I spent the last year -- in addition to
other stuff, like picking out this scarf -- thinking about optionality
and how it should work.

And in particular, I saw a lot of people struggling trying to use
spec, so I am going to talk about some of the areas in which things
could be better, I think you will all recognize how maybe they have
been hard.


[Time 0:32:33]
```
slide title: What do we want?

+ maximize schema reuse
  + don't want context-driven proliferation
    + yields more code, less reuse
+ support symmetric request / response
  + call partially filled in, get more filled in
+ information-building pipelines
  + many partial information increments
```

Because a lot of times, you just do not -- I gave it to you and it
looked good.  And it is good.  I am not saying it is bad, but it could
be better, especially right in this area.

So what do we want?  So it is easy to say that things are wrong.  What
would be right?  Well what we want is to maximize schema reuse.  We
want to maximize the reusability of the idea of a herd of information
that represents a car.  The kinds of things that we might think are
interesting about cars include these things.  And we are going to give
that a name.  That helps us communicate.  It can help us validate
things.  It can help us check for errors, even before we get to
optional requiredness.  There is a lot we can do with that notion.

The other thing that we want is we want to make sure that we do not
have a proliferation of different schemas just because the contexts
are different.  My car for passing to foo.  My car for passing to bar.
My car that gets returned by baz.  We do not want that.

What happens when you do that?  Well first of all, besides having a
proliferation of types, which -- how many people have worked in typed
languages and had a proliferation of types?  Yeah, I mean it is like
what happens.  The problem with that is that is not really helping
you.  Those names do not help you.  And they drive down the
reusability of your consuming code.  I write some code that deals with
my cars.  Well my code deals with my cars.  And your code deals with
your cars.  We do not have any code that deals with cars, because we
all had to make separate cars, because we all had to make a car that
had a different masking of optionality for use in a different context.

So we do not want that.  We want to maximize the reuse of the idea of
car, or other schemas.  Other shapes.  The shape is sort of a generic
idea.  It is not yet instantiated.  The schema is a form for a model.
It is not the thing.  It is sort of like the outline of a thing.  The
form.  That is what schema means.

We want to support a whole bunch of situations.  And these are the
situations I think people have encountered, and see if you recognize
them in trying to apply spec.  For instance, there are many kinds of
APIs, especially wire protocols and things like that, that have
symmetric request - response specifications from a schema standpoint.
Give me a partially filled in form, I will give you back a more filled
in form.  That is quite a common thing.

But with spec, if you had to say, well the thing I require is you must
give me the id and the database something context, and what I provide
will definitely inclujde the names and phone numbers, but maybe not
these other things, they were forced to become two different specs.
One was the spec for what is required, and the other is the spec for
what was provided.  And everybody wanted to reuse the specs across
those things, and they wrote really goofy predicates inside to try to
reuse some stuff.

[Time 0:35:55]
