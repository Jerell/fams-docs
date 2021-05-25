---
sidebar_position: 2
---

# Pipe

Pipes are connections between nodes.

A pipe's `in pressure` and `mass flow rate` are determined by its `source node`.

## Properties

| Property       | Unit                | Default      | Notes                                                                                  |
| -------------- | ------------------- | ------------ | -------------------------------------------------------------------------------------- |
| `name`         | -                   | pipe         |                                                                                        |
| `length`       | m                   | 200          |                                                                                        |
| `diameter`     | m                   | 2            |                                                                                        |
| `massFlow`     | kg/s                | 0            |                                                                                        |
| `pressure.in`  | Pa                  | 0            |                                                                                        |
| `pressure.out` | Pa                  | 0            |                                                                                        |
| `source`       | -                   | new `Node()` | Must be a `Node` object                                                                |
| `destination`  | -                   | new `Node()` | Must be a `Node` object                                                                |
| `direction`    | `boolean` \| `null` | `null`       | `true` if `pressure.in` > `pressure.out`<br/>`false` if `pressure.out` > `pressure.in` |

The `Pipe()` constructor accepts an `x` input, which sets the x position of its source node.

## Pressure drop

A pipe's `out pressure` is calculated based on its physical properties and the properties of the fluid. This is used to set the pressure at the destination node.

```js {5,10}
pressureDrop(): number {
  const P1 = this.pressure.in
  const viscosity = 1 // fluid property
  const L = this.length
  const Q = 1 // volumetric flow rate
  const A = 0.25 * Math.PI * this.diameter ** 2
  const d = this.diameter * 1000 // mm
  const z = this.destination.elevation - this.source.elevation
  const g = 9.81
  const density = 1

  return P1 - (32000 * (viscosity * L * Q)) / (A * d ** 2) - z * g * density
}
```

:::danger Incomplete

I imagine the volumetric flow rate shoule be calculated but I need more information to do that. I don't know what the fluid density is or where I'll be able to pull that from.

Also it isn't clear what the 32000 is or if that'll need to be replaced with another calculated value.

:::