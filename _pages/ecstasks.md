---
title: "ECS Task Testing"
permalink: /pages/ecstasks
---

*Some experiments with making a behaviour tree / FSM in ECS*

I wanted to create something in ECS (using enTT) that normally would be better suited to OOP methods and see how it would be implemented using ECS.
My aim was to create a behaviour tree system where a tree could be defined and all the behaviours and state changing was done using the Entity Component System model in order to better understand the limitations and implementation details of an ECS structure instead of an OOP one.



## TaskTreeComponent ##
We define a tree, like we would any other behaviour tree system.
In this one I have created 3 nodes, each with a different state and use Conditions to determine which node we move to after the current one.

This tree is held within the TaskTreeComponent, which knows about the tree and which current TaskNode the entity is on.

## TaskTransitionComponent ##
We use this as our method of determining when a task is finished.
The task system goes through every entity with a TaskTreeComponent and a TaskTransitionComponent, using the condition passed to the transition component to determine which node to move to next in the tree held by the tree component. It then adds that new component type to the entity and removes the TaskTransitionComponent.
_More info could be given to the task transition component and then that could be given to the new component when it is added but I found that for this test it wasn't needed._

Previously I had this doing an "any_of" check that would see if any of the Task type components were on the entity but found a dedicated task transition component to be the easiest. It allows allows for more functionality as we could implement more features into the transition to make it slower between transitions etc.
_If we wanted multiple tasks to run at once we would have to be careful with this approach however, my assumption would be that either the TaskTreeComponent could have multiple runningTasks it knows about and the transition component would have to take into account which "stream" of task it is on or we would have sub-entites that would handle the multiple running tasks._


## The states ##
Idle, Walk, Chase

### Idle ###
During Idle, we wait until a target has been found or the timer has ran out.
If the timer runs out, we do a task transition into walk
If a target is found, we task transition into chase

### Walk ###
During Walk, we pick a random direction to look at and walk in that direction at a set speed.
We run a timer and if that runs out, we do a task transition back to idle.
If a target is found, we task transition into chase.

### Chase ###
During Chase, we run in the look direction, which will be towards the direction where the target was viewed due to the TargetSystem.
We run a timer and if that runs out, we do a task transition to idle.
We also check if the ViewTargetComponent is on this entity and task transition to idle early if the target is lost.


## TargetSystem ##
The target system was done independently from the states but could be anything really, it could be unique to the states or completely separate, like in this example.
There is a LookirComponent that defines where the current entity is looking as well as its view distance and angle
During the target system update we use this along with the STransformComponent to find all entities within its view

_Here we could add an extra component to define components we actually want to target (like players) and not just everything with a TransformComponent (like another NPC or a random static object) but this test doesn't have any of those in the scene._

When a target is found, we adjust the look direction inside of the LookDirComponent so it is looking directly at the target add a ViewTargetComponent onto the entity that is doing the searching and pass it the entity ID of the target it views.
During this update we can also check every entity with a ViewTargetComponent and a LookDirComponent to see if the target specific is still in view. If not, we remove the ViewTargetComponent.
We also remove the ViewTargetComponent if the target is very close to this entity and flip the look direction just so that we're not locked into staring at the target as we don't do anything else when we get this close.
