---
layout: post
title: "Queue-based approach for solving the rat in a maze problem in C++"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

The rat in a maze problem is a classic algorithmic problem where a maze is represented as a matrix and we need to find a path from the starting position to the end position. The rat can only move in four directions: up, down, left, and right.

One approach to solve this problem is to use a **queue** data structure. This approach is based on the breadth-first search (BFS) algorithm, where the neighboring cells are examined and added to the queue for further exploration. The idea is to start from the source cell and keep exploring its neighboring cells until we reach the destination cell or exhaust all possible paths.

Here is an implementation of this approach in C++:

```cpp
#include <iostream>
#include <queue>
using namespace std;

// Maze size constants
#define N 4

// Structure to store cell coordinates
struct Point {
    int x, y;
};

// Function to check if a given cell (x, y) is valid or not
bool isValid(int x, int y) {
    return (x >= 0 && x < N && y >= 0 && y < N);
}

// Function to solve the rat in a maze problem using queue-based approach
void solveMaze(int maze[N][N], Point start, Point end) {
    // Array to store visited cells
    bool visited[N][N] = {false};

    // Queue to store the cells to be visited
    queue<Point> q;

    // Push the starting cell into the queue
    q.push(start);
    visited[start.x][start.y] = true;

    // Arrays to explore the 4 neighboring directions: up, down, left, right
    int dx[4] = {-1, 1, 0, 0};
    int dy[4] = {0, 0, -1, 1};

    while (!q.empty()) {
        // Pop the front cell from the queue
        Point curr = q.front();
        q.pop();

        // Check if we reached the destination
        if (curr.x == end.x && curr.y == end.y) {
            cout << "Path found!" << endl;
            return;
        }

        // Explore the 4 neighboring cells
        for (int i = 0; i < 4; ++i) {
            int nextX = curr.x + dx[i];
            int nextY = curr.y + dy[i];

            // Check if the neighboring cell is valid and not visited
            if (isValid(nextX, nextY) && maze[nextX][nextY] && !visited[nextX][nextY]) {
                // Mark the neighboring cell as visited and push it into the queue
                visited[nextX][nextY] = true;
                Point nextCell = {nextX, nextY};
                q.push(nextCell);
            }
        }
    }

    // If no path was found
    cout << "No path exists!" << endl;
}

int main() {
    // Maze matrix (0s represent walls, 1s represent paths)
    int maze[N][N] = {
        {1, 0, 1, 1},
        {1, 1, 1, 0},
        {0, 1, 0, 1},
        {1, 1, 1, 1}
    };

    Point start = {0, 0};  // Starting position
    Point end = {3, 3};    // Destination position

    solveMaze(maze, start, end);

    return 0;
}
```

In the above code, we define a `Point` struct to store the coordinates of a cell. The `isValid` function checks if a given cell is within the maze boundaries. The `solveMaze` function takes the maze matrix, starting position, and destination position as parameters.

We initialize an array called `visited` to keep track of the visited cells. We also create a queue and push the starting cell into it. Then, we iterate through the queue until it is empty. In each iteration, we pop the front cell, check if it is the destination cell, and explore its neighboring cells. If we find a valid neighboring cell that has not been visited, we mark it as visited and push it into the queue. If no path is found, we output a message indicating that no path exists.

In the main function, we define a maze matrix, starting position, and destination position. We call the `solveMaze` function with these parameters to find the path from the starting position to the destination position in the maze.

By using a queue-based approach, this algorithm is able to find a path through a maze efficiently. It explores all possible paths from the starting position to the destination position, ensuring that the shortest path is found.