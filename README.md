This repository aims start a collaboration among geospatial software developers to establish a core set of RESTful JSON-based standards to share geospatial information online. At the core it is an update or refactoring of the core ideas of the venerable OGC W\*S standards, taking the core concepts but starting over in a way that is in line with what modern developers expect from their standards.

The collaboration is rooted in open source principles and tools, but focused on the creation of open standards. Open Source implementations are encouraged but by no means required. Anyone is welcome to participate, but must back up 'ideas' with working code. Our goal is to be a collaboration of developers, not [architecture astronauts](http://www.joelonsoftware.com/articles/fog0000000018.html). 

A large hat tip goes to the group that built [GeoJSON](http://geojson.org) - [Hobu](https://github.com/hobu), Martin, Allan, [Sean](https://github.com/sgillies), [Tim](https://github.com/tschaub) and [Chris](https://github.com/crschmidt) set a great example of how to build an open geospatial specification that understands the complexity of the geospatial domain while keeping the specification simple and implementable. 

## In this repo

This repository contains the core [Principles](principles.md) that govern the collaboration. It also contains a [roadmap](roadmap.md) for the core specifications, as well as a [doc of ideas](roadmap-next.md) of what pieces will likely come next if the core is successful. 

## Philosophy
 

The core philosophy is to specify simple interfaces that enable developers to grow in to geospatial complexity. A developer with no background in geospatial data who is asked to add bounding box search to their API should be able to find a specification that saves them time. It shouldn't require them to grok all the subtleties of the geospatial domain; it should give them parameters and responses to add in to their API, ideally including libraries in their language of choice. 

But the pieces a developer adds should anticipate what they may be asked for next, and not paint the developer in to a corner. Many developers invent their own geospatial responses as the first request is always simple, but then end up with crufty code reinventing the wheel when they get asked for more complex use cases (lines and polygons, polygons with holes, data that crosses the dateline, alternate projections, complex geospatial operations like buffering).

The goal of open geospatial standards should be to provide simple API components and formats that can be incorporated in to a developer's work. But these simple components should include all the thinking about how they can expand for the complex use cases. Extensions to the core specifications should handle all the complexity that might be required. 

We want to work hard to make the core as simple as possible, but with great extensions to handle any complex use case. Any developer should feel a net savings in time when finding, understanding and implementing a standard. They should use standards not because of a greater 'interoperability' goal, but because a group of experienced people have distilled their knowledge in to practices and code that save time. And through that we hope to achieve greater interoperability and less needless replication in the world.

## Collaboration

Please review and edit to improve this repository through pull requests. If you pledge to put in time to help realize the goals add your name and github to the list below.

Chris Holmes [@cholmes](https://github.com/cholmes)
(add your name when you contribute)


