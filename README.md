# Geometry Module (Carp)

A lightweight, deterministic collision and intersection library for 3D geometry.  
Supports both **query-based intersection tests** and **contact-based collision resolution**.

---

## Overview

This module provides:

### Ray Queries (non-penetrating)
Used for:
- visibility tests
- picking / selection
- raycasting
- bullet tracing

Returns: `RayHit`

---

### Contact Collisions (penetration-based)
Used for:
- physics resolution
- overlap correction
- broad-phase interaction responses

Returns: `Contact`

---

## Core Types

### Primitives
- `Sphere`
- `AABB`
- `Plane`
- `Segment`
- `Ray`

### Outputs
- `RayHit`
- `Contact`

---

## Coordinate Conventions

### RayHit
- `t` = distance along ray
- `point` = world-space hit position
- `normal` = outward-facing surface normal

### Contact
- `depth` = penetration depth
- `point` = approximate contact point
- `normal` = separation direction (toward second object in most operations)

---

## Key Rules

- All `Ray.direction` and `Plane.normal` vectors are always normalized.
- Segment operations internally use ray casting with clamped distance.
- Degenerate cases (zero-length vectors, overlapping centers) use stable fallback axes.
- EPSILON is used for numerical stability.

---

## Modules

### Geometry

Entry utilities:
- `create-ray`
- `create-plane`

---

### Geometry.Ray

- `at(ray, t)`
- `intersect-sphere(ray, sphere) -> Maybe RayHit`
- `intersect-aabb(ray, aabb) -> Maybe RayHit`

---

### Geometry.Sphere

- `collide-sphere(s1, s2) -> Maybe Contact`
- `collide-aabb(sphere, aabb) -> Maybe Contact`
- `contains?(sphere, point)`

---

### Geometry.AABB

- `collide-aabb(a, b) -> Maybe Contact`
- `contains?(aabb, point)`

---

### Geometry.Plane

- `distance-to-point(plane, p)`
- `project-point(plane, p)`

---

### Geometry.Segment

- `length(segment)`
- `direction(segment)`
- `intersect-sphere(segment, sphere)`
- `intersect-aabb(segment, aabb)`

---

## Design Philosophy

This library prioritizes:

- Determinism (no randomness, no frame dependence)
- Numerical stability over geometric perfection
- Simple primitives over complex manifolds
- Fast rejection before expensive computation
- Clear separation between:
  - intersection queries (`RayHit`)
  - collision resolution (`Contact`)

---

## Performance Notes

- AABB ray tests use slab method (O(1))
- Sphere tests use quadratic solve (O(1))
- Segment tests are ray-reduced (no extra math cost)
- No allocations beyond `Maybe` result construction

---

## Limitations

- No continuous collision manifold generation
- No mesh or triangle support
- No rotational physics (AABB only)
- Contact points are approximations for simplicity

---

## Typical Use Case

- Game physics core
- Simple collision systems
- Ray-based weapon systems
- Spatial queries and triggers
