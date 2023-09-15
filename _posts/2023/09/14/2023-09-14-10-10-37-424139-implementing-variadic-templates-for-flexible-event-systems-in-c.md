---
layout: post
title: "Implementing variadic templates for flexible event systems in C++"
description: " "
date: 2023-09-14
tags: [include, VariadicTemplates]
comments: true
share: true
---

Events are an essential part of many software applications. They allow different components or modules to communicate and respond to specific actions or changes. In C++, implementing a flexible event system can be achieved using variadic templates.

Variadic templates in C++ allow us to define functions or classes that can accept a variable number of arguments of different types. This feature can be leveraged to create a flexible event system that can handle events with different arguments.

To implement a variadic template-based event system, we can start by defining an `Event` class that will act as the base class for all events. This class can be a simple empty shell to provide a common base for all event types.

```cpp
class Event {};
```

Next, we can define a template class `EventDispatcher` that will be responsible for dispatching events to their corresponding handlers. The `EventDispatcher` can use a `std::unordered_map` to store event type to handler mappings.

```cpp
#include <unordered_map>
#include <functional>

class EventDispatcher
{
public:
    template <typename EventType, typename... Args>
    void Dispatch(Args... args)
    {
        static_assert(std::is_base_of<Event, EventType>::value, "EventType must be derived from Event");

        auto it = m_EventHandlers.find(typeid(EventType));
        if (it != m_EventHandlers.end())
        {
            auto& handlers = it->second;
            for (auto& handler : handlers)
            {
                handler(static_cast<EventType&>(*this), std::forward<Args>(args)...);
            }
        }
    }

    template <typename EventType, typename HandlerType>
    void AddHandler(HandlerType&& handler)
    {
        static_assert(std::is_base_of<Event, EventType>::value, "EventType must be derived from Event");
        m_EventHandlers[typeid(EventType)].emplace_back(std::forward<HandlerType>(handler));
    }

private:
    std::unordered_map<std::type_index, std::vector<std::function<void(Event&, Args...)>>> m_EventHandlers;
};
```

In the `Dispatch` function, we check if there is a matching event type in the `m_EventHandlers` map and invoke all the corresponding handlers with the provided arguments. The `AddHandler` function allows adding event handlers for specific event types.

To use this event system, we can define event types by inheriting from the `Event` class. Each event type can have its own set of arguments.

```cpp
class PlayerMovedEvent : public Event
{
public:
    PlayerMovedEvent(float x, float y) : m_X(x), m_Y(y) {}

    float GetX() const { return m_X; }
    float GetY() const { return m_Y; }

private:
    float m_X;
    float m_Y;
};
```

We can then create an instance of the `EventDispatcher` and add event handlers for specific event types.

```cpp
EventDispatcher eventDispatcher;

eventDispatcher.AddHandler<PlayerMovedEvent>([](const PlayerMovedEvent& event, float newX, float newY) {
    // Handle player moved event
    // newX and newY can be accessed using `event.GetX()` and `event.GetY()`
});

// Add more event handlers for other event types
```

Finally, when we want to dispatch an event, we can do so by calling the `Dispatch` function of the `EventDispatcher` with the appropriate event type and arguments.

```cpp
PlayerMovedEvent playerMovedEvent(10.0f, 20.0f);
eventDispatcher.Dispatch<PlayerMovedEvent>(playerMovedEvent.GetX(), playerMovedEvent.GetY());
```

By utilizing variadic templates, we can create a flexible event system in C++ that allows different event types to have different sets of arguments. The event system can be easily extended to handle new event types by adding event handlers and dispatching events with the appropriate arguments.

#C++ #VariadicTemplates