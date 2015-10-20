Goal 3500 to 4000 words for 30 minutes

Okay, let's get started. My name's Amar Shah, and I'm a developer at
ShareProgress, where I work on our social media analytics platform using
open-source tools from the Ruby on Rails ecosystem. ShareProgress is a
great place to work, and I'd love to talk with you about it, so please
catch me sometime during the conference if you're interested in hearing
more.

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
start over, she said. With two votes to axe the project, management agreed.
They were starting to see that their software ambitions were not going to
come easy.

But we had dodged a bullet. When I was preparing to sell the idea of
ditching the mobile app and starting over, I rehearsed this line:
"What do you want me to be doing in five years?" As I saw it, we could
either sink years into rehabilitating this project or we could try again.

And it worked. Management agreed. Having secured their faith and blessing
to start over, I got to the drawing board, researching the most solid
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
both end-of-life. I described the entity relationships as a "star
topology"; what I was conveying was that it was a giant clusterf---.
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
were out-of-date and sometimes completely dead. The words flashed
in front of me again: "What do you want me to be doing in five years?"

I get upset just thinking about these moments, because of the
emotions I recall feeling when I discovered that the app that my
company depended on every day was a ticking time bomb, and that I
was the only one in the whole organization who understood what that
meant.

I was terrified that I would be blamed if an intruder hacked our
app, or if EngineYard yanked support for Ruby 1.8, or if our deployment
couldn't scale along with increasing loads, since the app used file
storage and therefore could not run on a many-instance cluster.

I dealt with my fear by turning it into anger at the developer at
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
about him. All in all, I'm pleasantly surprised that I was able to
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
no one wanted enough to actually use. We were in a war zone. I was a
battlefield medic: hacking, squeezing, extracting, injecting, slashing
limbs and yanking out shrapnel.

I told my non-technical friends that every day at work was like
prodding a sick man through a desert. Keep going, I said to his many
pleas to stop and rest. I spared him whatever kindness I could, but
it wasn't much.
