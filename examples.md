# Examples

## Raycasting against AABBs

Useful for mouse picking or simple projectile physics.

```carp
(use Geometry)

(let [box (AABB.init (Vector3.init -1.0 -1.0 -1.0) (Vector3.init 1.0 1.0 1.0))
      ray (Ray.init (Vector3.init 0.0 0.0 -10.0) (Vector3.init 0.0 0.0 1.0))]
  (if (Ray.intersect-aabb? &ray &box)
    (IO.println "Ray hit the box")
    (IO.println "Ray missed")))
```

## Sphere-AABB Collision

Standard for character controllers or item pickups.

```carp
(let [player (Sphere.init (Vector3.init 0.5 0.5 0.0) 0.5)
      wall (AABB.init (Vector3.init 1.0 0.0 0.0) (Vector3.init 2.0 1.0 1.0))]
  (if (Sphere.intersect-aabb? &player &wall)
    (IO.println "Player is touching the wall")
    (IO.println "Clear path")))
```

## Plane Math

Projecting a point onto a plane (useful for shadows or sliding physics).

```carp
(let [ground (Plane.from-point-normal (Vector3.init 0.0 0.0 0.0) (Vector3.init 0.0 1.0 0.0))
      p (Vector3.init 10.0 5.0 10.0)
      proj (Plane.project-point &ground &p)]
  (IO.println &(format "Projected point: %s" &(Vector3.str &proj))))
```
