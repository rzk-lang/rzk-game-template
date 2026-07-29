---
id: data-and-checks
title: Data and behaviour
role: bridge-in
---

So far the puzzles have lived over the directed interval. This chapter switches substrate to plain inductive data, to show two authoring features that come with it.

The first is **inductive types**. A prelude declares one with `#data`, for example `#data Bool := false | true`, and the engine generates its induction and recursion principles. A proof takes a value apart with a `match` expression, and both compute definitionally. In a hole, a hypothesis of a `#data` type offers a `match` over it as a tap-to-fill move, so the player can case-split by tapping.

The second is **behaviour checks**. A goal type does not always pin the answer: `not : Bool → Bool` is inhabited by the constant `\ _ → false`, which is well-typed but wrong. A level states what the solution must actually *compute* with checks, verified once the proof is otherwise complete. There are two ways to write them, shown in the next two puzzles: closed one-liners in the `checks:` front-matter, and a `rzk postcheck` block for a check that quantifies over the level's parameters.

The two puzzles also show the **Moves panel** controls. `moves: on | obscure | off` sets how much the tap-to-fill panel gives away — `obscure` hides the moves behind a "find it, or reveal" nudge, `off` hides the panel entirely — and `autohide-single-move` obscures a hole only when exactly one move applies. A separate "⌨ typing" badge is added automatically to any level that cannot be solved by taps alone; the `requires-typing` field overrides that judgement when you need to.
