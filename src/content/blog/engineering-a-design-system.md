---
title: 'Engineering a Design System'
description: ''
pubDate: 'Mar 9 2026'
heroImage: '../../assets/blog-placeholder-3.jpg'
---

*This article was originally published 28th June 2021 on [devs.veeqo.com](https://web.archive.org/web/20210919075100/https://devs.veeqo.com/engineering-a-design-system/). A few years have passed since then, so I'll follow up with another post soon to discuss what I learned and how things evolved.*

> On my bookshelf is a copy of the [New York Transit Authority Graphics Standards Manual](https://web.archive.org/web/20210919075100/https://standardsmanual.com/products/nyctacompactedition), a 350 page book originally published in 1970 that describes the design and construction for the iconic NYC subway signage. The manual contains colour swatches, typeface specifications, shape geometries and more. It goes on to define rules for composing signs by combining arrows, directional information and colour coded identifiers (stations, lines, etc). It even offers guidance about how signage should be mounted at optimal heights for the best visibility. Everything you need to know to design signage for the NYC subway in the 1970’s is included in this manual.

Modern design systems are an evolution of those original ideas. Within the context of digital product development, they allow us to distil years of knowledge and hundreds of decisions down into a collection of connected tools that empower the design and development of user interfaces. It’s an expansive topic for which the motivations, benefits and challenges have been discussed at length.

This is not an introduction to design systems. Instead, I offer a first-hand account as we start the engine on our own design system at Veeqo.

## A brief history

Over the years the design of Veeqo’s user interface has changed. There are well worn reminders of the past when the product was young and offered a fraction of the functionality that it does today. As with any successful startup the focus was on delivering value for customers and moving quickly. More and more features were added and the product began to outgrow the original design.

To accommodate this growth and the needs of the product we adopted Google’s Material Design. With it’s comprehensive specifications and authoritative guidelines, Material Design quickly gained popularity and gave teams without a dedicated design team the tools they needed to build high quality user interfaces. However over time it became apparent that it was not a silver bullet. At that time Google offered no first-party implementation of the UI components, and third-party libraries were inconsistent and restrictive. The design system may have served Google well (which is debatable) but it could never accommodate the needs of every other product with different requirements.

This period taught up some valuable lessons:

1. To develop our own product identity, we need to design our own components that solve Veeqo specific problems and give us full control for future iterations.
2. Material Design was popular because it was comprehensive, well documented and authoritative.
3. Without first-party implementations of UI components (i.e. a code library) there will always be inconsistencies and miscommunication.

It was time for Veeqo to take back control and develop a design system in-house that was specific to our needs.

## Foundations
Since then, our growing design team has been developing a refreshed, modern visual design for Veeqo, focusing on composition of smaller UI components. The reality of continuing to deliver value and improvements to a maturing product means that we cannot afford to rebuild the entire application and start with a clean slate.

The development of this new UI design coincided with a few key milestones. Firstly, we fully embraced React as our primary frontend framework and from a technical perspective this new component driven design fits perfectly with React’s own concept of “components”. Secondly, we were planning to develop a brand new feature (the inventory) and rebuild other key features (the orders list and reports) so these were perfect opportunities to implement the new visual design.

As we’ve been developing these new features a few things have happened. The design team continued to formalise and expand their library of Figma UI components, using them to compose high fidelity mockups. This flexibility meant that they could explore ideas quickly and easily make changes. On the other side, our engineering teams had been implementing the designs and began extracting common React components into a separate library. We quickly realised that while running in parallel, these processes were not synchronized. React components might be named differently to their Figma counterparts and their visual design didn’t fully align.

This is the point where we acknowledge the “system” in “design system”, which has the following definitions in the Oxford English Dictionary:

* “a set of things working together as parts of a mechanism or an interconnecting network; a complex whole.”
* “a set of principles or procedures according to which something is done; an organized scheme or method.”

Our two component libraries were disconnected. Which was the source of truth? The design team holds the vision and leads the creative process from which new features emerge, but ultimately it’s the application built by the engineering team that customers interact with. Our goal is to create a design system that promotes collaboration between designers and engineers. We had to create connections between teams and the different tools they were using.

## Set in motion

We began by establishing a regular meeting between designers and frontend engineers which brought everyone together in the same (virtual) room and allowed us to share what was happening across the different product teams. Engineers could find out about new designs that were in the pipeline and identify which components already existed and which did not, and designers could help review and refine code components. Having those conversations helps build trust between the different teams and develop a plan to kickstart our design system project.

It involves 3 stages:
1. **Align** our existing components by using the same names and fixing the visual design.
2. **Extract** fundamental visual design properties that transcend any specific medium.
3. **Develop** resilient user interfaces that can adapt as tools change.

The alignment stage has already been completed. We compared our React and Figma components to identify where there were naming conflicts and where their visual styles differed. For the majority of naming conflicts, we chose (for a number of reasons) to change the name of the component in the React library. To ensure that we didn’t break compatibility with our apps that were consuming the library, we actually created a copy of the offending component using the new name and deprecated the existing one. If there was a naming conflict with no clear right or wrong choice, we would change the name of the Figma component because it was instant and didn’t break existing instances of that component. When we identified a difference in the visual design between a React and Figma component we always changed the code to adhere to the designer’s vision. With that done, we now had a reliable language to use when referring to components.

The extraction stage is where we currently find ourselves. The reason we maintain separate component libraries is because the tools we use operate on different mediums, and though some claim it, there is no silver bullet that can generate production-quality code from a visual design (yet). Having said that, there are still fundamental visual design properties that transcend those tools. For example, a simple button consists of a box with some text. That box might have a colour and rounded corners. The text also has a colour with a certain font and size. These can all be described without using any tooling-specific language. We’ve been experimenting with design tokens to try to create a source of truth for these properties that can be translated into different formats (CSS, Javascript, JSON, etc.) and consumed by the different tooling that we use. It’s still early days but we’re excited by the possibilities.

The final stage is to build on that foundation and create a system of UI components that adapt to meet our needs as we continue to build a great product. Trends in design and technology come and go so it makes sense to avoid coupling such an important part of our application to any specific tool where possible. If we need to throw together a quick prototype for user testing we shouldn’t need to use React. Our interface design should follow us wherever we go.

We’re just at the beginning of our design system project and there is a lot more work to be done but thanks to everyone that has contributed so far, we’re already seeing good results.