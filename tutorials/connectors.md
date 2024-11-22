# Connectors

The connectors workflow is the last I developed, but in my opinion it is the easiest to used and most expressive workflow in most situations. The only situation when for example the [neighbors from mesh workflow](neighbors-from-mesh.md) would be better, is when you have a large amount of unique neighbors, so you would need a large amount of connectors, which could be hard to manage.

## 1. Tile set

In this tutorial I will define the connections for the spaceship example scene, here you can see the tileset:

<figure><img src="../.gitbook/assets/01 TileSet.jpg" alt=""><figcaption></figcaption></figure>

I've already created a TileCollection component as parent for all tiles. Each of the tiles has to have the Tile component, you can use one of the [helper tools](../documentation/helpful-tools.md) to add batch add the tile component to all objects. The TileCollection uses a Box grid, but in this case it could have been a Rectangle grid instead, as the model always stays in one layer. You could easily extend it to create spaceships with 3d structures.

The ring tile isn't composed of multiple tiles, instead it is a single tile that goes beyond its tile size. Without additional constraints, the ring tiles can intersect with other parts of the spaceship. The second ring uses the first ring as base tile, the only difference is that it rotates in the opposite direction.

The only tile that will be rotated is the transition between thin maintenance and thick spaceship sections. We could also duplicate the tile and rotate it by 180°, that would also improve the performance of the Wave Function Collapse solver.

## 2. Empty tiles

We only need a single empty type, all outside areas of the spaceship are allowed to neighbor it, while the connection parts, where the spaceship will be connected to other spaceship tiles must not neighbor empty areas.

I'm using the Tile Collection Empty Assignment tool to change which sides may neighbor empty tiles.

<figure><img src="../.gitbook/assets/02 EmptyAssignment.jpg" alt=""><figcaption><p>To activate the empty assignment mode, press the assign button, right of the empty types name.</p></figcaption></figure>

<figure><img src="../.gitbook/assets/02 Empties.jpg" alt=""><figcaption><p>Then click all circles where you want the empty tile to be allowed. If the circle is green, it means that the tiles side may neighbor the empty tile.</p></figcaption></figure>

## 3. Connectors

Next let's set up the connectors themselves. In the tile collection I've created 4 connectors. One each for the large and small connections between spaceship parts, I called them Main and Maintenance, both of them bidirectional. Next we need two directional connectors, I called them Utility and Solar panel.

{% hint style="info" %}
Bidirectional means that the connector doesn't have a direction, all sides with this connector can be connected, at least if their rotation allows it. Directional connectors have in and out directions. Outgoing connectors can only be connected to ingoing connectors, connectors with the same type can't be connected. You can still add both In and Out to a tile side, which means it can be connected to all sides with the same connector type.
{% endhint %}

<figure><img src="../.gitbook/assets/03 Connectors.jpg" alt=""><figcaption><p>The final connector setup.</p></figcaption></figure>

Next we have to assign connectors to the tiles. Once again, I'm using the Tile Collection assignment tool. Here are the final assignments:&#x20;

{% hint style="info" %}
The color of each circle represents their status with the connector you're currently assigning. Yellow represents connections that are bidirectional, Green is In, Red is Out
{% endhint %}

{% hint style="warning" %}
Be careful, some of the circles are colored more transparent, because the editor doesn't recognize orthographic view at the time of writing this tutorial.
{% endhint %}

<figure><img src="../.gitbook/assets/f3f81dbc59366ee9701866c722dd6aed1fadb4bb-04main.jpg" alt=""><figcaption><p><strong>Main</strong>: All sides with a large spaceship opening.</p></figcaption></figure>

<figure><img src="../.gitbook/assets/41cbdf7102b6eaadebefb2b6d27185a89f4b4034-04maintenance.jpg" alt=""><figcaption><p><strong>Maintenance</strong>: All sides with a small spaceship opening.</p></figcaption></figure>

<figure><img src="../.gitbook/assets/4d23554ae16dad22f10c42b558fd0c6e70655751-04utility.jpg" alt=""><figcaption><p><strong>Utility</strong>: We want solar panel sockets to only connect to the spaceship utility sockets, not to each other (which would lead to free floating solar panels), so we use an In connector for each utility port on the spaceship and an Out connector on each solar panels base plate. </p></figcaption></figure>

<figure><img src="../.gitbook/assets/97959cc2c680efd030bcaf8ac604b014cddc3c38-05solarpanel.jpg" alt=""><figcaption><p><strong>SolarPanel</strong>: Once again, we don't want free floating solar panels, to we use In and Out connectors to restrict their direction. Now solar panels can only connect to each other and have to be connected to a spaceship at their base.</p></figcaption></figure>

## 4. Tile Composer

The last step is to set up the Tile Composer component. There are a few steps for this model:

* Add the tile collection to the Tile Composer component.
* Block the cockpit tile on the whole grid, we only want a single spaceship.
* Create a border of empty space around the model, otherwise we might get cut off spaceship parts at the border.
* Set a fixed position for a cockpit tile, this overrides the block.
* Optional: Select a seed with a good looking result (you can fine tune the weights of each tile to improve the results)

<figure><img src="../.gitbook/assets/05TileComposer.jpg" alt="" width="563"><figcaption><p>The final Tile Composer settings.</p></figcaption></figure>

## 5. Result

<figure><img src="../.gitbook/assets/06Result.jpg" alt=""><figcaption><p>One of the possible results.</p></figcaption></figure>
