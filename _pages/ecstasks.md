---
title: "ECS Behaviour Tree / FSM"
permalink: /pages/ecstasks
---

*Some experiments with making a behaviour tree / FSM in ECS*

I wanted to create something in ECS (using enTT) that normally would be better suited to OOP methods and see how it would be implemented using ECS.
My aim was to create a behaviour tree system where a tree could be defined and all the behaviours and state changing was done using the Entity Component System model in order to better understand the limitations and implementation details of an ECS structure instead of an OOP one.

# Behaviour Tree #

A simple demo can be seen here:

<iframe width="1280" height="720" src="https://www.youtube.com/embed/r6j57a73wGg" title="ECS Behaviour Tree Demo" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Behaviour Tree Definition ##
In order for this to function well with ECS, I made some modifications to what is the classic behaviour tree.
The step in the behaviour tree only changes when the running behaviour finishes, which then queries the tree to evaluate which node is next.
Each node has a "Runtime" and a "Blueprint". The runtime exists only when we need it, containing all current state data and points to the blueprint version of the node.
The root node is started up as a runtime, it then evaluates its next node and starts a runtime of it, this then continues almost like a linked list until a leaf node is reached.
Once we have a leaf node, we read its behaviour and pass this to the TaskTreeComponent to hold onto.

_NOTE: This means that our evaluating of where we are on the tree is more OOP-like but if we turned this into pure ECS then we would take N frames to evaluate the next leaf node behaviour for N steps from the root. The rest of the behaviour systems (the bulk of our time) do run properly using ECS however._

Once a runtime node is finished its operations and returns back to its parent, it clears up its children runtime nodes.

![SelectorNode]({{ "/assets/ECSTasks/BehaviourSelector.png" | relative_url }})

_I am currently working on a version that allows for asynchronous operations on the tree to make the behaviour tree function more like a classic behaviour tree, as this method currently waits on a behaviour to fully finish before being able to do another. This approach will be using sub-entites to run nested trees._

## TaskTreeComponent ##
This holds onto the current node that the entity is on and uses this to evaluate what node to move to next, based on the condition of its exit, once it is transitioning out of its current state.

![TaskComponents]({{ "/assets/ECSTasks/BehaviourTaskComponent.png" | relative_url }})

![TaskSystem]({{ "/assets/ECSTasks/BehaviourTaskSystem.png" | relative_url }})

## TaskTransitionComponent ##
We use this as our method of determining when a task is finished.
The task system goes through every entity with a TaskTreeComponent and a TaskTransitionComponent, using the condition passed to the transition component to determine which node to move to next in the tree held by the tree component. It then adds that new component type to the entity and removes the TaskTransitionComponent.

## Go To Behaviour ##
Here is an example of one of the behaviours, which simply goes to a specified position. If no position is given, it picks a random one.
This position is passed to the GoTo component by the node through the AdditionalData that can be set for any node and given during the component's creation.
_My intention is to modify this to do a blackboard lookup for the position rather than a hard...dataed? (one time data-defined) value._

This goto system returns a success if it can get to the position in time and a failure if it can't.
![GotoSystem]({{ "/assets/ECSTasks/GotoBehaviour.png" | relative_url }})

**If you have any thoughts or questions about this behaviour tree in ECS please feel free to contact me.**

------------------------------------------------------------------------------------------------------

_**This FSM version is very similar but I thought I'd leave it as it is a little simpler and I covered it in a bit more detail but has a bit of duplicate info.**_

# Finite State Machine #
This was developed first as a simpler approach to the behaviour tree but works in a similar fashion.

A simple demo can be seen here:

<iframe width="1280" height="720" src="https://www.youtube.com/embed/ysepPS2qPec" title="ECS Task Demo" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## TaskTreeComponent ##
This is the same as the behaviour tree implementation, we define a tree, like we would any FSM system.
In this one I have created 3 nodes, each with a different state and use Conditions to determine which node we move to after the current one.

This tree is held within the TaskTreeComponent, which knows about the tree and which current TaskNode the entity is on.

![TaskComponents]({{ "/assets/ECSTasks/TaskComponents.png" | relative_url }})

## TaskTransitionComponent ##
This is the same as the behaviour tree implementation, it helps us to determine when a task is finished.

_More info could be given to the task transition component and then that could be given to the new component when it is added (like the behaviour tree does) but I found that for this FSM test it wasn't needed._

Previously I had this doing an "any_of" check that would see if any of the Task type components were on the entity but found a dedicated task transition component to be the easiest. It allows allows for more functionality as we could implement more features into the transition to make it slower between transitions etc.

_If we wanted multiple tasks to run at once we would have to be careful with this approach however, my assumption would be that either the TaskTreeComponent could have multiple runningTasks it knows about and the transition component would have to take into account which "stream" of task it is on or we would have sub-entites that would handle the multiple running tasks._

![TaskSystem]({{ "/assets/ECSTasks/TaskSystem.png" | relative_url }})

## The states ##
Idle, Walk, Chase

![BehaviourComponents]({{ "/assets/ECSTasks/BehaviourComponents.png" | relative_url }})

### Idle ###
During Idle, we wait until a target has been found or the timer has ran out.
If the timer runs out, we do a task transition into walk
If a target is found, we task transition into chase.
![IdleSystem]({{ "/assets/ECSTasks/IdleSystem.png" | relative_url }})

### Walk ###
During Walk, we pick a random direction to look at and walk in that direction at a set speed.
We run a timer and if that runs out, we do a task transition back to idle.
If a target is found, we task transition into chase.
![WalkSystem]({{ "/assets/ECSTasks/WalkSystem.png" | relative_url }})

### Chase ###
During Chase, we run in the look direction, which will be towards the direction where the target was viewed due to the TargetSystem.
We run a timer and if that runs out, we do a task transition to idle.
We also check if the ViewTargetComponent is on this entity and task transition to idle early if the target is lost.
![ChaseSystem]({{ "/assets/ECSTasks/ChaseSystem.png" | relative_url }})


## TargetSystem ##
The target system was done independently from the states but could be anything really, it could be unique to the states or completely separate, like in this example.
There is a LookDirComponent that defines where the current entity is looking as well as its view distance and angle.
During the target system update we use this along with the STransformComponent to find all entities within its view.

![TargetComponents]({{ "/assets/ECSTasks/TargetComponents.png" | relative_url }})

_Here we could add an extra component to define components we actually want to target (like players) and not just everything with a TransformComponent (like another NPC or a random static object) but this test doesn't have any of those in the scene._

When a target is found, we adjust the look direction inside of the LookDirComponent so it is looking directly at the target add a ViewTargetComponent onto the entity that is doing the searching and pass it the entity ID of the target it views.
During this update we can also check every entity with a ViewTargetComponent and a LookDirComponent to see if the target specific is still in view. If not, we remove the ViewTargetComponent.
We also remove the ViewTargetComponent if the target is very close to this entity and flip the look direction just so that we're not locked into staring at the target as we don't do anything else when we get this close.

![TargetSystem]({{ "/assets/ECSTasks/TargetSystem.png" | relative_url }})

