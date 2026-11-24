# Thinking In Data

* **Speaker: [Stuart Sierra](https://twitter.com/stuartsierra)**
* **Conference: [Clojure/West](http://clojurewest.org/) - March 2012**
* **Video: [https://www.infoq.com/presentations/Thinking-in-Data/](https://www.infoq.com/presentations/Thinking-in-Data/)**
* **Transcript source: [YouTube auto-generated captions](https://www.youtube.com/watch?v=cidchWg74Y4)**

[00:00:17] um uh you can you can um don't do it during the talk but later if you want do a Google search for simple programming languages or simple programming or simple whatever and and just follow your nose and and the me is is downright

[00:00:31] hysterical I'm going to share some samples of that so uh people use Simple to mean a lot of different things uh one thing that it often means is has something to do with keeping count right it's a scorekeeping

[00:00:45] thing so having one of something is simple and two of something is some somewhat more complicated and three of something and in fact some of you probably remember the interminable thread uh on

[00:00:59] the Google group how many people read this thread right the the title of the thread was simple things should be simple and it was all about the um stuff that Chaz would really uh care about right was all about automation effort

[00:01:13] around shipping some simple hello program right the the basic Automation and it was all about counting right how many lines how many lines are this how many lines are that how many are boiler plate how many tools it's all about

[00:01:26] counting uh and the presumption here is that that a small small count is simple and a big count is complex let's think about that there's a bunch of arrows all connecting something or going in One Direction that's pretty

[00:01:41] simple and if I add more arrows pretty much the same amount of simple hat tip to Rich for this example uh then I go and add one of them or two of them route in a different way right and that starts to

[00:01:57] be complex and obviously if I wanted to take more time in keynote I could make this really complex right we could have you know more and more things but the complexity here is coming not from numbers it's coming from

[00:02:12] interactions uh and varieties of interactions and things working in different ways another thing that people talk about uh when they talk about something being simple is maybe beginner friendly uh so there's a great quote

[00:02:24] here from the O'Reilly net Blog the most important gauge of programming language is how easily a novice programmer can maintain a significant Pro program in any problem domain

[00:02:41] wow I just want to let that sit there right right somebody actually stated this and it was not on April Fool's Day take pick any profession you want and translate that right the most important gauge of

[00:02:58] any basketball Playbook is how easily a junior varsity High School athlete can compete in the NBA Finals right this is this is the most you know it's it's a wonderful example of that whole sort of uh in 21 days for

[00:03:15] dummies school of thought and in Fairless to O'Reilly I don't think that that is widespread at O'Reilly at all but um since we're name it's the end of the day it's rant time so we'll do name calling a related one and this one

[00:03:28] actually has the word simplicity in it Simplicity should be fairly simple to read learn and understand python is good PHP is great C++ and Scola not so good well one of our own who's here today uh Brenton

[00:03:45] Ashworth I think had a quote that for me really uh undercuts this sort of ease of learning argument right if you were really concerned about ease of learning and that was your primary measure uh for for something being you know insert any

[00:04:01] positive thing here where are you going to end up and I think that that ease of ease of getting started is certainly a a value right that's that's absolutely something that well I shouldn't say absolutely

[00:04:18] this is one of the problems about doing a a weenie talk about words is you become incredibly paranoid about your own words so retract the word absolutely it is certainly in many settings of value that something be incredibly easy

[00:04:29] to learn I would argue that one thing you could sort of tweak that value a little bit is that if I'm going to pick a hobby that I'm going to spend a few hours on it would be really nice if that was easy to

[00:04:39] learn right plants and zombies is great right you can learn that uh extremely quickly it's not a really good basis for building a career right being able to learn something in an hour is doesn't seem to

[00:04:52] be a good way to build a career of course given that we're talking about uh closure here at the conference uh I would be Miss not to talk about Syntax for a moment because there are a lot of conversation about Simplicity uh that is

[00:05:07] about syntax and so you get this great quote we need constructs that are natural to humans not mathematics this is actually a sub bullet point to Simplicity and the construct should be consistent with the normal average non-

[00:05:21] mathematically trained brains wow the red highlighted words are the places where this is at maximum these are these are all words that people throw around rhetorically right these are all words that people throw

[00:05:38] around as generic positive right anytime you see the word natural or normal or average non-mathematical is a little bit more domain specific but natural and normal and average are all rhetorical trick words right they used to have some

[00:05:54] meaning in the Deep darkness of time but uh it's gone whatever it once was and so this is basically we're going to pick one word Simplicity and then we're going to U uh sort of weasle that with a bunch of other weasel

[00:06:07] words another one that's good is minimal maybe simple as minimal so you get this nice quote if the semantic model of a language is clear if the rules are simple and precise the language will be more

[00:06:22] productive to use less is more that's actually not half bad it has nothing to do with simple um but it's not half bad the amusing part of this is that this is from a technical article explaining what

[00:06:39] language Java so minimal is minimal is valuable but I don't want to really stop there either uncomplicated maybe simple is the opposite of complicated some of you have

[00:06:55] perhaps seen this cartoon which is a great cartoon so if you can't read the red boxes the product on the top is an Apple product which just has a button the product in the middle is a Google

[00:07:14] product which just has somewhere you can type in the find button and the picture on the bottom is your [Music] app so these things are all I mean this and this matters I think this is a great

[00:07:27] cartoon to show anybody who's doing usability design if you're worried about usability this is a great image this is from twitch if anyone uh doesn't read it it's fun cartoon on occasion

[00:07:37] and I want to be clear that a lot of these things that I've talked about uh when people use the word simple to describe it I don't think for the most part that they were being malicious they they were actually doing

[00:07:51] malice to the word simple but they were actually trying to State something that they wanted and to some degree the things that they wanted uh you know possibly put up against other constraints were good things right how

[00:08:05] many people want their programming environment and the tools they use to be convenient friendly to learn easy familiar minimal and uncomplicated that all sounds that all sounds

[00:08:16] great so interestingly one conclusion that you might come to after looking at all these things is I give up it's hopelessly subjective and i' I've been grabbing all these quotes from you know blogs and the

[00:08:31] web the great thing about the web is it's sort of like the lorites right anything that can be thunk has been thunk before and so I wasn't the first person to think this maybe we should just give up right so one man's simple

[00:08:44] is another man's complex this is this particular blog post uh was from a person who took Umbridge to Martin Fowler's refactoring book and the particular thing was that that the conclusion that they came to was that

[00:08:57] 90% of refactoring was making things shorter um those of you who work at relevance remember back in the day when I said that that no uh no function or method could ever be longer than seven lines and if you showed me one I would

[00:09:09] prove that it was wrong in some way so I haven't on occasion been on the Martin Fowler side of this conversation this actually harks back to an earlier uh implied definition of simple though doesn't it right it was about count

[00:09:23] right this is a counting sort of a counting characterization of simple if it's got a few things in it it is therefore simple if it has a lot of things in it uh it's the opposite of simple which since we haven't defined

[00:09:36] simple yet I'm not going to LEAP to conclusions and and say what word would be the opposite of it this is not correct right simple is not subjective simple has an objective definition the definition informs

[00:09:52] designs and that's really important right this not only does it have an objective decision but you should care about it if you write programs and unsurprisingly right none of this is closure specific at all right everything

[00:10:05] I'm want to say today to the extent that it is useful at all is going to be useful uh in closure but also outside also Simplicity is fundamental so what does it mean it's

[00:10:21] actually literally quite simple simple means not compound that's it not compound right and in a lot of the original usage uh this notion of being not compound was literally like

[00:10:37] compounds medicines right and so uh medicines that were made of one thing were called simples and people who went out and looked for them there was actually a verb right simpling I'm going to go out and and do some simpling right

[00:10:53] I'm going to go find some simples that I'm going to use to treat your rash or whatever and so how did we get from this which is a terrific definition and we're going to do all sorts of fun things with this how

[00:11:04] did we get from simple becoming so complicated you think the beer oh I do not plan to wake up tomorrow morning

[00:11:22] with any major problems solved so in order to understand this we need to turn to one of the greatest programming minds of the 20th century CS

[00:11:42] Lewis little known fact so on the left here we have a nice picture of CS Lewis and on the right we have this wonderful book called studies in words uh that CS Lewis WR definitely pick it up on Amazon played this game to see which speaker

[00:11:55] can get most people going over to Amazon buying stuff and on the right there is a bottle of um really py Scotch that's just product placement it actually has nothing to do with the talk it was in it actually the book was

[00:12:09] next to it in my office but other than that just coincidence and a a key element that informs this book is the notion of verbicide now in in a closure context we're used to thinking uh nouns and

[00:12:27] verbs and Kingdom of the nouns versus functional programming but actually verb itself has kind of been verici right because verb where does it come from it means word right verbum is word and so verbicide is actually not the killing

[00:12:41] and CS Lewis being a language weenie um verbicide is not the killing of verbs it's the killing of words and the specific killing is in his opinion is the fact that people are far more interested in expressing their opinion

[00:12:56] especially I approve or disapprove of this message than they are in evaluating and describing and being analytical about things and there are a lot of great examples of this uh in American English um a particularly potentially

[00:13:12] Politically Incorrect one and I like to use those in my talks uh is that uh in English at one time there were a bunch of specific terms for different kinds of mental defect right they had meanings right so idiot

[00:13:29] and and these many of these words if you actually look up their origin they actually had definitions now the social science and IQ testing and so forth that supported those definitions may or may not be well founded but they

[00:13:42] had specific definitions what do they all mean now I don't like I don't like you they don't even mean they don't even mean anything about your intelligence right they just mean I don't like you and in that context you can sort of

[00:13:54] understand what simple is did simple become a generic term of a of praise or a generic term of disapproval trick question she kind of kind of became both right so let's look at how the original

[00:14:09] definition of simple ramified over time we start with not compound and then we get sort of three branches uh the first branch is unconditional so you have the notion of simple as being unconditional the thing

[00:14:23] in itself and so you say to really abuse words closure is simply awesome right what is what does that even mean that's right closure is generic praise word generic praise

[00:14:39] word right it is it is in and of itself awesome and it actually is very difficult to come up with things that are um in and of themselves good uh CS Lewis as a devout Christian his examples about this of things that were true in

[00:14:53] and of themselves were usually religious examples so he would say that you know God is simply good chocolate is good to me but not to my dog right so chocolate is not simply good there is a second branch of evolution of the meaning of

[00:15:12] the word simple which is not duplicitous and this one has a really amazing series of Transformations you go from I'm not duplicitous right I'm not of two minds I'm not of compound mind if you will I'm not duplicitous I I'm not

[00:15:27] guileful and in fact in fact if I'm not guileful what we know about people who are not full of gu is they don't tend to notice gu in others right so I'm unaware of gu and actually I'm credulous and then

[00:15:39] by the time it's finished being dumbed down the word actually just means stupid right so you are a simpleton and then finally you get the beginnings of the meaning that people are scratching back at a little bit when

[00:15:53] they use Simple in debate and that is uncomplicated and the uncomplicated meaning is actually complex and that it has multiple uh sub branches uncomplicated goes towards easy wow it's so simple to do that it also goes to not

[00:16:10] Posh right um I live in a simple home you know that sort of thing um and the not Posh one sort of further branches to is it a positive or A negative distinction to be Posh right and when I say my home is simple am I saying it's

[00:16:25] poor and second rate am I insulting myself or am I saying saying you know Umble in some sort of positive way and all of the senses of simple under the not duplicitous branch and under the uncomplicated Branch kind of eventually

[00:16:41] head down to sort of this General appealing and disarming this and so simple becomes an emphasis word that is inoffensive uh to the extent that whether it's positive or negative it's unthreatening right so um you know I

[00:17:00] am a simple man right I and the there's there's some small positive notion to that probably depending on how I say the word but it really is just you know a generic term and all these examples really aim at the part of when

[00:17:20] you start using the word in these ways really aim at the part of rhetoric which is called pathos right we've gone from appeal to analysis to appeal to what what is pathos appeal to emotion which there's

[00:17:33] nothing wrong with there's nothing wrong with appealing to emotion appealing to emotion without having anything else is somewhat pathetic which is related to Pathos now I just want to make a a a

[00:17:47] tiny digression which was which really floored me when I was rereading Lewis's book because I didn't really realize what a computer programmer he was right it's not something that people generally talk about but he makes the observation

[00:17:58] the specific specific observation that how words grow like this is a persistent data structure he actually says words grow as a tree right what does ramify mean it means to Branch out but the original

[00:18:14] nodes are not gone you can still access them you can still get back to the original meaning and so Lewis is quite specific that words evolve like a tree they do not uh evolve in a mutational way right

[00:18:32] like a they do not metamorphose in place and so one thing I want you to go away from the closure conference realizing is that mutable programming is like liking mosquitoes better than trees right things that metamorphose in

[00:18:47] place are are really mosquitoes you got another one of those another hour so we can talk a minute about mainstream

[00:19:06] object-oriented programming and in mainstream oo objects are compound they're the opposite of simple from our definition right that's the that's the dichotomy that I'm laying out here simple versus

[00:19:23] compound and objects give you a lot of stuff they have methods they have polymorphism they have types and interfaces they have name spaces they have structure they have uncontrolled mutation in most

[00:19:34] languages and it's difficult to explain closure some of you are probably going to go home and want to explain closure to an object-oriented programmer or convince a team of objectoriented programmers uh to

[00:19:47] give this a spin and it's not particularly constructive to say closure rocks o sucks or to say o rocks enclosure sucks right I mean the whole notion of being passionate about Simplicity would be to

[00:20:02] say let's break it down closure does not stand diametrically opposed to all of the things on this slide in fact it's not opposed to very many of them right these are I mean there's a ton of good stuff

[00:20:15] in oo but the good things in oo are delivered in most languages in a fashion which is both complex and complicated right so features in O are delivered as compounds right you get objects and they have all those things built into them

[00:20:31] those compounds tend to contain more than you need right it's actually rarely the case that you would need everything uh that objects give you say in Java and this snowballs from the language into the libraries right using oo with all

[00:20:47] these features compounded together leads to a snowballing of complexity and complication in libraries that are built in this pattern what we want is the goodness of objects but we want it delivered alak cart we

[00:21:03] want it delivered as symbols and if you look at what closure does and this doesn't really need to be stated much to this crowd it delivers every single one of the features that objects delivered in the other picture but it delivers

[00:21:16] them all a cart and so I've drawn all these the pieces spread out and then I have also added a dotted line around the foundation what is the one thing in the O world that we absolutely stand against as closure programmers UNC the

[00:21:31] uncontrolled mutation right the other stuff is fine it's it's a positive good right but we want to have it delivered a piece at the time the other thing is we we we're going to have an interesting discussion about the relative importance

[00:21:45] of different things right and maybe you don't agree with this relative importance we can talk about it over beers later but we have a foundation we have a super structure

[00:21:55] now let's talk about this with a few specific examples from closure so it's it's well and good to draw a picture uh but it may help to see some particular examples so polymorphism polymorphism is delivered

[00:22:11] allart enclosure via protocols and so this is from a recent checkin to closure the diff protocol diff is a generalization of equals so instead of the notion of I want to compare something and find out yes it's equal or

[00:22:27] no it isn't I want to compare something and I want to find out what's different about the the first thing what's different about the second thing and what's shared by both things right so diff the function which you actually

[00:22:38] don't see here does that and then the notion of comparing things for difference is actually built around uh uh being able to compare the different equality partitions in closure and it turns out that that set list and

[00:22:52] map are the three pieces that are needed in this particular case but the thing that's going on here from a Simplicity perspective is that the protocol is being delivered as a simple allart it's not being

[00:23:05] compounded back into java. .set it's not being compounded back into java. ud. list it's not being compounded back into java. .m I'm not going to beat up on this because anybody who's been awake for the last two days who already talked

[00:23:18] about this we had a whole talk right Sean talked about protocols yesterday he made the specific some of the specific points about what's good about delivering this as a simple right we extend to existing types and I

[00:23:33] do want to talk about one side effect though one thing that falls out of this because this is was kind of surprising to me as we started to use protocols inside closure that the implementation contract is not equal to the caller API

[00:23:45] that can be true in a Java or C app as well right we can have and then you would call it adapters or Bridges or you know who knows what design pattern but it just falls out of delivering things this way that diff similar is not a fun

[00:23:58] function that any client's ever going to call they actually call a function diff which delegates uh under different circumstances to diff similar in other things and that notion of using uh protocols as the implementation contract

[00:24:14] is a positive consequence of having delivered a simple thing to begin with right it's a it's a side benefit if you will name spaces enclosure names the naming of things is all a cart through vs and so a name could just be a raw

[00:24:30] name it could point to data it could point to a function it could point to a class or to a polymorphic function and namespaces themselves are mere Maps I substituted the word mere in for simple um realizing that I was

[00:24:45] getting myself into some sort of recursive trouble there the namespace piece is really powerful because if namespaces are a good idea at all it's nice to have them available everywhere to everything else

[00:25:01] implementation reuse is delivered all a cart so if you look at uh this example is taken from closure. java.io if you look at uh the stream implementation it is a map of keys to functions and then various uh classes like buffer input

[00:25:18] stream have the protocol IO Factory extended to them using that map but also not having to have a special Mixon API right there's no special API for mixin with closure protocols what's the API it's the collections right this is a

[00:25:37] point that um uh Mark MC granan made earlier today right this is exactly the same point that he was making about ring that because things are built out of symbols they're built out of values and

[00:25:49] functions you don't have a special API for building mixins now you might choose to write uh a collection processing function of some kind to help you make mixin if that use case came up you know multiple times and that thing wouldn't

[00:26:05] be simple and I would talk about that in terms of creature comfort and convenience uh but you don't have to syntax again given us a list we have to keep coming back to

[00:26:19] this this one is particularly funny because the proponents and detractors seem to agree this is Paul Graham and you can't see it from this quote but the context um should be followed by lisp is simply awesome right

[00:26:33] lisp looks strange not so much because it has a strange syntax but because it has no syntax this is from a blog post that could be summarized as Ruby rocks lisp sucks and it says the problem with lisp

[00:26:48] is that it doesn't have syntax so much that it has no syntax um this being a a rocks sucks kind of blog post it also uses a lot of other words as generic terms of Praise or criticism it uses the word technical to mean bad it uses the

[00:27:07] word regular to mean good the word sensible to mean good and the word clean to mean good so if you really wanted to take the amazing thought that went into this Pro Ruby anti- closure argument you could actually reduce it to lisp sucks

[00:27:25] because it's Technical and Ruby rocks because it's regular sensible and clean with none of those words defined by the way it's a rhetorical trick on my part right as I'm telling this story right have I said anything

[00:27:43] about how much closure or Ruby actually rock or suck I haven't said anything right i' I've maybe moved you slightly emotionally like anti some hypothetical Ruby people you don't even know right so it's like a character assassination of

[00:27:56] some person but I haven't really proven anything here I'm not being analytical right I'm drinking a beer and it's a Saturday afternoon so in what way though is syntax

[00:28:09] simple it's simple in that in a particular setting you have only one thing in play you don't have a compound in play so when you look at uh and this particular example is true for lisps in general right open parenthesis followed

[00:28:26] by verb and so people who find lisps Simplicity to be beneficial appreciate this right it could be a function or an operator or a method call or an import or metadata or control flow scope it doesn't matter open parenthesis verb

[00:28:42] go a second example closure specific bindings right bindings are always housed in a vector and this is a particular point you want to make when someone's talking about all the irritating parentheses right closure is

[00:28:56] not full of parentheses and in fact it uses different punctuation in order to enforce Simplicity right so when I see square brackets in code I know that names are being bound to something and all these

[00:29:11] things work in basically the same way right and in particular they have access to what what is closure's amazing sleeper feature that looks really creepy when you first start but just grows on you destructuring right these all get

[00:29:26] access uh to the same goodness because of that not binding not binding right so I I will point out here's the advanced version of the conversation which we can't have here but there there are two wrinkles to this particular slide I

[00:29:40] actually have notes at the bottom of slide which you can't see there are two wrinkles to this one of the wrinkles is binding which doesn't let you do destructuring and there's a reason for that and it's still

[00:29:49] simple U or actually you could argue that there's that it's uh complex and warranted um also fun and defin are different from the others and and there's a a a more elaborated version of the Simplicity argument that

[00:30:03] I think is in play there as well but we don't have time for that now so argument from Authority it's [Laughter] simple this is a particularly good one and this is one that I flubbed the first

[00:30:16] time that rich and I were teaching together I was conflating in my vocabulary reppel and shells and everybody almost everybody does this actually somebody was wrong on the internet about this just like 48

[00:30:29] hours ago and it's been all I can do to not go on the Internet and try to fix it uh but there was I think it was it was probably some of you if you follow the closure hashtag it was some python programmers

[00:30:40] first reaction to closure and then The Hacker News thread there was a big conversation about whether the reple was special to lisp or not and in the entire conversation it was clear that in the minds of both the pro and con arguers on

[00:30:53] the point that reppel and shell were synonymous well app and shell are not synonymous um and they are both compound things right neither one is simple however which one is made of simple things the repple right the a repple is

[00:31:11] one of my favorite things in closure now because it has an acronym to remind you that it's a compound of simple things what simple things is it made of read eval print I don't want to spend a lot of time beating up on the Fallout of

[00:31:25] failing to be simple because I think as the closure crowd you probably already have felt this pain and that's perhaps why you're here but just think for a minute about what this I mean this maybe doesn't matter very much in arguments

[00:31:36] about the Shell versus the reppel but what is the Fallout from not perceiving re and P as being different things what do you end up with well okay the reader converts serialization into data

[00:31:52] structure um eval does stuff and P prints stuff if you don't have r p in your world if you lived in a bereft World Without r&p You would have to invent data interchange formats right all of Json and XML and

[00:32:09] all the problems that they cause fall out of not understanding this distinction and you've probably heard lisp programmers complain that we invented s Expressions you know 50 years ago this XML stuff is silly um which is

[00:32:25] a whiny way to say it right because because it's because it's important and it's too easy to discredit them when they say it that way but it's important to it's only understood to be important when you realize what the Fallout of

[00:32:37] this is right and not only is it not simple it's also in in my view a stratification problem right that if you don't have uh reading and writing of data structures at the bottom then rediscovering in that later it's upside

[00:32:50] down and it causes all kinds of problems I mean how many people have ever been seen in a website that got burned by somebody eval and Json because they didn't have a reader there's a ton of Downstream

[00:33:02] problems that come out of this now what about vs closure vars actually suck right and why do they suck they suck because they don't deliver this promise of Simplicity uh Rich laid out four things that vs

[00:33:20] might let you do yesterday rebinding air handling redefining and Global mutable State and as they're today they are less good than they could be right as they're delivered today fars are rebindable you could rebind them for air handling you

[00:33:35] could redefine them you shouldn't use them for Global mutable State fine we're we're not going to worry too much about that and the code that he talked about yesterday the changes that are in master now make rebinding and error handling

[00:33:48] one simple and redefining a different one right redefining is one use case it's supported by DEA rebinding and error handling are one use case they're supported by Dynamic now you can all count so somebody should probably raise

[00:34:04] their hand here and say well Ste there not one use case you've clearly got two use cases called out in the chart there but really error handling is a subcase of rebinding and I think the reason that rich called it out yesterday is because

[00:34:17] it was a motivating use case for him when he designed it and so but those two and the flip side of that is if you can come up with a motivated argument for where those would ever be different then we're not simple enough enough yet and

[00:34:29] this is a perfect example of the kind of design thing that you know Rich was talking about when you analyzing what you were thinking when you woke up I think these two things are the same they're really part of the same simple

[00:34:39] they're not a compound I don't need to tease them apart any further I'm done but I did have two kind of use cases so let me just sort of document that structure closure delivers structure all cart and so you have this

[00:34:55] ability to say I'm going to have a map and I'm going to do all my map stuff with it keyword access nested access what have you and I can switch to records and Records just deliver structure right records document

[00:35:08] structure but do nothing else so records have first name last name address whatever right that structure delivered all a cart without any answer stuff and the API Remains the Same right

[00:35:23] all the stuff all the calls right everything is still data it still looks like Maps now this is the point in the talk where I have lied to you because records don't really deliver structure alart what do

[00:35:36] they deliver they deliver type and they they deliver all kinds of stuff right they Implement all these closure interfaces and so thinking about records for a while

[00:35:47] you might realize that there's something simpler underneath there's a distinction between data as information right which is what records are for and mechanism and so you end up having De Record uh being built on top

[00:36:00] of a simpler thing de type right and de type really is a simple thing and the only ways in which def type is not simple you start talking about giving getting type and uh field access in the same go um that's

[00:36:13] actually pretend like that didn't happen we'll talk about it in a minute so what's the most important thing to do if we're if we're thinking about using Simplicity as an organizing

[00:36:29] metaphor for how we think about designing good code looking at closure for inspiration wanting to do this in our own code uh what rich said in his talk is that who needs to be a really harsh criticism of this thinking we do

[00:36:43] right if we're going to look at this and say we think this is good we need to use that waking mind and ask ourselves what tradeoffs do you make in the name of Simplicity because all those things that I named earlier all those things that

[00:36:54] people called Simplicity that weren't were valuable they just weren't simple and the first thing I want to say about this is that there are no trade-offs in defining Simplicity right in this talk I'm squatting on the

[00:37:10] correct definition simple equals not compound all the definitions that I gave earlier all the definitions that come out of the pathos from uncomplicated to easy to simpleton and all that stuff those are literally follow-on

[00:37:25] definitions they are not the original definition more importantly Simplicity is fundamental it's literally fundamental if you look in the dictionary one of the definitions of simple is fundamental so

[00:37:41] I win right we get to we get to keep this what does fundamental [Music] mean yeah it does mean simple right it's at the bottom in what in what specific

[00:37:52] sense what other word in English is related to fundamental found Foundation right so it comes from Latin fund mum right it means the foundation and the point that I'm making here and by the way again I'm going to have to make this

[00:38:03] is going to be your Socratic homework assignment so you need to have a Socratic dialogue with yourself in which you pick any of the other definitions of Simplicity from the beginning of this talk so easy to learn

[00:38:18] or made of a small number of pieces or minimal and make that your foundation and then try to build stuff with it right try to design stuff with that as your foundation and then try to get to Simplicity as a

[00:38:29] follow on or a derivative concept and see how that works for you and then try the way I'm recommending is the correct way which is make Simplicity your foundation and design things that way and see where that gets you and if I had

[00:38:44] an extra hour I think I could have a lot of pathos appealing slides to make a stronger argument or a stronger emotional appeal that making Simplicity the foundation is the right way to go but try it for yourself now I've just

[00:38:59] actually performed another rhetorical trick because I told you that I was going to talk about trade-offs but what did I then do I said this is not a trade-off right there's no trade-off made here there was

[00:39:10] no alternative choice for a design uh method there was no other goal other than Simplicity that I was comparing it to I used it as a rhetorical trick to go back and and and just piss on the other definitions of Simplicity one more

[00:39:23] time but there is a really big tradeoff that closure makes that compromises Simplicity and it's systemic and it's painful and what is it it's living on the jvm right it's living on the jvm so why

[00:39:39] do we make why did Rich make this trade-off what does the jvm give us it gives us performance it gives us power it gives us reach right uh we're not list we're not on an island the jvm trade-offs include

[00:39:53] primitive operations conforming to the Java collection apis lack of tail call optimization uh weird oo interrupt forms that don't represent how to do work the right way but are necessary so gen class and proxy alternate numeric operations

[00:40:07] unchecked integer math and so forth and these bubble up to more painful and more perhaps regularly occurring API trade-offs if I'm consuming a Java API I may still have to deal with uncontrolled mutation I will have to deal a lot with

[00:40:21] premature abstraction right which we remove that's called distracting DEC right going back and getting rid of abstraction and turning things back into sets and Maps I have to deal with implementation

[00:40:33] inheritance annotations and pattern bloat and I put bloat there with a question mark because I would normally make the argument that patterns are just bad period um but that requires another hour so we'll just say that that too

[00:40:45] many patterns is bad and then you can all agree with that because it's in the definition of too [Laughter] many and then you get ecosystem trade-offs so there's a presumption in

[00:40:58] the Java world of binary delivery that's pretty hostile right to aisp we don't really need to have compiled binaries match up with each other but it causes pain points inferior serialization we're spending time worrying about XML and

[00:41:11] Json apis version linearity this is actually an ecosystem tradeoff that everyone's dealing with right now right this is actually probably doesn't really fit in this slide but I wanted to mention it because it's an issue right

[00:41:21] there's a presumption of version linearity in how we deal with deployment and that's not really true with Git anymore but there are a lot of tools that think that and then living in the Java ecosystem we actually have to

[00:41:30] wrestle with a lot of tool sub ecosystems right so it now works on net beans and it doesn't work on eclipse and tomorrow we get it working on eclipse and then it doesn't work in intell idea I mean this is the uh pain reward

[00:41:42] trade-off for being on a big platform where lots of things happen so there's a ton more I would like to say about the ecosystem tradeoffs there are a lot of specific things that we do

[00:41:59] in ecosystem tradeoff land that are complex and complicated because we're on the ecosystem and we have to make really hard design choices and I think there are really fun conversations here and

[00:42:10] they are around things like how lining and lives on top of Maven those kinds of questions there's a lot of interesting stuff that happens there um we're going to have to save it for beer and barbecue the other thing I want to talk

[00:42:20] about is using this to improve your own designs so it's great that to some degree or not the Rich has drunk from The Well of Simplicity and has visited closure on us but I want to be more than just a consumer of these benefits right

[00:42:38] I don't want to have a superficial head start using closure just because there's a bunch of good stuff already there I want the things that I write and the things that other people in the community write to also embody this kind

[00:42:48] of Simplicity and so there's kind of a and now now this is I'll call this my this is opinion subjective portion of the talk there's kind of a formula you might follow that's right everything else was

[00:43:01] fact fact there's there's a model you could follow to try to make things simple and and I'm going to walk through this in the design of a specific API so broaden your context tease apart known compounds

[00:43:17] so when there's something already floating out there that's a compound break it apart into simples find new symol go directly to data sleep on it and I'm going to go through these steps in the design of a

[00:43:29] specific API and how we got there so when closure went to one two uh I made a great effort and other people in the community made a great effort to get a bunch of things in contrib promoted into closure so that certain projects

[00:43:41] wouldn't have as many dependencies uh into closure and one of the things that didn't get there is a wonderful little uh function that chower wrote called show and what show does rich is putting his head in his hands

[00:43:57] yet again Rich looks at Cher's code and puts his head in his hands so what show does is gives you reflective introspection over the Java thing you're working with I think closure is a kick-ass environment for

[00:44:11] exploring Java libraries and I'm not the kind of guy that goes to Java do I'm much more likely to look reflectively at objects and understand what they do so I wanted this and I proposed that we uh promote it forward and Rich put his head

[00:44:22] in his hands just like he just did and the problem here is that this API is well let's walk through the issues and see where we end up so broader context it turns out that the

[00:44:38] compiler needs reflection too so if you're going to write something that's going to be reflective it's not just repple consumers right you have to think about other potential consumers and this is one of the things you might not know

[00:44:47] unless rich just told you some users of reflection don't have classes in hand other users of inflection must have classes in hand Java apis for a reflection can't be instantiated by normal code I can't

[00:45:04] create a java. lang. method or or Java Java Lang reflect method or a Java Lang reflect field the only thing I can do is get them from a class which means that they are not useful as a baseline for reflection if my goals include people

[00:45:18] that don't have a class in hand and people that do have a class in hand so the first cut that I took at writing code that would solve these problems worked as follows there was a reppel API designed to replace Cher's

[00:45:31] show called describe which called a more datadriven API so I'm calling down to something simpler reflect which had a pluggable implementation via a protocol that allowed me to use different reflectors in particular to handle the

[00:45:43] different use cases of people who have a class in hand or people who don't a set of predicates were used to limit the results and then a rebel format protocol printed things out as a table and so now you got a reflection API that looked

[00:45:56] like this describe string named last and so this finds java. lang. string the print output tells me things that start with last and then prints out other things am I being inadvertently funny now what's that oh head his hands again

[00:46:15] yeah so this is the first design that I showed rich and um that was painful so this this does not suck compared to a lot of stuff that's out there I mean there's there there are several

[00:46:29] things it doesn't right um uh you know there's a nice little mini DSL for describing and it wasn't just named there were a bunch of little predicates and you know lots of little helpers so that all the reppel

[00:46:41] use cases were covered and this actually did Cover the reple use cases and the compiler use cases but iterating through it we said okay maybe this is still compound given that the whole point of this talk is using simple as a design

[00:46:53] principle this is still compound what things are conf at in here well there are multiple entry points both describe and reflect is that really necessary right if we can find a world in which there's only one entry point that would

[00:47:05] be better there's explicit wiring right so the API actually had slots in it where you dropped in the next step and then slots in and where you dropped in The Next Step there were specialized matchers specialized matchers feels like

[00:47:18] failing on the promise of having General data and there was custom printing at the end and so the next round is currently in and looking for feedback was that there's a single function reflect which uses the reflector

[00:47:32] protocol that part was good generic wiring and the generic wiring is already inclosure right I don't need to have all these little API slots to channel one thing to the next we could just use the arrow

[00:47:43] operators predicates are just generic functions right there's no special thing there um there could be a really cool closure. data. match that did that but there's not there now and then another simple print table so instead of having

[00:47:57] something that could print out a nice tabular representation of reflection how about something that prints out a nice tabular representation of what anything and so the new version looks like this you Arrow reflect java. lang.

[00:48:12] string you grab the members you filter with anything you want you print table now this is not as concise as the inferior API but it would be um if we had closure. dat. match right we'd have a way to do matchs in the middle and

[00:48:27] that would be fully composable and the big thing here is what was an originally a compound of solving the reflection part which was done okay and doing the filtering which was compounded in unnecessarily and doing the printing

[00:48:40] which was compounded in unnecessarily has now been realized in three separate pieces one of which still represents work to be done so one of the reasons that I jumped to the wrong way to do it is I wanted to kind of solve the

[00:48:49] complete problem and uh one of the things that falls out of wanting to be simple is needing to be a little bit more patient so so the practices that we saw here broadening your context asking who the other users were teasing apart

[00:49:03] known compounds right so finding out that Printing and uh filtering all those things were separate items looking for new simpol getting straight to data and several iterations of sleeping on it without having any alcohol or how to get

[00:49:25] there it's really good Newcastle so there's a ton more I would like to say about this uh one thing I'd like to say is I do think that there are other things that compete with Simplicity as a decent Foundation as as

[00:49:41] a decent place to start uh and I think there's interesting discussions to be had about that but we're done we are at the end of our time here [Applause]

