---
layout: post
title: "Queue-based maze solving algorithm in C++"
description: " "
date: 2023-10-10
tags: [maze, algorithm]
comments: true
share: true
---

In this blog post, we will explore a queue-based algorithm for solving mazes using C++ programming language. Mazes are a classic problem in computer science and solving them using different algorithms can provide insights into various data structure and algorithm techniques.

## Understanding the Problem

Before diving into the algorithm, let's first understand the problem statement. A maze can be represented as a two-dimensional grid, where each cell can be either a wall or an open space. The objective is to find a path from the starting position to the goal position in the maze.

## Queue-based Algorithm

The queue-based algorithm we will be discussing is a modified version of the breadth-first search (BFS) algorithm. It uses a queue data structure to keep track of the cells to explore. Here are the steps of the algorithm:

1. Create an empty queue.
2. Enqueue the starting position of the maze.
3. While the queue is not empty:
   - Dequeue a position from the front of the queue.
   - If the dequeued position is the goal position, stop algorithm and return the path.
   - Mark the dequeued position as visited.
   - Enqueue all the neighboring positions that are not walls and have not been visited before.
4. If the queue becomes empty and the goal position has not been found, return that the maze has no solution.

To implement this algorithm in C++, we need to define a `Position` struct to represent a cell in the maze. Additionally, we need to keep track of visited positions and the path taken to reach each position.

## Implementation in C++

```cpp
#include <iostream>
#include <queue>
using namespace std;

const int MAX_SIZE = 100; // maximum size of the maze

struct Position {
    int row, col; // row and column index of the cell
};

bool isValid(int row, int col, int numRows, int numCols) {
    return (row >= 0 && row < numRows && col >= 0 && col < numCols);
}

bool isWall(int maze[MAX_SIZE][MAX_SIZE], int row, int col) {
    return (maze[row][col] == 1);
}

// Function to solve the maze using the queue-based algorithm
string solveMaze(int maze[MAX_SIZE][MAX_SIZE], int numRows, int numCols, Position start, Position goal) {
    queue<Position> q;
    bool visited[MAX_SIZE][MAX_SIZE] = {false};
    int parentRow[MAX_SIZE][MAX_SIZE], parentCol[MAX_SIZE][MAX_SIZE]; // to keep track of parent positions

    q.push(start);
    visited[start.row][start.col] = true;

    while (!q.empty()) {
        Position current = q.front();
        q.pop();

        if (current.row == goal.row && current.col == goal.col) {
            // Goal position found, reconstruct the path
            string path = "";
            while (current.row != start.row || current.col != start.col) {
                int parentRow_ = parentRow[current.row][current.col];
                int parentCol_ = parentCol[current.row][current.col];
                if (parentRow_ == current.row + 1)
                    path = 'D' + path;
                else if (parentRow_ == current.row - 1)
                    path = 'U' + path;
                else if (parentCol_ == current.col + 1)
                    path = 'R' + path;
                else if (parentCol_ == current.col - 1)
                    path = 'L' + path;
                current.row = parentRow_;
                current.col = parentCol_;
            }
            return path;
        }

        // Explore neighboring cells
        int deltaRow[] = {-1, 0, 1, 0};
        int deltaCol[] = {0, 1, 0, -1};
        for (int i = 0; i < 4; i++) {
            int newRow = current.row + deltaRow[i];
            int newCol = current.col + deltaCol[i];

            if (isValid(newRow, newCol, numRows, numCols) && !isWall(maze, newRow, newCol) && !visited[newRow][newCol]) {
                q.push({newRow, newCol});
                visited[newRow][newCol] = true;
                parentRow[newRow][newCol] = current.row;
                parentCol[newRow][newCol] = current.col;
            }
        }
    }

    // No solution found
    return "No path exists.";
}

int main() {
    int maze[MAX_SIZE][MAX_SIZE] = {
        {0, 1, 0, 0, 0},
        {0, 1, 1, 1, 0},
        {0, 0, 0, 0, 0},
        {0, 1, 1, 1, 1},
        {0, 0, 0, 0, 0}
    };
    int numRows = 5;
    int numCols = 5;
    Position start = {0, 0};
    Position goal = {4, 4};

    string path = solveMaze(maze, numRows, numCols, start, goal);
    if (path != "No path exists.")
        cout << "Path found: " << path << endl;
    else
        cout << "No path exists." << endl;

    return 0;
}
```

## Conclusion

In this blog post, we explored a queue-based algorithm for solving mazes using C++. We discussed the steps of the algorithm and provided an implementation. It's worth noting that there are other maze-solving algorithms, each with their own advantages and limitations. Experimenting with different algorithms can help in understanding various approaches to problem-solving.

#maze #algorithm