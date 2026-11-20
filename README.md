# Riemann

An archive of the material published with _The Riemann Hypothesis is the classic
problem in number theory_: the announcement itself, the fourteen-part Lean 4
archive that accompanies it, and that archive unpacked into a working Lake
project.

Nothing here is authored in this repository. Every byte under `Archive/` and
`Source/` is the publisher's own output, kept exactly as distributed. This
repository contributes the arrangement, and the documentation under
`Documentation/`.

---

## The claim

The announcement states that its author, working with Claude, has discovered a
proof of the Riemann Hypothesis; that the method extends to the Generalized
Riemann Hypothesis; that he expects it to reach the Extended Riemann Hypothesis
with more time; and that the arguments are formalized in Lean without
assumptions. It presents only the formalization, on the stated grounds that
posting a 250,000-page generated document would be worse than useless. Full
account, in the document's own terms, in
`Documentation/Reference/Publication.md`.

This repository does not assess the mathematics. It records what was published,
verifiably, and measures it.

---

## What is here

**`Archive/`** - the immutable record, 457 MB. This is the copy to trust.

- **`Archive/Publication/Riemann-Solved.pdf`** - the announcement as published,
  245,114 bytes.
- **`Archive/Distribution/lean.tar.gz`** - the formalization archive,
  239,275,554 bytes, assembled from the fourteen parts.
- **`Archive/Distribution/Part/`** - the same archive exactly as published,
  split into fourteen fixed-size chunks, `lean.tar.gz.part01` through
  `lean.tar.gz.part14`.
- **`Archive/Manifest.sha256`** - SHA-256 for every file under `Archive/`, with
  paths relative to `Archive/`, so `shasum -a 256 -c Manifest.sha256` runs from
  inside that directory.

**`Source/Lean/`** - the archive extracted and left alone: a Lake project named
`tree`, holding 175,187 files under `src/` alongside `lakefile.toml`,
`lake-manifest.json` and `lean-toolchain`. File names, directory names and file
contents are the publisher's; nothing is edited, reformatted or reorganised
inside it.

**`Documentation/Reference/`** - what this repository adds.

- **`Publication.md`** - what the announcement says, and what it explicitly does
  not claim.
- **`Project.md`** - the Lake project as configuration: toolchain, dependencies,
  libraries, elaboration options, build.
- **`Archive.md`** - provenance, the splitting scheme, reassembly, and the
  verification record.
- **`Inventory.md`** - the measured shape of the tree, library by library.

**`.gitattributes`** - line endings normalised to LF for every text file, and
the fourteen distribution parts routed through Git LFS, so the repository
carries LFS pointers rather than 234 MB of binary chunks. The PDF stays out of
LFS deliberately: at 245 KB it is ordinary blob territory, and a reader should
not need the LFS client to open the announcement.

---

## The formalization in numbers

Every figure below is measured from the extracted tree, not estimated. The
profile pass reads all 175,187 files once; declaration counts are textual and
line-anchored, which is stated again under _How these numbers were taken_.

### Closure

```
sorry          0
sorryAx        0
admit          0
axiom          0
```

**Seventeen million lines with no declared gaps and no assumed axioms.** This is
the statistic that matters for material whose claim is "formalized without
assumptions", and it holds at the textual level: no `sorry`, no `admit`, and no
`axiom` declaration anywhere in the tree. `sorryAx` - the axiom Lean itself
introduces when `sorry` is elaborated - appears zero times, which is consistent.

It does not follow that the mathematics is right. A closed proof of a mis-stated
theorem is still closed. These counts rule out the two ways a formalization
usually cheats; they say nothing about whether `Statements.lean` says what the
announcement says it says.

### Scale

```
files               175,187
lines            17,374,215
bytes         1,030,531,854
mean lines/file          99
median lines/file        58
largest file         17,981
```

The mean sits well above the median, so the tree is a long tail rather than a
uniform body of work.

### Declarations

```
theorem         784,092
def             212,819
lemma            34,663
abbrev           13,202
structure         8,286
instance          7,820
example           4,662
inductive           121
class                43
axiom                 0
total         1,052,596
```

One declaration every 16.5 lines. The theorem-to-def ratio is 3.68.

The ratio that says most about how this was built: **8,286 structures against 43
classes**. A library written for human reuse grows a typeclass hierarchy; this
tree grows concrete structures and named theorems. That is the signature of
goal-directed generation, not of a library designed to be learned.

### Distribution of file sizes

```
0-50 lines      80,084   45.7%
50-200          71,395   40.8%
200-500         21,280   12.1%
500-1000         2,105    1.2%
1000-2000          250   0.14%
2000+               73   0.04%
```

86.5% of files are under 200 lines. The tree is deep and granular - thousands of
small lemmas - with a thin crust of enormous files where the hard arguments
concentrate. The eight largest:

```
17,981  Formalism/HermitianCurvature/HermitianCurvatureProofs/IsAdmissibleSplittingCharPairMulTwist.lean
 9,252  Formalism/SharpRestriction/CuspSpanNormBounds/LatticeGluingRadicals.lean
 8,029  Development/AutomorphicArithmetic/IntegralCasts/CapelliIdentities/FixPiIff.lean
 6,945  Formalism/SharpRestriction/CuspSpanNormBounds/KappaEndpoints.lean
 6,929  Formalism/HermitianCurvature/HermitianCurvatureProofs/UnipotentCoordinatesMeasurePreserving.lean
 6,333  Formalism/SharpRestriction/CuspSpanNormBounds/OscillatoryIntegralBounds.lean
 6,205  Formalism/HermitianCurvature/HermitianCurvatureProofs/CoordinateCommuteRaisingConstant.lean
 6,170  Development/AutomorphicArithmetic/IntegralCasts/CapelliIdentities/CovariantDegrees.lean
```

### Where the mass sits

```
library              files      lines      MB     decl
Development        141,928 12,232,663   767.3  687,336
Formalism           18,254  3,200,748   164.9  237,674
GroundTheory         8,507  1,119,138    54.6   74,737
ReciprocityTheory    3,845    563,016    28.9   36,186
CompanionTheory      2,027    194,218    11.3   11,700
PositivityTheory       449     55,130     3.1    4,699
Lemmata                167      9,232     0.5      251
Main (src root)          2         28     0.0        9
Supplements              3         22     0.0        4
BuildAid                 5         20     0.0        0
```

`Development` is 70.4% of the lines, `Formalism` 18.4%. The two files that carry
the statement - `Statements.lean` and `Main.lean` - are **28 lines and 9
declarations between them**, against 1,052,596 declarations of machinery.

Inside `Development`, seven subtrees:

```
AbelianVarietyTheory        99,187
AutomorphicArithmetic       18,431
AutomorphicSpectrum         15,147
WeilBound                    7,051
EtaleCohomology              1,398
ResolutionOfSingularities      499
DiscreteGroups                 215
```

`AbelianVarietyTheory` alone is **56.6% of every file in the tree**. A Riemann
Hypothesis formalization whose centre of gravity is abelian varieties rather
than the zeta function is exactly what the announcement describes: the argument
runs through arithmetic geometry and automorphic forms, not through complex
analysis.

### What it imports

```
files importing something   175,187
import lines                  909,822
mean imports per file               5
files importing only Mathlib    5,905
distinct module names         175,534
files importing Mathlib       155,753   (88.9%)
```

**Every file imports something; only 5,905 import nothing but mathlib.** The
tree is densely interdependent - 175,534 distinct module names against 175,187
files - and 88.9% of files reach mathlib directly rather than through a
re-export shim. The most-imported local module is reached 3,088 times, so there
is no single hub: the dependency graph is broad, not a spine.

---

## What a regular proof looks like

The tree does not read like a paper, and the median file shows why. The examples
below are the files closest to the median line count in each of the two
libraries that matter - not chosen, selected by that rule.

### A statement file

`Formalism/GaussJetBounds/StatementM.lean`, 58 lines, the median `Formalism`
file. It contains no proofs at all:

```lean
import Formalism.GaussJetBounds.StatementK

noncomputable section
open scoped BigOperators

universe u

namespace Formalism.DworkPowerSeriesWeights

open Formalism.IncomingBounds

def IsGeneric {K : Type u} [NormedField K] {σ : Type} (l : ℕ) (Y : σ → K) : Prop :=
  ∀ P : MvPolynomial σ ℤ, MvPolynomial.map (Int.castRingHom (ZMod l)) P ≠ 0 →
    ‖MvPolynomial.aeval Y P‖ = 1

def ThmAGeneric : Prop :=
  ∀ (K : Type u) [NormedField K] [IsUltrametricDist K] [CharZero K] (l d N0 N1 : ℕ) [NeZero d],
    l.Prime → 3 ≤ l → 2 ≤ d → Even d → ‖(l : K)‖ < 1 → 0 < N0 →
    ∀ (K0 : Subfield K), Unram l K0 → ∀ ζ : K, IsPrimitiveRoot ζ (l ^ d - 1) →
    ∀ be : MvPowerSeries (ZMod d) K, BHyp l d K0 ζ be →
    ∀ g : ZV d N0 N1 → MvPowerSeries (ZV d N0 N1) K, (∀ y, MvPowerSeries.constantCoeff (g y) = 0) →
      (∀ y, MvPowerSeries.subst g (entLog (K := K) l y) = MvPowerSeries.X y) →
    ∀ U : MvPowerSeries (ZV d N0 N1) K, Integral U → ∀ (ε : K), (ε = 1 ∨ ε = -1) →
    ∀ (TT : Finset (ZMod d)) (colN : ZMod d → ℕ) (p : ∀ s, Fin (colN s) → ℕ)
      (hp : ∀ s c, p s c ≤ N0), (∀ s c, 1 ≤ p s c) → ∀ (I : ∀ s c, Fin (p s c) → Fin N1),
    ∀ Y : ZMod d × Fin N0 × Fin N0 → K, IsGeneric l Y →
    ∀ (nu1 nu2 size : ZMod d → ℕ), (∀ s, nu1 s = colN s) →
      (∀ s, nu2 s = (Finset.univ.filter (fun c => 2 ≤ p s c)).card) → (∀ s, size s = ∑ c, p s c) →
    ∀ a : ℕ, 1 ≤ a → (∀ s, size s ≤ a) →
    ∀ (J : ZMod d → ℕ) (lab : ∀ s, Fin (J s) → ZMod d × ℤ), (∀ s, Function.Injective (lab s)) →
      (∀ (s s0 : ZMod d) (j : ℤ), (∃ i, lab s i = (s0, j)) ↔
        (s0 ∈ TT ∧ Odd j ∧ s = s0 + (j : ZMod d) ∧ (0 < j → l ^ j.toNat ≤ nu1 s0) ∧
          (j < 0 → l ^ (-j).toNat ≤ size s))) →
      (∀ s, J s + (if s ∈ TT then 1 else 0) ≤ N0) →
    ∀ m : ℕ, (∀ s i, (-(lab s i).2).toNat ≤ m) →
      ‖jetPair (∏ s : ZMod d, minorProd
            (fun (i : Fin N0) (b : Fin N1) => (MvPolynomial.X (s, i, b) : MvPolynomial (ZV d N0 N1) K))
            (p s) (hp s) (I s))
          (MvPowerSeries.subst (linSub (frameM (N1 := N1) (genFrame TT l m Y)))
              (MvPowerSeries.subst g U) *
            mvExp (ε • bSum (frameM (N1 := N1) (genFrame TT l m Y)) be))‖ ≤
        ‖(l : K)‖ ^ ((∑ s ∈ TT, (topTerm l d TT nu1 nu2 s - gam l * (Wcap l d TT nu1 nu2 size s : ℝ))) +
          Fnum l d (fun s => (Dl d TT nu1 size s : ℝ)) -
          ((d : ℝ) * N0 * N1) * (Real.logb l (a : ℝ) + 1))

end Formalism.DworkPowerSeriesWeights
```

Quoted are its opening, its `IsGeneric` predicate and its main statement. The
file also declares a helper `genFrame` and a closing existence statement
`GenericExists`, both omitted here.

A statement of this size is a single `def ... : Prop`, quantified over a dozen
parameters and every hypothesis the later proof is allowed to assume. Nothing
here is proved; the file exists to fix the target. This is what `Formalism` is
for, and it is why the library carries 237,674 declarations in 3.2 million
lines.

### A proof file

`Development/AutomorphicArithmetic/AutomorphicVarieties/ConjugateRepresentations/LocalLimitConjugates/CharOf.lean`,
58 lines, the median `Development` file. Header, one of its three private
helpers, and the public theorem:

```lean
import Development.AutomorphicArithmetic.AutomorphicVarieties.ConjugateRepresentations.LocalLimitConjugates.CasimirResolventProjection
import Development.AutomorphicArithmetic.AutomorphicVarieties.ConjugateRepresentations.LocalLimitConjugates.TmulMem
import Development.AutomorphicArithmetic.AutomorphicVarieties.ConjugateRepresentations.LocalLimitConjugates.SqOrth
import Development.AutomorphicArithmetic.AutomorphicVarieties.ConjugateRepresentations.LocalLimitConjugates.ROpApply
import Development.AutomorphicArithmetic.AutomorphicVarieties.LiteratureResults.BorelHarmonicForms.LieOneComm

private theorem cmp_rT {W : Type} [AddCommGroup W] [Module ℂ W] {d : ℕ} (T : Module.End ℂ W) (i : Fin d)
    (x : W ⊗[ℂ] (Fin d → ℂ)) : cmp i (T.rTensor _ x) = T (cmp i x) := by
  induction x using TensorProduct.induction_on with
  | zero => simp
  | add x y hx hy => simp only [map_add, hx, hy]
  | tmul φ v => simp

theorem UpperTheory.V.Cj.H.charOf :
    UpperTheory.V.Cj.H.CharOf := by
  intro E _ _ _ a ha n e he Ξ r m hm q ω h1 h2 h3 h4 X i t u
  have hL := (sqLie E a r).2
  obtain ⟨-, -, c3, c4⟩ := capSm E a Ξ t u
  have hx := wigSm E a Ξ (sqSub E a r) hL t (m t) (hm t) u q ω h1 h2 h4
  have hv : Val (sqSub E a r) (app (cap t u - ((m t).map (u + ·)).prod • 1) ω) := fun Y j => by
    rw [app_apply, cmp_rT, LinearMap.sub_apply, LinearMap.smul_apply, Module.End.one_apply]
    exact Submodule.sub_mem _ (c4 _ hL _ (h4 Y j)) (Submodule.smul_mem _ _ (h4 Y j))
  have hc := cocl_app Ξ r e (cap t u - ((m t).map (u + ·)).prod • 1) (fun Y φ => by
    have := LinearMap.congr_fun (c3 Y).eq φ
    simp only [Module.End.mul_apply] at this
    simp only [LinearMap.sub_apply, LinearMap.smul_apply, Module.End.one_apply, map_sub, map_smul, this]) ω h3
  have h0 := (sqOrth E a ha n e he Ξ r q).1 _ hv hc hx
  have h5 := congrArg (fun η : Co Ξ q => cmp i (η X)) h0
  simp only [app_apply, cmp_rT, AlternatingMap.zero_apply, map_zero, LinearMap.sub_apply, LinearMap.smul_apply,
    Module.End.one_apply] at h5
  exact sub_eq_zero.1 h5
```

Five imports, three private helpers, one public theorem. The `open` block
between them is omitted here; the proof itself is nine steps: `intro` to
discharge the binders, three `have`s that invoke previously proved results by
name (`sqLie`, `capSm`, `wigSm`, `sqOrth`), two sub-goals discharged inline, a
congruence, a `simp` normalisation, and `exact`.

**That is the regular shape of a proof here.** Not a paragraph of argument, but
a short chain of named lemmas applied to named hypotheses, closed by a term. The
mathematical content is in _which_ lemma to invoke, and that choice was made
once, when the lemma was written - not here, where it is merely cited.

### What this is not

A regular mathematical proof is prose. It says "hence", "by compactness", "it
follows that", and leaves the reader to fill gaps; its unit of work is the
paragraph, and its audience is a human who can reconstruct what was skipped. The
gap-filling is where understanding lives, and it is not written down.

Nothing in this tree works that way. A proof is a term the kernel typechecks, so
no step may be skipped and none may be asserted. The consequence is the shape
the numbers describe:

- **17.4 million lines for an argument a paper might state in fifty pages.** The
  elaboration is not verbosity; every skipped inference a paper makes silently
  becomes a lemma here.
- **1,052,596 declarations, of which the human-readable statement is 9.** The
  proof is a dependency graph. A reader who wants the argument must trace a path
  through it, which is why the announcement says the 250,000-page generated
  document is unreadable and presents only the Lean.
- **A median file of 58 lines with a mean of 99.** Work is atomised: one lemma,
  one file, its dependencies imported by full path. That is what makes 175,187
  files navigable at all, and it is also why no single file explains anything.

The honest summary: **a formal proof is checkable and unreadable; a paper proof
is readable and uncheckable.** This archive contains only the first kind, and
its author says so.

---

## Why it is arranged this way

**Three layers, one direction of authority.** `Archive/` holds bytes that must
never change, `Source/` holds the same content unpacked for use, and
`Documentation/` describes both without ever being their source. Where they
disagree, `Archive/` wins, and `Manifest.sha256` is how a disagreement is
settled.

**The published split is kept, not discarded.** The assembled `lean.tar.gz` is
convenient, but it is derived: the parts are what was actually served, and
keeping them means the distribution can be re-checked rather than taken on
faith.

**The extracted project keeps its own casing.** It sits at `Source/Lean/` while
the archive's root directory is `lean/`. That difference is deliberate and
inert: `lakefile.toml` declares `name = "tree"` and `srcDir = "src"`, both
relative and neither referring to the containing directory, so the outer name
can be recased without touching a single project file. Verification was run
before the recasing, while the directory still carried its published name, and
the recipe for repeating it is in `Archive.md`.

**Only build output is excluded from git.** The PDF, the fourteen parts, the
manifest, the whole extracted tree and this documentation are all tracked. Two
paths are not: `Archive/Distribution/lean.tar.gz`, because it exceeds GitHub's
per-file limit and is one command away from the parts, and `Source/Lean/.lake/`,
because it is what `lake build` writes. The Lean sources themselves are tracked
deliberately - they are the artifact a reader actually opens and diffs, which a
tarball is not.

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

The build needs the toolchain pinned in `lean-toolchain`
(`leanprover/lean4:v4.33.1`), mathlib at the rev named in `lake-manifest.json`,
and patience: 175,187 source files, 70% of the lines in one library, with
heartbeats raised fortyfold. Details in `Documentation/Reference/Project.md`.

The parts are stored in Git LFS, so `git lfs install` is a prerequisite before a
clone can rebuild the archive.

---

## How these numbers were taken

One pass over every `.lean` file, reading bytes and counting:

- **Lines** - newline count, plus one when a file does not end in a newline.
- **Declarations** - a keyword at column zero, optionally preceded by an
  attribute (`@[...]`) and modifiers (`private`, `protected`, `noncomputable`,
  `partial`, `unsafe`, `nonrec`, `scoped`). An indented declaration inside a
  term is therefore **not** counted, which is a deliberate definition rather
  than a parse.
- **`sorry`** - word boundary, so `sorryAx` is not counted as `sorry`; the two
  are reported separately and both are zero.
- **Imports** - `import` at column zero, split on whitespace, so `import A B`
  counts as two.

Known limits, stated rather than glossed: a `sorry` inside a comment would not
be caught by any textual method; mathlib's own axioms (`propext`, `Quot.sound`,
`Classical.choice`) live outside this tree and are not in these counts; and only
`lake build` plus an axiom audit can settle closure beyond doubt. The mathlib
cache plus a full build is the only honest confirmation.

---

## Standing caveat

The announcement is a claim by its author, published as an announcement and a
formalization rather than as a refereed paper. It states that the argument is
currently extremely long, that it is not readable in its present form, and that
its simplifications have not yet been written. This repository records the
material as published; it does not endorse, verify or assess the mathematics.
