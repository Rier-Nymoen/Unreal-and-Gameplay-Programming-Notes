# Unreal-and-Gameplay-Programming-Notes
A place to jot down knowledge I've gained

Will improve formatting as I get a feel for organizational issues.

## Contents
- [Gameplay Programming Tips](#gameplayprogrammingtips)
- [C++ Specific](#cpp)
- [Premature Optimization](#prematureoptimization)
- [Math](#math)

# cpp
- It is generally unsafe to do a range-based forloop ``` for(Type something : Container) ``` over a container and remove from that container. Use an iterator instead.

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
