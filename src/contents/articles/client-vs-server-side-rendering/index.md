---
title: Client vs server side rendering
author: Nick Collings
date: 2014-04-05 16:00
template: article.jade
---

One of the biggest problems with the front end web application stack is the lack of code sharing. This is particularly frustrating when it comes to rendering. We are forced to have two different rendering contexts; one for the server, one for the client. At first this seems reasonable - the server needs only produce one mammoth piece of static HTML whilst the client needs to be more dynamic and modular. While this will always be true, I believe we have overlooked some opportunities for code sharing.

The old web application architecture (Rails and Django etc) saw all the logic and rendering on the server. The client was little more than a web page renderer with full reloads between each view/action. This resulted in a clunky feel to the application which ultimately could not compete with a native experience.

More recent solutions like Backbone (which I have been using for 3 years or so now) sought to take advantage of AJAX to provide richer interfaces. Apps started to feel faster, slicker, and allowed for more complex visuals and interactions. Definitely a positive move. Unfortunately this richness came with the caveat that all the rendering takes place on the client. This has reuslted in many apps having slow initial render times and sometimes even the dreaded loading bars of the Flash era. Where we have gained we have lost elsewhere. Apart from anything else this clearly wastes the power of the server turning it into a dumb web server and data provider.

While I understand you cannot always expect complete render parity between client and server (the server shouldn't be handling every single interactions via full page reloads and the client probably shouldn't be juggling massive data sets either) I feel the black or white options we have available to us are too simple. A balance must be struck. We can do better.

#### What can we do?

As I mentioned in an [earlier post](/articles/front-end-analysis/) I believe templating is a key area to look at. Templates can do more than just compile down to HTML. In fact we are seeing solutions like [Ractive](http://www.ractivejs.org/) from the tech heads at the Guardian take bolder steps. They take an only slightly enhanced super set of [Handlebars](http://handlebarsjs.com/) and give you back a nice two-way bound DOM, ready to roll. Everyone knows Google's [Angular](http://angularjs.org/) gives us the same in a more declarative form, using the DOM as the template. Again another great step but both solutions leave the server out in the cold, rendering partial views and leaving the rest to the client.

To improve on this, I'd like to see templates treated like blueprints which could be used in one of the following ways; either

- taking a model and producing HTML or
- taking a model and producing a ready-bound DOM fragment or
- taking some unbound DOM and binding it to an existing model

The first is the process we are familar with from the Backbone universe - producing HTML is still a cumbersome approach on the client but still necessary for the server. The second covers client side rendering as with Ractive's techniques. The final approach would be massively useful when working with pages pre-rendered on the server (using the first approach incidentally). Angular has made a move towards the latter but expects templates in the DOM rather than the final mark up.

#### That's a tall order. What would this require?

Templates would need to output HTML/DOM such that the data model bindings can be inferred using only the original template as a reference. Essentially templates that allow for reverse compilation.

Current languages, such as Handlebars, support features that prevent the original template being inferred from the HTML, as highlighted by blerik's [this excellent Stack Overflow answer](http://stackoverflow.com/a/19271995). Using a subset, aligning to blerik's rules, should give us a workable solution.