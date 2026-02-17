# 🔌 Nonlinear Circuit Analysis Using Newton-Raphson Method (MATLAB)

This project solves a nonlinear electrical circuit using the Newton-Raphson method in MATLAB.

The circuit contains voltage-dependent resistors, making the system nonlinear. The node voltages are calculated iteratively using a Jacobian-based Newton-Raphson update.

---

## 📘 Problem Description

Given:

- Supply Voltage: Vs = 50 V
- R3 = 300 Ω
- Nonlinear Resistors:
  - R1 = 1000(1 + 0.01V1)
  - R2 = 500(1 + 0.02V2)

Using Kirchhoff’s Current Law (KCL) at two nodes, we obtain:

f1 = (Vs - V1)/R1 - (V1 - V2)/R3  
f2 = (V1 - V2)/R3 - V2/R2  

These nonlinear equations are solved using the Newton-Raphson method.

---

## 🧠 Method Used

Newton-Raphson Update Equation:

V_new = V_old - J⁻¹F

Where:
- F = Function vector
- J = Jacobian matrix
- Convergence condition: ||ΔV|| < 1e-6

Maximum iterations = 100

---

## 🛠 MATLAB Code

```matlab
clc;
clear;
Vs = 50;
R3 = 300;
V = [2; 1];
tol = 1e-6;
max_iter = 100;

for k = 1:max_iter

    V1 = V(1);
    V2 = V(2);
    
    R1 = 1000*(1 + 0.01*V1);
    R2 = 500*(1 + 0.02*V2);
    
    % Functions (KCL equations)
    f1 = (Vs - V1)/R1 - (V1 - V2)/R3;
    f2 = (V1 - V2)/R3 - V2/R2;
    
    F = [f1; f2];
    
    % -------- Jacobian Matrix --------
    
    dR1_dV1 = 1000*0.01;
    dR2_dV2 = 500*0.02;
    
    df1_dV1 = (-1/R1) - ((Vs - V1)/R1^2)*dR1_dV1 - (1/R3);
    df1_dV2 = 1/R3;
    
    df2_dV1 = 1/R3;
    df2_dV2 = (-1/R3) - (1/R2) + (V2/R2^2)*dR2_dV2;
    
    J = [df1_dV1  df1_dV2;
         df2_dV1  df2_dV2];
    
    delta = -J\F;
    V = V + delta;
    
    if norm(delta) < tol
        break;
    end
end

fprintf('Converged in %d iterations\n',k);
fprintf('V1 = %.6f V\n',V(1));
fprintf('V2 = %.6f V\n',V(2));
```

---

## 📊 Output

The program displays:

- Number of iterations taken for convergence
- Final values of:
  - V1 (Node 1 voltage)
  - V2 (Node 2 voltage)

---

## 🚀 How to Run

1. Open MATLAB
2. Create a new script file (e.g., `nonlinear_circuit.m`)
3. Paste the code
4. Run the script

---

## 📌 Applications

- Nonlinear circuit analysis  
- Numerical methods implementation  
- Newton-Raphson method practice  
- Power system and electronic simulations  

---

## 👨‍💻 Author

Developed as part of numerical methods and circuit analysis practice.
