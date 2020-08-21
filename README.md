# Reprojection Resources

Resources for using non-web-mercator projections with Mapbox GL JS

## Description

While working on Covid-19 related maps, I encountered situations where a different map projection would be handy, where we are showing data at a national or worldwide scale. Mapbox GL is limited to web mercator, but it is possible to reproject coordinates into web mercator in a way that looks like a different projection. This repository brings together scripts, tools, and demos help accomplish that affect.

## Getting Started

### Install dependencies

- Dirty Reprojectors: `npm install -g dirty-reprojectors`
- Tippecanoe: [installation instructions](https://github.com/mapbox/tippecanoe#installation)
- MBUtil: [installation instructions](https://github.com/mapbox/mbutil#installation)

## Road Bumps

If you run into an issue where the reprojection produces unexpected shapes that look like graticules or boundinb boxes, take a look at [this issue](https://github.com/developmentseed/dirty-reprojectors/issues/13). `dirty-reprojectors` seems to have an issue with [RFC 7946-compliant GeoJSON](https://github.com/developmentseed/dirty-reprojectors/issues/13#issuecomment-662715598).
