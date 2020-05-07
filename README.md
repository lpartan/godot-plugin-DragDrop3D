# Use

1. Add the `DragDropController.gd` as an `AutoLoad` (aka singleton) to your project.
2. Populate your 3D scene with physical objects
3. As a sibling to the Physics object (e.g. Area, KinematicBody, RigidBody, etc...), add a `Draggable` node
4. Register to the signals of the Dragable node as you see fit, especially the `drag_move` signal

## drag_move signal

The DragDropController uses raycasting to detect where the mouse is hovering over (excuding the dragged object).
Use this signal to update the position of your object as it is being draged. It is done this way since you may want a snapping, animation, or something else, so it is for you to decide.
The signal sends two variables, the draggable object and the raycast dictionary output (see https://docs.godotengine.org/en/3.2/classes/class_physicsdirectspacestate.html#class-physicsdirectspacestate-method-intersect-ray for more details)

As an example, you may want to receive the signal as the following to simple slide over the collider object:

```godot
func _on_Dragable_drag_move(node, cast):
	set_translation(cast['position'])
```

Remember to use pivot points or references to properly position and avoid object overlaps.

## Example project

There is an example project provided where a draggable box slides above a plane.