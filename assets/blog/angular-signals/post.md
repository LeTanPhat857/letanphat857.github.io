---
title: Getting Started with Angular Signals
slug: angular-signals
date: 2026-06-10
author: Phat Le Tan
tags:
  - angular
  - signals
  - frontend
---

# Getting Started with Angular Signals

Signals are Angular's reactive primitive. A signal is a value that notifies
consumers when it changes.

## Writable signals

```typescript
const count = signal(0);
count.set(1);
count.update(n => n + 1);
```

Read a signal by calling it: `count()`.

## Computed signals

`computed()` derives a value from other signals and re-evaluates lazily:

```typescript
const doubled = computed(() => count() * 2);
```

## Why it matters

Signals make change detection precise — Angular updates only what actually
depends on a changed value. Combined with zoneless change detection, that means
less work per render and simpler mental model than `Zone.js` change detection.
