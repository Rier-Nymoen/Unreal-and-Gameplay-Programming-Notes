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

- implicit function deletion.
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

-Dynamic delegate parameters MUST support reflection.

#VisualStudioShortcuts

"ctrl + minus" - navigates backwards in visual studio. Useful for searching definitions briefly and getting back to where you were writing code.

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

## Plane Equations:

Amazing resource for understanding why the equation for planes describes the plane.
https://www.youtube.com/watch?v=HjJ140TYbXQ


# UnrealEngine
## MemoryManagement-SmartPointers
- Use smart pointers for non-uobjects to make memory management easier.

- https://docs.unrealengine.com/4.26/en-US/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/SmartPointerLibrary/

## GameplayAbilitySystem

### Gameplay Cues

UGameplayCueNotify - can be called from GameplayEffects. GameplayCues are automatically subscribed to the event system based on their  member variable: ```GameplayCueTag```. 

## Iterators
- (As far as I have learned) In UE, you aren't given a new iterator. Because TArray (which is the underlying datastructure for a lot of containers) ". . . stores an index, not a pointer, it won't be invalidated by reallocations" - Laura from the (Unreal Slackers/Unreal Source discord).

## CharacterMovementComponent
### System Architecture
- The UCharacterMovementComponent::TickComponent function is called every frame. This function calls ControlledCharacterMove().
- Inside UCharacterMovementComponent::ControlledCharacterMove(), if the CharacterOwner is has the Authority role, PerformMovement() is called. In Autonomous Proxy, ReplicateMoveToServer() is called.
- PerformMovement calls StartNewPhysics(). When StartNewPhysics() returns, UpdateCharacterStateAfterMovement is called.
-  UCharacterMovementComponent::ControlledCharacterMove() calls ACharacter::CheckJumpInput() which given the necessary conditions calls UCharacterMovementComponent::DoJump()


## AI Behavior Trees
- BTServices - for things that happen at an interval, and updating the blackboard for information required at lower nodes. Best used at the start or end of branches.

- Receive Activation when a branch is entered.

- Nodes - nodes have to be specified whether they create speciifc instances or not. This allows for agent-specific data to be safe to store.
- https://docs.unrealengine.com/4.27/en-US/InteractiveExperiences/ArtificialIntelligence/BehaviorTrees/BehaviorTreeNodeReference/


## AI Perception Component
How data is received from the environment.

https://dev.epicgames.com/documentation/en-us/unreal-engine/ai-perception-in-unreal-engine

## AI Environment Query System (EQS)
The Environment Query System is for asking questions about the environment.

### EQS Generator
A generator produces "items" (locations or actors) that can be tested for various conditions and scored.

### EQS Context
EQS Contexts act as a frame of reference for EQS Tests and Generators. A basic example of a context is a querier, where a generator can use the pawn querier to generate points around it. A context can even give multiple locations for which a generator would generate items for each context.



