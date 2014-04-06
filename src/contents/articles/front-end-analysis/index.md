---
title: Front end analysis
author: Nick Collings
date: 2014-04-05 15:00
template: article.jade
---

I've had my frustrations with front end application frameworks/libraries for a while now. None of them are quite perfect. I'd like to get down what I'd like to see and feel should be feasible.

1. Self contained functional view components - pass them data, a template and a little view-model mapping magic and you're off! On the server these return HTML, on the client they produce ready-bound DOM.
	1. Two-way data binding built in as standard on the client side.
	1. View logic defined declaratively in the templates.
	1. A simple way to map the data-model to the view-model.
1. Sharable logic
	1. Routing - just needs to invoke a controller.
	1. Controllers - a controller defines a mapping of a layout, to functional components, to data. This mapping exists, in the same form, on both the server and client so it should be sharable.
	1. Models - business logic exists independent of any presentation format so should easily be sharable.
	1. Views - compiled as they are on the front end, not from some nested set of Jade templates but as the output of the controllers compilation of layout, model and view components.
1. Templates that can be used as blueprints to both compile and parse HTML/DOM. This is a big one. The ability to compile HTML is the well trodden path of templating languages. The next step, as I see it, would be to define a template once and then use it to both generate ready-bound DOM and also to augment any existing unbound DOM with bindings. The latter is particularly important as it opens up the options of server side view rendering. Perceived load times would be shorter and the requirement of JS rendering would be removed entirely.