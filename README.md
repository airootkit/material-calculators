# SquareFootCalcs

Free material calculators for home and yard projects. Measure the space, get the quantity to buy.

**→ [squarefootcalcs.com](https://squarefootcalcs.com)**

No account, no app, no tracking. Every calculation runs in your browser — nothing you type is
uploaded or stored anywhere.

---

## The calculators

| Calculator | Takes | Gives you |
|---|---|---|
| [Concrete Slab](https://squarefootcalcs.com/tools/concrete-calculator/) | Area + thickness, or post-hole dimensions | Cubic yards, bags by size |
| [Gravel & Crushed Stone](https://squarefootcalcs.com/tools/gravel-calculator/) | Area + depth + material | Cubic yards, tons |
| [Mulch](https://squarefootcalcs.com/tools/mulch-calculator/) | Bed area + depth | Cubic yards, bags, bulk-vs-bagged cost |
| [Topsoil & Garden Soil](https://squarefootcalcs.com/tools/topsoil-calculator/) | Bed area, or raised-bed dimensions | Cubic yards, bags |
| [Sod & Grass Seed](https://squarefootcalcs.com/tools/sod-calculator/) | Lawn area | Rolls, pallets, or pounds of seed |
| [Paint](https://squarefootcalcs.com/tools/paint-calculator/) | Room dimensions + openings + coats | Gallons and quarts |
| [Tile](https://squarefootcalcs.com/tools/tile-calculator/) | Area + layout | Boxes, individual tiles |
| [Deck Board](https://squarefootcalcs.com/tools/deck-calculator/) | Deck dimensions + board + spacing | Boards, joists, screws |
| [Fence](https://squarefootcalcs.com/tools/fence-calculator/) | Run length + spacing + picket size | Posts, rails, pickets, concrete |
| [Roofing Shingle](https://squarefootcalcs.com/tools/roofing-calculator/) | Building footprint + pitch | Squares, bundles |

## What makes these different

Most material calculators give you a number and nothing else. These try to do three things better.

**Show the arithmetic.** Every page has the formula and a worked example underneath the tool, so
you can check the answer against your own measurements and know what to change when the job is not
a plain rectangle.

**Handle real shapes.** An L-shaped patio, a bed that wraps a corner of the house, two rooms in the
same colour — split the area into rectangles and add a section for each. Feet-and-inches can be
typed the way people actually write it: `12' 6"`, `12 ft 6 in` and `12-6` all work. Metric too.

**Produce a shopping list, not a volume.** Bag yields and coverage rates match what is on the
shelf. Results are shareable by URL — the inputs live in the query string, so you can send the link
to whoever is picking up the material — and printable, so you can take the list to the store.

## Where the numbers come from

This is the part that decides whether a calculator is worth using, so it is worth being explicit
about. Every reference figure was checked against a primary source, and three of them turned out to
be wrong in the first draft:

| Figure | Source | Result |
|---|---|---|
| Concrete bag yields (40/50/60/80/90 lb) | QUIKRETE Concrete Mix data sheet no. 1101 | Confirmed |
| Bagged mulch volume, coverage per yard | Retail shelf standard (2 cu ft), 13.5 bags/yd³ | Confirmed |
| Paint coverage per gallon | Behr (250–400 sq ft/coat), Glidden (up to 400 primed) | Confirmed |
| Mulch depth | Penn State & U. Maryland Extension: 2–3 in, max 4 | Confirmed |
| Seeding rates by species | Penn State Extension, *Lawn Establishment*, Table 1 | Adopted |
| Roofing square, bundles per square | GAF, IKO — 100 sq ft, 3 bundles | Confirmed |
| **Door area deducted for paint** | Manufacturer calculators: 20 sq ft | **Corrected** from 21 |
| **Primer coverage** | Manufacturer guidance: 200–300 sq ft/gal | **Corrected** — it is lower than finish paint |
| **Driveway slab thickness** | Industry standard: 4–6 in by vehicle weight | **Corrected** — 4 in is enough for cars |

Roof slope factors are derived from the pitch (`√(rise² + 12²) ÷ 12`) rather than copied from a
table, because published contractor tables sometimes fold a waste allowance into the figure and
then disagree with each other.

Each tool page cites its sources and carries the date the figures were last checked.

## How it is built

The interesting part is the plug-in structure. Adding a calculator is **one directory and three
files** — no framework code changes anywhere:

```
src/tools/<slug>/
├── meta.ts        name, category, keywords, disclaimer, FAQ (emits FAQPage structured data)
├── index.vue      the calculator itself
└── content.mdx    the long-form explanation: how to use it, the formula, reference tables
```

A build-time glob picks up `meta.ts` and `content.mdx`, and validates that the slug matches the
directory name. Each calculator compiles to its own JS chunk, so opening one tool page downloads
only that tool — the home page ships no framework JavaScript at all.

All the unit conversion and rounding lives in one shared module with unit tests. That is
deliberate: a unit-conversion bug is the single failure mode that would quietly waste people's
money, so it is the one part of the codebase that is covered by tests rather than by care.

## Sister site

[theprintablehome.com](https://theprintablehome.com) — the same jobs from the other end. Work out
how much to buy here, print the paperwork there: the quote you hand a client, the punch list you
walk before final payment, the maintenance calendar for the thing you just built.
([source](https://github.com/airootkit/printable-home-checklists))

## What these are not

Estimating tools, not engineering calculations. They will tell you how many bags of concrete a slab
takes. They will not tell you whether the slab is thick enough for what you are putting on it,
whether it needs reinforcement, or whether your local code requires a permit.

For anything structural — footings that carry a building, a deck ledger, a roof — ask someone who
can see your site.

## Corrections

If a bag yield, coverage rate or formula does not match what you found on the product, the figure
here is the one that should change. Open an issue with the brand, the product and the number
printed on the label, or email **hello@squarefootcalcs.com**.
