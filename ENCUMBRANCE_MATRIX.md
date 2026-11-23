# The Encumbrance Matrix

*Companion document — Human Layer applied. See [HUMAN_LAYER.md](HUMAN_LAYER.md) and [LAYER_NEG1.md](LAYER_NEG1.md); Bitcoin application in [UNENCUMBERED_BITCOIN.md](UNENCUMBERED_BITCOIN.md).*

## Background

Layer −1 gives a generic process for handling any allocation problem: measure what you have, see the constraint, choose, live with the result, review daily, repeat. It doesn't tell you *what* to point that process at — it's domain-agnostic on purpose.

The Encumbrance Matrix is the first concrete domain the process gets pointed at: the fixed set of forces that hold a claim on an adult's time, money, or decisions. An encumbrance is anything that isn't fully your own choice — a person, institution, or condition with power over you or a hold you can't simply walk away from.

The starting observation was that these forces sort along two independent axes:

- **Coercion vs. scarcity** — coercion means a specific entity with its own will has power over you: it can compel you, grant you permission, or withdraw something you need. Scarcity means no one is imposing anything — a resource (time, money) is simply finite, and its finiteness constrains you regardless of anyone's intent.
- **Systemic vs. individual** — systemic means the constraint comes from a structure with no alternate counterparty (you can't escape the tax system by picking a different taxman). Individual means it's a specific relationship — this landlord, this employer — that could in principle be renegotiated, ended, or replaced.

Plotting encumbrances on these two axes produces a quadrant, and placing each one by how hard it is to become free of it (distance from center) turns the quadrant into a working map rather than just a classification.

A handful of encumbrances don't sit cleanly on one axis — a credit card company has a will (coercion) but the lever it pulls is engineered scarcity of money through compounding debt. These are kept as an explicit third, hybrid category rather than forced onto one side, since the blend is real and worth seeing.

The board that resulted has 13 near-universal encumbrances — taxman, immigration/citizenship, regulatory/licensing, boss, landlord, spouse/partner with legal claim, credit card companies, bank, insurance requirements, inflation, doctor, family/social obligation, internet/utility providers — close to the same set for anyone operating inside a modern economy.

A separate, adjacent list holds personal **resources** rather than encumbrances: clock (time), calendar (your own commitments), health/energy, knowledge/skills, and physical assets (land and buildings held outright). These aren't plotted on the board — they're the capacity you spend moving encumbrance dots inward, and the thing a resource like land or savings ultimately buys you out of a dependency like landlord or bank.

## The personal overlay

The 13-dot board is universal and fixed — same reference structure for everyone. What's individual is where a given person actually sits on it: age, health, family situation, and stage of life all shift the same dots inward or outward, and can add entirely new dots that aren't on the universal board at all (a custody arrangement, a business partner, a specific health condition).

This split gives the tool two layers:

1. **The universal board** — teachable once, comparable across people, doesn't change.
2. **The personal overlay** — where the Layer −1 loop actually runs. "Measure what you have" becomes plotting your own coordinates; "see the constraint" is reading the dot positions; "choose" is deciding which dot this period's allocation goes toward; "review daily" (or periodically) is re-plotting the overlay and comparing it to the last snapshot.

## The tool

[`tools/encumbrance_matrix.html`](tools/encumbrance_matrix.html) is a self-contained, offline-capable webapp implementing the board and overlay as one interactive artifact rather than two separate steps:

- The 13 universal dots are fixed and solid — reference only, not editable.
- Personal dots are added via **+ Add dot** (click the board, label it, assign it to one of the four categories) and rendered as outlined circles so they're visually distinct from the universal set.
- Personal dots can be dragged to reposition, selected with a click, and removed (via **Remove selected** or double-click).
- A note field lets each snapshot carry a short annotation (e.g. *"Q1 2027 — landlord dot moved in, bank dot moved out"*).
- **Save as PNG** rasterizes the board plus the dated note into a single downloadable image — the snapshot artifact.

There is currently no persistence between sessions — each visit starts from the universal board with no overlay dots, and the PNG export is the only record of a given state. Adding stored history (so snapshots accumulate into a visible trend rather than living only as separate exported images) is the identified next step, deferred deliberately rather than an oversight.

## How this fits Human Layer

Human Layer names the mantra; the Encumbrance Matrix is the first instrument built to run it against a specific, named domain rather than time-allocation in the abstract. The relationship is roughly:

- **Layer −1** — the generic process (measure, see, choose, live with it, review, repeat).
- **Layer 0** — the universal Encumbrance Matrix: the fixed reference structure the process gets applied to.
- **Layer 1** — the personal overlay: an individual actually running the Layer −1 loop against their own coordinates on the Layer 0 board.

There is no win condition in the sense of a cleared board — taxman and inflation, in particular, are permanent fixtures, not removable dots. The tool is closer to a periodic health check than a game: an **Unencumbered Score** isn't a final grade, it's a vital sign, expected to be re-measured on a cadence and read for direction of travel rather than completion. Every move against a dot draws on the same finite pool Layer −1 already names — man-hours and energy — so a period where nothing moved but nothing slid backward either counts as maintenance, not failure. Encumbrance reduction is a maintained state, not a one-time unlock: debt regenerates, skills atrophy, dependency relationships quietly re-tighten if left unattended.
