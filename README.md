# PRIMORDIUM

**A self-contained artificial-life simulation. Watch evolution happen, live, in your browser.**

**[▶ Live Demo](https://switchfire6.github.io/primordium/)**

No build step, no dependencies, no server. One HTML file. Open it and life begins.

```
open primordium/index.html      # macOS
xdg-open primordium/index.html  # Linux
# …or just double-click the file
```

---

## What it is

A few hundred organisms drift through a wrap-around primordial soup. Each carries a **genome**:

- **body traits** — size, top speed, sense range, and *diet* (how carnivorous it is)
- a tiny **neural-network brain** (10 → 10 → 2, tanh) wired from random weights

Every tick, a creature's brain reads its world — the direction and nearness of the closest food and the closest other creature, its own hunger, an internal oscillator — and decides how to **turn** and how hard to **swim**. Nobody is taught anything.

Creatures that find energy and survive long enough **split in two**. The child inherits its parent's genome with small random **mutations** to both the brain weights and the body genes. Creatures that run out of energy vanish. That single loop —

> **eat · reproduce · mutate · die**

— is natural selection, and over a few minutes it quietly rewrites the whole population.

## What to watch for

- **Foraging emerges.** At first most creatures wander blindly. Watch the survivors begin to *steer* toward food — behaviour no one programmed.
- **A food web forms.** Diet is a real trade-off: herbivores digest food efficiently but can't hunt; carnivores hunt well but barely digest plants. So the world settles into small fast **grazers** at the base and larger **predators** on top.
- **Predator–prey waves.** Predators boom, exhaust their prey, crash, and recover — the classic oscillation. The **predator %** readout and the trait chart make the cycles visible.
- **Speciation.** Colour is an inherited lineage marker. The **species spectrum** bar shows which lineages dominate; watch bands appear, split, and go extinct.
- **The trait chart** plots live population averages of size, speed, sense and carnivory, so you can literally see selection pushing the genome around.

## Play with it

| Action | Effect |
|---|---|
| **drag** on the canvas | sow food, feed a region |
| **shift-click** | drop a brand-new random creature — an invasive species |
| **food** slider | trigger booms and famines |
| **mutation** slider | crank up for chaos, down to freeze evolution |
| **speed** slider | up to 8× — pass an hour of evolution in a minute |
| **vision** toggle | see what a sample of creatures are sensing |

**Keys:** `space` pause · `r` new world · `t` trails · `v` vision · `[` `]` speed · `h` / `?` help

## Under the hood

Pure vanilla JS + Canvas 2D, ~750 lines, no libraries.

- Feed-forward neural net with weights in flat typed arrays, so cloning and mutating a genome is trivial.
- A toroidal spatial-hash grid keeps neighbour queries cheap (~2,000 simulation steps/second single-threaded).
- A fixed 1/60 s timestep decoupled from the render loop, so fast-forward stays deterministic.
- Cached additive radial-gradient glow sprites (one per hue) give the bloom look without per-frame gradient cost.

The metabolic costs are deliberately shaped to create **trade-offs** — size is super-linear (giants are expensive) and speed is far dearer for a big body — so evolution must *choose* a strategy instead of maxing every trait. That tension is what keeps the ecosystem diverse and alive rather than collapsing into a monoculture.

---

*Each run is different. Nothing here is scripted — it's just selection, all the way down.*
