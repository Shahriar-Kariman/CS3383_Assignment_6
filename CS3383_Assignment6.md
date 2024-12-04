# CS3383 - Assignment 6

**Author:** Shahriar Kariman

**Date:** Dec 6th

## Question 1 - 8 Queen Problem

So I know best first search is through having a priority queue and keep expanding the node with the most promise on each turn. And you find the most promising node through a huristic like $f_n = g_n + h_n$.

Here I can define the number of queens I have on the board for a particualr node as $g_n$ and the number of possible positions the next queen could go on on the next row.

```py
# for the purpouse of this question lets
# assume the board noation is just 0-7
# for both column and rows
# so the a1 square would be {"column": 0, "row": 0}
class queen:
  def __init__(self, column, row):
    self.column = column
    self.row = row
  def can_go(self, column, row):
    if self.column == column or self.row == row:
      return True
    c = abs(self.column-column)
    r = abs(self.row-row)
    if c==r:
      return True

class board_state:
  def __init__(self, queens):
    self.queens = queens
  # how many queens are already placed
  def calc_g(self):
    return len(self.queens)
  # how many squares are avalible in
  # the next row for the next queen
  def calc_h(self):
    next_avalible_squares = 8
    for col in range(8):
      for q in self.queens:
        if q.can_go(col,len(self.queens)):
          next_avalible_squares -= 1
          break
    return next_avalible_squares
  def calc_huristic(self):
    return self.calc_g() + self.calc_h()

def 8_queens():
  # lets just assume I have a priority queue class
  queue = new PriorityQueue()
  queen_array = []
  for column in range(8):
    queen_array.append({'column':column, 'row': 1})
```

## Question 2 - (0-1) Knapsack Problem

## Question 3 - Traveling Salesman Problem
