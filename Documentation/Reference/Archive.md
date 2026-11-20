# Archive

Provenance of the archived bytes, how they were split, how to put them back
together, and what was checked.

---

## Provenance

**The announcement** was supplied locally and is stored unchanged at
`Archive/Publication/Riemann-Solved.pdf`, 245,114 bytes. Its only citation for
the formalization is a footnote naming fourteen URLs,
`https://alpo.ge/lean.tar.gz.part01` through
`https://alpo.ge/lean.tar.gz.part14`.

**The archive** was retrieved from those fourteen URLs. They are the complete
resource set: the announcement cites nothing else, and the site they are served
from does not link them, so the footnote is the only route to them.

**Nothing else was pulled.** The same host carries the author's other papers and
a CV; none of it is referenced by this document, so none of it is here.

---

## How the archive was split

The distribution is a plain byte split, not a multi-volume archive with headers
of its own.

- **Parts 01 through 13** are each exactly 18,000,000 bytes.
- **Part 14** carries the remainder, 5,275,554 bytes.
- **Total**, 13 x 18,000,000 + 5,275,554 = 239,275,554 bytes.

Each part answers HTTP 200. The server sends no `Content-Length` (the responses
are chunked), so the sizes above are measured on disk rather than declared by
the origin, and the assembled total is the only authority on the original size.

The two-digit zero padding in `part01` is load-bearing: it makes a shell glob
sort the parts correctly. Renaming them breaks reassembly silently, producing a
corrupt archive rather than an error.

---

## Layout

- **`Publication/Riemann-Solved.pdf`** - the announcement.
- **`Distribution/lean.tar.gz`** - the assembled archive, 239,275,554 bytes.
- **`Distribution/Part/lean.tar.gz.part01` ... `part14`** - the distribution as
  served.
- **`Manifest.sha256`** - checksums of everything above, paths relative to
  `Archive/`.

---

## In git

**The fourteen parts are stored in Git LFS.** `.gitattributes` routes
`Archive/Distribution/Part/lean.tar.gz.part*` through the LFS filter, so a clone
carries fourteen pointers of about 130 bytes each rather than 234 MB of binary
chunks. The content lives in `.git/lfs/objects` and is materialised on checkout.
Without the LFS client a checkout still succeeds, but the parts arrive as
pointer text and reassembly produces a corrupt archive rather than an error, so
`git lfs install` is a prerequisite for anyone rebuilding from the parts.

**The assembled archive is not tracked.** It is derived by concatenation, and at
239 MB it would double the repository's binary weight for a file that one `cat`
rebuilds.

**The PDF is an ordinary blob.** At 245 KB, LFS would impose a client dependency
on the one file most readers open, for no benefit.

**Line endings are normalised to LF.** `* text=auto eol=lf` in `.gitattributes`
applies to the extracted tree as well, so a checkout on any platform yields
files byte-identical to the archive and to `Manifest.sha256`.

---

## Reassembly

From `Archive/Distribution`:

```
cat Part/lean.tar.gz.part* > lean.tar.gz
gzip -t lean.tar.gz
```

`lean.tar.gz` is ignored by git because it exceeds the per-file limit on the
hosting side; the parts are not, so a clone can always rebuild it.

---

## Verification record

Each check below was run against the files now in this repository.

- **The parts are one valid gzip stream.** Concatenating them and piping through
  `gzip -t` exits 0. A single truncated or reordered part fails this.
- **The assembled archive is one valid tar.** A full `tar -tzf` walk completes,
  listing 175,190 entries.
- **The assembled archive is reproducible.** `shasum -a 256` over the
  concatenated parts and over the assembled file give the same digest,
  `9631b4f020199e580ba86178cb56c6e9b09f690c2369a80dc4334aa93f49c7fc`.
- **The extraction is faithful.** After `tar -xzf lean.tar.gz -C Source`,
  running `tar -dzf lean.tar.gz -C Source` reports no differences. This compares
  every member's content, mode, size and timestamp against the filesystem, so it
  is a byte-level check of all 175,190 files rather than a count.
- **The recasing moved no content.** The extracted directory was renamed from
  `lean` to `Lean` only after the check above passed. To repeat the check now,
  extract to a scratch directory and compare:
  `tar -xzf Archive/Distribution/lean.tar.gz -C /tmp/riemann-check && diff -r /tmp/riemann-check/lean Source/Lean`.
- **The manifest matches.** `shasum -a 256 -c Manifest.sha256`, run from
  `Archive/`, reports OK for every listed file.

---

## What the archive does not contain

**No directory entries.** The tarball holds 175,190 regular files and no
directory members, so the extraction reproduces the project's files but not any
empty directory the original project may have had. Nothing in a Lake project
depends on an empty directory, so this is inert here, but it does mean the
archive is not a full filesystem image.

**No build output.** No `.lake`, no oleans, no dependency checkouts. The project
is source only.

**No mathlib.** Dependencies are named in `lake-manifest.json` by git revision
and fetched at build time; they are not vendored.

**No second copy of the argument.** The announcement mentions a 250,000-page
"book" generated from the formalization. It is not part of the distribution and
is not here.
