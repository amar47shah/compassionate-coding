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
in other words, the API had exactly one route. The request took minutes,
if it succeeded at all. It was a soul-crushing spectacle: developers
as second-class citizens, users as a despised and outcast underclass.

Luckily, I wasn't the first developer to see this. Though I was the first
full-time developer in-house, I had been preceded by a short-term lone-wolf
contractor with significant mobile experience, who had passed up the
full-time gig and moved on. I had her commits and some of her notes,
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
components and extensive automated tests. And then the bugs began to
file in.

What bugs? Production bugs, from the Rails app. Remember that thing?
Five in-house users furiously POSTing new records copied off of
paperwork, waiting sometimes 30 seconds for forms to load, realizing
there was no way to undo mistakes, and hacking creative workarounds
that mangled the underlying data. Perhaps ten more users around the office
checked in once in a while: lost, disoriented, and most of the
time, running away before they realized that the data just wasn't
adding up. The longer I worked at this company, the more apparent was
its office mantra: See something, don't say anything.

That is, after all, what external contractors had been doing whenever
our bugfixes rose to the tops of their queues. Form loading slow? Ok,
one-line fix, one hour billed. A week goes by. Another slow-loading form?
Rinse and repeat, ignore the cut-and-pasted forms with the same bugs on
each. What would be the motivation for an external contractor
to attempt a refactoring in a code base without tests?

Yes, that's right. This Rails app that I inherited, the one that had
been described by my boss (a marketer!) as "pretty solid," had no
automated tests. It was stuck precariously on Ruby 1.8.7 and Rails 2.3,
both end-of-life. I described the entity relationships as a "star
topology"; what I was conveying was that it was a giant clusterf---.
The 70,000 lines read like they were written on a whiteboard at a
dismal job interview. "I was hoping you'd use Enumerable#select,"
the interviewer lamented. It was a relief that it seemed that customers
barely used the app, since the data presented in the customer portal
was simply wrong, and anyway, if they didn't like their data, they
could change everything (for anyone) by pointing their browsers to
the admin portal, which any user could access as long as they had the
link. The fact that we hadn't been hacked yet, at least meant that
nobody cared enough to hack us. How long could we keep getting away
with that?

So here I was, with a production application with no automated tests,
with gaping security holes, stuck on dead and out-of-date gems. The
words flashed in front of me again: "What do you want me to be doing
in five years?"

I get upset just thinking about these moments, because of all the
emotions I recall feeling when I discovered that the app that my
company depended on every day was a ticking time bomb, and that I
was the only one in the whole organization who understood what that
meant.