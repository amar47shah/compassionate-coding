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


