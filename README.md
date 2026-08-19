# glTF-Schema (Fork)

This repository is a fork of [KhronosGroup/glTF](https://github.com/KhronosGroup/glTF) and contains only the glTF 2.0 JSON Schema files.

## Scope

- Kept: glTF 2.0 core schemas under specification/2.0/schema.
- Kept: glTF 2.0 extension schemas under extensions/2.0.
- Removed: content outside schema definitions that is not needed for this fork.

## Gestaltor-specific additions

This fork includes additional custom properties required by Gestaltor.
These properties are added in a backward-compatible way so standard glTF 2.0 data remains valid.

## Folder layout

- specification/2.0/schema: glTF 2.0 core JSON Schemas
- extensions/2.0: glTF 2.0 extension JSON Schemas (Khronos and vendor)

## Notes

- Upstream basis: KhronosGroup/glTF
- Purpose of this fork: provide a focused schema set for tooling and validation workflows used by Gestaltor
- all properties in the schemas beginning with "ux3d_" are custom properties added by Gestaltor and are not part of the official glTF 2.0 specification.
