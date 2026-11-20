# Riemann

An archive of the material published with *The Riemann Hypothesis is the classic problem in number theory*: the announcement itself, the fourteen-part Lean 4 archive that accompanies it, and that archive unpacked into a working Lake project.

Nothing here is authored in this repository. Every byte under `Archive/` and `Source/` is the publisher's own output, kept exactly as distributed. This repository contributes the arrangement, and the documentation under `Documentation/`.

---

## Layout

**`Archive/`** - the immutable record. This is the copy to trust.

- **`Archive/Publication/Riemann-Solved.pdf`** - the announcement as published, 245,114 bytes.
- **`Archive/Distribution/lean.tar.gz`** - the formalization archive, 239,275,554 bytes, assembled from the fourteen parts.
- **`Archive/Distribution/Part/`** - the same archive exactly as published, split into fourteen fixed-size chunks, `lean.tar.gz.part01` through `lean.tar.gz.part14`.
- **`Archive/Manifest.sha256`** - SHA-256 for every file under `Archive/`, with paths relative to `Archive/`, so `shasum -a 256 -c Manifest.sha256` runs from inside that directory.

**`Source/Lean/`** - the archive extracted and left alone: a Lake project named `tree`, holding 175,187 files under `src/` alongside `lakefile.toml`, `lake-manifest.json` and `lean-toolchain`. File names, directory names and file contents are the publisher's; nothing is edited, reformatted or reorganised inside it.

**`Documentation/Reference/`** - what this repository adds.

- **`Publication.md`** - what the announcement says, in its own terms, and what it explicitly does not claim.
- **`Project.md`** - the Lake project read as configuration: toolchain, dependencies, libraries, elaboration options, build.
- **`Archive.md`** - provenance, the splitting scheme, reassembly, and the verification record.
- **`Inventory.md`** - the measured shape of the tree: file counts per library and the top-level map.

**`.gitattributes`** - line endings normalised to LF for every text file, and the fourteen distribution parts routed through Git LFS, so the repository carries LFS pointers rather than 234 MB of binary chunks. The PDF stays out of LFS deliberately: at 245 KB it is ordinary blob territory, and a reader should not need the LFS client to open the announcement.

---

## Why it is arranged this way

**Three layers, one direction of authority.** `Archive/` holds bytes that must never change, `Source/` holds the same content unpacked for use, and `Documentation/` describes both without ever being their source. Where they disagree, `Archive/` wins, and `Manifest.sha256` is how a disagreement is settled.

**The published split is kept, not discarded.** The assembled `lean.tar.gz` is convenient, but it is derived: the parts are what was actually served, and keeping them means the distribution can be re-checked rather than taken on faith.

**The extracted project keeps its own casing.** It sits at `Source/Lean/` while the archive's root directory is `lean/`. That difference is deliberate and inert: `lakefile.toml` declares `name = "tree"` and `srcDir = "src"`, both relative and neither referring to the containing directory, so the outer name can be recased without touching a single project file. Verification was run before the recasing, while the directory still carried its published name, and the recipe for repeating it is in `Archive.md`.

**Only build output is excluded from git.** The PDF, the fourteen parts, the manifest, the whole extracted tree and this documentation are all tracked. Two paths are not: `Archive/Distribution/lean.tar.gz`, because it exceeds GitHub's per-file limit and is one command away from the parts, and `Source/Lean/.lake/`, because it is what `lake build` writes. The Lean sources themselves are tracked deliberately - they are the artifact a reader actually opens and diffs, which a tarball is not.

---

## Working with it

Reassemble the archive from its parts:

```
cd Archive/Distribution
cat Part/lean.tar.gz.part* > lean.tar.gz
gzip -t lean.tar.gz
```

Check the archived bytes against the manifest:

```
cd Archive
shasum -a 256 -c Manifest.sha256
```

Build the formalization:

```
cd Source/Lean
lake exe cache get
lake build
```

The build needs the toolchain pinned in `lean-toolchain` (`leanprover/lean4:v4.33.1`), mathlib at the rev named in `lake-manifest.json`, and patience: 175,187 source files, 81 per cent of them in one library. Details in `Documentation/Reference/Project.md`.

---

## Standing caveat

The announcement is a claim by its author, published as an announcement and a formalization rather than as a refereed paper. It states that the argument is currently extremely long, that it is not readable in its present form, and that its simplifications have not yet been written. This repository records the material as published; it does not endorse, verify or assess the mathematics.
