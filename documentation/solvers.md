# Solvers

Creating a model from tiles is a very general problem (basically an SAT problem), so there can be multiple ways of solving it. Each solver has their advantages and disadvantages. Use this guide to help you choose the right solver for your project.

## Wave Function Collapse

Wave Function Collapse is a fairly new technique. Its basis is quite simple:

1. Select a grid position (in most implementations based on entropy; simplified: select the grid position where the least number of tiles are possible)
2. Randomly select one of the tiles that are allowed at this position.
3. Tell all neighboring grid positions which tiles are no longer allowed next to the selected tile. This process is propagated, so if one of the neighbors can no longer be a certain tile, it continues informing neighbors of the change.
4. Repeat until tiles have been selected for all grid positions.
5. In case there is a grid position where **no** tiles are allowed, either abort or start failure recovery.

A lot of work while developing this asset has gone into failure recovery techniques. You will likely have to play around with the different settings yourself, as each tile collection requires very different error handling. Even with the improved error handling, it is still a fairly simple technique, so if you want to use a very complex tile collection, with dependencies over multiple tiles (e.g. one tile requires exactly one other tile, which again requires exactly one other tile...) you should consider another solver type, or if possible simplify your model dramatically, to decrease the calculation time.

Wave function collapse always operates within the grid (unlike Z3, which works with logical formulas), so it is possible to watch it work. This can be extremely helpful for debugging your tile collections. Use the Debug Settings on the Tile Composer component to enable slow debug generation.

Unlike for example the Z3 solver, Wave Function Collapse never realizes when a model is impossible, so in case your tile definitions are wrong, it might not be obvious when using this solver.

### Settings

For more information on each of the settings specific to Wave Function Collapse, look at their tooltips.

### Comparison

**Advantages:**

* Very fast for simple models
* Model generation can be slowed down and viewed, for debugging

**Disadvantages:**

* Can't solve very complex models
* Can't detect impossible models#

**Use cases:**

* Tile collection where there are almost no failure states, e.g. add a tile for each combination of neighbors.
* Tile collections with some complexity, like the "asian village" example or the "cyberpunk city" example" , can be solved for some seeds and the right failure recovery settings, but might be impossible with others.

## Z3 Solver

The Z3 Solver is a SMT solver originally developed by Microsoft and is now freely available under the MIT license. An SMT solver is a program that lets you input formulas or more mathematical theorems and logically tries to find an answer to the problem. It is far more complex than wave function collapse, which helps it solve extremely complex problems, but unlike Wave Function Collapse, it was not created for this specific problem. Both the complexity and the lack of specialization make the solver a lot slower in our case. That still doesn't mean the Z3 solver can't be useful.

### Settings

Z3 allows more complex rules, so it is possible to restrict the count of a tile type, instead of changing its weight. Be careful, percentage and absolute constraints can make the solver extremely slow.

For more information on each of the settings specific to the Z3 solver, look at their tooltips.

### Comparison

**Advantages:**

* Can solve extremely complex problems.
* Allows additional restraints, for example, a minimum or maximum count of a specific tile.
* Can mathematically prove if your problem is impossible. This way you can easily test if your tile or model definition is wrong.

**Disadvantages:**

* Slower than wave function collapse (at least for simple models)

**Use cases:**

* Models with high complexity
* Very small models
* Models where complex restrictions are necessary
* Debugging your model, e.g. checking if it is possible to create a model with your current settings
