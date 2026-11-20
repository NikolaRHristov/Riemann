# Inventory

The measured shape of the extracted tree. Every number here comes from walking
the archive or the extracted files, not from estimating; the commands that
produce them are named where the number is not self-evident.

This page is about _shape_ - how many files, where they sit, how large they are.
For the statistics of the formalization itself (declaration counts, closure,
imports, and what a median file actually contains) see the `README.md`.

---

## Totals

**Members** - 175,190, and every one is a regular file. The archive carries no
directory entries at all, so directory structure exists only as prefixes of
member paths.

**Content bytes** - 1,030,536,719 in total, a mean of 5,882 bytes per file. That
is 983 MiB of actual content.

**On disk** - `du -sh Source` reports 1.3 GB rather than 983 MiB, because
175,190 files of under 6 KB each round up to filesystem blocks. The difference
is allocation, not extra data.

**Extensions** - 175,187 `.lean` files, plus exactly three others:
`lakefile.toml`, `lake-manifest.json`, and `lean-toolchain`. There is no README,
no licence file, no CI configuration, no test directory and no documentation
inside the archive. It is source only.

**Timestamps** - every file carries mtime 0, the Unix epoch. The archive was
packed with normalised times, so nothing in it records when a file was written
and extraction is independent of when it is run.

**Depth** - the deepest path is twelve directories below the project root:
`Development/WeilBound/RepresentationTheoryGL/ArchimedeanBaseChange/ArchimedeanBaseChangeProof/ArchimedeanGelfandKernels/LeftEquivariantFunctions/ComplexMatrixCalculus/InverseLineDerivatives/DeterminantRankOneUpdate/DetOneAddSingle.lean`.
The directory names carry the structure of the argument, so the paths are part
of the documentation the tree provides.

---

## Files per library

Counted from the archive listing, which is authoritative for what the
distribution contains.

- **`Development`** - 141,928 files, 1.0 GB. 81 per cent of the tree.
- **`Formalism`** - 18,245 files, 195 MB.
- **`GroundTheory`** - 8,507 files, 71 MB.
- **`ReciprocityTheory`** - 3,845 files, 35 MB.
- **`CompanionTheory`** - 2,027 files, 15 MB.
- **`PositivityTheory`** - 449 files, 3.8 MB.
- **`Lemmata`** - 167 files, 824 KB.
- **`BuildAid`** - 5 files, 20 KB, named `D1.lean` through `D5.lean`.
- **`Supplements`** - 3 files, 12 KB.
- **`Main`** - the two files directly in `src/`, `Main.lean` and
  `Statements.lean`, 4 KB each.

---

## Inside GroundTheory

`GroundTheory` is the one library the build does not glob wholesale, so its
subtrees matter individually. Sizes are file counts.

- **`HeightsAndTheta`** - 6,410. By itself larger than any library except
  `Development` and `Formalism`.
- **`AutomorphicForms`** - 542.
- **`ProfiniteCohomology`** - 450.
- **`GlobalFields`** - 384, built as part of `GroundTheoryFields`.
- **`PAdicHodge`** - 226.
- **`ArithmeticGeometry`** - 218.
- **`LocalFields`** - 159, built as part of `GroundTheoryFields`.
- **`TateCohomology`** - 56.
- **`PowerSubgroups`** - 20.
- **`Brauer`** - 20.
- **`FunctionField`** - 12.
- **`IdeleRoots`** - 10.

---

## Largest files

The five biggest members, in bytes:

- **913,995** -
  `Formalism/HermitianCurvature/HermitianCurvatureProofs/IsAdmissibleSplittingCharPairMulTwist.lean`
- **732,359** -
  `Development/AutomorphicArithmetic/IntegralCasts/CapelliIdentities/FixPiIff.lean`
- **504,790** -
  `Development/AutomorphicArithmetic/IntegralCasts/CapelliIdentities/CovariantDegrees.lean`
- **478,050** -
  `Development/AutomorphicArithmetic/IntegralCasts/CapelliIdentities/MemOfClosed.lean`
- **454,809** -
  `Formalism/SharpRestriction/CuspSpanNormBounds/LatticeGluingRadicals.lean`

Half a megabyte in a single Lean file is roughly ten thousand lines, which is
where the raised heartbeat ceiling stops being surprising.

---

## Top-level map

```
Source/Lean/
    lakefile.toml
    lake-manifest.json
    lean-toolchain
    src/
        Main.lean
        Statements.lean
        BuildAid/
        CompanionTheory/
        Development/
        Formalism/
        GroundTheory/
            ArithmeticGeometry/
            AutomorphicForms/
            Brauer/
            FunctionField/
            HeightsAndTheta/
            IdeleRoots/
            PAdicHodge/
            PowerSubgroups/
            ProfiniteCohomology/
            TateCohomology/
        Lemmata/
        PositivityTheory/
        ReciprocityTheory/
        Supplements/
```

---

## What the shape says

**The statement is two files; everything else is machinery.** `Main.lean` and
`Statements.lean` sit at the top of `src/` and are the roots the `Main` library
builds from. The other 175,185 files exist to make those two check.

**`Development` is a workbench, not a section of the argument.** At 81 per cent
of the tree and 1 GB, it dwarfs every named theory library. Its directory
names - `AutomorphicArithmetic/IntegralCasts/CapelliIdentities`,
`WeilBound/RepresentationTheoryGL/ArchimedeanBaseChange` - read as exploration
that the final argument passes through rather than as the argument itself.

**The named libraries are the argument's skeleton.** `Formalism` states what is
to be shown, `GroundTheory` supplies the arithmetic and automorphic ground,
`ReciprocityTheory`, `CompanionTheory` and `PositivityTheory` are the three
moves the announcement describes, and `Lemmata` holds what is shared.

**There is nothing to read first except the two roots.** No README, no overview
file, no module docstring at the top of the tree. A reader has to enter through
`Statements.lean` or through the library names, which is why those two files are
worth opening before anything else.
