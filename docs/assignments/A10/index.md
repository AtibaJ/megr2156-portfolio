# A10 – Lead Screw Translating System


# Group Portfolio: Lead Screw Design

## Leadscrew Sizing, Speed, Torque & Flange Nut Selection (Randy Hoang)

For my part of the project, I focused on sizing the leadscrew drivetrain for our 2kN testing frame. I established our center-to-center span at 150mm (5.91in), worked through the minimum root diameter required to handle the axial load safely, found the motor rotational speed range needed to hit our 1--50mm/min crosshead travel speeds, calculated the peak input torque per screw, and picked out a matching bronze flange nut ([`97790A110`](https://www.mcmaster.com/97790A110/)) from McMaster-Carr so the rest of the team has the exact mounting dimensions for the crosshead and CAD assembly.

<div align="center" style="margin: 20px 0;">
  <figure style="display: inline-block; width: 100%; max-width: 900px; margin: 0 auto;">
    <iframe src="Leadscrew_Hand_Calculations.pdf" width="100%" height="600px" style="border: 1px solid #ccc; border-radius: 4px;">
      <p>Your browser does not support iframes. 
         <a href="Leadscrew_Hand_Calculations.pdf">Download the Hand Calculations PDF instead.</a>
      </p>
    </iframe>
    <figcaption style="font-size: 0.85em; color: gray; margin-top: 8px;">
      Hand Calculations &amp; Free Body Diagrams
    </figcaption>
  </figure>
</div>

### Component Selection & Design Notes
- **Dual-Screw Span & Load Split (Lb=150mm / 5.91in):** Placing the two identical leadscrews at a 150mm center-to-center distance keeps the crosshead compact and prevents beam sagging under load. Running them in parallel splits our 2000N (2kN) total load evenly to P=1000N (224.8lbf) per screw, which keeps the crosshead balanced and prevents binding.
- **Leadscrew Size:** Even though axial stress with a safety factor of 4 only requires a 3.66mm (0.144in) root diameter, going with a standard **$1/2^{\prime\prime}-10$ Acme** single-start steel screw gives us plenty of stiffness over the 18-inch minimum height and pairs easily with standard hardware.
- **Why Part [`97790A110`](https://www.mcmaster.com/97790A110/):** A lot of standard bronze flange nuts on McMaster aren't load-rated, so I went with [**97790A110**](https://www.mcmaster.com/97790A110/) (932 Bearing Bronze, Acme Class 2C) because it is explicitly rated for **1,200lbf dynamic thrust** and **35,000psi tensile strength**. Against our 224.8lbf load per screw, that gives us a real safety factor of 5.34.
- **Self-Locking Lead:** The $1/2^{\prime\prime}-10$ single-start profile has a $0.1^{\prime\prime}$ (2.54mm) lead, meaning the system won't back-drive when the motors stop and only needs $1.26\text{ N}\cdot\text{m}$ of torque per screw at peak load.

<div align="center" style="margin: 20px 0;">
  <figure style="display: inline-block; width: 100%; max-width: 900px; margin: 0 auto;">
    <iframe src="Precision Acme Flange Nut, 1_2_-10 Thread Size _ McMaster-Carr.pdf" width="100%" height="600px" style="border: 1px solid #ccc; border-radius: 4px;">
      <p>Your browser does not support iframes. 
         <a href="Precision Acme Flange Nut, 1_2_-10 Thread Size _ McMaster-Carr.pdf">Download the McMaster-Carr Flange Nut Spec Sheet PDF instead.</a>
      </p>
    </iframe>
    <figcaption style="font-size: 0.85em; color: gray; margin-top: 8px;">
      McMaster-Carr Spec Sheet &amp; Drawing — <a href="https://www.mcmaster.com/97790A110/" target="_blank">Part 97790A110 (932 Bearing Bronze)</a>
    </figcaption>
  </figure>
</div>

---

### Analytical Calculations

1. **Baseline Inputs:**
   - Center-to-center span: Lb=150mm (5.91in)
   - Total axial load: Ptotal=2000N  Load per screw: P=1000N (224.8lbf)
   - Safety factor: ns=4
   - 1060 Steel yield strength: y=380MPa (380106N/m2)
   - Lead ($1/2^{\prime\prime}-10$ Acme): L=0.100in=2.54mm (0.00254m)

2. **Minimum Root Diameter (dr):**
   
allow=yns=380MPa4=95MPa
   
dr4Pallow=4(1000N)(95106N/m2)=0.00366m=3.66mm (0.144in)

3. **Rotational Speed Range (N to N):**
   
N=vL=1mm/min2.54mm/rev=0.39rpm
   
N=vL=50mm/min2.54mm/rev=19.69rpm

4. **Max Input Torque per Screw (T):**
   - With mean diameter dm=d-L2=0.01143m (0.450in) and steel-on-bronze friction f=0.15:
   $$T = \frac{P d_m}{2} \left( \frac{L + \pi f d_m}{\pi d_m - f L} \right) = \frac{(1000\text{ N})(0.01143\text{ m})}{2} \left( \frac{0.00254\text{ m} + \pi(0.15)(0.01143\text{ m})}{\pi(0.01143\text{ m}) - (0.15)(0.00254\text{ m})} \right) = \mathbf{1.26\text{ N}\cdot\text{m}} \ (\mathbf{11.15\text{ in}\cdot\text{lbf}})$$

5. **Flange Nut Safety Factor Check:**
   
ns,actual=1200lbf224.8lbf=5.344.0

---

### Handoff Specs for Crosshead & CAD

| Component | Part & Material | Key Dimensions | Rating | Notes for Crosshead / Assembly |
| :--- | :--- | :--- | :--- | :--- |
| **Leadscrews (x2)** | $1/2^{\prime\prime}-10$ Acme, 1060 Steel | $\varnothing 0.500\text{ in}$ Nominal, 18.0in Long, L=0.100in (2.54mm) | Right-Hand, Single-Start, Class 2C | Spaced Lb=150mm (5.91in) center-to-center |
| **Flange Nuts (x2)** | McMaster [**97790A110**](https://www.mcmaster.com/97790A110/) (932 Bearing Bronze) | Barrel $\varnothing 1.000\text{ in}$, Total Length 1.750in, Flange $\varnothing 2.000\text{ in} \times 0.375\text{ in}$ thick | 1,200lbf Thrust, 35,000psi Tensile | Needs $\varnothing 1.000\text{ in}$ clearance hole in crosshead + custom bolt holes in the 2.000in flange |

---

## Crosshead Design (Noah Nicholson)

<div align="center" style="margin: 20px 0;">
  <figure style="display: inline-block; width: 100%; max-width: 900px; margin: 0 auto;">
    <iframe src="A10CrossheadDesign1.pdf" width="100%" height="600px" style="border: 1px solid #ccc; border-radius: 4px;">
      <p>Your browser does not support iframes. 
         <a href="A10CrossheadDesign1.pdf">Download Crosshead Work.</a>
      </p>
    </iframe>
  </figure>
</div>

### Notes on Work
Given the constraints on the crosshead, I had to find the stress and deflection on the crosshead from the given 2000N load. I found that the minimum thickness to meet the stress requirement was 12.77mm. However, the deflection analysis stated that the minimum thickness would need to be at least 8.94mm. Since the stress analysis yielded a larger minimum thickness, we found that the minimum thickness needed on the crosshead would be 12.77mm. I rounded this number to 15.00mm in the rest of my work as shown.

---

## Bill of Materials / Table Data (Atiba Johnson) 

| Item # | Qty | Name | Cost / Item | Total Cost | Purchase Link |
| :---: | :---: | :--- | :---: | :---: | :--- |
| 1 | 2 | Precision Acme Lead Screw, 1060/Alloy Steel, 1/2"-10 Thread, 2 ft. Long | $65.24 | $130.48 | [Link](https://www.mcmaster.com/6350K61/) |
| 2 | 2 | Precision Acme Flange Nut, 932 Bearing Bronze, 1/2"-10 Thread | $178.60 | $357.20 | [Link](https://www.mcmaster.com/97790A110/) |
| 3 | 4 | T-Slotted Framing Single Rail, 40 mm x 40 mm, 2 ft. Long | $21.15 | $84.60 | [Link](https://www.mcmaster.com/6575N25/) |
| 4 | 8 | T-Slotted Framing Bracket | $7.06 | $56.48 | [Link](https://www.mcmaster.com/5537T937/) |
| **Total** | | | | **$628.76** | |

<script>
  MathJax = {
    tex: {
      inlineMath: [['',''], ['\\(', '\\)']],
      displayMath: [['
','
'], ['\\[', '\\]']]
    }
  };
</script>
<script id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js">
</script>

