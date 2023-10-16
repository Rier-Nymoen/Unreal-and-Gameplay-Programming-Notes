# Unreal-and-Gameplay-Programming-Notes
A place to jot down knowledge I've gained

Will improve formatting as I get a feel for organizational issues.

## Contents
- [Gameplay Programming Tips](#gameplayprogrammingtips)
- [C++ Specific](#cpp)

#cpp
- It is generally unsafe to do a range-based forloop ``` for(Type something : Container) ``` over a container and remove from that container. Use an iterator instead.

# GameplayProgrammingTips

## Input

- Let objects manage the binding and unbinding of their own input for encapsulation.
