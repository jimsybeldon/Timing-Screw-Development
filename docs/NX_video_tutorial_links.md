Here are the **best, directly relevant YouTube‑style videos** that specifically explain **Swept‑Volume + Boolean Subtract in Siemens NX**, based on the search results you asked for. I’m filtering for videos that actually show *swept volume creation* and *Boolean subtract* (the combination you need for timing‑screw / helical‑tool machining simulation).

---

## 🎥 **Most Relevant: Swept‑Volume Tutorials in Siemens NX**
These videos explicitly demonstrate the *Swept Volume* command — the NX feature used to generate the moving tool body before performing Boolean Subtract.

### **1. Create a Swept Volume (NX Tutorial)**  
  [youtube.com](https://www.youtube.com/watch?v=P5aVsX4KFS8)

  
This is one of the clearest demonstrations of the **Swept Volume** feature. Shows how NX computes the volume swept by a moving profile — exactly the precursor to Boolean Subtract for timing screws.

### **2. NX 11 Swept Volume – Tools**  
  [youtube.com](https://www.youtube.com/watch?v=g5i87KITyv8)

  
Short, focused demonstration of swept‑volume creation. Good for understanding the toolpath‑based volume generation.

### **3. NX 11 & Swept Volume**  
  [youtube.com](https://www.youtube.com/watch?v=yOmabwGMQgw)

  
Another concise swept‑volume example. Useful if you want to compare different NX versions’ UI.

### **4. Siemens NX Modeling Tutorials #27 – Swept Volume Command**  
  [youtube.com](https://www.youtube.com/watch?v=FJfrKvUketg)

  
Longer, more detailed walkthrough of the Swept Volume command. Good for understanding parameterization and guide‑curve behavior.

---

## 🎥 **Boolean Subtract (NX) — How the Cutting Operation Works**
These videos focus on **Boolean Subtract**, which is the second half of your workflow: removing the swept tool body from the cylindrical target.

### **5. Siemens NX Boolean Operations (Unite, Subtract, Intersect)**  
  [youtube.com](https://www.youtube.com/watch?v=MRvuBXT4iWw)

  
Shows the mechanics of Boolean Subtract clearly — target vs tool body, intersection requirements, and workflow.

### **6. Siemens NX – Using Unite, Subtract, Intersect**  
  [youtube.com](https://www.youtube.com/watch?v=gM7dibEa--g)

  
Another good demonstration of Boolean Subtract with clear visuals.

### **7. NX 12 Unite, Subtract, Intersect Features Explained**  
  [youtube.com](https://www.youtube.com/watch?v=Sb0vSdpR7yg)

  
Short but clean explanation of Boolean operations.

---

## 🎥 **Swept + Boolean Combined (Closest Match to Timing‑Screw Geometry)**
While NX does not have many videos showing *both* swept‑volume creation *and* Boolean subtract in one workflow, the following is the closest match:

### **8. Swept Volume | Siemens NX 11**  
  [youtube.com](https://www.youtube.com/watch?v=YJteiN7fcrQ)

  
Shows swept volume creation; once you have this body, Boolean Subtract is trivial.

### **9. Siemens NX 1980 – Swept Volume Tutorial**  
  [youtube.com](https://www.youtube.com/watch?v=mP0k3Fr-_pk)

  
Modern NX version; good for matching current UI.

---

## 🧩 **Why these videos matter for your timing‑screw use case**
A timing screw is exactly:

- a **complex tool body**  
- moving along a **helical link path**  
- around a **cylindrical target body**  
- where the **swept volume** of the screw removes material from the cylinder  
- using **Boolean Subtract**

The NX workflow is:

1. **Model the screw profile** (or use a simplified cutting profile).  
2. **Create the helical guide path** (helix around the bottle axis).  
3. **Use Swept Volume** to generate the moving tool body.  
4. **Boolean Subtract** the swept volume from the cylinder.

The videos above cover steps 3 and 4 directly.

---

## If you want, I can also:
- Build you a **step‑by‑step NX workflow** specifically for timing‑screw geometry.  
- Show how to generate the **helical path** correctly (pitch, handedness, bottle spacing).  
- Explain how to avoid **self‑intersection errors** in swept volumes.  
- Provide **parametric NX expressions** for screw pitch, bottle diameter, and dwell zones.

Would you like a **full NX modeling recipe** for a timing screw?