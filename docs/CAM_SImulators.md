You’re asking a *very* sharp question, James — and the answer is **yes**, there *are* public, community‑available CAM simulation environments that can model **full rigid‑body cutter motion**, including:

- arbitrary cutter solids  
- arbitrary tool‑axis rotation  
- FK‑driven transforms  
- helix‑driven translation  
- multi‑axis interpolation  
- swept‑volume visualization  

These are not “cartoon CAD solids.”  
They are **true kinematic simulators** that treat the cutter as a rigid body and simulate material removal.

Below is the **real list** — the ones that actually work for your timing‑screw project.

---

# ⭐ 1. **Open‑Source CAM Simulator: OpenCAMLib (OCL)**  
This is the *closest match* to what you want.

### ✔ Supports arbitrary cutter solids  
### ✔ Supports arbitrary 5‑axis motion  
### ✔ Computes true swept volumes  
### ✔ Used by academic research groups  
### ✔ Free and open source  

OCL is used inside FreeCAD’s Path Workbench and can simulate:

- ball mills  
- lollipop cutters  
- form tools  
- rectangular cutters  
- arbitrary STL cutter bodies  

It also supports:

- 5‑axis toolpaths  
- tool‑axis rotation  
- curve‑driven motion  
- swept‑volume computation  

This is the **only open‑source engine** that can do what NX CAD cannot.

**Search:**  
“OpenCAMLib 5‑axis simulation”  
“FreeCAD Path 5‑axis OCL”

---

# ⭐ 2. **FreeCAD Path Workbench (with OCL)**  
FreeCAD’s CAM module uses OCL for advanced simulation.

### What it can do:
- import your rectangular cutter STL  
- import your helix curve  
- import your FK‑driven orientation vectors  
- simulate the cutter motion  
- visualize the swept volume  
- export the swept volume as a mesh  

This is the closest you’ll get to a **public timing‑screw CAM simulator**.

---

# ⭐ 3. **Blender + CNC Add‑ons (community projects)**  
Blender is not a CAM system, but several community projects use it for:

- rigid‑body cutter motion  
- swept‑volume visualization  
- Boolean subtract of cutter solids  
- animation of toolpaths  

This is useful for **visualization**, not machining.

Search:  
“Blender CNC simulation”  
“Blender CAM add‑on”  
“Blender swept volume animation”

---

# ⭐ 4. **PyCAM (open source)**  
PyCAM is simpler but can:

- simulate cutter motion  
- visualize toolpaths  
- handle custom cutter shapes (limited)  

Not as powerful as OCL, but still useful.

---

# ⭐ 5. **Machine‑Tool Simulators (public demos)**  
These are not open source, but they have **public demo versions** that show:

- full 5‑axis motion  
- arbitrary cutter geometry  
- swept‑volume material removal  

Examples:

### ✔ NCViewer (free online)  
### ✔ CAMotics (free)  
### ✔ Simumill (demo)  
### ✔ ModuleWorks demo videos  
### ✔ Autodesk Fusion 360 simulation (free for hobbyists)

CAMotics is the most accessible:

- supports custom cutters  
- supports multi‑axis motion  
- shows real swept‑volume removal  

---

# ⭐ 6. **Academic research simulators (public papers + code)**  
Several universities publish open‑source or semi‑open simulators for:

- swept‑volume computation  
- 5‑axis cutter kinematics  
- arbitrary cutter geometry  

Search terms:  
“5‑axis swept volume simulation GitHub”  
“rigid body cutter simulation research”  
“toolpath swept volume academic code”

These projects often include:

- Python  
- C++  
- MATLAB  
- OpenGL visualization  

They are extremely close to what you want.

---

# ⭐ 7. **Open‑source robotics simulators (repurposed for CAM)**  
Robotics simulators can model:

- rigid‑body transforms  
- FK motion  
- swept volumes  
- collision detection  

Examples:

### ✔ ROS + MoveIt  
### ✔ Gazebo  
### ✔ PyBullet  
### ✔ Webots  

These can simulate your cutter motion perfectly.  
You simply treat the cutter as a robot end‑effector.

---

# ⭐ Summary — the best options for your timing screw
If you want **true swept‑volume visualization** with a rectangular cutter:

### **Best choice:**  
✔ **OpenCAMLib (OCL)**  
✔ **FreeCAD Path Workbench**  
✔ **CAMotics**  

These are public, free, and capable of:

- arbitrary cutter solids  
- arbitrary tool‑axis rotation  
- helix‑driven motion  
- FK‑driven transforms  
- swept‑volume visualization  

This is exactly what you need.

---

# If you want, I can build you:
- a **Python → OCL pipeline**  
- a **FreeCAD project file** with your cutter and helix  
- a **CAMotics simulation setup**  
- a **Blender animation** of the cutter motion  
- a **full timing‑screw swept‑volume simulator**  

Just tell me which platform you want to use.