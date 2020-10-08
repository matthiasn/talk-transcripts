# Running With Scissors: Live Coding With Data

* **Speaker: Stuart Halloway**
* **Conference: [Strange Loop 2018](https://www.thestrangeloop.com/2018/sessions.html) - September 27-28, 2018**
* **Video: [https://www.youtube.com/watch?v=Qx0-pViyIDU](https://www.youtube.com/watch?v=Qx0-pViyIDU)**


[Time 0:00:00]

```
slide title: 

```

My name is Stuart Halloway, and this talk is "Running With Scissors:
Live Coding With Data".

I want to start by saying how thrilled I am to be back at one of the
most fun software conferences I have ever been to: Strange Loop.  I
hope you guys are having a great time so far as well.


[Time 0:00:20]

```
slide title: About Me

30 years programming

Languages: 8086 Assembly, C, C++, Clojure, Java,
JavaScript, Ruby, Obj-C, Perl, Python, Smalltalk

Roles: developer, founder, manager, operations, owner,
stakeholder, support, tester, trainer

Developer: Clojure, ClojureScript, Datomic
```

I usually do not do a bio slide, but as I was thinking about this one,
I felt like it was somewhat of a big deal, and I noticed I had been
doing this for 30 years.  So I have been writing software for 30 years
in a variety of programming languages, from assembly -- kind of at the
bottom of the abstraction pyramid -- to Clojure and Smalltalk at the
top of the abstraction pyramid.

And I have taken on just about every role one can have in a software
project, including often being a developer, founding a couple of
companies, managing other people, being responsible for operations,
running a support team, being a stakeholder, being a tester, and being
a teacher.

In particular, I have worked at a place that I created for 15 years
now.  And as a result of that, I have had to live with the
consequences of my past choices for quite a long time.  So a lot of
this talk is informed by living a life where you -- I tried to not
have it be a brown field, but living in a world where you are reaping
the consequences of things you did 5, and 10, and more years ago.

I am a developer on Clojure, the programming language, and very
briefly on ClojureScript.  I worked on it during its first 6 months of
life.  But anyone who has ever seen me do anything in a browser knows
that once the foundations were laid, I needed to move along.  And I am
the lead developer of the Datomic database.

In those roles, I have worked on a daily basis with Rich Hickey,
pretty much every day for the last 8 years.  He is the designer and
architect of all of those things, and deserves the lion's share of the
credit for anything that they do, and I deserve some of the credit
when they have bugs.

So let us say something about Clojure.


[Time 0:02:02]

```
slide title: About Clojure

Dynamic
Functional     [ Clojure logo ]
Hosted
Lisp
```

Clojure is a dynamic functional hosted Lisp.  When Rich started
working on Clojure, there was not a lot of demand for that.  If you
had polled focus groups, you would not have found people in 2006,
2007, saying: "You know what?  You know what we are really missing
here is a functional Lisp.  That would be super awesome."  What a
strange idea this Clojure thing is.  And yet this crazy thing has
happened that I want to take a minute to enjoy it, because it is hard
to believe, and as Clojure continues to succeed, we just keep moving
the goal posts.


[Time 0:02:36]

```
slide title: 

[ Scatter plot chart with "Average years of professional programming
experience" on horizontal axis, versus "Median salary (USD)" on
vertical axis, with many programming languages shown. ]

https://insights.stackoverflow.com/survey/2018#work-salary-and-experience-by-language
```

But I want to stop for a minute and say: "Look!"  If you look at the
StackOverflow surveys for happiness, for salary, for salary per unit
experience, Clojure is killing it.


[Time 0:02:46]

```
slide title: 

[ Scatter plot chart with "Popularity Rank on Github (by # of
Projects)" on horizontal axis, versus "Popularity Rank on Stack
Overflow (by # of Tags)" on vertical axis. ]

https://redmonk.com/sogrady/2018/08/10/language-rankings-6-18/
```

If you look at the RedMonk quadrant, nobody would have said 10 years
ago somebody was going to stick a dynamic functional Lisp in the top
right of any analyst quadrant of anything.  And that is amazing.  And
I just want to get a quick show of hands.  How many people here have
programmed Clojure professionally?  Look at that.  Nobody would have
believed that this would be possible.  Now you can applaud.  Go ahead.
That is good.  Woohoo!


[Time 0:03:14]

```
slide title: Rationale

Dynamic
Functional     [ Clojure logo ]
Hosted
Lisp
```

And so the question I want to ask is a little bit about how that
happened.  I think a lot of it, for many people, was Rich's
evangelism, and the videos that he did very early on, and has
continued to do, and conference keynotes.  And also the rationales
that he provides for these things.  So you can go to the web site, and
you can look at what we mean when we talk about being dynamic, or
functional, or hosted, or a Lisp.  And those things have been
remarkably stable over a decade now.

And so there is a ton of motivations and reasons to come and give this
Clojure thing a try.  But there is not a whole lot of: "OK, I am
sitting at the keyboard.  Now what?"  In fact, if you read the web
site, it is almost like sort of: OK, boy this hammock is super
comfortable.  I just hopped out of it, and I have this whole program
in my head.  What do I do next?


[Time 0:04:04]

```
slide title: Running with Scissors:
             Live Coding with Data

(a Clojure dev workflow)
```

And this talk is about that.  So this talk is all about Clojure dev
work flow that I use.  And I will just say right now: all caveats
apply.  There is nothing new under the sun.  There is not a single
thing that I am going to show you today that has not been different,
better, cooler in some other language, some other person, or whatever.

But I have also watched people struggle to be effective in Clojure.
And I think it is good for us to have a conversation about the things
that we do when we are sitting at the keyboard.


[Time 0:04:36]

```
slide title: Running

Work inside your running program

REPL: Read, Eval, Print, Loop

Fast feedback loop
```

So let us start with running.  What do we mean by running?  Let us not
pick up the scissors quite yet.  Running means that you develop the
program inside the program.  The program is running the entire time.
Maybe the program runs only once during its entire initial
development, and you turn it off when you are completely happy with
it.

And this is really the Lisp secret sauce: the read, eval, print, loop.


[Time 0:05:00]

```
slide title: 

[ drawing of relationship between read, eval, print, loop ]
```

And it is important to deconstruct that a little bit.  It is right
there in the acronym.  The REPL is a composition of three functions.
Read, which takes text and returns data.  Eval, which takes programs
and does something.  And print, which takes output, usually data, and
turns them back into text again.

And when people start looking at Lisp, there is one box on here that
they usually go to and they get all excited.  Right.  They see that
box in the middle of eval called "macros", and they are like: "Oh, it
is on!"  I am going to go in there and do all kinds of crazy things.

And years ago, I made the mistake of saying what the first mistake of
macro club is, and people took at as dissing of macros.  So I am going
to try to amend that today and say that the first rule of macro club
is: Don't forget all of the other clubs shown on this slide.  Macro
club is a very cool club and it is fun to hang out there, but it is
really fun to hang out in these other clubs as well.

And so I am going to give a few examples of a la carte usage of these
other functions, the functions that make up the REPL.


[Time 0:06:08]

```
slide title: A La Carte Read

    reducing over
financial transactions
                                          read
  1 (let [db (d/db conn)                instruction
  2       ent (d/entity db ftx)]       /
  3   (println (d/touch ent))         /
  4   (flush)                        /
  5   (let [action (edn/read in)  <--
  6         result (perform-cat-action action conn ftx)]
  7     (case result                ^
  8           :quit (reduced total)  \
  9           :next (inc total)       \
 10           :skip total           polymorphic
 11           :again (recur))))       processing
```

So this is a la carte usage of read.  So this is from my personal
financial management software, which I wrote for myself in Clojure,
using Clojure and Datomic.  It is completely bespoke, and it knows
specific details about the banks and credit cards that I have, and so
forth.

But when I sit down to actually process data in there, I get a stream
of data coming out of a database that represents things that banks and
credit cards know about me, or about transactions that I have
performed.  And I want to do things to those transactions.  I want to
annotate them in some way.

So this is a little bit like an inverted REPL.  There is a loop where
data is coming from the world, and I respond to it.  And that is what
that call to read is.  So what this is showing is how easy it is to do
what some people call an internal DSL in a language like Clojure.  I
have a whole dialog that I made up that I have with my data, that is
entirely specified in Clojure data.  So I did not have to write a
parser, or come up with any grammar or anything like that.  I just
said: "Look!"  I have lists and vectors and keywords.  So a keyword
categorizes a transaction.  And a map with a keyword and a string in
it categorizes the transaction and adds a comment.  And so on and so
forth.

And then that perform categorization action function is polymorphic
processing that is driven entirely by data.  So there is never any
classes or interfaces, or anything like that made.

So that is just a simple example that read is a function that you
actually call.  It does not just happen on your behalf inside the
REPL.


[Time 0:07:44]

```
slide title: Custom Print

 1 (require '[clojure.pprint :as pp]
 2          '[clojure.main as :main])
 3 (clojure.main/repl :print pp/pprint)

[ copy of REPL diagram seen earlier ]
```

Similarly with print.  This is a tiny little snippet of code that
reinstalls your REPL running the pretty printer instead of the regular
printer.

So I see people all of the time -- I see people -- I have sat down
with people at Strange Loop in the last 24 hours and had them print
some horrible ugly thing at the REPL, and then stare at it, and try to
understand what it meant.  And I agree with you -- that would suck.
Don't do that.

So this is just the tip of the ice berg of the kinds of things you
could do if you wanted to customize printing, of course.


[Time 0:08:13]

```
slide title: Custom Error Printing

[ screen shot of web browser at a page on Maria environment, available
somewhere on https://maria.cloud ]
```

This next slide shows maria.cloud.  Now if you followed along efforts
to teach beginners programming, in particular teach them Clojure, this
is a nifty little environment.  It is at maria.cloud on the web.  That
is based on the ideas of Maria Montessori, of Montessori school fame,
if your kids go to Montessori school, or you did.  And what they have
done here is: they have built an entire literate web environment.  It
is commingled text and places where you can type in code.

And when you type in code, they send it off to an evaluator.  And then
they have completely overridden print on the way back so that the
printing actually does not show you Clojure's error messages, which
are somewhat famous, shall we say.

And so this says, and I do not know whether you can read it, but I
will post these slides later.  You type in "(1+1)", and it says:
"Awww.  I see you have not done prefix notation yet.  That 1 is in
function position, not what you want."  Instead of whatever Clojure
would do, which is like: ClassCastException, jump back in the hammock.
Or something like that.

So the REPL is a powerful thing.


[Time 0:09:21]

```
slide title: Common REPL Concerns

I already have a a shell ...

Typing into a REPL sucks ...

Somebody made spaghetti code at a REPL once ...
```

That being said, there are a lot of concerns that people raise about
it.  Common concerns that I hear are: "I already have a shell.  Isn't
this just the same as that?"

Or "Typing into a REPL sucks."  Or "I saw somebody make spaghetti code
at a REPL once, and I don't want spaghetti code."


[Time 0:09:37]

```
slide title: "Just a Shell" is Not Enough

                       |         REPL            |  "Sidecar" Shell
-----------------------+-------------------------+--------------------
  program semantics    |  sequential evaluation  |  files, modules,
                       |        of forms         |  projects, etc.
-----------------------+-------------------------+--------------------
interactive semantics  |  sequential evaluation  |  special, maybe not
                       |        of forms         |    like programs
-----------------------+-------------------------+--------------------
      text -> data     |         read            |    literals?
                       |                         |    parser?
-----------------------+-------------------------+--------------------
      text -> code     |         read            |
-----------------------+-------------------------+  parser to AST?
       execute         |       eval data         |   eval text?
-----------------------+-------------------------+  object to text?
      data -> text     |         print           |     toString?
-----------------------+-------------------------+--------------------
```

Well just a shell is not enough.  And we have already seen one reason
why.  That text to code, and execution, and data back to text are all
separate functions that are composed.  Any language that you sit down
with that is not a Lisp has to answer these questions.  And if it does
not break them apart like this, then the answer is complected.

Everybody drink.

But additionally, you have the ability to turn text to data.  How much
time do you spend in non-Lisp languages taking data from primitive
formats that do not have fidelity to your language, and then turning
it into your language, and then turning that data back out again.

But equally importantly -- and this is the top couple of rows here --
when you are working at the REPL, your program semantics and your
interactive semantics are identical.  A Clojure program is the result
of sequentially evaluating a bunch of forms.  This is true even when
you layer abstractions on top of that like files, and require, and
reload, and all that sort of thing.

When people build shells on top of existing languages, it is usually
the case that those languages have a set of rules about how code comes
to be a live program, and those rules tend to be, let me say more
elaborate than "evaluate one form at a time".

They tend to have things like: "Well there are preambles, and
declarations, and you have to consider a whole file before you can
decide that it is a program."  And there are benefits to that, but I
think that there are clear benefits to having this environment that
you dev [develop] in be interactive, and be identical to the
environment in which your programs are made.


[Time 0:11:18]

```
slide title: Sidecar Shells: JShell

"The JShell state includes an _evolving code and
execution state_.  To facilitate rapid investigation
and coding, statements and expressions _need
not occur within a method_, and variables and
method _need not occur within a class_."

               -- https://openjdk.java.net/jeps/222
```

As a concrete example of the kinds of problems I am alluding to here,
we can consider the new shell that Java has.  Java added a shell, and
they added it specifically to address the problem that students,
computer science students, really do not like Java.

And they do not like Java because when they are first -- especially --
my daughter is taking AP computer science right now, and she was
exposed to a tiny bit of JavaScript and a tiny bit of Clojure before
she started her class, which is preparing her for the AP exam, and now
it is all in Java.  And she is like: "What is this?!?  Why do I have
to do all of these things before my program will start running?"

And so JShell was designed to address that, but of course they had to
go back and say: "Well what are the semantics of being a shell?"  Java
is not an interactive environment.  So Java has classes and methods,
and all of these things that have to be evaluated in a context.  And
so they had to make up a bunch of rules.

And so there are a dozen or 15 rules about how the shell is not your
program.  I do not want to write my program in that shell, because
that is not my program.  It does not provide a suitable environment to
live in.


[Time 0:12:21]

```
slide title: REPL is Not About Text Entry

[ image of computer display showing a window with a text editor split
into a top and bottom half.  The top half is file containing a Clojure
program.  The bottom half is a Clojure REPL session. ]
```

The REPL is not about text entry.  And I see this one quite commonly.
I think this is the very earliest thing that people get over.  But
when you are working at a REPL, of course you _can_ type at a REPL.
There is nothing that says there is a law that you cannot.  But that
is not how Lisp programmers have ever worked.  You work in your
favorite tool.  You can work in Cursive in IntelliJ, or Emacs, or Vim,
or Spacemacs, or VScode.  Whatever you want.  And you have all of the
affordances of a modern editor there.

And then when you want to evaluate forms, you send them to the REPL.


[Time 0:12:59]

```
slide title: Spaghetti Code?

REPL + imperative = faster spaghetti

[ photo of spaghetti on a plate, with mold growing on it ]
```

What about the spaghetti code problem?  Lots of people sit at shells
and make spaghetti, and it gets ugly fast.  I get it.  This is a real
problem.

But the problem here is not the REPL.  The REPL makes you faster, and
imperative makes spaghetti.  So REPL plus imperative is faster
spaghetti.  If you are a net negative producing developer and we speed
you up ...

[audience laughter]

we have just made things worse.  That is bad.


[Time 0:13:34]

```
slide title: Functional Code

REPL + Functional = faster bricks

[ photo of solid brick wall ]
```

This one is pretty easy, and I am actually not going to spend any time
at this conference talking about why functional programming is
important.  I will just give you a metaphor.  Functional programming
at the REPL helps you make bricks faster.  Things that you understand
how they are going to work.  They always work the same way, and you
can compose them to build your system.

So the spaghetti argument is true, but it is only true when you are
combining a shell the sort of ball of mud, ball of spaghetti
programming that we are accustomed to in imperative and most object
oriented programming.


[Time 0:14:06]

```
slide title: ... with Scissors

Don't run your entire program!

Focus: cut your code and data
  down to match the job at hand
```

What about the scissors part?  When you run your program, what are you
running?  A lot of programming languages make you think of your
program as a thing.  That is your program, and you go run it.  And
maybe you made a special program to evaluate your program.  You run
your unit tests, or whatever.

But this is not really the sort of focused way at all.  So the
scissors are about cutting your code and your data down to exactly
what you are working on.


[Time 0:14:38]

```
slide title: Talk-Specific Dev

Start with example data

  maybe generate data for exploration

Interactively test some fns

Load what you need (namespaces, vars, etc.)

Custom UI
```

And so the style here is -- I am calling for today, shopping these
names around -- task-specific dev.  And it begins, quite often, not
with code, but with example data.

And then it moves, quite often, not from the example data to code, but
from example data to generated data.  So we start with imagining the
data that our system is going to be manipulating.  And then, and only
then, interactively at the REPL develop and test functions.  When you
are doing that, you are not going to write the entire universe from
scratch.  Load what you need to make your function go.  And load
precisely what you need to make your function go.  Load just the
namespaces you need.  It is not your entire program.  It is not
necessarily what is going to happen when you run main, or whatever,
when you are in production.

And if you need to, build a little bit of custom UI to help yourself
out along the way.  A UI whose only purpose is to assist you as a
developer.


[Time 0:15:29]

```
slide title: Example Data

 1 (def dominator
 2   "Map from a move to its dominator."
 3   {:rock :paper
 4    :scissors :rock
 5    :paper :scissors})
 6
 7 (def moves
 8   "The set of legal moves."
 9   (into #{} (keys dominator)))
```

So here is an example from -- this is taken from one of these old Ruby
quizzes still on the web.  I do not know if they are still adding
them.  This is quite a few years old.  I ported this to Clojure when I
was first learning Clojure.  And so this is designing and then
building a system to play rock, paper, scissors.

So the first thing we are going to do is make some data.  The
dominator map is a map from things to the things they dominate -- or
things they are dominated by.  I get confused about that.  So the rock
is dominated by paper, scissors are dominated by the rock, the paper
is dominated by scissors.

And then moves is another piece of data.  It is just the set of legal
moves.  Note that we have not introduced any new data structures.  We
have not made any new types.  We have just walked up and said: "Look,
we have perfectly good generic data here: keywords can enumerate
things, and maps and sets can collect things."


[Time 0:16:16]

```
slide title: Generating Data

[ image of a computer screen containing code in top half:

(defn winner
  "Returns the winning move, or nil if a draw."
  [m1 m2]
  (cond
   (= m1 m2) nil
   (= (dominator m1) m2) m2
   (= (dominator m2) m1) m1
   :default (assert false)))

(s/fdef winner :args (s/cat :m1 moves :m2 moves))

(s/exercise-fn `winner)

then REPL output in bottom half]
```

Then when we go to actually develop a function that tells who the
winner is, we can test that function interactively.  And we can use
spec to generate a bunch of sample data.  So maybe rather than writing
any unit tests for a single example, I would rather generate 100
examples.  Or in this case 10, since that is what fit on the screen.
And just eyeball those examples and say: "Hey, does this look right?"

Obviously you could still add tests.  I am not advocating at all that
you do not write tests.  But when you are doing this initial
exploration, it is valuable to say, instead of look at one example,
show me what my program is going to do with 100 examples.
 
Now in this particular program, I ended up not needing to load any
code.  But in more elaborate things I do.


[Time 0:16:59]

```
slide title: Load What You Need

                          -- code
                         /
                        V
 1 (require '[clojure.data.csv :as csv]
 2          '[clojure.java.io :as io]
 3          '[clojure.pprint :as pp]
 4          '[clojure.spec.alpha :as s]
 5          '[datomic.api :as d]
 6          '[pfinance.repl :refer :all])
 7
 8 (set! *print-length* 50)
 9 (def uri "datomic:dev://localhost:4334/pfinance")
10 (def conn (d/connect uri))
11 (def db (d/db conn))  <--
                            \
                             state
```

This is the setup stanza I use when I am doing my personal finances.
So there is a "require" that installs a bunch of namespaces that I
need.  And then it connects to the database where I have my data.  And
then I am ready to go.

And this is not, in some sense -- I have never actually run this
program from main.  Not that there is anything wrong with that, but
this is just a start-at-the-REPL, build a thing you need, and then
move along with that.

The next thing that people hit with this is: as soon as the data gets
large ...


[Time 0:17:30]

```
slide title: Custom UI

Don't pound your head against a wall of text

  pretty-print (and print-table) it

  inspect it

  make a spreadsheet

  make HTML

  make a picture
```

they are pounding their head against a wall of text.  Do not do this.
I have already showed pretty print.  Clojure also has print-table.
Clojure has an inspector.  Or you could send your data to a
spreadsheet.  Or you could make HTML.  Or you could create a picture
with it.  But don't do things like this.


[Time 0:17:46]

```
slide title:  No

[ very large list of maps filling the screen as text, without
pretty-printing ]
```

So here I have just made up some junk data.  It is a bunch of alpha
beta values between zero and 100.  And it is deliberately
en-small-enated so that you cannot necessarily read it.  Because you
do not want to try to look at something like this.

But you do not have to do this.


[Time 0:18:05]

```
slide title: Inspect It

(require '[clojure.inspector :as ins])
(ins/inspect-table data)

[ image of window on screen showing what the code above creates ]
```

The inspector is six inches away from you when you are programming in
Clojure.  Stand up the inspector and call inspect or inspect-table.
Now I will tell you that if you are coming from almost any other Lisp,
Clojure's inspector is quite primitive.  And I am astonished that
somebody has not made one or even ten more better ones than we have
seen out there.  And I know there are stuff.  I am not trying to diss
things that have been made, because I know there are things out there
that are cool.

But I think part of the reason for this is that many people came to
Clojure not from Lisps and they did not have high expectations in this
area.  Because they were not used to having these things in other
environments, and that may be a contributing reason.  And I hope that
this talk will agitate somebody into making a cool inspector.

But -- so I do not like the inspector very much.


[Time 0:18:48]

```
slide title: Spreadsheet It

(with-open [w (io/writer "temp.csv")]
 (csv/write-csv
  w
  (map->csv data [:alpha :beta])))
(sh/sh "open" "temp.csv")

[ image showing screen shot of a spreadsheet window ]
```

That is fine.  I like spreadsheets just fine.  The spreadsheet is six
inches away from you.  Take your data, throw it into a spreadsheet,
look at it there.  Take your data, throw it into Mathematica, look at
it there.


[Time 0:19:00]

```
slide title: Picture It

Specviz: generate Graphviz from Clojure spec

[ image of drawing produced by Specviz ]

https://github.com/jebberjeb/specviz
```

Take your data and make a picture of it.  This is a coworker of mine
at Cognitect, Jeb, who has made Specviz.  So Specviz is a program that
will take Clojure specs and turn them into Graphviz.  And this is the
example from the site.

There is obviously, these kinds of pictures, there are all kinds of
fiddly things that you and make them domain specific.  But the thing
that I would say about this is that the amount of effort to produce
these data visualizations is small enough to fit inside of a single
story card.  We are not talking about making a general purpose
inspect-all-the-things thing.  We are talking about making a special
purpose, show me exactly what I need to do to help me do what I am
doing right now.


[Time 0:19:45]

```
slide title: Too Much Work?

"With a REPL first I need to do a load of import
statements.  Then populate my objects.  Then get started
with the actual debugging.  I personally don't find it
anywhere near as efficient as an IDE that has been setup."

         -- https://news.ycombinator.com/item?id=16315552



     "do" block, anyone?
                         -- me
```

Is this too much work?  I gave a talk last year about REPL-Driven
Development in Chicago at the Chicago Clojure users group.

[ https://github.com/matthiasn/talk-transcripts/blob/master/Halloway_Stuart/REPLDrivenDevelopment.md ]

And I actually never noticed the Hacker News thread on it, but while I
was researching this talk, I went back and found it.  And I found this
statement.

With the REPL, I have all of this stuff to do, blah, blah, blah, and
this is not nearly as efficient as an IDE that has been set up.  To
which I say: "Put all of the stuff that you wrote to make your REPL
exactly perfect for you inside of a "do" block.  And now you have a
single key "get back to where I was, when I want to do that thing
again".

And there are examples of this lying around all over the Clojure
repository itself.


[Time 0:20:30]

```
slide title: Rich Comment Blocks

At end of a .clj file

Sample data

Sample invocations

_Durable history of the dev process_
```

They are what I call "Rich comment blocks".  A Rich comment block
lives at the bottom of a clj file.  It contains some sample data.  It
contains some sample invocations of the code that is in that library.
And -- and this is incredibly important -- it records a durable
history of the dev process, which often includes things not done.

Sort of by definition the things that are not done are not going to be
in your code.  If they were in your code, you would have to admit that
you did them, probably.  So the things that are not done ...

But it is quite often the case that if you look through most of the
namespaces in Clojure, they have a little comment at the bottom.
These comments are rich because they provide rich detail about the
development process, and because they were written by a person named
Rich.


[Time 0:21:16]

```
slide title: Rich Comments

(comment
(do
  (refer 'set)                            setup
                                          /
  (def xs #{{:a 11 :b 1 :c 1 :d 4}    <---
           {:a 2 :b 12 :c 2 :d 6}
           {:a 3 :b 3 :c 3 :d 8 :f 42}})

  (def ys #{{:a 11 :b 11 :c 11 :e 5}
           {:a 12 :b 11 :c 12 :e 3}
           {:a 3 :b 3 :c 3 :e 7 }}))

(join xs ys)
(join xs (rename ys {:b :yb :c :yc}) {:a :a})

(union #{:a :b :c} #{:c :d :e })      <-------  expedition
(difference #{:a :b :c} #{:c :d :e})               log
(intersection #{:a :b :c} #{:c :d :e})

(index ys [:b])
)
```

And here is just one as an example.  This is a slightly modified
version of the on that is at the bottom of set.clj.  I have put a "do"
block around the top, showing that this is the part that is setting up
the state you would need to try this out.  I think that Rich did not
even bother -- I hypothesize that he did not even bother when he was
doing this because he touched it so few times that it just did not
matter.  But I put the "do" block around just so you could see the
"advanced" configuration capabilities that Clojure provides.

And then you have the expedition log.  Writing software is a journey.
But because I have had to live with the software I have written over
the last 10 years, I am always coming back and looking at it.  And I
love having these expedition logs at the bottom of files.  They take
me right back to where I was when I was doing it.

And of course if you put them -- I am not saying you have to put them
in the file with your shipping code, but if you do, if you choose to
put them there, then they are in source control.  They are not
sequestered in somebody's IDE configuration.

And because it is all made of data, you can manipulate it.  In
particular, it is about time for someone, if I was going to let you
speak, to say: "What about tests?"


[Time 0:22:27]

```
slide title: What About Tests?

Automate (re)running of REPL interactions

Instead of testing specialness, lean on language for
  lifecycle / reuse / scope / state / validation
```

Well obviously the style I am laying out today could cohabitate with
any way of writing tests you have ever done.  So I am not necessarily
saying you have to write tests differently.  But having adopted this
style of working at the REPL, I write my tests entirely differently.

After I have made a set of REPL interactions, I add some validation
checks to those interactions.  And then I have a program that runs
them as if I were at the REPL.  So it just grabs a file that gives a
log, and runs through that file, evaluates all of the forms, printing
out the results, and has maybe some checks and sanity checks where it
can blow up where things are wrong.

And I released this, I do not know, a year or two ago as a Clojure
library called transcriptor.  Transcriptor's source code is smaller
than the build file for almost any other testing framework.  I will
say that again.  Transcriptor's source code is smaller than the build
file for almost any other testing framework.

https://github.com/cognitect-labs/transcriptor

And the reason is: it does not do anything.


[Time 0:22:31]

```
slide title: Transcriptor

 1 ;; my-test.repl
 2 (require '[cognitect.transcriptor :refer (check!)])
 3
 4 ;; check exact match
 5 (+ 1 2)
 6 (check! #{3})
 7
 8 ;; check predicate (or any spec!)
 9 (+ 1 1)
10 (check! even?)


              1 ;; my-suite.repl
              2 (require '[cognitect.transcriptor :refer (check!)])
              3 (xr/run "my-test.repl")
```

Transcriptor does two things.  Actually, it does three things, maybe.
It has the ability to run a file, by which I mean evaluate it a form
at a time, printing out the results.

It has a single function called check!, which compares the result of
the most recent evaluation using Clojure spec.  So unlike testing
frameworks, I get to stand on top of a ton of great work that is in
Clojure.  I do not have to worry about -- every testing framework
eventually discovers writing its own return value comparison language.
Right?  I got back a return value.  I want to compare it to what I
think is right.  A lot of basic tests, that is an equality comparison.
But as you write more complicated tests it is no longer an equality
comparison.  I have all of Clojure spec to help me do that.


[Time 0:24:17]

```
slide title: Sets: Scissors-Ready Data

Just do it

Strongly-named keys

                    {:github/id "stuarthalloway"
                     :github/location "Chapel Hill, NC"}

    {:name/last "Halloway"
     :name/first "Stuart"}

                   {:twitter/id "stuarthalloway"
                    :twitter/joined #inst "2008-03"}
```

That is the code side, but the scissors also apply on the data side.
When you are writing programs in Clojure at the REPL, you model
information about the real world as maps, with keywords as keys and
values as values.

I have three maps on this page.  All three of them happen to be about
me.  One of them -- I know.  I am that kind of person.  Sorry.

One of them is my name, one of them is information about my Github
account, and one of them is about my Twitter account.  Imagine an
alternate reality that I am going to call slot-based programming.  And
the way slot-based programming works ...


[Time 0:24:56]

```
slide title: Slots

Enumerate prior to use

Specify names, or types, or both

Sorry, No Scissors!  -- separate API per struct

     struct Person {            struct GithubAccount {
       String last;               String id;
       String first;              Date joined;
     };                         };

               struct TwitterAccount {
                 String id;
                 Date joined;
               }
```

... is that before you can use any information, you have to enumerate
the complete set of what that information is going to be.  I am going
to use the keyword struct.  This is not any actual programming
language, but I am going to use the keyword struct.  And then in this
programming language, I make slots.

So the person has a first name and last name.  The Github account has
an id and the date joined.  And the Twitter account has the id and the
date joined.  Whatever.

Well guess what?  All of your data manipulation scissors are gone now.
You do not have generic data any more.  Each one of these structs
requires its own custom special scissors to manipulate it.

And that would be bad enough to put me off wanting to do this, but it
gets even worse when you start combining things.  Because all three of
those maps were information about me.


[Time 0:25:45]

```
slide title: Ad hoc Merge

  (def about-me
    (merge
     {:github/id "stuarthalloway"
      :github/location "Chapel Hill, NC"}
     {:name/last "Halloway"
      :name/first "Stuart"}
     {:twitter/id "stuarthalloway"
      :twitter/joined #inst "2008-03"}))


         multiple ids ok, no collision
         thanks to namespace names
```

In Clojure, if I want to put them together, I can use my scissors.  I
can call merge.  And because Clojure has qualified names as a first
class concept, when I merge things -- if I am planning on playing in
the big pond, where I am going to get data from other sources that I
do not control, I am using keywordized keys so the :github/id does not
conflict with the :twitter/id.

So I can take data in the world that I have discovered is about the
same entity and merge it together.


[Time 0:26:14]

```
slide title: Ad Hoc Enumeration

(defn keys-named
 "Given map m, return all the keys whose name
  component is n."
 [m n]
 (filter #(= (name %) "id") (keys m)))

(keys-named about-me "id")
=> {:github/id :twitter/id}
```

[ Note: Probably the intent was to have n instead of "id" in the body
of function keys-named above. ]

Because I did not pour concrete on my data, I care about, and have
good facilities for, discovering information about my data at run
time.  And this is not sequestered in a reflection API.  This is a
primary part of the programming experience.

So here I have a little helper function that says "Give me all of the
keys that have an unqualified name of whatever".  And so then I can
walk up to the information about me and say: "Which things look like
identifiers?"  Like their local part is "id".

And the important thing here is that I can combine things in
context-specific ways.  As soon as you model an entity, you are going
to have a context in which you know more about it.  As soon as you
model an entity, you are going to have a context in which you know less
about it.


[Time 0:26:57]

```
slide title: Perfectly Good Fact,
              or Broken Struct?

(select-keys about-me [:github/location])
=> {:github/location "Chapel Hill, NC"}
```

So what happens if I walk up to the Github information me, and I say:
"Select my location"?  I say select-keys, return a map of just the
location.  Is that a perfectly good fact, or a broken struct?  I want
to work in a world where it is a perfectly good fact.


[Time 0:27:13]

```
slide title: Slots vs. Sets

                    |     Slots     |     Sets
--------------------+---------------+----------------
     worldview      |    closed     |     open
--------------------+---------------+----------------
     genericity     |      no       | it's just maps
--------------------+---------------+----------------
    ad hoc usage    |      no       |   carve away!
--------------------+---------------+----------------
 scaling dev effort | combinatorial |     linear
```

So to run this down, slots model a closed world.  They undermine
genericness.  They undermine ad hoc usage.  And scaling the dev effort
is combinatorial.  Because once you find two pieces of information in
the world are about the same thing, you make a third thing.  That is a
combination of those.  And then you make a fourth thing, and a fifth
thing, and so on.

Now I have deliberately laid this comparison out as starkly as
possible.  I am not denying the possibility of middle ground here --
that there is a broad middle ground.  But I see a lot of people
working in a style that really looks like the left side of this table.

And, in fact, so much so that we have a special industry name for that
unnecessary combinatorial effort.


[Time 0:27:58]

```
slide title: Celebrate Needless Effort

[ Image of this book's cover:

Design Patterns

Elements of Reusable Object-Oriented Software

Erich Gamma
Richard Helm
Ralph Johnson
John Vlissides ]


https://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612
```


[Time 0:28:09]

```
slide title: Live Coding

Your running program is _tangible_

  query it

  transform it

  _program it_
```

Your running program is tangible.  Tangible means that you can query
it.  It means that you can transform it.  And it means that you can
program it.


[Time 0:28:20]

```
slide title: Query the Program

 Clojure API |    args    |    returns    | count
-------------+------------+---------------+-------
   apropos   |   stringy  |    symbols    |   N
-------------+------------+---------------+-------
   find-doc  |   stringy  |   docstrings  |   N
-------------+------------+---------------+-------
     doc     |   symbol   |   docstring   |   1
-------------+------------+---------------+-------
    source   |   symbol   | source string |   1
-------------+------------+---------------+-------
    all-ns   |      -     |  namespaces   |  all
-------------+------------+---------------+-------
  ns-publics | namespacey | map sym->var  |  all
-------------+------------+---------------+-------
    imports  | namespacey |    classes    |  all
-------------+------------+---------------+-------
```

Clojure has a bunch of functions that are about doing this.  We do not
have to go through the details of all of them, but you can call
functions that say: "Find me documentation."  You can call functions
that say: "Give me the source code."  You can call functions that say:
"Enumerate all the vars in this namespace, or all of the vars in this
program."


[Time 0:28:38]

```
slide title: Transform the Program

finish experiments / undo mistakes

  without ever leaving your running program

 Clojure API |     args      |    change
-------------+---------------+---------------
    in-ns    |      sym      |     *ns*
-------------+---------------+---------------
     def     | symbol, init? | new var root
-------------+---------------+---------------
   ns-unmap  |    ns, sym    | remove symbol
-------------+---------------+---------------
  ns-unalias |    ns, sym    | remove alias
-------------+---------------+---------------
  remove-ns  |      sym      |   remove ns
```

And you can transform the program as you go.  So you can finish an
experiment off, and then transform the program away from it.  That was
an interesting experiment.  And without leaving the program.

You can discover a mistake, repair the mistake, evaluate that form
again, and continue programming without leaving the program.  And
there are some more advanced carving thing here like removing
namespaces entirely, and so forth, that you might use occasionally.

I want you to imagine what this process is like when you are ...


[Time 0:29:09]

```
slide title: Codeveloping Two Libs

Load both libs from the REPL

Jump in and study data

  including ad-hoc programs

Make changes one def form at a time

Leave test setup in a comment
```

... for example, codeveloping two libs.  I often find myself working
in the code base of a client and a server, where in order for them to
work correctly they have to agree about things.  When I am doing this,
I load both of the libraries from the REPL, sometimes in the same
process.  Often in the same process.  That does not have to be the
case.  You could have more than one REPL process.

I jump right in and study the data.  I use the "in-ns" form to move
into a namespace and look around.  I use "def" forms to redefine
things.  I write ad hoc programs on the fly, usually very short, but
little tiny programs that help me explore the situation when something
goes wrong, and make changes one "def" form at a time.

And when I am done, I leave this setup from my exploration in a rich
comment at the bottom of the file.  I work like this all of the time.

It has come to my attention that there is another work flow ...


[Time 0:30:03]

```
slide title: Live Coding vs. Reloading

"workflow, reloaded" operates one level higher

  files and namespaces, tools help keep track

  app state must adhere to certain idioms

live coding is targeted surgery

  more precise

  developer keeps track

both have utility

https://thinkrelevance.com/blog/2013/06/04/clojure-workflow-reloaded
```

[ As of 2020-Oct, it seems that link, which redirects from
thinkrelevance.com to cognitect.com, no longer exists. ]

... advocated by another Stuart.  He wrote a blog post, Stuart Sierra,
about 5 years ago when he was working with us at Cognitect, or maybe
even it was Relevance back at that time.

And it was called workflow, reloaded, and this is the component
library in Clojure.  And I think there are a half dozen competitors to
component now.  And that is perfectly fine.  If you were working that
way, great, but I do want to draw out the contrasts.

Workflow reloaded tends to work at one level of abstraction higher
than what I am talking about.  It is working at the level of your
project, and your files, and your namespaces, and -- and this is
something that I do not have in this workflow -- it offers tooling to
help you keep track.  So it says: "You know what?  I am going to make
a change in this namespace.  That implies cascading changes to that
namespace, and that namespace, and that namespace, and I will help you
reload them."

I do not have any tools like that to help me.  As a result, the way I
work is much more targeted surgery.  I go in and I make a change to
the namespace, and I make a change to a single form.  I do not reload
the namespace.  And if that change is going to cascade other places,
then I have to think through that.

And often that is not a problem.  Often this technique helps me focus
enough that I do not have to worry about it.  But let us think about
the moments when it is a problem.  Let us say I am working in form foo
in namespace A, and I realize that that is going to have a cascading
effect.  I might be better off to track that down in my head, and
think through it, and ask the question: "Why is this effect cascading
so much?"

I think that by working at a lower level, you put yourself -- it is
that old adage of: "If something hurts, do it all of the time."  When
I am working at this level, when things slip into becoming
unnecessarily dependent on each other, it is in my face.  And so it
provides a pain point that I think, in my experience, leads to have
less coupled code.

That being said, by all means both of these things have a ton of
utility.


[Time 0:32:09]

```
slide title: What About GUI Debuggers?

"Off the rack" experience

  improved visibility

  limited/special transformations

  no/weak programmability

Not scissors
```

What about GUI debuggers?  Well GUI debuggers are what I call the "off
the rack" version of what I am talking about here.  They have a lot of
improved visibility.  They add a lot of visibility.  They give you
cool widgets.  They tend to have rather limited and special abilities
to transform things, to say I want to work on my running program while
I am in here.

Although they certainly do.  There is fix bug and restart at
breakpoint, and things like that.  But when they have those things,
they tend to be special.  They are not part of my program.  They are
not a part of my debugger.  And as a result, they tend to have no, or
very weak, programmability.  So the UI that is in my debugger are not
functions that I can call, typically.

That being said, I can imagine a world where these things come more
together, and I am sure that there are more programmable debuggers out
there.  But in my experience, debuggers do not feel like scissors.
They are not things I can take and write programs out of, and build
things on top of.


[Time 0:33:10]

```
slide title: Live Data: Clojure spec

a la carte specificity without sacrificing generality

  you get to keep your scissors

dynamic leverage

  anytime, anywhere, up to you

  fantastic for brownfield development
```

The last thing I want to talk about is Clojure spec.  Data is alive in
your Clojure program.  You are not putting it in slots.  You are
making it, manipulating it, seeing what it does.  And spec allows you
to add specificity without throwing away your scissors.  You are still
using the generic manipulation tools that can cut any kind of data.
You are still using assoc, and dissoc, and select-keys, and things
like that.

But you can add specificity when you want to.  And this is terrific
for brown field development.  So I gave a spec talk at Strange Loop a
few years ago.  I am not going to recapitulate that now.

[ He is likely referring to his talk "Agility & Robustness: Clojure
spec" given at Strange Loop in 2016:

https://github.com/matthiasn/talk-transcripts/blob/master/Halloway_Stuart/AgilityRobustnessClojureSpec.md ]


[Time 0:33:49]

```
slide title: spec as Exploration Tool

             What                           How
---------------------------------    ---------------------
what are the building blocks?        declarative structure
what invariants hold?                arbitrary predicates
how do I check?                           validation
what went wrong?                         explanation
what went right?                         conformance
docs please                                autodoc
examples please                        sample generator
am I using this right?                  instrumentation
is my code correct?                   generative testing
can I recombine pieces like this?          assertion

        https://www.youtube.com/watch?v=VNTQ-M_uSo8
```

I am going to focus on a few aspects of spec that are particularly
helpful when you are working in an existing code base.  And this is
based off a sample project that I did last year exploring a Clojure
library that wraps a Java library called clj-xchart.


[Time 0:34:06]

```
slide title: clj-xchart

note scissor-ready
   generic data
             \                 [ Image of pie chart produced here. ]
              \
               |
(c/pie-chart   V
 [["Not Pacman" 1/4]
  ["Pacman" 3/4]]
 {:start-angle 225.0
  :plot {:background-color :black}
  :series [{:color :black} {:color :yellow}]})

https://cognitect.com/blog/2017/6/19/improving-on-types-specing-a-java-library
```

So clj-xchart wraps a Java library called xchart, and it makes it
Clojurish, by which I mean it turns all of the interactions with
charts into generic data.  Which is a beautiful thing.  This is why I
picked this library.  There are dozens of Java charting libraries, and
Clojure wrappers for each.

But this one had a particularly clean: "I solved a problem with this
library."  Which is: I went from an imperative thing to: you make a
single call with data and make stuff.

So that is great.  Imagine that I have to be a programmer who is going
to maintain xchart, or clj-xchart, either one, and make changes to it.
I want to understand how it works.  And I want to dig in deeper than
what I can see from static analysis of the code.


[Time 0:34:51]

```
slide title: From Basic Predicates

(s/def ::chartable-number (s/and number? finite?))
(s/def ::x (s/every ::chartable-number :min-count 1))
(s/def ::y (s/every ::chartable-number :min-count 1))


https://cognitect.com/blog/2017/6/19/improving-on-types-specing-a-java-library
```

So I start by making some really basic predicates.  A chartable number
is something I am going to need to have.  It is a number, and it is
finite.  And an X axis is a collection of chartable numbers that has
at least one thing in it.  And a Y axis is a collection of chartable
numbers that has at least one thing in it.

Admittedly, I could say most of that even with Java's very primitive
types.


[Time 0:35:15]

```
slide title: To Testable Types

(defn axis-counts-match?
  [{:keys [x y error-bars bubble] :as args}]
  (and (= (count (second x))
          (count y)
          (count (or error-bars y))
          (count (or bubble y)))))

(defmethod data-compatible-with-render-style? :area
  [series]
  (ordered? (second (:x series))))


https://cognitect.com/blog/2017/6/19/improving-on-types-specing-a-java-library
```

But then I move on to arbitrarily complex types.  And I am using types
here not in the static typing sense, but in the generic sense of: a
type represents a set of possible values.  I can write any program I
want to decide what is a possible value.

So the predicate at the top here, axis-counts-match, it turns out that
there are multiple different ways to specify axes in the data language
in xchart, and so this predicate is verifying that all of the
different things that have to have identical cardinality, have
identical cardinality.

And then some of the data rendering styles have requirements on the
ordering of the data.  So one of the axes has to be ordered ascending.
And so the second thing here is a multimethod saying that for this
particular style of data, this data has to be ordered.

Once I have written specs like this, I can explore the domain


[Time 0:36:04]

```
slide title: Exercising Data

(s/exercise ::series/line-width)
=> ([2.0 2.0] [23 23] [16 16] [1.0 1.0]
    [0.5 0.5] [0.9375 0.9375] [74 74] [1 1] [1 1] [39 39])

(s/exercise ::series/series-name 5 generators)
=> (["Grommets" "Grommets"] ["Emacs Users" "Emacs Users"]
    ["Grommets" "Grommets"] ["Vim Users" "Vim Users"]
    ["Expected" "Expected"])


https://cognitect.com/blog/2017/6/19/improving-on-types-specing-a-java-library
```

So I can exercise data.  Here I am exercising some line widths, and
then exercising generators.

And, in a few hours ...


[Time 0:36:12]

```
slide title: Exercising Code

[ image of chart created from randomly generated data ]
```

... I was able to get all the way up to exercising code.  So this is a
randomly generated chart.  Every aspect of its configuration was
randomly generated from spec, including the names.  It is comparing
"Hit Points" and "Global Warming" and "Emacs Users" and "Pirates" and
"Vim Users".  I am not sure what we get from that.

But the interesting thing about this is: when I want to get power from
spec, I can use as much power, or as little power, as I want.  And so,
having made all of these predicates about the world, I can turn them
on selectively.


[Time 0:36:42]

```
slide title: Instrumentation

(xchart/xy-chart {"bad-chart"
                  {:x [3 2 1] :y [4 5 7]
                   :style {:render-style :area}}})

=> ExceptionInfo Call to #'com.hypirion.clj-xchart/xy-chart
   did not conform to spec:
val: {:x [:numbers [3 2 1]], :y [4 5 7],
      :style {:render-style :area}}
fails spec: :com.hypirion.clj-xchart.specs.series.xy/series-elem
at: [:args :series 1] predicate: data-compatible-with-render-style?
```

So I turned on a little bit of instrumentation, and I called xy-chart.
This was a bug.  This is a bug that the Java program does not catch.
So the underlying Java program does not catch, and the data
transformation layer does not catch.  Basically there is an invariant
about the data, and the way it catches it is that the Swing AWT thread
blows up.  Which is not very useful.  Your thing does not get drawn.
It blows up.

But I can turn on this instrumentation.  And I can turn it on at dev
time only.  I can say: "You know what?  We are going to use this in
development to make sure we are not making this mistake."


[Time 0:37:13]

```
slide title: Reflections

spec-ing (can be) interactive

specs need not be complete or exact

specs work for you, not you for specs

add support where you need/want it

get your exercise!

  generative testing found a bug _in the JVM_!
```

So what can I take away from this?  The first thing I would say is
that spec is an enormous addition to the tool belt of working
interactively, and it is totally compatible with the interactive
tangible programming style that I have been talking about here.

Secondly, specs do not need to be complete or exact.  It is not a type
system.  It is not a thing you have to jump over before your program
is allowed to do anything.  It is entirely the opposite for that.  In
particular, the specs work for you, not you for the specs.  When I was
writing the specs for this library, I was not using them to
definitively say how the library worked.  I was using them as tools to
get to exactly one piece of information that I wanted.

And so I know -- the specs are clearly marked as, well this spec does
not actually cover the entire truth of this.  Guess what?
Specification probably never does.  So might as well admit it up
front.  And you can use spec to add support where you want and need
it.

Perhaps most amazingly, when I started exercising this, within one
minute of generating charts, I uncovered a bug not in clj-xchart, the
Clojure program, nor in xchart, the Java program, but in the JVM
itself.  So as soon as I started using generative testing.

So small testing takeaway from today's talk.  If you test only by
examples, start generating data for your tests, because you are going
to find things that surprise and pain you.


[Time 0:38:36]

```
slide title: [none]

Running

  work inside your program, from a REPL

with Scissors

  precision cut your code and data down to size

Live coding

  against a tangible runtime

Live data

  explore and extend programs with spec
```

So what we have seen today is running, work inside your program from a
REPL.  With scissors -- tools where you can precision cut your code
and your data to exactly the size and shape you need to do your job,
the job you are doing.

Coding alive against a tangible runtime where you are in your program
invoking your tools, instead of living in your tools invoking your
program.  I will say that again, because it is cool.  You are living
in your program invoking your tools, instead of living in your tools
invoking your program.

With live data that you can explore and extend using spec.


[Time 0:39:15]

```
slide title:


    Running with Scissors:
    Live Coding with Data

        @stuarthalloway
```

That is running with scissors.  I am not going to take questions up
here today because we are right at the time, but I will happily stand
outside and take questions for as long as people want to talk.  I
assure you I can talk longer.  Thank you very much.

[audience applause]

[Time 0:39:30]
