# Transfer function GUI for GLFW3

Graphical user interface for transfer function used in volume rendering, originally created by Luiyit Hernandez. Now the interface works with OpenGL 4.5, using shaders.

### Usage

In `TransferFunction.h` include glfw3 and glm header files. In `TransferFunction.cpp` edit the way to load the textures in the `initContext` method, in this case was used [DevIL](http://openil.sourceforge.net/).

In the program initialization: 
```cpp
TransferFunction *g_pTransferFunc = new TransferFunction();   
g_pTransferFunc->InitContext(GLFWwindow *window, int *windowsW, int *windowsH, int posx, int posy);
```
In the glfw3 callback function `MouseButton`:
```cpp
double x, y;   
glfwGetCursorPos(g_pWindow, &x, &y);   
// This method returns a bool depending on whether an event is captured or not
g_pTransferFunc->MouseButton(x, y, button, action); 
```
In the glfw3 callback function `CursorPos`:
```cpp
// This method returns a bool depending on whether an event is captured or not
g_pTransferFunc->CursorPos(x, y); 
```

In the display function:
```cpp
g_pTransferFunc->Display();
```

In the main loop:
```cpp
// Check if the color palette changed
if(g_pTransferFunc->NeedUpdate())    
	UpdatePallete();
// Update the color palette
g_pTransferFunc->SetUpdate(false);
```

Finally, the texture can be bound to an active texture unit with:

```cpp
// Check if the color palette changed
g_pTransferFunc->Use(GL_TEXTURE0);
```

Some functions have been added to load transfer functions from a file and to save the actual transfer function in a file.

[Click here](https://www.youtube.com/watch?v=2ONEKOq4d0U) to see the general characteristics of this GUI in a video.

### Feedback

Pull requests, feature ideas and bug reports are welcome.

### License

MIT.
