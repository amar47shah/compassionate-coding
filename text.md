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
a relationship. And coming from the standpoint of someone who has
has been cruel both to people and to code, I want to tell you why
you should try to be compassionate instead.
