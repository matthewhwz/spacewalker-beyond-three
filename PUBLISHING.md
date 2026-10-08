# Publishing these notes

Use the contents of this directory as the root of a new GitHub documentation repository. A suitable name is `spacewalker-beyond-three`.

Suggested repository description:

> Engineering notes from personal five- to nine-screen AR desktop experiments: display mapping, 3D geometry, calibration, and validation.

## Included material

This package contains newly written Markdown explanations and a defensive `.gitignore`. It deliberately excludes executable code and vendor implementation details: no source excerpts, decompiled listings, instruction bytes, offsets, patch scripts, app bundles, libraries, SDKs, fonts, icons, or extracted UI resources. The conceptual grid and geometry discussion are written explanations of the local experiment.

Private paths, device calibration, raw logs, preference files, and device identifiers are also excluded. Product names are used for context, and the README states the project's independent status.

This describes the package's contents; it is not a legal determination about the underlying experiment or a guarantee of publication rights.

## Upload steps

1. Create a new repository for these notes.
2. Upload the contents of `github-share`, with `README.md` at the repository root. The supplied ZIP contains the same package; extract it before using GitHub's file upload interface.
3. Review GitHub's file list. It should contain eight Markdown files and `.gitignore` only.
4. Commit the documentation. You do not need to upload the surrounding local project.

No license has been selected for you. If you choose one later, scope it to material you have the right to license, such as your documentation. It must not imply a grant of rights over third-party applications or assets.

The `.gitignore` is an additional guard against accidental additions. It does not remove files already tracked by Git and does not make uploading the whole experimental workspace appropriate.
