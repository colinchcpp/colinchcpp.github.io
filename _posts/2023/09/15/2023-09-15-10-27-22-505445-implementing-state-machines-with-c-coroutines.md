---
layout: post
title: "Implementing State Machines with C++ Coroutines"
description: " "
date: 2023-09-15
tags: [programming, cppcoroutines]
comments: true
share: true
---

State machines are a popular design pattern used in many software systems to manage state transitions and behavior. Traditional implementations of state machines using switch statements or if-else chains can quickly become complex and hard to maintain.

However, with the introduction of coroutines in C++20, implementing state machines has become more intuitive and readable. Coroutines allow us to write asynchronous code in a linear fashion without the need for complicated callbacks or nested logic.

In this blog post, we will explore how to implement state machines using C++ coroutines. We'll demonstrate a simple example that showcases the power and elegance of this technique.

## Prerequisites

To follow along with the examples in this post, you'll need a C++ compiler that supports C++20 and coroutines. Additionally, you should have a basic understanding of coroutines and how they are used.

## Example: Traffic Light State Machine

Let's consider a simple example of a traffic light state machine. The traffic light can be in one of three states: Red, Yellow, or Green. The state machine should transition from one state to another based on predefined rules and timings.

To implement this state machine using C++ coroutines, we'll define a `traffic_light` coroutine. Inside the coroutine, we'll use `co_await` to perform non-blocking delays between state transitions.

```cpp
#include <iostream>
#include <chrono>
#include <thread>
#include <coroutine>

enum class TrafficLightState { Red, Yellow, Green };

class TrafficLight {
public:
    TrafficLight() : state(TrafficLightState::Red) {}

    auto operator co_await() const {
        return TrafficLightAwaiter{ this };
    }

private:
    friend class TrafficLightAwaiter;

    TrafficLightState state;

    void transition() {
        switch (state) {
            case TrafficLightState::Red:
                state = TrafficLightState::Green;
                break;

            case TrafficLightState::Yellow:
                state = TrafficLightState::Red;
                break;

            case TrafficLightState::Green:
                state = TrafficLightState::Yellow;
                break;
        }
    }
};

class TrafficLightAwaiter {
public:
    TrafficLightAwaiter(const TrafficLight* tl) : traffic_light(tl) {}

    bool await_ready() const noexcept {
        return false;
    }

    void await_suspend(std::coroutine_handle<>) noexcept {
        std::this_thread::sleep_for(std::chrono::seconds(3));
        traffic_light->transition();
    }

    TrafficLightState await_resume() const noexcept {
        return traffic_light->state;
    }

private:
    const TrafficLight* traffic_light;
};
```

In the above code, we have defined the `TrafficLight` class and `TrafficLightAwaiter` class. The `TrafficLight` class represents the state machine, and the `TrafficLightAwaiter` class handles the `co_await` operation.

The `TrafficLight` class contains a state variable `state`, which represents the current state of the traffic light. The `operator co_await` overload allows us to use the traffic light object in a coroutine context.

Inside the `TrafficLightAwaiter::await_suspend` method, we simulate a delay of 3 seconds using `std::this_thread::sleep_for`. After the delay, the `traffic_light->transition()` method is called, which updates the state of the traffic light.

To use the traffic light state machine, we can write a coroutine function like this:

```cpp
#include <iostream>

int main() {
    TrafficLight traffic_light;

    auto run_traffic_light = [traffic_light]() -> TrafficLightState {
        co_await traffic_light;  // Await the traffic light state change

        std::cout << "Traffic light is now ";

        switch (traffic_light.state) {
            case TrafficLightState::Red:
                std::cout << "RED";
                break;

            case TrafficLightState::Yellow:
                std::cout << "YELLOW";
                break;

            case TrafficLightState::Green:
                std::cout << "GREEN";
                break;
        }

        co_return traffic_light.state;
    };

    run_traffic_light().resume();

    return 0;
}
```

In the `run_traffic_light` coroutine, we `co_await` the traffic light object, which suspends the coroutine until the state of the traffic light changes. After the `co_await`, we print the current state of the traffic light and then `co_return` the final state.

By leveraging coroutines, we can write clean and readable code that closely models the desired behavior of the state machine.

## Conclusion

C++ coroutines provide a powerful mechanism for implementing state machines in a more elegant and readable way. By using coroutines and the `co_await` operator, we can write state machines that are easier to understand, maintain, and reason about.

In this blog post, we demonstrated a simple example of a traffic light state machine implemented using C++ coroutines. However, the technique can be applied to more complex state machines as well.

Using C++ coroutines for state machine implementation can improve code quality, reduce complexity, and lead to more robust software. So next time you need to implement a state machine, consider leveraging the power of C++ coroutines for a more efficient and elegant solution.

#programming #cppcoroutines