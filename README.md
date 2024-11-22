# Introduction

{% embed url="https://www.youtube.com/watch?v=H9B88kh6ECs" %}

## Introduction to Tile Composer

Before diving deep into the individual parts of Tile Composer, let's start with what its goal is and what the workflow looks like.

***

Tile Composer is a constraint based model generator, so basically you give it a set of constraints (your tiles) and it tries to fill a grid without breaking any of your rules. Depending on your rules the result might be unexpected, but with some refinement you'll be able to prevent the generator from taking any shortcuts.

Here's a simplified version of how you can use the asset:

1. Create a tileset: An artist (or programmer, with nice programmer art) creates a set of models or textures that can be used to fill a grid.
2. Define neighbor restrictions: Use one of the different workflows to define which neighbors are allowed for each tile.
3. Create a grid where you want to place your tiles.
4. Optionally: Add additional constraints, like blocking tiles (e.g. you want a house at one position, but nowhere else), change the probability of each tile, etc.
5. You're done: The algorithm tries to find a combination of tiles that fits perfectly into the grid.

{% tabs %}
{% tab title="1. Create Tiles" %}
<figure><img src=".gitbook/assets/Model Tiles.jpg" alt=""><figcaption><p>Setup your tile models or textures</p></figcaption></figure>
{% endtab %}

{% tab title="2. Define neighbors" %}
<figure><img src=".gitbook/assets/Tile Constraints.jpg" alt=""><figcaption><p>Define neighbor restrictions with one of the workflows</p></figcaption></figure>
{% endtab %}

{% tab title="3. Create grid" %}
<figure><img src=".gitbook/assets/Create Grid.jpg" alt=""><figcaption><p>Create a grid where the tiles will be randomly placed</p></figcaption></figure>
{% endtab %}

{% tab title="4. Additional constraints" %}
<figure><img src=".gitbook/assets/Create Restrictions.jpg" alt=""><figcaption><p>Add additional constraints, like setting the grid border to be empty</p></figcaption></figure>
{% endtab %}

{% tab title="5. Generate model" %}
<figure><img src=".gitbook/assets/Generate a model.jpg" alt=""><figcaption><p>Generate a model</p></figcaption></figure>
{% endtab %}
{% endtabs %}

Now in reality it's not quite as simple, each tile constraint can have a lot of unexpected consequences, but with a bit of tinkering and trail and error, you've just created your own bit of procedural creation, without having to touch any code!

In this documentation, I will walk through all parts of this process:

* Creating tilesets using a variety of different methods of creating the initial constraints, for example, directly from a base mesh, using connectors, or by defining every constraint by hand
* How to create a tile set that can be easily solved
* How to accomplish complex restriction (which is always a trade of complexity vs speed)
* Defining the model, including the two types of solvers, with their various advantages and disadvantages.
