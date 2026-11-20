# Publication

What the announcement says, in its own terms. Every claim on this page is
attributed to the document. Nothing here is an assessment of whether any of it
is true.

The text is stored unchanged at `Archive/Publication/Riemann-Solved.pdf`. It
names no author in its own body; it is served from a personal mathematics
homepage that also hosts the archive it cites.

---

## What it claims

**The result** - the author states that, working with Claude, he has discovered
a proof of the Riemann Hypothesis. He states that the method extends to the
Generalized Riemann Hypothesis, and that he expects it to reach the Extended
Riemann Hypothesis with more time.

**The formalization** - the arguments are stated to be formalized without
assumptions. The fourteen-part archive cited in footnote 1 is that
formalization, and it is the only artifact offered in support.

**What is presented, and what is not** - only the Lean. The author writes that
it would be inappropriate to post "some massive unreadable travesty of slop", so
no prose proof accompanies the announcement. He states that producing a huge
unreadable document from the formalization would be routine, and that in his
view of his own path he has taken a step rather than finished.

**The stated limits of the presentation** - the argument is described as
incredibly long at present, its simplifications as likely immediate but not yet
found, and the author's own mastery of the surrounding mathematics as
incomplete: he says he has little command of automorphic forms on higher-rank
groups, and that parts of the timeline are his paraphrase of a summary rather
than his own understanding.

---

## The one technical claim stated in full

The announcement singles out a single line as sufficient to make the point, and
it is worth recording exactly as given.

- **The lineage** - Stepanov's argument resolving Riemann over function fields
  uses a divisor involving multiplicity. This argument is described as a
  descendant of it.
- **The obstacle** - multiplicity is hard to find over the integers,
  corresponding to something like differentiating whole numbers.
- **The substitution** - the Fourier-analytic ideas of an earlier toy setting
  led to chaining theta lifts, so that the same tricks recur but work in a
  natively automorphic manner, each lift mimicking a square root of
  multiplicity.
- **The consequence** - for the von Mangoldt sum of length _X_, the chain length
  used is stated to be the square root of _X_.

---

## Structure of the document

**The opening** - the claim, the occasion, and the author's history with the
problem, including the admission that his student plans were to spend decades on
it.

**A note on timing** - the announcement landed on a Sunday night against an
existing constraint on announcing, which the author addresses directly and
defends against a cynical reading.

**Acknowledgements** - a long list, described as an incomplete one, with a
proper writeup promised.

**A dated timeline** - twenty steps from 10/6/26 to 11/16/26, offered as a rough
sequence after the author was advised to get to the point. Dates are written
month/day/26.

**Seven footnotes**, carrying the archive URLs, the page count of the generated
book, the sum formula behind one of the steps, and several asides.

---

## The timeline

The twenty steps, in the order given, with the mathematics in the original
typeset form rather than in the flattened text of the PDF. Subscripts,
superscripts and symbols do not survive text extraction, so each entry here
records the step's subject and its role rather than reproducing the formula.

1. **10/6/26** - Stepanov determinant.
2. **10/9/26** - a divisor vanishing on a CM curve for a prime inert in the base
   field, with the invariant derivation, and divisibility of the period lattice
   by a prime power.
3. **10/19/26 onward** - the identity relating the norm, the multiplicity count
   and a remainder term; wanting automorphy of the norm since the measure is
   automorphic from a theta on a sixfold cover of GL5 as a period integral of
   thetas; the quadric read on the corresponding CM field; the Poincaré bundle
   placed on the edges to obtain the thetas.
4. **10/6/26 onward** - the positivity of a weighted sum via a determinant, read
   again as Stepanov with multiplicity one; the author's own word for what
   follows is "bootstrap".
5. **10/20/26** - the definitive switch to the von Mangoldt sum, with
   Guinand-Weil supplying the sign and a variance test-function trick making it
   look trace-formula-like.
6. **10/8/26** - the two-interval inequality giving a bound above 1 minus eta.
7. **10/14/26** - determinants containing the desired periods, GGP periods, with
   values 0 and 1 meaning interlacing weights, or up to m non-interlacing ones.
8. **11/15/26** - iterated theta lifts between totally definite unitary groups,
   the representation mapped through successive theta lifts, winning
   multiplicity m; then taking m of order the square root of X.
9. **11/15/26** - norms of the lifts, the level, and cancellation of order-m
   terms with divisibility proven through Chowla-Selberg, Weyl and the Siegel
   mass formula.
10. **11/15/26** - a sufficient lower bound on the divisibility of the m-fold
    iterated lift.
11. **10/6/26** - an Iwasawa tower built by analogy with pigeonhole over finite
    field extensions.
12. **11/15/26** - the seesaw: the period of the iterated lift is a Bessel
    period independent of the Hecke characters, after Rallis.
13. **10/6/26** - the Bost slope inequality.
14. **11/15/26** - the precise "cost" of each lift, showing that one would stop
    at two thirds a priori; the attempt to obtain a main term and transfer the
    constant to a function field, or kill it by twisting; the need for
    "division".
15. **11/15/26** - gluing an integral structure across Hecke characters to
    obtain a "gcd", that is extra averaging.
16. **10/14/26** - a relative trace formula, seen in a different half-plane
    argument through sixfold-cover GL5 automorphy of the measure, reduced by
    Cauchy-Schwarz to a bound on the norm of a suitably projected Poincaré
    series, with approximate orthogonality of the columns of the integral
    structure.
17. **11/15/26** - for the classes that could not be killed by twisting, a
    significant weakening of Vandiver.
18. **11/15/26** - covolumes, the theta series' index, and congruences between
    lifts and forms.
19. **10/19/26** - the precise choice of the Iwasawa tower, specifically using
    Behrend.
20. **11/16/26** - GRH.

The dates are not monotone and the list is not presented as a chronology of
discovery. Several entries are marked with the same day because that is when the
author's summary placed them, and step 19 is dated earlier than steps 8 through
18 that precede it.

---

## The footnotes

**Footnote 1** - the fourteen archive URLs, `https://alpo.ge/lean.tar.gz.part01`
through `.part14`. This is the entire citation apparatus for the formalization.

**Footnote 2** - the page count. The author states he amused himself and "hit
250,000+ pages", and that Claude called it the GRH "book". He reports that
Theorem 1 of it began by noting that because the reals are totally ordered, a
real different from one half is either greater or less than it.

**Footnote 3** - the sum formula behind the left-hand side of one of the steps,
summed over the auxiliary variable first.

**Footnote 4** - an admission that the parts where the author's vague intuition
worked out through Claude's technical mastery are less familiar to him, that the
parts where Claude was the expert are paraphrases of a summary that might make
zero sense, and that the Lean is the thing that will clarify everything.

**Footnote 5** - a note on lossy compression in the timeline, and on the
difficulty of fighting for an F1-style approach.

**Footnote 6** - attached to the weakening of Vandiver: the author believes the
vanishing of a number of K-groups of the integers follows, and cyclicity up to
about 100 maybe, and says he had Lichtenbaum in mind so he knew there would be
slack.

**Footnote 7** - attached to the choice of Iwasawa tower: the author says this
is the sort of trick that to him is obviously going to be unnecessary.

---

## What the document does not do

**It does not present a proof in prose.** The Lean is the proof, by the
document's own account, and the reader is expected to take it or check it.

**It does not present the generated book.** The 250,000-page document is
described, counted, and withheld.

**It does not claim the Extended Riemann Hypothesis.** That is stated as an
expectation for later work, not as a result.

**It is not refereed.** It is an announcement with a formalization attached,
published ahead of any journal process, and the author says so plainly when
explaining the timing.

---

## On this transcription

Text extraction from the PDF flattens every typeset formula: subscripts and
superscripts become inline digits, fractions and radicals lose their structure,
and symbols are approximated. Where the mathematics matters, the PDF at
`Archive/Publication/Riemann-Solved.pdf` is the authority and this page is not.
The quotes above are reproduced because they are words rather than formulas, and
words survive extraction intact.
