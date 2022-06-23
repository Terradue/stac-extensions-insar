# Interferometry Extension Specification

- **Title:** Interferometry
- **Identifier:** <https://stac-extensions.github.io/insar/v1.0.0/schema.json>
- **Field Name Prefix:** insar
- **Scope:** Item
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Proposal
- **Owner**: @fabricebrito, @emmanuelmathot

This document explains the interferometry Extension to the [SpatioTemporal Asset Catalog](https://github.com/radiantearth/stac-spec) (STAC) specification.

Interferometric synthetic aperture radar, abbreviated InSAR (or deprecated IfSAR), is a radar technique used in geodesy and remote sensing. This geodetic method uses two or more synthetic aperture radar (SAR) images to generate maps of surface deformation or digital elevation, using differences in the phase of the waves returning to the satellite or aircraft. The technique can potentially measure millimetre-scale changes in deformation over spans of days to years. It has applications for geophysical monitoring of natural hazards, for example earthquakes, volcanoes and landslides, and in structural engineering, in particular monitoring of subsidence and structural stability.

- Examples:
  - [Item example](examples/item.json): Shows the basic usage of the extension in a STAC Item
- [JSON Schema](json-schema/schema.json)
- [Changelog](./CHANGELOG.md)

## Item Properties 

| Field Name                   | Type                      | Description |
| ---------------------------- | ------------------------- | ----------- |
| insar:parallel_baseline      | \[number]                 |             |
| insar:perpendicular_baseline | \[number]                 | The distance between two acquisition spots perpendicular to the satellite viewing direction            |
| insar:temporal_baseline      | \[number]                 | The time period between the reference and secondary acquisitions |
| insar:height_of_ambiguity    | \[number]                 |  This height of ambiguity is the 2 π interferometric phase cycle scaled with the perpendicular baseline between both satellites. The smaller the height of ambiguity is, the lower is the influence of errors caused by the instrument or the different decorrelation effects. |
| reference_datetime           | \[string]                   | Date of reference acquisition, in UTC. It is formatted according to [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6).  |
| secondary_datetime           | \[string]                   | Date of secondary acquisition, in UTC. It is formatted according to [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6).  |

## Best Practices

One of the emerging best practices is to use [Asset Roles](https://github.com/radiantearth/stac-spec/tree/master/item-spec/item-spec.md#asset-roles) 
to provide clients with more information about the assets in an item. The following list includes a shared vocabulary for some common SAR assets. 
This list should not be considered definitive, and implementors are welcome to use other asset roles. If consensus and tooling consolidates around 
these role names then they will be specified in the future as more standard than just 'best practices'.

| Role Name       | Description                                                            |
| --------------- | ---------------------------------------------------------------------- |
| coherence       | 2D Coherence [0-1] from filtered interferogram                         |
| phase           | 2D Filtered wrapped interferogram geocoded in radians                  |
| unwrapped_phase | 2D Filtered unwrapped interferogram geocoded in radians                |
| amplitude       | 2D Amplitude of interferogram in Watt                                  |

## Contributing

All contributions are subject to the
[STAC Specification Code of Conduct](https://github.com/radiantearth/stac-spec/blob/master/CODE_OF_CONDUCT.md).
For contributions, please follow the
[STAC specification contributing guide](https://github.com/radiantearth/stac-spec/blob/master/CONTRIBUTING.md) Instructions
for running tests are copied here for convenience.

### Running tests

The same checks that run as checks on PR's are part of the repository and can be run locally to verify that changes are valid. 
To run tests locally, you'll need `npm`, which is a standard part of any [node.js installation](https://nodejs.org/en/download/).

First you'll need to install everything with npm once. Just navigate to the root of this repository and on 
your command line run:
```bash
npm install
```

Then to check markdown formatting and test the examples against the JSON schema, you can run:
```bash
npm test
```

This will spit out the same texts that you see online, and you can then go and fix your markdown or examples.

If the tests reveal formatting problems with the examples, you can fix them with:
```bash
npm run format-examples
```
