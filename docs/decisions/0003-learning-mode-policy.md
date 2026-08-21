# Decision 0003: Learning Mode Policy

Status: Accepted
Date: 2026-08-21

## Context

The project must increase the learner's reasoning ability rather than merely maximize AI implementation speed.

## Decision

New concepts begin in Learn Mode with default hint level H1. The learner produces the first model/hypothesis and, when implementation begins, the first production attempt unless they explicitly request a higher hint level or full solution. Pair Mode follows demonstrated understanding; Execute Mode is reserved for explicitly delegated low-learning-value mechanical work.

## Consequences

Passing tests does not automatically mean the learner understands a concept. Prediction, counterexamples, debugging, and explain-back are first-class learning evidence. Premature full solutions or silent assumption selection are harness failures.
