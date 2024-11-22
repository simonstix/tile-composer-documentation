# Custom Grid Types

{% hint style="danger" %}
&#x20;I'm not sure how much demand will be for custom code like this, so for now it will be a fairly minimalistic guide. In case you need more information, please contact me. I will try to help you with your problem and consider extending this guide.
{% endhint %}

{% hint style="info" %}
&#x20;In case you're wondering why the IGrid interface is so large: It's mostly for optimization and because of annoying properties of grids that aren't rectangular. I'm always open for ideas how to simplify the whole thing, especially as most of the functions are only used at a single point in the code.
{% endhint %}

## Create an implementation of IGrid

Look at the Doc comments of IGrid and the implementation of hexagon grids (I've tried to keep this one clean) for help.

You should be aware of the following implementation details:

* The grid itself is stored as a single array, the IGrid is responsible for mapping the represented grid to this array.
* The implemented solvers (Wave Function Collapse, Z3) support arbitrary grids, so the IGrid has to tell them details about their nature, e.g. how many rotational axes exist for tiles of this grid, how many sides per tile, etc.

I personally find it extremely helpful to put as much of the internal implementation into helper functions, so you don't have to think about Coordinate - Index relationships, or which index is the neighbor in a certain direction.

## Add the new grid to other scripts

1. Add the grid to the GridType enum, in `Scripts/Grid/GridType.cs`.
2. Add it to the TileCollection. Just search for all uses of GridType in that file and imitate what's being done with the other grid types.
