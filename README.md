# VisualShaderImportToGodot4Bug
Minimal Project showcasing a bug in the import of Visual Shaders

# Bug Description

It appears that under certain conditions, the import of a Visual Shader attached to a node in a Godot 3.5.1 project causes an error in the conversion.

It appears that the issue lies with the fact that in Godot 3, Texture offered both a "Color" and "Alpha" output, whereas in Godot 4, the latter is considered a component of the former (which makes perfect sense). Because of this, any connection from the "Alpha" output is now lost and, worse, there seems to be an error (see below). The error message seems to suggest that it tries to connect the second (index=1) port, which was "Alpha" beforehand, which no longer exists.

```
  scene/resources/visual_shader.cpp:723 - Condition "g->nodes.has(p_id)" is true.
  scene/resources/visual_shader.cpp:723 - Condition "g->nodes.has(p_id)" is true.
  scene/resources/visual_shader.cpp:723 - Condition "g->nodes.has(p_id)" is true.
  scene/resources/visual_shader.cpp:723 - Condition "g->nodes.has(p_id)" is true.
  scene/resources/visual_shader.cpp:970 - Index p_from_port = 1 is out of bounds (g->nodes[p_from_node].node->get_expanded_output_port_count() = 1).
```

Here are screenshots of the Visual Shaders as they appear. In the Godot 4-screenshot, I have moved the Nodes slightly to ensure they fit the screenshot, their positions were as imported (just their size is now different)

Godot 3.5.1:
![VS_G3](https://user-images.githubusercontent.com/58372501/219147561-52ab6dca-30a5-4021-b55b-9aed73ffb372.PNG)

Godot 4, RC2:
![VS_G4](https://user-images.githubusercontent.com/58372501/219147625-2122b5a3-f84d-420b-9446-7fadfc1a9afd.PNG)

