---
sidebar_position: 3
---

# PipeSeg

The `PipeSeg` class is for transporting `Fluid`s between components. The properties of the incoming fluid are used in a calculation with the properties of the pipe segment to determine the outgoing fluid pressure.

| Property             | Unit       | Default | Notes                         |
| -------------------- | ---------- | ------- | ----------------------------- |
| `name`               | -          | -       | Required as part of `pipeDef` |
| `physical.elevation` | m          | -       | Required as part of `pipeDef` |
| `physical.length`    | m          | -       | Required as part of `pipeDef` |
| `physical.diameters` | m`[]`      | -       | Required as part of `pipeDef` |
| `fluid`              | `Fluid`    | null    |                               |
| `source`             | `IElement` | null    |                               |
| `destination`        | `IElement` | null    |                               |

`pipeDef` is a constructor parameter.

## get `effectiveArea`

Returns the effective cross sectional area of the pipe segment.

A pipe can have several 'lines,' each with their own diameter. The sum of the cross sectional areas is used in pressure drop calculations.

## `removeLine()`

| Parameter | Description |
| --------- | ----------- |
| size      | number      |

Removes the first occurrence of `size` from `this.physical.diameters`.

## `addLine()`

| Parameter | Description |
| --------- | ----------- |
| size      | number      |

Appends `size` to `this.physical.diameters`

## `setDestination()`

Sets an `IElement` component as the destination of this component.

## get `height`

Returns the difference between `this.destination.elevation` and `this.elevation`.

A pipe segment going uphill will have a positive height.

## `endPressure()`

Returns the pressure of the fluid at the end of the pipe segment, based on changes due to friction and elevation.

Return value is capped: 0 - 135 bar

## async `process()`

Creates a new `Fluid` object with the same temperature and flowrate as the incoming `Fluid` but with pressure equal to `this.endPressure()`.

If the new fluid pressure is below 1000 Pa, returns `PressureSolution.Low`.

Passes fluid to the destination component.

Returns the status (pressure high/low/ok) of downstream components.
