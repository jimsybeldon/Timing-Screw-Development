Here is the **full NX roadmap**, rewritten cleanly in **Markdown**, with **explicit toolbar paths** and **step‑by‑step instructions**.  
This version will copy cleanly.

---

# **NX Roadmap: Timing‑Screw Geometry (Swept‑Volume Boolean Subtract)**

## **1. Create the Cutting Tool Body**
You can use any solid shape — a profile, a loft, or an imported STEP.

### **Toolbar Path**
**Menu → Insert → Design Feature → Extrude**  
or  
**Home Tab → Feature Group → Extrude**

### **Steps**
1. Sketch the tool profile  
   - **Home → Sketch**  
   - Draw the 2D cross‑section of your cutting tool.
2. Extrude the sketch into a solid  
   - **Extrude → Direction → Along Z**  
   - Set the thickness to match your tool body.

> Result: A solid cutting tool body.

---

## **2. Create the Target Cylinder (Screw Blank)**

### **Toolbar Path**
**Home → Feature → Cylinder**  
or  
**Insert → Design Feature → Cylinder**

### **Steps**
1. Select **Cylinder**.
2. Pick the origin or any point as the center.
3. Enter:
   - **Radius** = screw blank radius  
   - **Height** = screw length

> Result: A cylindrical blank ready for subtractive swept‑volume cutting.

---

## **3. Create Three Helix Guide Paths**

NX calls these **Helical Curves** or **Spiral Curves**.

---

### **3.1 Standard Helix**

### **Toolbar Path**
**Insert → Curve → Helix**

### **Steps**
1. Set **Type: Helix**  
2. Define:
   - **Pitch** (constant)  
   - **Turns**  
   - **Radius** (constant)  
3. Choose **Axis** = cylinder axis.

> Result: A standard helix curve.

---

### **3.2 Helix with Progressive Lead (Variable Pitch)**

### **Toolbar Path**
**Insert → Curve → Helix → Law‑Controlled Helix**

### **Steps**
1. Set **Type: Law Controlled**.
2. Under **Pitch Law**, choose:
   - **Law Type: Linear** or **Expression**.
3. Define:
   - Start pitch (e.g., 10 mm)
   - End pitch (e.g., 40 mm)

> Result: A helix whose pitch increases along its length.

---

### **3.3 Helix with Increasing Radius**

### **Toolbar Path**
**Insert → Curve → Helix → Law‑Controlled Helix**

### **Steps**
1. Set **Type: Law Controlled**.
2. Under **Radius Law**, choose:
   - **Law Type: Linear** or **Expression**.
3. Define:
   - Start radius (e.g., 40 mm)
   - End radius (e.g., 60 mm)

> Result: A helix whose radius grows along the axis.

---

## **4. Define the Motion Path for the Tool Body**

You can use any of the helix curves as the motion path.

### **Toolbar Path**
**Insert → Motion → Path**

### **Steps**
1. Select **Tool Body** as the moving object.
2. Select **Helix Curve** as the motion path.
3. Set **Orientation Control**:
   - **Tangent** (tool rotates with path)
   - **Fixed** (tool orientation constant)
   - **Law‑Controlled** (advanced)

> Result: A motion definition that NX can use for swept‑volume computation.

---

## **5. Generate the Swept Volume**

This is the key NX feature SolidWorks does not have.

### **Toolbar Path**
**Insert → Design Feature → Swept Volume**

### **Steps**
1. Select **Tool Body** as the “Swept Object.”
2. Select the **Motion Path** (one of your helices).
3. Choose **Motion Type**:
   - **Along Guide**  
   - **Along Guide + Rotation**  
   - **Law‑Controlled Motion**  
4. Preview the swept volume.

> Result: NX computes the exact 3D volume traced by the moving tool body.

---

## **6. Boolean Subtract the Swept Volume from the Cylinder**

### **Toolbar Path**
**Home → Feature → Boolean → Subtract**  
or  
**Insert → Combine → Subtract**

### **Steps**
1. **Target Body** = Cylinder (screw blank)
2. **Tool Body** = Swept Volume
3. Apply the Boolean.

> Result: The timing‑screw geometry is carved into the cylinder.

---

# **7. Optional: Multi‑Helix Combination**
If you want all three helices to contribute:

### **Steps**
1. Create **three separate swept volumes** (one per helix).
2. Combine them:
   - **Home → Boolean → Unite**
3. Subtract the combined volume from the cylinder.

---

# **8. Optional: FK‑Driven Motion (Python → NX)**
If your tool body motion comes from linkage FK:

### Workflow
1. Generate transforms in Python.  
2. Export as a **Motion Table** (CSV).  
3. In NX:
   - **Insert → Motion → From Table**  
4. Use **Swept Volume → Motion Type: Table‑Driven**.

This gives you exact rigid‑body motion, not just curve‑based motion.

---

# **Complete Roadmap Delivered**
This Markdown version will copy cleanly into your notes or project log.

If you want, I can also generate:

- A **Python FK → NX motion table template**  
- A **full NX part‑file workflow**  
- A **timing‑screw parametric generator**  
- A **SolidWorks → NX migration checklist**

Just tell me which direction you want next.