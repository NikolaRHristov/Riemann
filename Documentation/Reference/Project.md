# Project

The extracted archive is a Lean 4 project built with Lake. Its own configuration files are the authority for everything on this page; the page records what they declare and what that implies in practice.

---

## Identity

**Name and source root** - `lakefile.toml` declares `name = "tree"` and `srcDir = "src"`. The project name has no relation to the subject matter and no relation to the containing directory.

**Toolchain** - `lean-toolchain` pins `leanprover/lean4:v4.33.1`. Lake and elan both read this file, so the correct compiler is selected automatically on entering the directory; nothing needs to be installed by hand as long as elan is present.

**Manifest** - `lake-manifest.json` is format version 1.2.0 with `packagesDir = ".lake/packages"`, so dependencies land inside the project at `.lake/packages` rather than in a shared store.

---

## Libraries

`defaultTargets` lists the libraries in this order: `BuildAid`, `CompanionTheory`, `Development`, `Formalism`, `GroundTheory`, `GroundTheoryFields`, `Lemmata`, `PositivityTheory`, `ReciprocityTheory`, `Supplements`, `Main`.

**One library per top-level name**, each declared with a glob of `<Name>.+`, which takes everything under that directory.

**`GroundTheory` is the exception to the glob**, declaring ten explicit subtrees instead of one wildcard: `ArithmeticGeometry`, `AutomorphicForms`, `Brauer`, `FunctionField`, `HeightsAndTheta`, `IdeleRoots`, `PAdicHodge`, `PowerSubgroups`, `ProfiniteCohomology`, `TateCohomology`. A new directory under `src/GroundTheory/` therefore does not join the build until it is added here.

**`GroundTheoryFields` is split out of `GroundTheory`** by name, globbing `GroundTheory.LocalFields.+` and `GroundTheory.GlobalFields.+`. It carries a library-level `synthInstance.maxHeartbeats` of 400,000, an order of magnitude below the project ceiling and an order of magnitude above Lean's default, which marks these two subtrees as the place where instance search is expensive.

**`Main` is not a glob** but a root list: `Statements` and `Main`, the only two files sitting directly in `src/`.

---

## Elaboration options

The `[leanOptions]` table sets `autoImplicit = false`, `relaxedAutoImplicit = false`, `maxSynthPendingDepth = 3`, `pp.unicode.fun = true` and `maxHeartbeats = 4000000`, and `moreLeanArgs` passes `--tstack=400000`.

**`autoImplicit = false` is the consequential one.** Lean's default silently binds unknown identifiers as implicit variables; with it off, every variable is bound explicitly. The tree is written to that discipline and will not elaborate under default settings, so these options are part of the proof, not tuning.

**`maxHeartbeats = 4000000`** is forty times Lean's default ceiling of 100,000 per declaration. Long proofs here are expected to be long-running, and a build with default limits would fail on timeouts rather than on errors.

**`--tstack=400000`** raises the kernel's type-stack depth. Deeply nested types overflow the default and produce an internal error rather than a diagnostic.

---

## Dependencies

`mathlib` is the single direct dependency, at rev `0df444a360eaa60ab8c11dca51a86af692955474` from `leanprover-community/mathlib4`. Everything else in the manifest is inherited through it.

- **`plausible`** - `b7eb3304aeae`
- **`LeanSearchClient`** - `5f4d51b81cbd`
- **`importGraph`** - `16f02aa76428`
- **`proofwidgets`** - `4be2e3d5087e`
- **`aesop`** - `3448c0bcc5ce`
- **`Qq`** - `92c15be17b7c`
- **`batteries`** - `4488d40d070b`
- **`Cli`** - `6130a47896ce`

None are vendored. A first build resolves all of them over the network, and mathlib in particular is large enough that fetching its prebuilt oleans is not optional in practice.

---

## Building

```
cd Source/Lean
lake exe cache get
lake build
```

**`lake exe cache get`** downloads mathlib's precompiled oleans for the pinned revision. Skipping it does not fail; it elaborates mathlib from source instead, which takes hours.

**`lake build` with no target** builds everything in `defaultTargets`, which is the whole project. Building one library by name is possible and much faster, for example `lake build Formalism`.

**Expect the build to be heavy.** 175,187 source files, 81 per cent of them in `Development`, with heartbeats raised fortyfold because the arguments are genuinely long-running. The announcement itself describes the current argument as extremely long and routine to turn into a huge unreadable document, so the tree is sized for machine checking rather than for reading.

---

## Reading it

The two files directly in `src/` are the entry points: `Statements.lean` and `Main.lean`. They are the roots `Main` builds from, and they are where a reader looking for the shape of the argument should start, rather than in `Development`, which is where its bulk lives.
