---
id: allowed
gated: true
inventory:
- 'x        : A'
- 'id-hom   : (A : U) → (x : A) → hom A x x'
statement: hom A x x
title: Only what's allowed
---

The goal is the identity once more, but this level is **gated**. The inventory grants `id-hom` and nothing else. The prelude also defines `shortcut`, another path that would solve the goal — but it is not in your inventory, so reaching for it trips the gate and the success is withheld.

Solve it with the granted move. Then, to see the gate, try `shortcut A x` instead and watch the red notice.

The prelude is split across two blocks, to show that `prelude` fences are concatenated in order. Run `make format-game` from a checkout to tidy them in place.

```rzk prelude
#lang rzk-1
#def Δ¹
  : 2 → TOPE
  := \ t → TOP
#def hom (A : U) (x y : A)
  : U
  := (t : Δ¹) → A [ t ≡ 0₂ ↦ x , t ≡ 1₂ ↦ y ]
```

```rzk prelude
#def id-hom (A : U) (x : A)
  : hom A x x
  := \ t → x
#def shortcut (A : U) (x : A)
  : hom A x x
  := \ t → x
```

```rzk template
#def allowed (A : U) (x : A)
  : hom A x x
  := ?
```

```rzk solution
#def allowed (A : U) (x : A)
  : hom A x x
  := id-hom A x
```

## Conclusion

The gate keeps a puzzle honest. Only the granted moves count, so a level about building a thing by hand cannot be cleared by a shortcut. The scan looks only at proof bodies, so the type formers in the goal are never flagged.
