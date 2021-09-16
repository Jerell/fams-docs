---
sidebar_position: 1
---

# Inlet

The `Inlet` class sets fluid properties at the start of the pipe network and searches for an inlet pressure that satisfies the downstream components.

| Property      | Unit       | Default | Notes                          |
| ------------- | ---------- | ------- | ------------------------------ |
| `name`        | -          | -       | Required                       |
| `elevation`   | m          | -       | Required as part of `physical` |
| `fluid`       | `Fluid`    | null    |                                |
| `destination` | `IElement` | null    |                                |

## async `applyInletProperties()`

| Parameter   | Description                |
| ----------- | -------------------------- |
| pressure    | `Pressure`                 |
| temperature | `Temperature`              |
| flowrate    | `Flowrate`                 |
| skipProcess | boolean (default: `false`) |

Creates a new `Fluid` object with the specified pressure, temperature and flowrate.

If skipProcess is true, `Inlet.process` will not be called.

## async `searchInletPressure()`

Performs a binary search to find a fluid pressure value that satisfies downstream components.

Search range: 1 bara - 140 bara

## `setDestination()`

Sets an `IElement` component as the destination of this component.

## async `process()`

Passes fluid to the destination component.

Returns the status (pressure high/low/ok) of downstream components.
