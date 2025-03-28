### The world genration


The world is composed with chunks
Chunks is charged by the server when a client entry in the chunk
If the chunk doesn't exist, the server generate it

#### The generation of the chunk

The generation of the chunk is composed of 3 steps

1. Choose the biome
To choose the biome, the server generate 2 random numbers between 0 and 1 (humidity and temperature) thanks to a Perlin noise and the seed of the world
The biome is chosen by the server with the humidity and temperature (for example, if humidity is high the biome is ocean an if temperature is high and humidty is low the biome is desert)

2. Generate the heightmap
Each biome has a value of minimum height (in blocks) and a value of height variation 
The server generate the heightmap with the information of the biome and with the neighborhood of the chunk (to have a smooth transition between chunks) thanks to a Perlin noise and the seed of the world

3. Generate the blocks
The server generate the blocks with the heightmap and the biome
The server generate the blocks with the information of the biome (for example, if the biome is ocean, the server generate water blocks, if the biome is desert, the server generate sand blocks, etc.) each biome has a surface block and a underground block
The level of ocean is 62 blocks, so ocean biome is generated under 62 blocks and the other biomes are generated above 62 blocks

The trees, the flowers and the cactus are generated in the chunk with the information of the biome

#### The generation of the trees

There are 2 types of trees: the big trees and the small trees
Each tree has a random value of height

1. Small trees
The folliage is a pyramid of leaves and some random blocks of leaves are generated around the folliage
The trunk is a column of blocks of wood

2. Big trees
The folliage is a pyramid of leaves with a double layer of leaves on the base of the folliage 
There are some random branch generated on the trunk
The trunk is a column of blocks of wood

#### Weakness of the generation

- Lack of variety of the biomes
- Lack of variety of blocks
- The underground is not generated (one type of block)
- There are no structures (villages, dungeons, etc.)
- In general, the generation is poor


#### The generation of the world






### Movement calculation player

- Jump is possible only if the player is on the ground
- If the player is not on the ground, the player falls (except if the player is in fly mode), the velocity of the player is limite to 0.9 blocks per tick. The server check if the player is on the ground after the fall thanks to the collision with the blocks
- Thanks the keys pressed by the player, the server calculate the the direction in each axis (x, y, z) and the movement for each axis (movement = direction * speed)
The server check if the player can move in the direction calculated (if there is a block in the direction)
- If the player fall in the void, the player is teleported to the spawn point
- If the player is in fly mode, the player can move in all directions (even if there is a block in the direction) an the speed is increased by 4

This simulation of movement is call by the server and the client
The client make his own simulation of movement to have a smooth movement (when a keys is press and at each tick) and the server check the movement of the player to avoid the cheating then the server send the new position of the player to the client

