# carp-geometry

A mathematically rigorous real-time geometry library for the [Carp](https://github.com/carp-lang/Carp) programming language.

## Features

- **Spatial Primitives**: `Ray`, `Sphere`, `AABB`, and `Plane`.
- **Intersection Tests**: Optimized checks for Sphere-Sphere, AABB-AABB, Ray-Sphere, Ray-AABB, and Sphere-AABB.
- **Point Queries**: `contains?` for volumes and `distance-to-point` / `project-point` for planes.
- **Zero Allocations**: Designed for performance in real-time loops.

## Usage

```carp
(load "carp-geometry/geometry.carp")
(use Geometry)

(defn main []
  (let [sphere (Sphere.init (Vector3.init 0.0 0.0 0.0) 1.0)
        ray (Ray.init (Vector3.init -5.0 0.0 0.0) (Vector3.init 1.0 0.0 0.0))]
    (if (Ray.intersect-sphere? &ray &sphere)
      (IO.println "Hit!")
      (IO.println "Miss!"))))
```

## Testing

Run the test suite with:

```bash
carp -x test/geometry_test.carp
```

## License

MIT
