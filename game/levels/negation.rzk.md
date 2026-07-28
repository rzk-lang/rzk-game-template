---
id: negation
title: Negation
statement: Bool → Bool
checks:
- not true = false
- not false = true
autohide-single-move: true
---

Negate a boolean: send `false` to `true` and `true` to `false`. The prelude declares `Bool` with `#data`, so `match` takes a boolean apart, and both compute definitionally.

The goal type `Bool → Bool` does not pin the answer — the constant `\ _ → false` has that type too. So this level carries two `checks:`, `not true = false` and `not false = true`, that the finished proof must satisfy. Each is a bare string, proved by `refl`; because `#data` computation is definitional, `refl` holds exactly when `not` really computes the boolean, so the constant is rejected with a "so close" notice. A truth-table `checks:` is the honest way to author a puzzle whose type is looser than its intent.

This level also sets `autohide-single-move: true`. The first step is forced — the only move is to introduce the coordinate, `\ b → ?` — so the panel obscures it behind a nudge instead of handing it over. Once `b : Bool` is in context the hole offers a `match b` move, and, with more than one move on offer, the panel is shown as usual.

```rzk prelude
#lang rzk-1
#data Bool := false | true
```

```rzk template
#def not
  : Bool → Bool
  := ?
```

```rzk solution
#def not
  : Bool → Bool
  := \ b → match b
       ( false ⇒ true
       | true ⇒ false)
```

## Conclusion

The goal type asked for any function `Bool → Bool`; the checks asked for the *right* one. `refl` decides each case because `match` on a constructor reduces on the spot.
