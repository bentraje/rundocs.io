---
layout: default
permalink: /blender/rigging/
---


# General


- Blender, to some degree, demands a Y-axis aim for its bones. Its Inverse kinematics are computed through Y-axis. It’s not a thing for the rigs you are about to create but it becomes a problem if you are importing skeleton/animation from other DCC. See Appendix for Case Study.
- Bones are somewhat a deity in rigging for Blender. Bones can be mainly classified to deforming, control or both. Yes, the curves you see in a standard Blender rig is actually a joint, which shape modified to look like a curve.
- You can specify if its a deforming bone through Bone Panel>Deform (Checkbox). The control bone is just semantics, which means you can still make it a control bone even though it is a deforming bone.
- Control bones are basically the bones you key in animating your character.
Another misnomer, the control curves are actually meshes with only vertices and edges (i.e. no faces). Apparently, the bone deity only accepts meshes as a custom shape. No other object type is worthy.
What are leaf joints.
After binding, blender will automatically create vertex groups
You only need one armature for every character.
Supposing you already have a spine bone and wanted to add a thigh bone? Either Shift+D to duplicate a bone or Shift+A (under Edit Mode) to create bone under the same armature.
Re-orient joints? Armature>Joint Roll
In manipulating/rotating bones, you must be on pose mode rather than edit mode
Add Spline-IK? Creature your own curve. Add a Bone Constraint>Spline IK, Set the target to the recently created curve
Add Shape Keys (blendShapes)? Object Data>Shape Keys. It’s not a constraint or a deformer or a modifier object.
Track to is like the aim constraint with a handy feature where if the name turns to red means something is wrong (i.e. Up axis is Z and the Tract to axis is also Z)
Normalize is not enabled by default when setting automatic weights. Weight paint mode: Tool>Weight Tools>Normalize All
Selecting influence weights while on weight paint mode? Ctrl Click on the bone.
In other software, each bone is a different object, and dummies or helpers (called empties in Blender) are also objects that are used by a rig. That can make it difficult to control the full rig at the same time and can mess everything up when you want to scale your character up or down, or duplicate it if need be. In Blender, on the other hand, a character’s rig is a single object, which makes it really easy to place it in the scene, scale it, or duplicate it. Inside that object are only #. bones, to which you can add custom shapes to make them look better, more intuitive, and easier to select.
Bone layers are similar to scene layers, but they work only inside the armature. On the Armature tab, the Skeleton panel has four sets of little squares. The first two sets, in the Layers section, are the layers themselves. The other two sets, in the Protected Layers section, allow you to mark specific layers as protected to prevent other users of the rig from manipulating them when linking the character. (I talk about linking near the end of this chapter).
Aligning the fingers may be difficult, as the pole is not always aligned in a single axis. In such a case, put the pole in place in Pose Mode until the finger bones are in line with the model. Then select the bones you tweaked in Pose Mode, and go to the 3D View header. In the Pose menu, look for the Apply option, and choose Apply Pose As Rest Pose. Alternatively, press Ctrl+A in 3D View and select the same option. This option transfers the current transforms of the bones in Pose Mode to Edit #. Mode.
When you extrude a bone from the tail of another, the new one is a child of the existing one. If
If you select one or more bones, you can roll them by pressing Ctrl+R to control orientation. Pressing Ctrl+N gives you several automatic orientation options.
If you select two bone tips and press F, Blender creates a new bone to fill the gap. This process is similar to how the Make Edge modeling tool creates an edge to connect two vertices in a mesh.
you can switch the direction of a bone by pressing Alt+F. This keyboard shortcut switches the head and tail of a bone, changing the direction of the hierarchy.
you extrude from the head, Blender creates a new bone, with no parenting applied to it.
A faster method is to select the target bone first and then select the one to which you want to add the constraint while holding down Shift. Press Shift+Ctrl+C to open
Although the eyedropper tool is available for bone constraints, its behavior is a bit tricky. You can use it to pick the armature’s name (Object), but the eyedropper won’t work with bones, which you have to select from a list or type yourself.
When you mirror bones, some of them may get rotated in a weird way as an effect of inverting their X axis, and you’ll have to fix these rotations manually. Even though that’s not very cool, it’s usually less work than creating both sides manually!
Here are some tips you can use to adjust everything after mirroring:
Later, when you add all the constraints, you can mirror that half to the other side, carrying constraints with it; otherwise, you have to add the constraints to the other side manually.
Create an armature.
    Enter the Edit Mode of that armature, and create the main bone structure.
    In Pose Mode, add constraints to set up the rig, and jump to Edit Mode as needed to add helper bones.
    When the rig is working, add custom shapes to it, organize the bones in layers, hide the bones that are not meant to be seen, and add anything else that will help you control the rig later.
    Skin the meshes to the skeleton so that it deforms, and through weight painting, define the influence that each bone has over the vertices of the model. Your character is ready to animate!
you must model in z-forward. It’s an absolute basic in video game production.
Bone group layer. Clicking it won’t change the color. You need to go to the custom
IK Constraint Supercedes all other constraints (like limit constraint etc)
You can’t select a joint if its hidden
Copy data path not working? Must be in property mode
If you want to hide. Hide per layers rather than hihding from the object itself
For referencing, in the rig file, need to have lock for the bones so any changes will be propagated to anim/reference file
For the anim file, need to make make proxy for the bones/armature to be able to animate it.


Bone Modes

Unique to Blender, the bones can be accessed in three ways: Object Mode, Edit Mode and Pose Mode. For animators, the workflow makes sense since they can’t accidentaly modify structure or changed the build pose. For riggers, the process is somewhat cumbersome since you’d have to switch to one mode to parent and another mode to constraint.

For comparison, Maya, Max and Cinema4D only has one mode. The animators need not worry about screwing the rig since they will be working on a reference file.

The list below shows what can do in specific modes
Object Mode

    Bind bones to a mesh (through Make Parent command)
    Shows the current pose

Edit Mode

    Create/Modify/Delete bones
    Show/Modify the bind/rest pose
    Scale the rig in edit mode (as opposed to object mode)

Pose Mode

    Shows the current pose (unless you enable the Rest Position button of the Armature panel).
    Animate
    You can’t select anything except bones in Pose Mode
    Creating Constraints
    Creating Bone Layer
    Assigning Custom Shape (which only works with meshes)


Drivers Editor

    Generator Modifier in the Drivers Editor. Modifiers how will it be affected.
    Driver Name Space. Saving a script within the Blender file and referencing it in the Drivers Editor
    One definitive resource for Useful for Drivers Name Space
    Can be used also on cycle shading
    https://blender.stackexchange.com/questions/104638/establish-a-variable-inside-a-driver-expression
    Just FYI
    https://blender.stackexchange.com/questions/71902/invalid-python-expression-when-using-driver-with-python-script
     

1
2
3
4
5
6
7
8
9
10
11
12
	
(var + 3.5) if var > 0 else (var - 3.5) if var < 0 else 1
import bpy
def x(var):
    if var > 0:
        return var + 3.5
    elif var < 0:
         return var - 3.5
    else:
         return 1
bpy.app.driver_namespace["x"] = x
And then use x(var) as your driver expression.
Thanks. One thing worth mentioning is the use_self option, which is the object being driven, passed as an argument, for example x(self) and var = self.location.x in the method instead of setting up a variable of the same in driver panel is worth looking into.
Skinning Workflow

    weight paint through a mesh. use 2d fall off and tick off front faces
    Select the armature first, then object then weight paint mode
    Brute force is select point. Then go to the vertex groups, then assign or remove button


Constraints

    You have two constraints panel: object and bone (appears only when you are in pose mode). For general rigging that requires skeleton/armature, you’ll most likely use bone constraints.
    Parent (Child of) constraint is buggy. Better off to use Copy Location and Copy Rotation constraint with offset joints/groups.
    When you delete the constraint, the driven object snaps back to the original position as if no constraint was made. To “apply” the constraint, perform Apply Visual Transform
    When driving modes through the Driver Editor, you’ll most likely use Transform Space.
    For some reason, Blender IK does not wholly abide with planar positioning of the joint hierarchy. It either totally flips, which is fortunate since you’ll only need to input fix values such as 90 or 180 degree, or it nudges randomly, of which you have to eyeball. See Appendix for Case Study.

`bpy.context.collection.objects.link(ob) bpy.data.collections[“Collection Name”].objects.link(ob)`


Workflow

    For binding? Select mesh first. Armature second. Then Ctrl+P.
    Adding additional bone? Click the bone tip and extrude (E) it like a mesh. I know! Weird!
    Adding in-between bone? Click the bone and Tool>Subdivide
    Need to make distinction between Pose Mode and Edit Mode
    Snapping on volume. To snap at the center.

#. It’s not joint. It’s a bone. Fudge! Shift+N recalculate roll Controller bones vs bind bones? Alt+P to clear parent. Ctrl+P to parent. You need to check Bone>Connected for it to draw properly

## [Auto Rigging](blender/auto-rigging/)

