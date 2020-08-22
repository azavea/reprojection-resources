# Reprojection Resources

Resources for using non-web-mercator projections with Mapbox GL JS

## Description

While working on Covid-19 related maps, I encountered situations where a different map projection would be handy, where we are showing data at a national or worldwide scale. Mapbox GL is limited to web mercator, but it is possible to reproject coordinates into web mercator in a way that looks like a different projection. This repository brings together scripts, tools, and demos help accomplish that affect.

## Why and Why Not?

### Why?

Mapbox GL JS, by default, uses the Web Mercator projection, as does most of the maps on the web. The Mercator projection, created in the 1500's was designed for navigation. It represents north as up and south as down, and angles are locally correct.

Of course, most of the maps we make at Azavea are not intended for sailing around the world. Mercator distorts area, increasing the size of countries farther from the equator. A common example is that Greenland appears larger than Africa, while Africa is 14 times larger than Greenland.

Your choice of projections can impact issues of fairness and representation. It can support your narrative, allowing you to focus on a particular area of the world.

| Type                                                                                 | Directory                                                                                                                                                   |
| ------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| US-centric                                                                           | [albersUsa](https://github.com/d3/d3-geo/blob/master/README.md#geoAlbersUsa)                                                                                |
| World, equal area                                                                    | [cylindricalEqualArea](https://github.com/d3/d3-geo-projection#geoCylindricalEqualArea), [mollweide](https://github.com/d3/d3-geo-projection#geoMollweide), |
| World, good overall (compromise between preserving shape, area, distance, direction) | [robinson](https://en.wikipedia.org/wiki/Robinson_projection)                                                                                               |

[View all available projections](https://github.com/developmentseed/dirty-reprojectors/tree/master/projections)

### Why Not?

Using a different projection with Mapbox GL JS takes more work. You are unable to use any of Mapbox's basemaps or any of their data. You will need to bring all of your own data, including boundaries and place labels. This project contains some starter [`data`](/../../data/) that can be used, but it pales in comparison to what is available out the box with basemap providers.

In addition to being responsible for all data used on the map, you will need to style that data and run it through reprojection scripts.

If you are depending on raster layers, you will not be able to use any standard raster layers. Rasters will similarly need to be reprojected, so you wouldn't be able to plug in some pre-existing xyz raster tiles.

## Getting Started

### Install dependencies

- Dirty Reprojectors: `npm install -g dirty-reprojectors`
- Tippecanoe: [installation instructions](https://github.com/mapbox/tippecanoe#installation)
- MBUtil: [installation instructions](https://github.com/mapbox/mbutil#installation)

## Resources

### Data

A collection of data that works well with `dirty-reprojectors`, which can be used to jumpstart a new visualization project. Much of this data is modified from [Natural Earth](https://www.naturalearthdata.com/).

| Type          | Directory                         |
| ------------- | --------------------------------- |
| United States | [`data/us`](/../../data/us)       |
| World         | [`data/world`](/../../data/world) |

### Scripts

Example scripts are available in [`visualizations`](/../../visualizations). These can be a useful reference point for how the general process works. Each visualization will need its own custom script to process its unique layers.

### Visualizations

Example projects that show reprojected tiles in action. These can be a helpful resource for cartography, how to apply custom styles to reprojected layers.

| Type                       | Directory                                                             |
| -------------------------- | --------------------------------------------------------------------- |
| US Congressional Districts | [`visualizations/congressional`](/../../visualizations/congressional) |

#### Run test script

Run the test script
`./scripts/process-congressional`

Tiles will be generated at `data/_reprojected/tiles`. You can use these tiles in the visualization found at `visualizations/congressional`.

## Road Bumps

If you run into an issue where the reprojection produces unexpected shapes that look like graticules or boundinb boxes, take a look at [this issue](https://github.com/developmentseed/dirty-reprojectors/issues/13). `dirty-reprojectors` seems to have an issue with [RFC 7946-compliant GeoJSON](https://github.com/developmentseed/dirty-reprojectors/issues/13#issuecomment-662715598).
