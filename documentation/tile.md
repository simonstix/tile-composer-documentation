# Tile

Tiles are the building blocks for your model. The tile script has to be on the root of your tile, its children can be anything your want (except other tile components, that would probably lead to problems). In theory you could even create tiles that consist of Tile Composer components, so each tile in turn generates another model. Each tile has to be part of a tile collection.

## Editor Settings

These settings are meant to help you get information about the tiles faster and other tools to simplify your workflow. Read the tooltips for more information.

## General Settings

### Base Tile

The base tile setting can be used if you want to create a slight variation of another tile type. The child tile will have the same tile type as the parent tile. For example if you have a wall type and want to have a window type with the same neighbor restrictions.

A tile with a base tile can use overrides to change some of the parents settings. This can be useful if you want to have a tile that is not distinguished from the base tile, but has slight additional constraints, e.g. a wall with door shares neighbors with a regular wall, but must be placed at the ground floor.

### Tile Type

The name of your tile type. This name has to be unique.

### Base Weight

At its core the base weight simply increases the probability at which the tile will be selected in the model. However this doesn't necessarily mean it will also occur more often in the final model.

The probability is calculated for all currently allowed tiles, so if your tile has very hard restrictions, it might be that it doesn't get selected, even with a high weight. On the other hand it's possible that your tile collection frequently leads to situations where only low weight tiles are possible, in that case those tiles will be selected frequently as well.

In the end you will have to use slow generation to look at the dynamics of your model and change weights of secondary tiles.

### Can neighbor self

As the name suggests, this setting can be used to prevent automatic workflows from allowing the tile to neighbor itself. If you use the Tile Neighbor settings manually, you can still overwrite this feature, it is only relevant for the automatic workflows.

## Variations

### Rotation axes

If you want a street tile to be rotated in different directions, it's not necessary to create two tiles, instead you can select the rotation axis and the tile collection will automatically create all rotated versions along this axis.

The system will automatically remove variations with the same rotation, so you don't have to be careful when rotating around multiple axes.

## Connectors

[Connectors ](../tutorials/connectors.md)are a way of defining neighbor restrictions, without having to handle each pair of neighbors individually.

Each side of the tile can have any amount of connectors, once you generate your model the editor will match up all tiles with the same connector.

If the selected connector is not bidirectional, you also get a dropdown selector for `In`, `Out`, and `Both`. Only connections between `In` and `Out` are accepted, `Both` can connect to either. Connections between `In` - `In` or `Out` - `Out` are not allowed.

## Neighbors

These settings can be used to manually select the possible neighbors for each side of your tile.

### Empty Neighbors

This area is used by all workflows to specify which empty types are allowed on each side of your tile. Simply enable the check if the empty type is allowed on this side. You can use the "Show connection names" editor setting the check if you have selected the correct sides.

### Tile neighbors

Here you can match up each side of your current tile with any side (in case they are rotated) of other tiles.

#### Use connection lines

For ease of use you could use the "Use connection lines" feature instead of setting the neighbor matrix manually. Simply drag a line from one of the circles to another circle, either on the same tile or another tile, to allow or to prevent two tiles from neighboring each other.

#### Neighbor matrix

This is basically the raw view on how the connections are saved. There are probably easier ways of editing neighbor restrictions, but in case you need to use is for one reason or another, here's how the connections are defined:

1. Tile neighbor: The first level defines which pair of neighbors you are editing, e.g. the currently selected tile and another tile of your collection. All changes are bidirectional, so if you change something on one tile, the other tile will be updated with the same setting.
2. The side of your own tile: E.g. the left side of your tile can connect to the (...) side(s) of the other tile.
3. The sides of the other tile: E.g. the left side of your tile can connect to the right side of another tile.

<figure><img src="../.gitbook/assets/Tile matrix.png" alt=""><figcaption><p>Here we can see that the current tile's right side is allowed to neighbor the tile SolarPanelStartRight's left side.</p></figcaption></figure>

You can also use the editor settings "Show Connection Names" and "Show Connection Lines" to visualize the allowed connections.
