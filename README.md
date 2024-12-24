# Unreal-and-Gameplay-Programming-Notes
My personal notes for C++ Programming, Unreal, Etc.

** Formatting and Content is work-in-progress **

## Contents
@TODO update links with aliases to improve style and formatting
- [C++ Specific](#cpp)
- [Gameplay Programming Tips](#gameplayprogrammingtips)
- [Premature Optimization](#prematureoptimization)
- [Math](#math)
- [Unreal Engine](#unrealengine)

# VisualStudio
### Shortcuts
- **(CTRL + Minus )**- navigates backwards in visual studio. Useful for searching definitions briefly and getting back to where you were writing code.
- **(CTRL + K + O)** - switches between .cpp or .h file
- **(CTRL + J)** - can list members or display member information.

# C++
### Iterators
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

 TODO: ( add link to Unreal Engine Iterator Implementation)

-Dynamic delegate parameters MUST support reflection.

# Programming Lingo
### Terminology
- ```Context``` - is defined as: all the relevant information that a developer needs to complete a task.
- ```Statics``` - static helper functions.
- ```Handles``` not the data itself, but a way to get the data.

# Useful Practices/Things to Consider

## UI
- General consensus is that game logic should never know about UI. The UI should  either subscribe itself to certain events, or tick (poll) (performance allowing).
- UI should only hold state specifically for itself.

## Input
- Let objects manage the binding and unbinding of their own input for encapsulation.
  
## PrematureOptimization
- Premature Optimization is the root of all evil.
- Keep your code readable, micro performance optimizations don't matter.
- "Don't blindly optimize, figure out the **What, Why and How**" - Ari Arnbjörnsson in: Maximizing Your Game's Performance in Unreal Engine | Unreal Fest 2022
  - Whats slow?
  - Why is it slow?
  - How can it be fixed?
# Math

### Quaternions

When trying to understand quaternions, I found these resources helpful. (especially understanding them from the math point of view, and a programmer point of view)
- https://danceswithcode.net/engineeringnotes/quaternions/quaternions.html
- https://eater.net/quaternions
- Series by Jorge Rodriguez on math for game development, videos related to quaternion and axis-angle representation https://www.youtube.com/watch?v=dttFiVn0rvc

### Plane Equations:
Amazing resource for understanding why the equation for planes describes the plane.
https://www.youtube.com/watch?v=HjJ140TYbXQ

# UnrealEngine

## Editor Settings
- **Input Scaling** - By default input scaling is turned on (not mouse sensitivity). It can make you question your own math if you don't know about it.

## GameplayAbilitySystem

### Gameplay Cues

UGameplayCueNotify - can be called from GameplayEffects. GameplayCues are automatically subscribed to the event system based on their member variable: ```GameplayCueTag```. 

## Types
### Iterators
- (As far as I have learned) In UE, you aren't given a new iterator. Because TArray (which is the underlying datastructure for a lot of containers) ". . . stores an index, not a pointer, it won't be invalidated by reallocations" - Laura from the (Unreal Slackers/Unreal Source discord).
### MemoryManagement-SmartPointers
- Use smart pointers for non-uobjects to make memory management easier. https://docs.unrealengine.com/4.26/en-US/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/SmartPointerLibrary/

## CharacterMovementComponent
### System Architecture
- The UCharacterMovementComponent::TickComponent function is called every frame. This function calls ControlledCharacterMove().
- Inside UCharacterMovementComponent::ControlledCharacterMove(), if the CharacterOwner is has the Authority role, PerformMovement() is called. In Autonomous Proxy, ReplicateMoveToServer() is called.
- PerformMovement calls StartNewPhysics(). When StartNewPhysics() returns, UpdateCharacterStateAfterMovement is called.
-  UCharacterMovementComponent::ControlledCharacterMove() calls ACharacter::CheckJumpInput() which given the necessary conditions calls UCharacterMovementComponent::DoJump()

## AI

### AI Behavior Trees
- BTServices - for things that happen at an interval, and updating the blackboard for information required at lower nodes. Best used at the start or end of branches.

- Receive Activation when a branch is entered.
https://forums.unrealengine.com/t/bttask-nodememory/307078/2

Behavior Tree Nodes (referred to here as "nodes") exist as shared objects, meaning that all agents using the same Behavior Tree will share a single set of node instances. This improves CPU performance while reducing memory usage, but also prevents nodes from storing agent-specific data. However, for cases where agents need to store and update information related to a node, UE4 provides three solutions:

- Nodes - nodes have to be specified whether they create speciifc instances or not. This allows for agent-specific data to be safe to store.
- https://docs.unrealengine.com/4.27/en-US/InteractiveExperiences/ArtificialIntelligence/BehaviorTrees/BehaviorTreeNodeReference/

### AI Perception Component
How data is received from the environment.

https://dev.epicgames.com/documentation/en-us/unreal-engine/ai-perception-in-unreal-engine

### AI Environment Query System (EQS)
The Environment Query System is for asking questions about the environment.

### EQS Generator
A generator produces "items" (locations or actors) that can be tested for various conditions and scored.

### EQS Context
EQS Contexts act as a frame of reference for EQS Tests and Generators. A basic example of a context is a querier, where a generator can use the pawn querier to generate points around it. A context can even give multiple locations for which a generator would generate items for each context.

# Multiplayer / Networking
- Add resources for "Lag compensation" Networking techniques.

## Replication
- Only server to client 
- Anytime a replicated variable's value change, a good pattern is to call its OnRep_...() so the server can get the call.
- Best used for anything involving state.

You can use the ```Replicated``` **UPROPERTY** specifier to mark variables for replication. If you use the ```ReplicatedUsing``` specifier, this allows you to setup a **RepNotify** which is a function that is called when replicated information is received.

## Net Debugging
- add UnrealEditor-Engine!GPlayInEditorContextString to watch to see if code is executing on server or client.

## RPCS
Client to server, Server to client. Primarily for unreliable gameplay events.
# Game State, Game Modes, and Player State

## Game Mode
Defines the ruleset of your game.
- Only exists on the server.


