# Tile Collections

Tile collections are, as the name suggests, the container of tiles. Here you can change settings that affect all tiles in the collection. It also provides functionality to simplify creating the neighbor restrictions.

## Tile Collection Editor

### Automatic Neighbors

The editor tools in this category allow you to automatically set neighbor restrictions.

### **Clear neighbors**

In case you want to start from scratch, for example if you wish to switch to another workflow, you can press this button to clear all neighbors.

### **Auto-set neighbors from mesh**

This button can be used to create neighbor restrictions from the mesh of each tile. It compares each pair of tiles and checks if their borders fit together perfectly. If yes, it allows the tiles to be neighbors, otherwise they are blocked from being neighbors. For more information about this workflow check [Neighbors from mesh](../tutorials/neighbors-from-mesh.md).

### Empty Tile Assignment

Instead of having to make neighbor changes to each tile individually, you can use this tool to set empty connections on all tiles simultaneously. Select one of your empty tiles, then you can use the circles in the scene view to toggle which tiles are allowed to have this empty type as neighbor.

### Connector Assignment

Instead of adding connectors to each tile individually, you can use this tool to add/remove them on all tiles simultaneously.

To use this feature you need to add connectors in the tile collection settings.

## Tile Collection Settings

These settings change the size and shape of your grid and let you change settings that are shared by all tiles in this collection.

### Grid Type and scale

The grid type changes the shape and behavior of your tiles. For example a box grid, with box shaped tiles, makes it possible to create models with straight lines, while triangle shaped tiles can create hexagonal or rounded shapes. In the end it depends on what you want to accomplish, for most cases you will probably want to use a box or a rectangle grid.

The grid scale defines the size of your tiles. This has to match the size of your tiles perfectly, or your final model will not look right. You can still resize the model generator later.

### Grid Specifics

Some grid types have different settings, read the tooltips to see what each of them does.

### Empty tiles

Empty tiles are placeholders for spaces in the model where you don't want any tiles at all. For example in a city, you don't want to have any tiles above streets. Without an empty tile, it wouldn't be possible to create the model, because no tile is allowed to be above the street tile.

You can create multiple empty tiles, in case you want to have different empty areas that must not touch each other. Using our city example again: You can create an "Inside" empty type, to allow buildings to have space between their walls. Using the same empty type as outside here can lead to wrong models, for example a wall might be rotated inside out.

The weight of an empty type defines the probability at which it is selected in the model (same as for regular tiles).

**Is compressible** makes is easy to allow tiles with the same empty type to neighbor each other. For example, you might want to allow very small alleys between buildings, by neighboring the outside tiles of buildings directly. With the help of empty compression, you simply set both tiles to have the same empty neighbor and set it to compressible, the tiles are now allowed to neighbor each other.

### Connectors

Connectors are the basis of one of the workflows for creating neighbor restrictions. Instead of looking at each pair of tiles individually, you create connection types between multiple tiles. For example, if you want to create a street system, you could use a "Street" connector and put it on each tile side where the street will be continued, e.g. a crossing would have sides with the street connector, while straight roads and curves would have 2. Once you start the generation process, the system matches up all tiles with the same connector. Read more about this workflow on it's [documentation page](tile-collections.md#connectors).

`Is Bidirectional`makes it possible to toggle between connectors that have directional information or not. A bidirectional connector can be connected to all instances of itself if rotation and direction make it possible. A directional connector has an "In" and an "Out" variant. Only In-Out connections are allowed, In-In and Out-Out connections are forbidden. One possible use is to create rivers or roads that go from a goal to a target.

### Custom Properties

You can use custom properties to add additional information to your tiles, then add additional constraints based on them. For example, you could add the properties "Weight" and "Cost" and restict the maximum and minimum for the model.

{% hint style="warning" %}
Not all solver types support custom properties. For example, Wave Function Collapse does **not** work with custom properties.
{% endhint %}
