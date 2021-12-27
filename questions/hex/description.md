You are developing a turn-based game played on a hexagonal grid. Tokens are
placed on the grid and players take turns moving their token to an adjacent
tile. When a player moves their token, they remove the previously occupied
tile from the board. Players can only move to an unoccupied tile. The last
player to move wins.

<p align="center">
<img src="./questions/hex/diagram.svg" alt="Game Diagram" 
     style="width:20em;max-width:100%"></p>

In this figure, the blue player has just moved, taking a tile from the board. Now,
the red player can choose to move in one of five directions. The sixth direction
is unavailable since it does not have a tile.

The board is represented as a two-dimensional array. The layout follows a parallelogram
shape where each entry corresponds to the state of one hexagonal space. An empty
space is represented with `:x`, an unoccupied tile is represented with `:-`, and a
player token is represented with a number.

So for example, the collection `[[1 :- 3] [:x 2 :-]]` has the following shape:

```
 __
/1 \__
\__/:-\__
/:x\__/3 \
\__/2 \__/
   \__/:-\
      \__/
```
 

The spec for the game is:

```clojurescript
(s/def ::tile (s/or :- :x number?))
(s/def ::board (s/* (s/* ::tile)))
(s/def ::direction (s/or :up :down :up-left :up-right :down-left :down-right))
```

A move function takes a board, player, and direction. The return value is a new
board with the player in a new position and the previous tile removed. It
throws an exception if the function is given an illegal move:

```clojurescript
(s/fdef move-player
  :args (s/cat :board ::board :player ::player :direction ::direction)
  :ret ::board)
```
 
A `valid-moves` function takes the board and player. It returns a collection of
valid moves the player can make:

```clojurescript
(s/fdef valid-moves
  :args (s/cat :board ::board :player ::player)
  :ret (s/coll-of ::direction))
```
