---
layout: post
title: Conway's Game of Life
---

[Conway's Game of Life](https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life)
is the best-known implementation of a [cellular
automaton](https://en.wikipedia.org/wiki/Cellular_automaton). It was developed
in 1970 by British mathematician John Conway. You can [learn more about the Game
of Life from John Conway himself](https://youtu.be/E8kUJL04ELA).

## tl;dr
Here's a quick summary of the rules of Conway's Game of Life.

* start with an infinite 2D orthogonal square-cell grid
* each cell can be alive (1) or dead (0)
* a cell can have up to 8 neighboring cells

For each round:

* if a living cell has 2-3 living neighbors, it continues living
* if a dead cell has exactly 3 living neighbors, a new living cell is born
* if a living cell has 4+ living neighbors, it dies of overcrowding
* if a living cell has 0 or 1 living neighbors, it dies of isolation
* if a living cell travels west on the Oregon Trail, it [dies of
  dysentery](http://knowyourmeme.com/memes/you-have-died-of-dysentery)

The game is played by starting with any number and configuration of living
cells then observing how they interact with one another. There is no way to
"win" the game per se.
