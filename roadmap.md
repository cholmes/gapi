## About

This document serves as a list of core specifications that need to be created. It will likely evolve quite a bit, as it has large implications for the overall architecture. And indeed creating the actual specifications should reflect back in how we think about what's next.

## Core

These should be a small number of core web specifications that would be a first entry point to any developer interested in geospatial. They should build on common core components, presenting a coherent easy to understand interface that is relatively easy to build. There is lots of work to do to figure out the right divisions, how much the two major types of geospatial data (vector and raster) are represented similarly or differently. 

**Features Server** - Return vector data as GeoJSON: geometry + fields. Cacheable (compatible with CDN's, easily queried for latest changes), self-describing (using OpenAPI to describe itself), and assuming 2D flat feature structure (no nesting, no references). Extensible to enable alternate formats, notifications, crud operations, statistics/aggregation, styling, generalization, etc. But those should be independent specs. Inspirations should include Mapbox's [Datasets API](https://www.mapbox.com/api-documentation/#datasets), [FeatureServer](http://featureserver.org), Planet's [Data API](https://www.planet.com/api-explorer/), see its [OpenAPI spec](https://api.planet.com/data/v1/spec) and Esri's ? 

**Pixel Server** - Return vector + raster data as images (png/jpeg - with extensions for jp2k/mrf/geotiff/multi-band data,etc). Core should be tile based (cacheable) in web mercator, time / depth aware, described by JSON. [TileJSON](https://github.com/mapbox/tilejson-spec) is likely quite close. Extensions should allow for more flexibility - alternate projections, formats, more bands, time, no tiles, video frames, styling, etc. Assumes a grayer line between WMS (rendered pixels) and WCS (source pixels) concepts - both are pixels, coverage can just return more options. We will need to figure out how exactly we divide up needed functionality, but likely shouldn't be completely separate services, but different sets of capabilities that are enabled. 

**Processing** (2nd priority) - Run compute operations on vector or raster data, outputting it to online datastores. Should be built cloud-first, and assume moving processes to the data instead of uploading data to run an algorithm. The key piece is to track the 'provenance' of all data. Any manipulation of data in to a new data set should trace back to the online data store the data came from. Users should be able to run operations in the cloud and assume that all manipulations of data are recorded. 

## Core Components

These are a set of small API pieces that should be combined to build the core specs. But they should also be useful in their own right, for those who may not want the whole core interface but needs some geospatial pieces for their API.

**Capabilities** - How to negotiate between a client and server to obtain what operations it is capable of.

**Output formats** - How to request data in a different format.

**Core Filters** - numerical, time and string equals, comparison and range queries, plus BBOX geometry filtering.

**Advanced Filters** - More obscure geometry operations, like touches, contains, distance within, etc.

**Assets** - References to related data as a field from the core feature. Links to images, audio, video, etc.

**Reprojection** - How to respond to requests in different projections, and return data in a requested projection


## Profiles

These are extensions to the core that enable more specific functionality.

**Imagery Catalog Profile** - An API to search large imagery holdings, with set core shared schema. Likely quite similar to https://www.planet.com/api-explorer/ 

**Layer Catalog Profile** - CSW updated for REST+JSON, built on core feature server. The core metadata fields should be possible to add on to the core feature server. Ideally there's a simple flat feature response with like core dublin metadata, but it would enable more complex responses if needed.

**Domain Specific Profile** - Attempt to represent a domain specific GML profile as a feature server.

## Next Feature Extensions

**Notifications/Events** - Mechanism to get updates on changes on a core server, so client does not have to poll for updates. 

**Syncing** Use the notification mechanism to do server to server syncing, with provenance tracking. A server that is the canonical source of data should be able to recieve a 'pingback' so it also knows where/how its data is being used.

**Generalization / Simplification** - Way to specify a zoom level or simplification amount to a feature server and get a geometry that is the right complexity for the zoom level.

**Feature Transactions** - Enable CRUD (creation, updates and deletion) of fields and geometries on a Features Server.

**Static Services** - Create profiles for 'stupid' ways to just put data up on a cloud storage bucket or totally non-geo software (like CMS, etc) that can easily be crawled by other more advanced services. Likely a json sidecar file on each image or vector dataset, with a 'table of contents' that tells a service how to crawl it.

**Feature Statistics / Aggregation** - Queries to feature service may require more complex backend, for interesting statistics. Get counts, or bucketed counts (tell me the number of 'severe fires' for each month in the past 5 years) that can drive graphs, etc.

**Geometry Statistics / Aggregation** - Queries to feature services that give results of aggregated geometries (in heatmap, etc) on a regular grid. Perhaps include Torque type output (or do that in its own).

**Versioning** - Keep track of previous versions of features that have had transactions.

## Next Pixel Extensions

**Tileless responses** - Return the frame requested by the client instead of a regular tile grid. Some use cases will perform better this way. Tiles should be the core, and all should be able to respond by that grid. But streaming may work better if it's not trying to tile everything. Should also be useful for static image serving.

**Multi-band responses** - Should have ways to return data in multi-band formats (like geotiff or MRF), and to let users choose exactly which bands they want. 

**Clipping Responses** - Like a tileless response, but cut data to exactly the shape a client wants. May work very similarly, where tileless just gives a box and clipping can give a geometry. Should also be able to clip along with multi-band selection.

**Multi-dimensional querying** - Server representations for NetCDF and GRIB type multidimensional data. Look in to something like [xarray](https://github.com/pydata/xarray) interface

**Video / streaming** - Any needed extensions for high frame rate data, and to get real performance from sending data to the client. May want to investigate web workers.

**Data Tiles** - Provide way to map multi-band data to 3-band tile sets, and enable client side manipulation of algorithms in Canvas. See [Planet Ag demo](https://demo.planet.com/ag/ag-indices/) for an example.

**Image Operations** - Provide server side processing of images for certain optimizations before returning to the client. Should be fully compatible with 'processing' capabilities. See [ModelLab](https://www.azavea.com/projects/modellab/) and Esri's image server for inspiration.

## Beyond

Explore things like styling (CartoCSS?), on the fly styling (pull data from an online source and render), optimized formats like protobuf, and how vector tiles fit in to the picture.
