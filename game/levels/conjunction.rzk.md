---
id: conjunction
title: Conjunction
statement: Bool
checks:
- and true true = true
- and true false = false
moves: obscure
---

Now a function of two booleans: `and a b` is `true` exactly when both are. Case-split on `a` with `match`: if `a` is `false` the answer is `false`, and if `a` is `true` the answer is `b`.

This puzzle shows the second way to write behaviour checks. Two rows of the truth table, `and true true = true` and `and true false = false`, are closed one-liners, so they sit in the `checks:` front-matter. But the `false` row holds for *every* `b` — `and false b` is `false` whatever `b` is — a check that quantifies over the level's parameter. That one goes in a `rzk postcheck` block below, where it is written as an ordinary `#def` with `b` in scope, the natural way. A `-- label:` comment gives it the plain-English summary shown if it fails. The two forms are equivalent and combine freely; a block `#def` is checked independently, so a helper it needs belongs in the prelude.

The level sets `moves: obscure`. The Moves panel does not hand over the steps; it reports how many fit and offers a *Reveal* button, so the player is asked to find each move before being shown it.

```rzk prelude
#lang rzk-1
#data Bool := false | true
```

```rzk template
#def and (a b : Bool)
  : Bool
  := ?
```

```rzk solution
#def and (a b : Bool)
  : Bool
  := match a
       ( false ⇒ false
       | true ⇒ b)
```

```rzk postcheck
-- label: false on the left annihilates
#def and-false-left (b : Bool)
  : and false b = false
  := refl
```

## Conclusion

Three checks pin `and`: two closed rows in the front-matter, and the parametrised `false` row in the postcheck block. A wrong-but-well-typed answer — a constant, or one that returns `a` — trips at least one of them.
