# Unreal-and-Gameplay-Programming-Notes
A place to jot down knowledge I've gained. I try my best to quote and give credit to people I've learned from who helped "make it (something) click"

Will improve formatting as I get a feel for organizational issues.

## Contents
@TODO update links with aliases to improve style and formatting
- [C++ Specific](#cpp)
- [Gameplay Programming Tips](#gameplayprogrammingtips)
- [Premature Optimization](#prematureoptimization)
- [Math](#math)
- [Unreal Engine](#unrealengine)



# Programming Lingo
- Sometimes, you'll see variables that have the word ```Context``` in them. This is defined as:  all the relevant information that a developer needs to complete a task.



# cpp
- It is generally unsafe to do a range-based forloop ``` for(Type something : Container) ``` over a container and remove from that container without getting a new iterator. In C++ STL container ```container.erase()``` methods return a new iterator.  Bad Example:


```cpp
for(auto iter = container.begin(); iter !=  container.end(); ++iter)
{
    container.erase(iter);
}
```

Correct Example:
```cpp
for(auto iter = container.begin(); iter !=  container.end(); ++iter)
{
    iter = container.erase(iter);
}
```

- Handles: Not the data itself, but a way to get to the data.
- TODO: Statics - aka static helper functions 
 TODO: ( add link to Unreal Engine Iterator Implementation)

# GameplayProgrammingTips

## Input

- Let objects manage the binding and unbinding of their own input for encapsulation.
  
# PrematureOptimization
- Premature Optimization is the root of all evil.
- Keep your code readable, micro performance optimizations don't matter.
- "Don't blindly optimize, figure out the **What, Why and How**" - Ari Arnbjörnsson in: Maximizing Your Game's Performance in Unreal Engine | Unreal Fest 2022
  - Whats slow?
  - Why is it slow?
  - How can it be fixed?
 


# math

## Quaternions

When trying to understand quaternions, I found these resources helpful. (especially understanding them from the math point of view, and a programmer point of view)
- https://danceswithcode.net/engineeringnotes/quaternions/quaternions.html
- https://eater.net/quaternions
- Series by Jorge Rodriguez on math for game development, videos related to quaternion and axis-angle representation https://www.youtube.com/watch?v=dttFiVn0rvc



# UnrealEngine

## Iterators
- (As far as I have learned) In UE, you aren't given a new iterator. Because TArray (which is the underlying datastructure for a lot of containers) ". . . stores an index, not a pointer, it won't be invalidated by reallocations" - Laura from the (Unreal Slackers/Unreal Source discord).
