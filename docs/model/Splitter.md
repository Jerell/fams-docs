---
sidebar_position: 4
---

# Splitter

Takes a single `Fluid` and distributes its flow beterrn multiple destination branches. The preceding `PipeSeg` passes a `Fluid` object with a fixed flowrate to a `Splitter`, which performs a binary search for each destination branch to find a flowrate that satisfies the terminal nodes.

| Property             | Unit         | Default | Notes                          |
| -------------------- | ------------ | ------- | ------------------------------ |
| `name`               | -            | -       | Required                       |
| `physical.elevation` | m            | -       | Required as part of `physical` |
| `source`             | `PipeSeg`    | null    |                                |
| `destinations`       | `IElement[]` | null    |                                |

`physical` is a constructor parameter.

## `addDestination()`

| Parameter | Description |
| --------- | ----------- |
| dest      | `IElement`  |

Adds an `IElement` component as a destination of this component.  
The elevation of the destination must match the elevation of the splitter.

## `setDestinations()`

| Parameter    | Description  |
| ------------ | ------------ |
| destinations | `IElement[]` |

Adds each `IElement` component as a destination of this component.  
The elevation of the destinations must match the elevation of the splitter.

## async `applyFlowrate()`

| Parameter | Description |
| --------- | ----------- |
| branch    | number      |
| flowrate  | `Flowrate`  |

Creates a new `Fluid` object with the specified flowrate to pass to the branch. Passes the fluid to `this.destinations[branch]` and processes the outcome.

Returns the status (pressure high/low/ok) of downstream components.

## async `searchBranchFlowrate()`

| Parameter | Description |
| --------- | ----------- |
| branch    | number      |
| fluid     | `Fluid`     |

Performs a binary search to find a flowrate that satisfies the components in the selected branch.

Search range: 0 - `fluid.flowrate` (the upper bound is set to be the flowrate of the received fluid)

Stops searching if the search value is above 90% of the incoming flowrate or below 0.001 Kg/s.

Returns the status (pressure high/low/ok) of downstream components.

## async `process()`

Finds a satisfactory flowrate for each destination branch.

Returns the status (pressure high/low/ok) of downstream components.

![Flowchart: Search branch flowrate method logic](https://raw.githubusercontent.com/Jerell/parallel-reservoirs/main/public/images/searchBranchFlowrate.png)
