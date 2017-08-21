![logo](http://libgdx.badlogicgames.com/img/logo.png)
![logo](http://download.blender.org/institute/logos/blender-plain.png)

Blender G3D Exporter
====================

This is an addon for the Blender 3D modeling tool (http://www.blender.org). The purpose of this addon is to allow Blender to export 3D models as G3DJ files (G3D models written as JSON objects).

G3D is a custom 3D model file format compatible with the LibGDX framework (http://http://libgdx.badlogicgames.com/). The format is easy enough to allow use for other frameworks and is powerfull enough to support most features for game development, like multiple materials, multiple textures, different kinds of textures (diffuse maps, normal maps, etc.) and even armature based animations. The specification for this format can be found at [the project's wiki page](https://github.com/libgdx/fbx-conv/wiki) (work in progress).

This addon is currently compatible with Blender v2.76. I can't garantee compatibility with previous or future versions, but I'll try to update it if future Blender updates break compatibility.

This software is licensed under the [GNU General Public License Version 3.0](http://www.gnu.org/licenses/gpl-3.0.txt) (see LICENSE).

### Installation and Usage

Check out the [wiki page](https://github.com/Dancovich/libgdx_blender_g3d_exporter/wiki).

### Features

These are some of the things that get exported by this script:

* Multiple materials for the same mesh (will create multiple mesh parts)
* Diffuse, specular, opacity and shininess material attributes
* Multiple UV coordinates for texture mapping
* Various kinds of texture mappings (diffuse, normal, transparency, specular)
* Armatures
* Multiple bone animations

### About the license

The intention was to make this script licensed under the Apache License v2 (same as LibGDX) until I found out any Python scripts that use the Blender API need to be licensed under the GNU General Public License. The site says they're looking into a way to allow other licenses but until that this software will be licensed under GNU General Public License v3.

Any *.g3dj/.g3db* files exported by this script are considered program output and as such are copyrighted to the user. You are free to use them as you see fit.

**This addon uses Simple UBJSON module for Python**. Simple UBJSON is licensed under the BSD license, copyright information can be found in the LICENSE file contained inside the *simpleubjson* package. The source code was modified to generate binary JSON files that can be read by LibGDX UBJSON reader, this source code modification is permited by the author through the BSD license.

### Changes

* **0.2.7**
  - Fixed bug where having multiple objects use the same mesh data on Blender would result in multiple meshes being exported

* **0.2.6**
  - Fixed crash when using Python version 3.5.2 and up (thanks to thbell for finding and fixing this: https://github.com/thbell).

* **0.2.5**
  - Fixed wrong size of exported COLOR attribute, was exporting 3 floats when LibGDX expect four.

* **0.2.4.1**
  - Ops, changed default log level to INFO again, was set to DEBUG last version.

* **0.2.4**
  - Added option to choose between old format and new format for UBJSON data types (default is old format as in LibGDX, read 'Usage' section).

* **0.2.3**
  - Added exporter option to apply modifiers during export. Original model won't be touched and exported model will be the one after applying modifiers.
  - Support for handling vertices generated after applying modifiers. 
    - Support for correctly applying the Mirror modifier. The mirrored vertices will either inherit the bone weights of the original vertices or if you have mirrored bones (bone.L and bone.R) and the modifier option *Mirror Vertex Groups* is checked the exporter will correctly weight the mirrored vertices to the mirrored bone instead of the original one.
    - Support for correctly applying other modifiers that create vertices like subsurf, solidify and bevel. Generated vertices will inherit bone weights from the original one.

* **0.2.2**
  - Fixed bug where using the same material on more than one mesh caused the exported to export the material multiple times.

* **0.2.1**
  - Overall performance increase in export task.

* **0.2.0**
  - Overall refactoring of the addon. New options should be easier to implement from now on.
  - The exporter now supports both text and binary G3D formats.
  - Added option to convert coordinate systems.
  - Adjusted material exporting to match the ones generated by the FBX-CONV tool.
  - The exporter no longer creates a default material for objects missing one, now a warning message appears when such case occurs.
  - Added option to limit the number of bones per vertex, respecting LibGDX default of 4.
  
* **0.1.0**
  - First release
