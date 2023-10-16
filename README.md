# Unreal-and-Gameplay-Programming-Notes
A place to jot down knowledge I've gained

Will improve formatting as I get a feel for organizational issues.

## Contents
- [Gameplay Programming Tips](#gameplayprogrammingtips)
- [C++ Specific](#cpp)
- [Premature Optimization](#prematureoptimization)

# cpp
- It is generally unsafe to do a range-based forloop ``` for(Type something : Container) ``` over a container and remove from that container. Use an iterator instead.

# GameplayProgrammingTips

## Input

- Let objects manage the binding and unbinding of their own input for encapsulation.
- 
# PrematureOptimizaton
- Premature Optimization is the root of all evil.
- Keep your code readable, micro performance optimizations don't matter.
- "Don't blindly optimize, figure out the **What, Why and How**" - Ari Arnbjörnsson in: Maximizing Your Game's Performance in Unreal Engine | Unreal Fest 2022
  - Whats slow?
  - Why is it slow?
  - How can it be fixed?
