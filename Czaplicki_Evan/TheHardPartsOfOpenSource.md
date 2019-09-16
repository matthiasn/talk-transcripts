# The Hard Parts of Open Source

* **Speaker: Evan Czaplicki**
* **Meeting: [Strange Loop 2018](https://www.thestrangeloop.com/2018/sessions.html) - September 2018**
* **Video: [https://www.youtube.com/watch?v=o_4EX4dPppA](https://www.youtube.com/watch?v=o_4EX4dPppA)**
* **Slides: [https://prezi.com/oowcpzsnwp-8/the-hard-parts-of-open-source](https://prezi.com/oowcpzsnwp-8/the-hard-parts-of-open-source)**

[ References to videos, books, and articles mentioned in this talk:
https://gist.github.com/evancz/b29d1ce4166a557d03474278b2b44514 ]

[Time 0:00:00]
```
slide title: The Hard Parts of Open Source

Evan Czaplicki
Elm / NoRedInk
```

Welcome, everybody.  Thanks for coming to this session.

So I am Evan Czaplicki.  I am the designer of the Elm programming
language.

[Time 0:00:17]
```
slide title:

[image of first page of the paper "Elm: Concurrent FRP for Functional
GUIs", Evan Czaplicki, 30 March 2012]
```

And I got started on it about seven years ago with a paper called
"Elm: Concurrent FRP for Functional GUIs".  And I was like, "I really
think I can make this functional programming stuff easier".  And I did
not nail it immediately with that title, but I had this idea of this
experience with typed functional programming that was really joyful.

[Time 0:00:40]
```
slide title: 
[new text added to previous slide:]

Getting set up is easy

Writing programs is fun

Community is friendly
```

And what I wanted to get out with Elm was like I wanted to take that
part that I felt was so fun and make it accessible to other people,
and share that joy that I had felt.

And so part of that is technical.  You know, you have to write a
compiler and all of this kind of stuff.  But another part is practical
stuff, like getting set up should be easy.  And that was part of what
was important to me, having spent a whole day just trying to learn
something.  Trying to see if something was interesting, and being
really frustrated.

Another piece of that was: if programming was going to be fun, I
wanted the community to be friendly.  I did not want it to be cool
club for the cool kids.  Oh, we are functional programmers and you are
not, because you are dumb.  I did not relate to that.  I just had a
nice time programming, and I wanted to share that nice time, in the
same way that I like sushi, and I might say, "Hey, you should try it
out.  It is pretty nice."  And someone might say, "No thanks".  Oh,
OK.  You know?  That is the kind of interactions I wanted to have,
because it was just about having this experience.

[Time 0:01:45]

So as I have talked to more open source developers, people who design
languages, people who work on databases, people who work on machine
learning or discussion platforms or environmental sensors, however
much we disagree on design or what our goals are, we all have stories
in common about having a friendly community is really, really
difficult.

And that is one of the places in open source where, as good as you can
be at the technical stuff, ultimately you cannot control what is going
to happen.  And if someone is going to yell, it is like "ooohhhh, I
wish that did not happen."

So I have been doing this for about seven years now, and I have
started to notice some patterns of behavior that I think probably a
lot of people who have worked in open source with larger projects
[tbd?] will relate to.

[Time 0:02:35]
```
slide title: Pattern

"Why don't you just ..."

copy the JS API directly?

release 0.18.1 now instead?

derive JSON decoders?

It is more complex than it sounds.
```

So one is this, "Why don't you just ..."

And in Elm it is like, "Why don't you just get the JS API directly?"
Or release an incremental version, instead of a bigger release?  Or,
hey, can we derive JSON decoders?

And the short answer in all of these cases is that it is more complex
than it sounds.  Like if there is something that you can think of in
five minutes, or an hour, or a day, probably someone has thought about
that and considered it.  And there might be implications that you do
not see from your perspective, but someone else in the community might
have a problem with that, that is not obvious to you.

So when you are doing design, "Why don't you just ..."  It is like
there are all these different parties that we have to make things work
for.  And I can do my best on my intuition, but ultimately even after
I spend like a week trying to design something that way, I need to go
out and show it to people, and see what objections they bring.  And
then maybe do it with another design.

[Time 0:03:32]

So this "Why don't you just ..." is quite frustrating.  And one thing
that happens is there are a lot of people who are new to the project.
So maybe there are ten thousand people who might be curious.  Oh, why
don't you just try out this kind of thing?  And the number of people
who know the full context is pretty small.  So maybe there are like
ten, twenty people.

So if it takes five minutes to say "Why don't you just blah blah
blah?", and it takes two pages of writing, and you have to write it
very carefully because if you are an influential community member,
people will refer back to what you said four or five years ago, and
say like, "Man, they are such a jerk.  Here is the evidence.  They
said this in 2013."  And it is like, "Aaahhhh, yeah, I said that in
2013.  Yeah."

So one thing that is common is like, well if it is so much work, why
don't you just delegate the work?  Right?  So this is a comment I got
in real life, and the italics are from the person talking to me.

[Time 0:04:31]
```
slide title: Pattern
[new text added to previous slide:]

There's another way to deal with this that can improve the current
situation and keep everyone (most of the people?) happy: _delegation_.
```

They said, "There is another way to deal with this.  Delegation."  And
then they go on to describe how delegation works, and what benefits it
might have.  And I was like, "Oh, very interesting.  Yes.  I had not
thought about that."

[Time 0:04:44]
```
slide title: Pattern
[new text added to previous slide:]

"This _somebody_ can also be a "reverse proxy" who's gathering
feedback."
```

And they describe a person who can do all of this work, and they say
this _somebody_ -- again, that is their italics -- can also be a proxy
who is gathering feedback, so you do not have to be in these
discussions.

So I was initially very upset about this.  So the unfiltered, in my
own mind, version, was like [gestures as if holding a telephone up to
his ear and mouth]: "Oh, hello, is this the somebody store?  Yes, we
would like someone to take unsolicited advice on the Internet.  Oh,
yeah, it is really mean.  Yeah, it is going to be rough.  Yeah, no one
is going to say thank you.  No.  Yeah, it is unpaid.  It is unpaid.
You don't have anybody?  I was told there would be _somebody_ who
would do this."

So this was me in my own life, walking around my room, just like
[gesturing with hands in very frustrated upset manner].  And that is
not a healthy place to be.  That is not how I want to look to a
community.  That is not what I want the community I am a part of to
be, either.

And when I took some time and thought about it more, I realized there
is actually a pretty reasonable assumption going on here, which is:
"Free rice means you can take as much as you want."  The rice is free.
I will take a lot of rice.

[Time 0:06:02]

And so does that imply that free labor means you can use as much as
you want?  Well the labor is free.  But in fact, this is not how labor
works.  If you do not pay for labor, you get less.  And so I think
that is sort of the root thing.  It is like: oh, well it should be
unlimited.  Anyone can help.

Now let us assume it is unlimited.  That everybody in the world
actually can help.  In practice, you actually have to work together.
These are highly technical projects.  Are you able to work well
together?  Are your goals with the project aligned?  How much time
does it take to coordinate with that person to get stuff done?  So
even if you can work with anybody you want, there are still these
limitations on who is going to be really effective in doing the right
stuff.

[Time 0:06:47]
https://discourse.elm-lang.org/t/building-trust-what-has-worked/975

So I wrote about that a little bit in this post.  Or no, sorry,
Richard wrote about that in this post here, of what actually does it
take to get involved.  And it is not just the somebody store.

[Time 0:07:05]
```
slide title: Pattern

"On whose authority?"
```

So some people may be thinking: Evan, you are doing a lot of telling
us what is the situation.  But who are you to say that?  And so this
is another pattern that I see a lot: On whose authority?

And this is actually the title of a post that was sent to the Clojure
community.  And the post started out "F*** Clojure"

"There I've said it and God it feels good."

"I say it with much admiration and respect to all the community
members."

And then they go on to say some criticisms, and talk about their
relationship with women.  And it is quite a roller coaster of a post.

But what is interesting besides sort of like it as a journal entry is
that it gets a lot of engagement, right?  So 320 comments on the
Reddit thread.  I am sure people talked about it in other contexts as
well, where there would have been more comments.

[Time 0:08:08]

And as someone who has been working on an open source project for a
bunch of years now, enough people have told me that Elm is going to
die next month that I am like, "I don't think they are right this
time."  You know, like that fear does not speak to me any more,
because I have the experience.

But there are other people in the community who do not have that same
experience, and this can be like a scary thing.  "Man, people are not
liking this thing.  Are we doing something wrong?"  They feel like
maybe it could be better.  They might get defensive.

So in one of these 320 comments the creator of Clojure says:

    "I found out about this while sitting down to spend my weekend
    contributing to the Clojure ecosystem.  Time spent in lieu of
    spending time with my wife, having already spent my work week on
    other Clojure related stuff."

And I relate to this a lot.  I have definitely written like, "Hey, I
get that there are different viewpoints, but we can't yell our
viewpoints at each other."  And that was my Saturday.  And as you work
over the course of the years, there can only be so many Saturdays that
are like that before it starts to hurt you in larger ways.

[Time 0:09:25]

So Rich Hickey goes on to say:

    "Every time I have to process a diatribe like this, and its
    aftermath, the effects on myself, my family, and my coworkers, I
    have to struggle back from "Why should I bother?", and every time
    it gets harder to justify to myself and my family that it's worth
    the time, energy, and emotional burden."

Now I have talked to some people about this post, and they thought
different things stood out.  To me, this last part is what stands out,
because I think a lot of people in open source feel this way, and
would never say it out loud.  I was really surprised to see it that
way, and it kind of gave me some confidence to talk about that kind of
stuff as well.

So we have our posts like this in the Elm community, with a bunch of
comments as well:

    "Elm is Wrong" 346 comments

    "When will Elm grow up?" 46 comments

    "Is Evan Killing Elm's momentum?" 94 comments

And I see it not just as like: Oh, man, this is hard for me to
process.  But the people I work with have a hard time processing it.
And then if you just add up all of the time.  Let us say maybe ten
minutes is spent on each of these comments -- which I think is low,
like a conservative estimate -- we are talking about like fifty hours
for this one that is just like dealing with someone's anger.  And
could that have been helping someone new, or spending time with some
family members, or learning some hobby that could get you out of work
and get you a more healthy attitude?

So one thing I hear a lot when I talk about this stuff is: If it makes
you so mad, why don't you just not read it?  Why don't you just
... not read it?


[Time 0:11:04]
```
slide title: Pattern

"All discussion is constructive"
```

So another pattern that is really common is that all discussion is
constructive.  You know, "I am just saying how I feel."  I feel like
f*** you, and I respect you a lot.  And I think you are an idiot, but
I really learned a lot from you.  And that is a difficult personal
relationship to have.  I do not know if people have people like that
in their life, but that is a difficult thing to deal with a lot.

So one discussion that was along these lines was "Should Elm have
user-definable infix operators?"  This came up recently with our
recent release.  And if we just focus on this question textually,
someone might say, "Yeah, there are cases where it makes code shorter
and more convenient."  And someone else might say, "No, because it can
make code harder to read, especially in a large team."

And textually, this is an interesting argument.  Yeah, it can make
code shorter.  That is a good point.  And, eh, it might hurt people in
a large team.  And then onlookers will sort of say, oh, which one
seems to make more sense to me?

[Time 0:12:08]

But when you take a step back, and stop thinking of it as just a
textual argument about who is right, and who is wrong, and say, "All
of these people have different priorities."  Some of them may value
flexibility a lot.  And some people might value simplicity a lot.  And
all of these people exist with different priorities.  So this person
is like, "Yeah, we should have this", really might value flexibility.
And the person who says no, is saying, "Well, all of these benefits
you are telling me about flexibility, or how code can be shorter and
more convenient, that is not persuasive to me.  That is not a 'good
rational argument', because it is not important."

And likewise, "How does it work on a large team?"  Well this does not
matter.  It is not about that.  And all of the people exist on this
spectrum with different priorities as well.  They are evaluating it
not as "Which is the true objective argument?" but "Given my
priorities, which is the one that makes the most sense to me?"

[Time 0:13:11]

So I have come to see constructive discussion is about mutual
understanding, rather than mutual agreement.  And a lot of discussions
on line are like: We are going to get to a point where you agree with
me.  Rather than saying, "Huh, this person is seeing it different.
Why is that?  Maybe they are seeing something I don't."

So when I take a step back and think about these different patterns, I
just think like, "Why?"  Why is this happening?  I don't have problems
like this in normal life.  If I am at an Elm conference, or a meetup,
nothing ever is so emotionally difficult as these interactions.

So I found this documentary called "All Watched Over By Machines of
Loving Grace" by Adam Curtis.  It is excellent, as is all of his work.
And I found through that a book called "From Counterculture to
Cyberculture".  So this revealed to me an intellectual history going
back to the 1950s that really helps explain what is going on in open
source right now.

[Time 0:14:18]

So it traces things from a book called "The Human Use of Human
Beings".  So this came out of MIT in 1952, by a person who had created
artillery that could automatically track planes and shoot them down.

And then the "Whole Earth Catalog", which was popular in the back to
the land movement.  So a lot of people in communes might have bought
this, but it was a much larger thing than that.  And then finally the
Electronic Frontier Foundation.  And it sort of ties these together in
a very interesting way.

So we will look at some of the things going on here.  In The Human Use
of Human Beings, Norbert Wiener introduces the idea of cybernetics.
He defines it as "the study of messages as a means of controlling
machinery and society".  So it is a little weird.  OK, fine.  As you
start to read it, it is like this way of, "let us not look at the
person, but let us look at the messages going around".  And that is
how we will think about how the world works.

[Time 0:15:27]

And so you see things like: words such as life, purpose, and soul are
grossly inadequate to precise scientific thinking.  Which is like
"fair enough", but also, those things like life and purpose are pretty
important to people as well, to consider.

But a person is just a special sort of machine.  We can consider it as
a thing that takes inputs and does stuff.  Emotions are just a useless
epiphenomenon.  That is real.  He said that.

Another thing is: we have modified our environment so radically, that
we must now modify ourselves in order to exist in this new
environment.  So it is sort of: how can we take a person and simplify
it down to a machine, or a system that we can understand well?  And
then once we are starting to think of people that way, well we can
improve machines.  We can add things to them and the machines get more
capabilities.  Maybe that is how we move forward as people.

And life and purpose is like, we cannot go back to that.  It is too
different now.

[Time 0:16:36]

So the connecting thread in "Whole Earth Catalog", besides Stewart
Brand, the author of this, knowing a bunch of the people in the
cybernetics group, is this idea of access to tools.  So our
relationship with our tools is going to be how we move forward.  So
this catalog starts with "We are as gods and we might as well get good
at it.  So far, remotely done power and glory -- as government, big
business, formal education, church -- has succeeded to the point where
the gross defects obscure actual gains.  In response, personal power
is developing."

So he is focused on a bunch of different topics.  And so education,
finding inspiration, shaping his environment, sharing the adventure.
Now keep in mind, this is written in 1969.  So this is before the
Internet.  And if you read these points as what an ideal view of the
Internet should be, it works really well.  Like you can find out all
sorts of interesting stuff.  You can be inspired by what is going on
out there.  You can find a place where you really fit in, even if you
don't fit in in your local community that has different values than
you.  And you can share that with whoever you want to.  Like there is
this place for self expression.

[Time 0:17:58]

And so he says, "tools that aid this process are sought and promoted
by the Whole Earth Catalog".  So some people have argued that this is
sort of like what preceded the Internet.  It sort of foresaw what was
going to happen there.  And this publication and the creator, Stewart
Brand, have been really influential.

So one of the positive quotes is "When I was young, there was an
amazing publication called The Whole Earth Catalog, which was one of
the bibles of my generation."  So that was Steve Jobs.

There was a project that Stewart Brand created called The Ten Thousand
Year Clock, which Jeff Bezos helped fund with 42 million dollars.  So
what is this book that was popular on back to the land communes,
became very influential because of this how tools, and a rejection of
hierarchy, we are somehow in this new place where we are going to
choose our own future through our connection with tools.

And finally, the Electronic Frontier Foundation.  Interestingly, the
founders of this met on the Whole Earth Lectronic Link, one of the
earliest message boards.  And so one of the founders wrote "The
Declaration of Independence of Cyberspace".

"Governments of the Industrial World, you weary giants of flesh and
steel.  You have no sovereignty where we gather."

"I declare the social space we are building to be naturally
independent of the tyrannies you seek to impose on us."

So again you see this distrust of hierarchy.  Big business has failed.
The government has failed.  We are going to find a new way through
this thing.  So one of the early cases that the Electronic Frontier
Foundation, that inspired the creation of this foundation, was there
was a programmer called Lloyd Blankenship.  And Bell South found that
some of their 911 alert system documentation had been posted on a
bulletin board.  And so they got the Secret Service involved and took
some computers that might have sensitive information.

[Time 0:19:58]

So Lloyd was arrested, and the Electronic Frontier Foundation was
created around that time to help protect people in this situation.  So
after Lloyd was arrested, he wrote something called "The Hacker's
Manifesto", which I think gives a rawer version of what is going on in
this world.

So he says: "I'm smarter than most of the other kids, this crap they
teach us bores me."

"I've listened to my teacher explain for the fifteenth time how to
reduce a fraction.  I understand it.  "No, Ms. Smith, I didn't show my
work.  I did it in my head...""

And he says: "I made a discovery today.  I found a computer.  It does
what I want it to do.  If I make a mistake, it's because I screwed up.
Not because it doesn't like me, or it feels threatened by me, or it
thinks I'm a smartass, or it doesn't like teaching and shouldn't be
here."

[Time 0:20:53]

So this guy is 21 when he is writing this.  He is someone who is very
disillusioned, not just with government, or big business, but just his
classroom, the social environment he is living in.

And he goes on to say, "This is our world now.  We explore, but you
call us criminals.  You build atomic bombs, wage wars.  He is trying
to make us believe it is for our own good, yet we are the criminals."

So again you see that explicit distrust of hierarchy.  And then,
finally, "My crime is that of outsmarting you.  Something you will
never forgive me for."

So I do not know how many people who work on open source will
recognize aspects of this attitude in interactions they have, but
there is sort of such a strong rejection of the social things going
on.  It is like, the teacher who is not teaching you well has a bunch
of other students, and it is difficult to balance all of their needs.
Maybe it is malicious, but maybe there is another reason.  But this
world view is kind of like: I outsmarted you.  You don't see it how I
see it.

[Time 0:21:58]

So when I take a step back on this intellectual pathway, the things I
sort of draw out from reading these books and things is, one: we are
gods.  Two: hierarchy has failed us.  There is sort of a deep distrust
of hierarchical structures.  I think rightly: there are a lot of bad
things that come out of hierarchy.  And finally: order will emerge
from the new technology.

So when we reconsider the patterns we see in open source, this stuff
makes a lot of sense.

So it is like, "Why don't you just ...?"  It is like we can just
through reason and rationality, figure out the answer.  Why don't you
just do the obvious thing?

Hierarchy has failed us.  So again, "On Whose Authority?" is coming
out of this tradition of "hierarchical structures have not served us
well".  We need to find a way that is not structured in that way.
Like your authority, as the author, is not legitimate on those
grounds.

And "All discussion is constructive".  It is like, "well, this is the
new technology.  This is what the new technology is producing, so this
must be the way forward to this place that we want to go."

[Time 0:23:10]

So I found this pathway really interesting, and it helped me
understand a lot what was going on.  But it is just one of a couple of
different ways of looking at how we got to this level of conflict in
open source.  So I am calling this sort of the intellectual history of
people who are primarily prioritizing freedom.

But there are other ones, such as people who are primarily
prioritizing engagement.

So I want to start with a quote:

    "The enormous expansion of communications ... has entirely
    transformed the conditions of trade and commerce.  Everything is
    done in haste, at fever pitch.  The night is used for travel, the
    day for business; even 'holiday trips' put strain on the nervous
    system."

Do people relate to that?  Holiday trips being stressful?  I feel
that.  Or I struggle with that, at least.  I try to take a break, or
whatever.

[Time 0:24:07]

    "Great political, industrial, and financial crises carry this
    excitement into far wider areas of the population than ever
    before.  Interest in political life has become universal: tempers
    are inflamed by political, religious and social struggles, party
    politics, electioneering."

Does this sound familiar to anybody?  Finally:

    "People are forced to engage in constant mental activity and
    robbed of the time they need for relaxation, sleep and rest."

So if you had to guess when this was written, it is reasonable: it
could be this year.  It could be 2017.  Or maybe someone was really
prophetic and they wrote it in like 1980.  It is like: I see where
this is all going.

So this is actually from something Freud wrote in 1902.  The part I
left out is "due to the world-wide telegraph and telephone networks"
and "the immense growth of trade-unionism".  So I think it makes sense
that he would have seen these kinds of things.  He seems like a smart
dude, or at least someone who is very sensitive to human behavior.

[Time 0:25:09]

And so this is where this intellectual history starts.  So we have
Freud, but we are going to look at two other books.  One is called
Propaganda, from 1928, and one is called Nudge, much more recent, from
2008.

So Propaganda.  This is written by Edward Bernays.  This is actually
Freud's nephew.  The connections between all of these works are crazy,
and as you look into any parts of these, like everybody met.
Everybody worked with someone's nephew, or cousin, or Mom.  It is very
strange.

So this book is essentially a bunch of stories about how Edward
Bernays created the idea of public relations.

So one of the stories he tells is about "Torches of Freedom".  So this
was an ad campaign to break the taboo against women smoking.  At the
time, men would smoke and it was acceptable to some degree.  And
women, it was very looked down upon.  So the president of the American
Tobacco Company said, "If we can break this taboo, it will be like a
gold mine opening right in our front yard."

[Time 0:26:15]

So he hires Edward Bernays, and what Edward Bernays does is: he hires
women who are good looking, but not too model-y -- that is the quote I
found: "good looking, but not too model-y" -- to walk in the Easter
Sunday parade, and smoke.  He also hired photographers to get really
good photos of these women, and then distribute those photos through
newspaper connections that he had, to make sure they got published all
around the world.

So this Torches of Freedom idea was saying: we see this trend about
women's liberation happening, and like, this is aligned with that
movement, in that this is a way of punching up against those taboos.
But it is very focused on like, hey, we are going to make a bunch of
money here.

[Time 0:27:03]

And so one of the ads that came out of this was "An Ancient Prejudice
Has Been Removed".  And what is interesting about this ad is that,
visually, it is clearly about women smoking, but textually it is
saying: toasting did it.  It is because they toast the tobacco, it is
less harsh on your throat, and that is what has removed the prejudice.
So textually they can say: look, we are not getting into politics.  We
are just saying that toasting is cool, and that is a lady who smokes.
It is like: I don't see the problem.  But meanwhile, you have hired
Edward Bernays to actually run this campaign.

Oh yeah, I want to read a little bit from his book.  This is the book.
He says:

    "The old fashioned propagandist, using almost exclusively the
    appeal to the printed word, tried to persuade the individual
    reader to buy a definite article immediately."

So his example of this is like: "You buy O'Leary's rubber bands now!"
And he is like: "That is the old fashioned way."

[Time 0:28:10]

    "The modern propagandist therefore sets to work to create the
    circumstances that will modify the custom."

It doesn't matter what this ad says.  It is about creating
circumstances such that the custom will change in whatever direction
someone pays me to change it.

So another example he gives is for Mozart Pianos.  So I do not know
exactly the finances of Mozart Pianos, but let us say they had 30 per
cent of the market share, and he gets hired to make it higher, maybe
it can go up to 35 or 40.  That would be huge for Mozart Pianos.

So Bernays comes in and he says: "OK, I could say to people 'Will you
please buy a piano?'.  But I am not going to do that.  I know that
pianos have this kind of elite cachet.  And so what I am going to do
is: I am going to make an architecture expo in New York City where we
are going to showcase music parlors, and we are going to bring in
famous people, influential artists, and musicians to be in the rooms.
We are going to have expensive tapestries, and really lean in to this
elite picture, and promote it in our connections with newspapers.

[Time 0:29:15]

He also invites architects from all over the country.  He wants
influential architects.  And they will bring designs for music
parlors.  So what this expo does is: it creates a music parlor as an
aspirational goal.  And it brings in architects, who will then go back
to wherever they are from, with designs for music parlors.  And they
will start building houses that have that, and ideally they will
influence other architects, who are not as influential, to add music
parlors as well.

And so instead of saying, "Hey will you please buy this piano?"
people are now saying, "Hey, I have this piano shaped hole that I need
to fill?  Do you have something piano-shaped?"

So again, the modern propagandist sets to work to create the
circumstances that will modify the custom.

So this got modernized and sort of made a bit nicer in Nudge.  So here
we see a nudge is any aspect of a choice architecture that will alter
people's behavior in a predictable way, without forbidding any options
or significantly changing their economic incentives.

[Time 0:30:17]

So this book has been really influential in tech recently.  So one
thing that we are probably all familiar with that is an example of
this is auto play of videos.  So you just finished a show.  It ends on
a cliffhanger because they wrote it that way.  And you are like, man,
that was cool.  And you are like, oh, my body.  Is it hungry?  Does it
need a walk?  Did it have plans for today?  Or for anything?  And then
the music starts again, and you are like: No.  Ooohhh.

So this is a nudge, right?  You are free to do some other behavior,
but through the choice architecture that was created, a predictable
amount of people do not make that free choice.

[Time 0:31:13]

So this ended up being popular at Google.  So if anyone has visited
Google cafeterias, you will probably have seen that all of the food
has been marked with colors.  So green means "eat any time", yellow
means "once in a while", red means "not often, please".  And it is all
marked.  It is actually helpful.  You can be like "Oh, I just had
_one_ red thing today!"  It is kind of nice.

But this interest in colors changing people's behavior was used at
Google in other ways.  So when you look at the history of their ad
labeling, you see something similar.  So when ads started, they sort
of just started by playing around with colors.  So maybe green is,
like, fun, or maybe this lavender purple thing is the way to go.

So in a new phase of things you start to see: OK, well let's .. can it
be something more white?  Well maybe a little more white, you know?
Well how about something like a little more white.  Instead of all of
these colors, let us just put it all in one place.  Take all of the
saturation, put it in one place.  And like, hey, it works fine.  No
problem.

[Time 0:32:25]

And then it is like, well, yellow is pretty ugly.  We could just
... it is still labeled.  It is no problem.  And then it is like, I
mean, who wanted it to be yellow?  It was not really that important.
And then, it is like, you know, the background ...  I mean, people get
it.  They get it.

So when you search for "Italy tour", for example, everything above the
fold is an ad, and it is labeled in this very, you know, subtle and
nice way.

So I found this very interesting quote from the head of text ads at
Google.  He says "we want to make it easier for users to digest
information on the page, so we are gradually trying to reduce the
number of variations of colors and patterns on the page, and bring a
little bit more harmony to the page."  Like, "we just want harmony".
And that is why we reduced one of the color elements on the page.  We
could have reduced other color elements.  It is just one color
element.  What is the big deal?

[Time 0:33:35]

So some of you may be thinking, "Evan, if you are so mad about this,
why don't you just change your default search?"  Like you typed it
into Safari, so clearly that is the default.  Well, another thing I
learned when I was looking into this is: Google paid one billion to
Apple to keep the search bar on iPhones.  Furthermore, these sums,
called "traffic acquisition costs", rose to 5.5 billion dollars, or 23
per cent of ad revenue.

So we are in a situation where a choice architecture has been created.
The circumstances have been modified such that well, I don't mind
searching in this way.  Or, I could scroll down below these ads, but I
don't really want to.  So the circumstances have been created such
that custom is modified.  And if we wanted to mess with this, it is
going to cost a lot of money.  The fact that DuckDuckGo exists,
doesn't mean that they can compete with these kinds of numbers.

[Time 0:34:37]

So I think this whole intellectual lineage leads to something that we
see in on-line communities a lot, which is: things are viral by
design.  So when Bernays starts an advertising campaign, all these
stories he tells, he always starts with a psychological hook.  So you
might observe that people process emotions by sharing them with
others.

So that might look like, someone is going about their day.  It is
fine.  And someone shows up, and they are like, "That work you did
last week, it was terrible.  It is not going to work out.  It was
really not carefully considered."  And that person feels sad.  And the
person yelling at them goes away.

So they might mope around for a day, or however long.  And hopefully
they run into a friend who hears this story and says, "Aw, man.  That
sucks, but I don't think that was really a fair assessment."  And
through talking it through, the person can sort of deal with that and
move through.

[Time 0:35:36]

Another interaction that might be possible is: you are going about
your day, and someone says, "Did you hear about that terrible thing
that is happening over there?"  And you say, "Woah, that is terrible!"
And then you see a friend and you say "Hey, did you hear about that?"
And they are like, "Ah!  That's terrible!"  And they see some of their
friends.  And they are like, "Man, that thing over there is really
bad!"  Viral!

So when we are choosing what kind of messages we want to put into
society to control it, as the cyberneticists might say, this one has a
very interesting pattern.  So when you get something that has a viral
reaction, that is something that has more engagement.  And a lot of
people who are running Silicon Valley companies in an idealistic way.
They want to make the world better through tools, they are put in this
choice architecture.  Well, you have these investors, and you don't
want to disappoint them.  There are all of these people who work at
your company.  You don't want to lay them off.  So do you want hash
tag disappointing Q3?  Or do you want the viral one?

[Time 0:36:40]

So once you have this psychological hook, you can start designing ways
to make it work better.  So the ones I have sort of noticed have been
to mix extremes.  So if we come back to our priorities graph of
different people.  These people do not necessarily congregate in the
same place, but what we really want to happen is for the most extreme
people to yell at each other as aggressively as possible.  And so one
way to do that might be to put all of the different programming
communities in one place.

So if you look at different on line discussion forums, I think the
degree to which different communities collide will predict the amount
of conflict you see there.  So Hacker News, I find that most difficult
and most combative place.  And then on r/Programming
[reddit.com/r/Programming] you will see more of that, and on the
subreddits for individual languages you will see less.  On places that
are just community places, that do not have accounts that are shared
between, you will see less.

[Time 0:37:45]

So another approach is to decontextualize the person.  So instead of
two people talking, you have "tangodango" talking to "foxtrot".  And
what is interesting here is like, when they saw each other's faces
they might be able to say, "Oh, this person is not trying to be
malicious.  They feel this way."  But when it is "tangodango", it
_could_ literally be Hitler.  It could.  You don't know.  He is in
Argentina just being like, "infix operators are stupid".  "Unclean!"

So another way to decontextualize things is to limit the amount of
characters that are available to people.  Another way is to limit the
kind of feedback that is available.  So instead of saying, "Hey, that
was pretty hurtful", you say "down!".  Like a lot of nuance is lost in
that sort of thing.

[Time 0:38:38]

So when I take a step back on all of this, I think there is a big
conflict here where there are very powerful incentives for our
interactions to go really poorly.  And I do not think the intellectual
history of freedom is really well set up to protect against that.
Like if you are living in a choice architecture that predictably
alters people's behavior, yeah, you were given a free choice, but you
happened to choose a different thing 30 per cent of the time.

So this got me interested in a different pathway.  So I ask a lot,
"Why don't I have any of these problems in person?"  So like at work,
or at conferences, or at meetups, or on the street.  All of these
places are _for_ something.  So when a place is for something, you can
ask, "What is inappropriate behavior?"

If I am at work and a discussion keeps going and going, at some point
we have to stop having the discussion and make a choice.  We cannot be
in discussion forever.  It is clear because at work is for work.

[Time 0:39:40]

And at a conference it is against the norms to jump up on a stage and
be like, "That is wrong!"  The idea is that you carefully select
speakers who might have something interesting to say to folks, and try
to officially, and in a nice way, present that.

At a meetup, if someone is being really aggressive, there are ways to
say, "aaahhh, I need to go to the bathroom".  There are ways out of
those kinds of conflicts, and you are talking face to face.  On the
street someone is like standing outside of Starbucks and being like,
"I had better coffee one time", that is weird.  That is weird
behavior.  "And the croissants could be done better.  I don't know
how, but they could.  This isn't it."

[Time 0:40:32]

So this idea of a place being _for_ something, I think is really
important.  And so I had this idea for intentional communication.  And
so the idea is that instead of just having a blank box you write into,
you first choose some intent.  My intent is to learn, let us say.  And
I will get prompted to, say, "what is your background?"  Maybe they
just started using Elm, and they have been using Java for a long time.
And the question is, "Why do I have to explicitly cast between Int and
Float when doing math?"  And then I can submit the post.

So when that shows up, this question might have been read in a
combative way.  Like [said in a frustrated or bitter way]: "_Why_ do I
have to _explicitly_ cast between Int and Float when doing math?"  Or
[stated in kind, calm, curious tone]: "Why do I have to explicitly
cast between Int and Float ...".  Both of those are valid
interpretations of this text.  But when you give some background, it
is like, "OK, I see where this person is coming from.  I can see why
they would be frustrated with that."  And so it is way harder to read
it in a malicious way.

So instead of just having a "reply" button, maybe you can say, "OK, I
can either ask for clarification, or I can give an answer".  And so if
I say I am going to give an answer, again we might have this
structured way of replying.  Restate the question, answer it, and
then, hey we value citations.  People backing up with evidence or
experience, so maybe they give a citation.  And they can post it.

[Time 0:41:49]

And so again you get the answer.  And the person asking says, "Oh,
that is not the question I was asking, actualy."  So that can really
help clarify and make this process more efficient.  And so again,
instead of reply, maybe you say, "ask for clarification", or thank the
person.

And so there are a couple of things you can add to this that I think
would help.  So one is the idea of conversation flows.  So we saw
someone wants to learn, you can clarify or answer.  If they choose to
answer, they can ask a clarifying question, or thank you.  Now if they
clarify, maybe you give another answer.  But in the other path, "Hey,
maybe you can give me an example to clarify your question", they can
restate it, and then you can answer.  So the point here is just that
"Yell angrily" is not one of the states in the discussion flow.  It is
unreachable.

[Time 0:42:42]

So this isn't to say that all discussions should be this way, because
there are places where you want self-expression.  You say, "Hey, I had
a really nice time at the park.  Here is a photo of it".  And someone
says, "Oh, that is great.  That reminds me of last week.  We were
cooking something really nice."

And so you can have these cycles.  But when someone is doing
self-expression, and you say, "Man, that is really like a terrible
thing to say", maybe you could have this conversation flow that says,
"Hey, I want to learn about that perspective.  I don't want to tell
you it is wrong, I just want to know why you feel that way."

So what might be interesting here is, the discussion flows will be
different depending on the goals of the community.  If it is about
learning it might be one way.  If it is about self-expression it might
be another way.  And maybe you want safety valves to jump around.

So another thing that I think is interesting is, say discussion is
happening, and it is getting really out of control, and it is like,
"Hey, this is nice", and by the end they are like, "Your Mom is a bad
person, and she threw a bicycle on the ground".  I don't know.  So
this is where you really don't really want things to go.

[Time 0:43:46]

So one thing that might be interesting is when you see someone about
to reply, you say, "Hey, what would be a successful conclusion to this
interaction?"  Or, "Would it be easier to chat for five minutes?"  Is
there somewhere to take this that is going to be more constructive.
What do you want to get out of this?

Another thing that might be really valuable.  So we talked about up
vote, down vote stuff.  When someone gets down voted, they think to
themselves, "These are people who just can't take it.  I outsmarted
them, and they can't accept that."  But the people might actually be
saying, "Man, that was pretty rude and uncalled for."  And so that
feedback is not reaching that person that may feel increasingly
alienated by these kinds of reactions.  Furthermore, these buttons
sort of uniquely pick out, "Oh, I'm mad", or "Oh, I like that".

So what we might be able to do instead is say, "Hey, for any post,
here are a couple of things you might notice about it."  Is it off
topic?  Is it helpful?  And if the goal of the place is to help
professionals, maybe these are the ones you want to choose.

But if the goal is helping beginners, maybe you want to choose "Scary"
vs. "Encouraging", or "Confusing" vs. "Clear".  And if the place is
about self-expression, maybe you want to choose "Funny" and "Downer".

[Time 0:44:57]

So there are a bunch of extras.  I am running out of time, so I am
going to skip, but there are a lot of cool things to do here.

So some people may be looking at this and thinking, "If a planned
culture necessarily meant uniformity ..."  Like all of this planning
is going to ruin these communities.  So I found this book.  It says:

    "If planned culture necessarily meant uniformity or regimentation,
    it might indeed work against further evolution.  If men were very
    much alike, they would be less likely to hit upon or design new
    practices, and a culture which made people as much alike as
    possible might slip into a standard pattern from which there would
    be no escape.  That would be bad design, but if we are looking for
    variety, we should not fall back upon accident.  Many accidental
    cultures have been marked by uniformity and regimentation."

So this is from a book called "Beyond Freedom and Dignity" by
B. F. Skinner.  And I think this is one of the clearest books that is
recognizing that there are these people who understand choice
architectures, and that freedom does not help you escape from choice
architectures.  Design of other choice architectures is a way to deal
with that.

[Time 0:46:02]

So ultimately I am not here to say that, "Here is one way that is
right, or the others."  People are going to have different priorities
depending upon their life and their experiences.  I think the point
that is important is that there are a lot of people in open source
communities who are getting hurt.  So it is hard emotionally to work
on these kinds of projects.  You see people around you getting hurt.
And just saying, "Well, people are just expressing themselves" isn't
solving the question, and we have these very influential people
controlling billions of dollars who have particular goals for what
happens in these communities.

So I hope that is an interesting way to think about the hard parts of
open source, and I have a bunch of references if you are interested in
looking back on things.  And I hope people will explore, through
programming, like creating the communities that we talked about.
Maybe exploring intentional communication.  And maybe it will be
beautiful.  Maybe people won't use it.  Maybe people will use it and
then it will just become another tool for engagement.  That's likely.
We will see, but thank you very much for your attention and
consideration.

[Time 0:47:09]
