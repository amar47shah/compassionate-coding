Goal 3500 to 4000 words for 30 minutes

Okay, let's get started. My name's Amar Shah, and I'm a developer at
ShareProgress, where I work on our social media analytics platform using
open-source tools from the Ruby on Rails ecosystem. ShareProgress is a
great place to work, and I'd love to talk with you about it, so please
catch me sometime during the conference if you're interested in hearing
more.

This is a talk about compassion. So you can all guess right now that
I'm a practicing Buddhist, I'm a vegetarian, I abstain from all worldly
delights, I've been shortlisted a couple times for the Nobel Peace Prize.
Haha, no, I'm none of those things. I mean, here I am on the stage at
RubyConf, so you know I'm some kind of rockstar at software, right.
And I'm going to talk about emotions, so that means I'm a rockstar at
emotions.

No, I'm not any kind of rockstar. I'm just a software developer.
If you're a software developer too,
you know that means that I spend a lot of my daily life failing at
things and being confronted by my general lack of adequacy. Well, I do
that in my personal and emotional life too. Never fear though, I have
a word for this though: LEARNING.

I'm learning how to do life, just like I'm learning how to build software--
from experience, meaning from mistakes. I want to share a story with
you about some experiences I had with legacy code, because as I recall
these experiences, it's finally clear to me what kind of mistakes I
made and what I could have done differently.

When I started one of my previous gigs, I inherited full responsibility
over a 70,000-line Ruby on Rails app, a product that my company bought
from a local shop and used internally every day. On the outside, the app
looked like it worked reasonably well. The managers of the company
believed that they were ready to build on their existing software to
advance an exciting new strategy of automating their data entry via an
in-the-field mobile client. In fact, I was hired to evaluate the mobile
app they had bought from the same shop and ready it for production.

It didn't take long to discover that the unreleased mobile app was a
disaster in the making. The UI somehow managed to be both boring and
subtly mysterious. Performing a simple workflow on the app was impossible
to get right; the navigation was so confusing that I got lost every time.
It wasn't any better under the covers. The code was rotting. Its design
stunk of overengineered solutions to avoidable problems, like using
peer-to-peer connections to transfer data that could simply be shared
via email. The dependency list read like the roll call of forgotten
longshots at the Kentucky Derby:
[SQLitePersistentObjects](http://stackoverflow.com/a/3066689/2157021),
ASIHTTPRequest, ... Communication with the server took place in one
huge "sync" that users were expected to perform once every 24 hours;
in other words, the web server's API had exactly one route. The request
took minutes, if it succeeded at all. The app was a soul-crushing
spectacle: developers as second-class citizens, users as a
despised and outcast underclass.

Luckily, I wasn't the first developer to see this. Though I was the first
full-time developer employed in-house, I had been preceded by a short-term
freelance contractor with significant mobile experience, who had passed
up the full-time gig and moved on. I had her commits and some of her notes,
so I decided to give her a call. She was very nice, but her hatred for
this unreleased mobile app was chilling even over the phone. Kill it and
start over, she said. With two votes to axe the project, it was now or
never. It was time to make the case for starting over. To steel myself,
I rehearsed this line: "What do you want me to be doing in five years?"
As I saw it, we could either sink years into rehabilitating this project
or we could try again.

And it worked. Management agreed. They were starting to see that their
software ambitions were not going to come easily.

I got to the drawing board, researching the most solid
libraries for building data-rich iOS clients with modular, reusable
components and extensive automated tests. I was still at the drawing
board when the bugs began to file in.

What bugs? Production bugs, from the Rails app. Remember that thing?
Five in-house users furiously POSTing new records copied off of
paperwork, waiting sometimes 30 seconds for forms to load, realizing
there was no way to undo mistakes, and hacking creative workarounds
that mangled the underlying data. Perhaps ten more users around the office
checked in once in a while: lost, disoriented, and most of the
time, running away before they realized that the data just wasn't
adding up. But somewhere up the food chain, the message was getting lost.
The longer I worked at this company, the more apparent was its
office mantra: See something, don't say anything.

That is, after all, what external contractors had been doing whenever
our bugfixes rose to the tops of their queues. Slow-loading form? Ok,
one-line fix, one hour billed. A week goes by. Another slow-loading form?
Rinse and repeat, ignore the cut-and-pasted forms with the same bugs on
each one. What would be the motivation for an external contractor
to attempt a refactoring in a code base without tests?

Yes, that's right. This Rails app that I inherited, the one that had
been described by my boss (a marketer!) as "pretty solid," had no
automated tests. It was stuck precariously on Ruby 1.8.7 and Rails 2.3,
both end-of-life. I described the entity relationships in the database
as a "star topology"; what I was conveying was that it was a giant clusterf---.
The 70,000 lines read like they were written on a whiteboard at a
dismal job interview. "I was hoping you'd use Enumerable#select,"
the interviewer would have lamented. It was a relief that it seemed
that outside our office no one really used the app, since the data
presented in the customer portal was simply wrong, and anyway,
if they didn't like their data, any casual user could change everything
(for anyone) by pointing their browsers to the admin portal,
which any user could access as long as they could guess the URL.
The fact that we hadn't been hacked yet, at least meant that
nobody cared enough to hack us. How long could we keep getting away
with that?

So here I was, the lone maintainer of a production application with
no automated tests, with gaping security holes, with dependencies that
were out-of-date and sometimes completely dead, and with features so
unnecessary that users didn't know they were broken. The words flashed
in front of me again: "Amar, what do you want to be doing for the next
five years?"

I get upset just thinking about these moments, because of the
emotions I recall feeling when I discovered that the app that my
company depended on every day was a ticking time bomb, and that I,
as the only developer, the only person in the building who had even
the slightest interest in software, was the only one in the whole
company who understood that disaster was just around the corner.

I was terrified that I would be blamed if an intruder hacked our
app, or if our cloud service provider yanked support for Ruby 1.8
or Rails 2.3, or if our deployment couldn't scale along with
increasing loads, since the app used file storage and therefore
could not run on a distributed cluster.

I dealt with my fear by turning it into rage. I was angry at the developer at
the contracting shop, the one who wrote the bulk of the app. A bit
of googling and I knew a lot about him, and all of it disgusted me.
The app he built for us had no tests, but he was tweeting pithily in
praise of TDD. Our abandoned, forsakened API was a single route; he was
writing a book on microservice RESTful architectures. He had closed
his contracting shop and was now the CTO at a local company that
touted its software practices and promised to only hire the best
developers. Who were the best developers? Not me. When I had
applied there earlier that year, I never heard back.

I gave this developer an unflattering nickname, derived from his
unique git commit style, and took to the Twitterwaves to complain
about him. At local meetups, I'd hear his name and say, "Oh yeah,
I know ASDF. Not directly; I know him *through his work*."
All in all, I'm pleasantly surprised that I was able to
exercise any discretion at all. I hated this man; to me, he was
the embodiment of fraud, a snake-oil salesman leaving throngs of
sad, sick pioneer townspeople in his wake. I refused to consider
the possibility that building sick applications had taught him
to value healthy practices. In my eyes, there was no redemption
possible for a developer like this.

But even worse, I had a real job to do. I had to dig this app out
of its mess. Management agreed to spend the rest of the year shoring
up our legacy production Rails app. What choice did they have?
I ordered copies of Martin Fowler's _Refactoring_ and Michael Feathers'
_Working Effectively with Legacy Code_. Thumbing through Chad Pytel and
Tammer Saleh's book, I chuckled grimly as I noted that ASDF, like
an evil genius, had prodigiously employed every known Rails anti-pattern.

My fear drove me to work slavishly, hauling my computer home on
nights and weekends, afraid to let an hour slip by without pushing
this app to be more fully tested or more cleanly organized. I
ruthlessly scaled back features on the customer side of the app.
Customers weren't complaining about the debilitating bugs in the
"Advanced Search" feature. Do you think that was because they were
just being polite? This wasn't the time to polish up features that
no one wanted enough to actually use. We were in a war zone, and I was a
battlefield medic: hacking, squeezing, extracting, injecting, slashing
limbs and yanking out shrapnel.

I told my non-technical friends that every day at work was like
prodding a sick man through a desert. Keep going, I said to his many
pleas to stop and rest. I showed him whatever kindness I could, but
it wasn't much. I knew that if I let him drink the rest of our water
and lie down for a nap, then both of us would die out here.

Over the coming months, though the anger and the fear still smoldered
around us, things began to change. I started with the models, the
smallest ones first, breaking down each method and redoing it with
TDD, gradually replacing our galactic star database topology with
a simple tree. In a couple months, I couldn't put it off any longer.
It was time to confront the god-models, the ones with over a thousand
lines of Ruby code. These models weren't fat; they were pregnant: they
held inside them whole classes of their own, a service layer of plain-old
Ruby objects.

The old man and I wrapped our parched throats in this
spartan service layer and forged on through the deserts. We were
weighed down by thick controllers and extensive callbacks, so we
shed them. We stripped down to a predictable set of seven methods. We
closed the authorization and sql injection loopholes, maybe just
steps ahead of the intruders. We tore out the non-RESTful routes
and replaced them by modeling new resources.

Often, our dev branch was in a completely broken state. Having never
traversed this desert before, we had no map and no compass, just the
steady track of the beating sun. I didn't know the "right way" to
rewrite a legacy Rails 2.3 app--I wasn't even very experienced with
Ruby--and several lessons came in hindsight, some of them trivial and
commonplace, like where you can't remove `self`. Others were subtler:
use the Ruby style guide, and better yet, automate style-policing with
Rubocop; wait to rewrite the routes in the Rails 3 DSL until you are
restructuring the controllers. And this: get comfortable with saying
no.

The months wore on and deadlines loomed, but over the desolate horizon
we saw it: the first flickers of green, then rows upon rows, a
veritable forest of passing RSpec examples. We upgraded to Rails 3,
then 4. We brought our code coverage to 95% of the models, and all
of the controllers. Our mouths agape our eyes wide, we gasped in
relief at the sight of civilization. We fell to our knees in an
embrace, my partner and I, this legacy codebase and I.

In the abstract for this talk, I said that your legacy codebase is
your partner, like a husband or a wife, or any significant other.
I mean this, literally, legacy code is my boyfriend. I want to talk
a little today about how working with legacy code is like being in
a relationship. And as someone who has
has been cruel both to people and to code, I want to tell you why
you should try to be compassionate instead.

# Code as Partner, Code as Child

Something frustrating about dealing with other people is that they're
not you. Crazy, right? They just don't see things the way you do.
Sometimes it's hard to figure out why they do things the way they do
at all.

Other people do things that we wouldn't do. They do things we wouldn't
expect. They're so unpredictable.

Does it ever make you anxious that the people around you are so
*human* that you are never 100% sure what they will do? Does it make
you worry that maybe your house-sitter won't remember to let the dog
out or the barista won't remember to use skim milk in your triple
caramel mochaccino?

Other people are different partly because they have had different
experiences from you. Most of the time, there's no way to know what
all these experiences were and how they shaped this person.

Other people are the worst, right? Not only is it impossible to know
what they'll do, it's impossible to know why. There's no research
you can do to find out exactly how to interact with them so that they
give you the results you want. They're impossible to control.

Control. Are we trying to control our personal relationships? If you
are, please stop. We can't control anyone else. Our best option is
to position ourselves near good people and trust them to do their
best.

A legacy code base is not as complicated as, say, your boyfriend. But
the reasons why it does what it does are not easy to parse. Although
we have all the commits--we have artifacts--and we can expend a lot
of elbow grease to find out when a decision was made and a good deal
of mental real estate to guess why, in the end, we don't have the
full story.

When we make edits to a code base that we don't understand, we can never be
100% sure that the outcome will match what we expect. But any large
code base is difficult to understand; even with tests, it is not trivial
to predict the behavior of new code in a large system.

What if we stopped trying to control our code? What if we dropped the
illusion that we can predict what these large, unknowable systems will do,
and simply trusted--not that they will behave flawlessly--but just that
everything will turn out all right?

How does it feel when someone gives you a responsibility but doesn't
trust you with it? Maybe you've been the barista who gets an interrogation
when you hand over the drink: did you use soymilk? did you add caramel?
Maybe you've had partners or parents who always seem to be second-guessing
you. It doesn't feel good. And it ripples out. You start to feel like
controlling people is a reasonable thing to do, and you start to do it
yourself.

# It's 1s and 0s. But You're Not

Ok, so now you're probably thinking, code isn't a person, it doesn't
have feelings, and it doesn't mind if you insult it or complain about
it. It can't try to do its best; it just does what it does.

And technically you'd be right.

In fact, you are more than welcome to rag on your legacy code all day.
After all, you didn't write (most of) it. So it doesn't look bad on you,
or so you think.

## hacking your attitude for a better day

Here's what I want to propose: You have a choice. You have a choice
whether to look at this code as someone else's 

## hacking your attitude for a better career

# A Passion for Legacy Code

So now you know that it's good for you to try to like your legacy
code. So now you can all go home and eat your vegetables and go
jogging every morning and be in bed by 10, just don't forget to
floss. Because it's good for you.

But I want to let you in on a little secret. I actually don't mind
legacy code that much anymore. I actually...kind of like it. Without
having to force myself.

Isn't that gross? What is this guy talking about?

Here's why I love legacy code: when I work with code that is
badly structured or poorly tested, I learn more.

There's a not-so-secret secret about software developers, about
people like us. We love learning. You kind of have to, since
the list of things you have to know never stops growing.

When you work with a legacy code base, it's almost a given that you
are working with a production system that is of such value to your
organization that you are stuck with it. Otherwise, you'd throw it
out. When you work on a production system, what you do matters, so
it's important that you make a careful decision. But, paradoxically,
when you have a problem in production you have to do **something**,
and you don't have the luxury of unlimited time for research and
strategy.

This is a good thing. As much as we perfectionists love to be careful
and get things right--and as much as that's a valued and sought-after
personality trait--we can never know if we made a good decision until
after the deed is done. When you push your changes to a production
system, you have the opportunity for rapid and meaningful feedback.

Sometimes the feedback is that you failed, maybe spectacularly. That's
good. We learn so much more from mistakes that we do from careful
preparation. When you're working with an unhealthy, unpredictable
legacy codebase, no amount of careful preparation will give you
100% peace-of-mind that your solution is bulletproof. This is a
blessing in disguise. Keep your head up and keep shipping. And
welcome to Agile.

## clay for sculpting

Why else do I love working with legacy code? Because it's there.
Have you ever sat down, in your own personal time, to teach
yourself a new language or framework and been utterly at a loss
for where to start? This happens to me constantly. One of my
pet projects now is that I'm learning Haskell, and the idea
of conceiving and writing an app in Haskell still seems beyond
me. What should it do? Where should I start?

Somehow it's easy to make progress with the tiny example apps
and homework problems. Now if only I could get my hands on a
big production system.

Hmm... if only I could practice my skills on a big production
system that mostly works but needs a lot of tooling behind the
scenes. if only I could be paid a salary every day to practice
on a system like that. Something that already has a mostly
well-defined purpose and a lot of existing code to work
with, but could benefit from a series of incremental improvements.
Where could I find something like that? Hmm...


## the real culprit is the culture

I want to propose to you that legacy code isn't really all that
bad. And I've told you why. But why is it often such a bad experience
to inherit code?

## see clearly, be ready

# Ruby Culture, Your Culture

Culture, that's what it's about.

In the teaser for this talk, I asked you to let go of anger and fear,
to let go, and I promised, more or less, that letting go would bring
you joy. It's a safe promise to make, because it's not a new idea at all.

But I want to give you a little more than that. We're all here because
of Ruby. Thanks to people like Matz and DHH, we get to be paid to
spend all day sculpting with a language that's truly a joy to touch.
Ruby's not perfect, but for me and for many of you, I bet it comes close.

If that weren't enough, Ruby comes with a culture and a community,
and that's why we're all here today. Remember this? MINSWAN.
Matz is nice, so we are nice. So let's be generous with our kindness.
Let's be kind to our partners, and our children, and our family, and to
our coworkers, the people we mentor, and those who mentor us. Let's
be kind to ourselves, and let's be kind to our code. Even legacy code.

Be generous with your kindness. Spread that shit everywhere. It's the
most valuable thing in the whole wide world that you get unlimited
amounts of for absolutely fucking free.

Thank you.
