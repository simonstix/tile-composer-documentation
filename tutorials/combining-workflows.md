# Combining Workflows

All of the workflows supported by Tile Composer can be used in combination with each other.

## Workflow execution order

1. **BaseTile Overrides**: A copy of each tile is created, base tile values are overwritten by children. They use the neighbor matrix that is shown in the editor, so neigbors from mesh and manual changes are already included.
2. **Tile Connectors**: Tile connectors are used to add additional connections, this overwrites the previous matrix. Connectors can only _add_ allowed neighbors, not remove them.
3. **Empty Type Compression**: Tiles with the same compressible empty type neighbor can now neighbor each other
4. **Tile Rotation**: Tiles are rotated, their weight is divided between all rotations.
5. **Model Generation**: The tile variations are now handed to the selected solver, with their additional settings.
