# CS3383 - Assignment 6

**Author:** Shahriar Kariman

**Date:** Dec 6th

## Question 1 - 8 Queen Problem

So I know best first search is through having a priority queue and keep expanding the node with the most promise on each turn. And you find the most promising node through a heuristic like $f_n = g_n + h_n$.

Here I can define the number of queens I have on the board for a particular node as $g_n$ and the number of possible positions the next queen could go on the next row.

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
    # The huristic for a board state/node
    # can be calculated from the start
    self.huristic = self.calc_huristic()
  # how many queens are already placed
  def calc_g(self):
    return len(self.queens)
  # how many squares are avalible in
  # the next rows for the next queens
  def calc_h(self):
    next_avalible_squares = 0
    for r in range(len(self.queens),8):
      for col in range(8):
        for q in self.queens:
          if not q.can_go(col,r):
            next_avalible_squares += 1
            break
    return next_avalible_squares
  def calc_huristic(self):
    return self.calc_g() + self.calc_h()
  # duplicate array of queens
  # that way modifying the array wont change the
  # other board states/nodes
  def dup_queens(self):
    return [queen(q.column, q.row) for q in self.queens]

def 8_queens():
  # lets just assume I have a priority queue class
  queue = PriorityQueue()
  # at the start I can put the first queen
  # in 8 different squares that is 8 different
  # board states that will be ordered based
  # on the huristic in the queue
  for col in range(8):
    queue.add(board_state([queen(col, 0)]))
  while not queue.is_empty():
    state = queue.pop()
    if len(state.queens)==8:
      return state
    for col in range(8):
      is_avalible = True
      for q in state.queens:
        if q.can_go(col, len(state.queens)):
          is_avalible = False
          break
      if is_avalible:
        # Make a new board state for the case
        # where we place a queen on that square
        # remember board_state.huristic is created
        # upon initialization and queue is in order of board_state.huristic
        new_queens = state.dup_queens()
        new_queens.append(queen(col, len(state.queens)))
        queue.add(board_state(new_queens))
```

**Personal Note:** How is this question only 15 marks this was a really long question.

## Question 2 - (0-1) Knapsack Problem

Wouldn't this be similar to the greedy proof thing with the swapping?

Also I choose to have actual item objects in an array as opposed to keeping track of indexes it just seems more logical.

```py
def hillClimbin_knapsack(items, limit):
  # Lets assume items is an array of objects
  # containing attributes name, benefit and weight
  current_weight = 0
  knapsack = []
  remaining_items = []
  while len(items)!=0:
    obj = items[random.randint(0,len(items))]
    items.remove(obj)
    if obj["weight"]<(limit-current_weight):
      knapsack.append(obj)
      current_weight += obj["weight"]
    else:
      remaining_items.append(obj)
  # sort the remaining items in ascending order of value
  remaining_items = merge_sort(remaining_items)
  # get the highest value remaining item
  item = remaining_items.pop()
  # sort the knapsack item in ascending order of value
  knapsack = merge_sort(knapsack)
  for i in range(len(knapsack)):
    if calc_val(item)>calc_val(knapsack[i]) and (current_weight-knapsack[i]["weight"]+item["weight"])<limit:
      # swap the next least valuable item in the
      # knasack with the most valuable remaining item
      # if the swap does not go over the limit
      current_weight += item["weight"]-knapsack[i]["weight"]
      knapsack[i] = item
      if len(remaining_items)==0:
        return knapsack
      # onto the next highest value item
      item = remaining_items.pop()

def calc_val(obj):
  return obj["benefit"]/["weight"]
```

I figured using sorting would help find the best swap faster but then I don't see why we would even need to do this a greedy algorithm would work better.

## Question 3 - Travelling Salesman Problem

```py
def local_search_TSP(cities):
  current_tour = random_tour(cities)
  current_distance = calculate_distance(current_tour)
  while True:
    best_improvement = 0
    best_swap = NULL
    for i in range(len(current_tour)):
      for j in range(i+1, len(currnet_tour)):
        new_tour = swap_cities(current_tour, i, j)
        new_distance = calcualte_distance(new_tour)
        improvement = current_distance - new_distance
        if improvement > best_improvement:
          best_improvement = improvement
          best_swap = [i, j]
    if best_improvement > 0:
      current_tour = swap_cities(current_tour, best_swap[0], best_swap[1])
      current_distance = current_distance - best_improvement
    else:
      break
  return {"tour":current_tour, "distance": current_distance}
```
