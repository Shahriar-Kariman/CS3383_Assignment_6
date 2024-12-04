# CS3383 - Assignment 6

**Author:** Shahriar Kariman

**Date:** Dec 6th

## Question 1 - 8 Queen Problem

So I know best first search is through having a priority queue and keep expanding the node with the most promise on each turn. And you find the most promising node through a huristic like $f_n = g_n + h_n$.

Here I can define the number of queens I have on the board for a particualr node as $g_n$ and the number of possible positions the next queen could go on on the next row.

```py
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

def 8_queens():
  # lets just assume I have a priority queue class
  queue = new PriorityQueue()
  queen_array = []
  for column in range(8):
    queen_array.append({'column':column, 'row': 1})
```

## Question 2 - (0-1) Knapsack Problem

## Question 3 - Traveling Salesman Problem
