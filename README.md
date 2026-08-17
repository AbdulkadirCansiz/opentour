# OpenTour

**An open, portable package format for virtual tours.**

> Status: **draft** — the v0.1 specification is being written in the open. Feedback and issues are welcome.

## The problem

When a space is captured as a virtual tour today, the resulting data stays locked inside a closed
platform. A tour built on Matterport, Kuula or a similar service cannot be exported and moved
somewhere else in any meaningful form. When a museum, a municipality or a university archive
digitises its spaces, it becomes dependent on a single vendor: if that vendor shuts down, raises
its prices or changes its format, years of accumulated records become inaccessible.

There is no open, portable container for this kind of data. Viewers exist (Pannellum, Marzipano),
3D asset standards exist (glTF, OGC 3D Tiles), but nothing describes a *virtual tour as a whole* —
the panoramas, the links between scenes, the hotspots, the floor plans, the accessibility metadata,
the licensing.

## What OpenTour is

OpenTour is an open, versioned package format that describes a complete virtual tour independently
of any platform:

- **Panoramas** — equirectangular and cubemap images with standard metadata
- **Scene graph** — walkable positions and the links between them
- **Hotspots** — information points, media attachments, navigation targets
- **Floor plans** — with scene anchoring and measurement points
- **Multi-language content** — all user-facing text is translatable
- **Accessibility metadata** — alt text for scenes and hotspots, structured descriptions for
  screen readers, keyboard navigation hints
- **Licensing information** — machine-readable rights for every asset
- **Optional 3D assets** — point clouds and Gaussian splats, stored in existing open formats
  (glTF and friends), with chunking and level-of-detail defined for progressive loading

## Planned tooling

Alongside the specification, this project will provide:

1. A **reference read/write library** and a command line tool
2. A **validator and conformance test suite**, so implementations can prove correctness
3. **Converters** that read exports from closed platforms (Matterport, Kuula, Pano2VR) and
   produce OpenTour packages — so existing users can get their own data out
4. A **panorama processing library** that repairs the raw output of consumer 360 cameras:
   seam correction, tripod/nadir patching, horizon levelling, projection conversion, and
   face/licence-plate blurring for privacy

## Design principles

- **Build on existing standards, don't replace them.** 3D geometry stays in glTF; images keep
  their standard metadata; IIIF is the governance model we look up to.
- **Any implementer is first-class.** The format is designed so that anyone can produce and read
  OpenTour packages without our software. Our own commercial platform
  ([Tourision](https://tourision.com)) will be one consumer of the format, not its owner.
- **Longevity is a feature.** Versioning rules, backward compatibility, integrity checking and
  signing are part of the design from the start, not an afterthought.

## Who is behind this

OpenTour is started by [Fluxverys](https://fluxverys.com), a software company in Ankara, Türkiye.
We build virtual tour and 3D reconstruction software and run into the consequences of closed
formats daily — every time a customer asks whether their tour can be moved, archived or handed
to someone else.

## License

Specification text and all tooling in this repository are released under the
[Apache License 2.0](LICENSE).
