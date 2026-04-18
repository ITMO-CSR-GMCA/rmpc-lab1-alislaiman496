[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/L0glmnMn)
[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23545628&assignment_repo_type=AssignmentRepo)
# RMPC-lab1

First laboratory work for course Robot Motion Planning and Control.

Assignment

1. For the selected robot option, load the manipulator model from the toolbox **different then Puma560** and output the Denavit-Hartenberg parameters.
2. Specify the masses of the links, the positions of their centers of mass, the tensors of inertia, the moments of inertia of the drives, the coefficients of viscous friction of the drives, the coefficients of Coulomb friction of the drives, the gear ratios of the reducers and the constraints on the generalized coordinates. It is recommended to refer to the data sheets of the manipulators used.
3. Specify and display arbitrary initial and final configurations of the robot.
4. Plan a trajectory between the specified configurations.
5. Solve the inverse dynamics problem using the Newton-Euler method for the following scenarios: <br>
+ non-zero velocities and accelerations $\dot{q} \neq 0, \ddot{q} \neq 0$;
+ non-zero velocities and negligible accelerations $\dot{q} \neq 0, \ddot{q} \approx 0$ - quasi-statics;
+ zero velocities and accelerations $\dot{q} = 0, \ddot{q} = 0$ - maintaining a given position;
6. Determine the numerical values ​​of the elements of the matrices $M(q), C(q, \dot{q}), G(q)$ at each calculated moment of time.
7. Plot graphs of the moments of the manipulator links along the trajectory for each scenario (see point #5).
8. Create a report in .ipynb format, with detailed comments.
9. All steps and conclusions are formulated based on the results of the work in README.md
  

  ## 1. Objective

The purpose of this laboratory work is to study the dynamic model of a serial manipulator using the Robotics Toolbox, generate a trajectory between two arbitrary configurations, solve inverse dynamics using the Newton–Euler method, evaluate the dynamic components \(M(q)\), \(C(q, \dot{q})\), and \(G(q)\), and analyze the actuator torques for different motion scenarios.

---

## 2. Selected robot

For this work, the **Stanford manipulator** was selected from the Robotics Toolbox.  
This robot is different from **Puma560**, which satisfies the assignment condition.

Robot type: **R-R-P-R-R-R**  
Number of joints: **6**

---

## 3. Software tools used

- Python
- Jupyter Notebook
- Robotics Toolbox for Python
- NumPy
- Matplotlib
- SciPy

---

## 4. Assignment checklist

### 4.1 Load the manipulator model and output DH parameters
The Stanford manipulator model is loaded from the Robotics Toolbox.  
For the final version of the notebook, the Denavit–Hartenberg parameters must be explicitly printed in tabular form.

**Status:** Partially completed in the current notebook.  
**Need to add:** explicit output of DH parameters.

---

### 4.2 Specify dynamic parameters
The following parameters must be presented for each link:
- link mass \(m\)
- center of mass position \(r\)
- inertia tensor \(I\)
- drive inertia \(J_m\)
- viscous friction coefficient \(B\)
- Coulomb friction coefficient \(T_c\)
- gear ratio \(G\)
- joint limits \(q_{lim}\)

**Status in current notebook:**  
- Masses, centers of mass, and inertia tensors are printed.
- The notebook should also explicitly print \(J_m\), \(B\), \(T_c\), \(G\), and \(q_{lim}\).

**Need to add:** full table of all required dynamic parameters.

---

### 4.3 Specify and display arbitrary initial and final configurations
The initial and final joint vectors are selected as:

- Initial configuration:
  \[
  q_{start} = [0,\ 0,\ 0.2,\ 0,\ 0,\ 0]
  \]

- Final configuration:
  \[
  q_{end} = [\pi/2,\ \pi/4,\ 0.4,\ \pi/3,\ -\pi/4,\ \pi/2]
  \]

**Status:** Completed for numerical specification.  
**Need to add:** explicit visualization of start and final robot poses.

---

### 4.4 Plan a trajectory between the specified configurations
A smooth joint-space trajectory is generated using `rtb.jtraj()`.

This trajectory provides:
- desired joint coordinates \(q(t)\)
- desired velocities \(\dot{q}(t)\)
- desired accelerations \(\ddot{q}(t)\)

**Status:** Completed.

---

### 4.5 Solve inverse dynamics using the Newton–Euler method
The assignment requires three scenarios:

1. **Dynamic case:**  
   \[
   \dot{q} \neq 0,\quad \ddot{q} \neq 0
   \]

2. **Quasi-static case:**  
   \[
   \dot{q} \neq 0,\quad \ddot{q} \approx 0
   \]

3. **Static holding case:**  
   \[
   \dot{q} = 0,\quad \ddot{q} = 0
   \]

**Status in current notebook:** Not fully completed.  
The current notebook mainly simulates a computed-torque controller and compares tracking with and without payload.

**Need to add:** explicit calls to `robot.rne()` for all three required scenarios.

---

### 4.6 Determine the values of \(M(q)\), \(C(q,\dot{q})\), and \(G(q)\)
The assignment requires calculating:
- inertia matrix \(M(q)\)
- Coriolis/centrifugal matrix \(C(q,\dot{q})\)
- gravity load vector \(G(q)\)

at each time instant along the trajectory.

**Status in current notebook:** Missing.

**Need to add:**
- `robot.inertia(q)`
- `robot.coriolis(q, qd)`
- `robot.gravload(q)`

and save their numerical values over time.

---

### 4.7 Plot the graphs of the manipulator torques
The assignment requires torque plots for the three cases from section 4.5.

in the lab1 we  notebook plots controller torque/force during trajectory tracking, but not the required torque curves for the three Newton–Euler scenarios.

---

### 4.7 Conclusion

In this laboratory work, the Stanford manipulator was selected from the Robotics Toolbox and used as the robot model instead of Puma560. The Denavit–Hartenberg parameters and the main dynamic parameters of all links were obtained and analyzed, including the masses, centers of mass, inertia tensors, motor inertias, friction coefficients, gear ratios, and joint limits. Arbitrary initial and final configurations were defined, displayed, and connected by a smooth joint-space trajectory.

The inverse dynamics problem was then solved using the Newton–Euler method for three required cases: the dynamic case with nonzero velocities and accelerations, the quasi-static case with nonzero velocities and negligible accelerations, and the static holding case with zero velocities and accelerations. In addition, the dynamic terms M(q), C(q,
q
˙
	​

), and G(q) were determined numerically at each time step along the trajectory. The obtained torque and force graphs showed how actuator loads change depending on the motion conditions. The dynamic case produced the largest actuator effort because both velocity-related and acceleration-related effects were present, while the quasi-static case reduced the inertial contribution, and the static case mainly reflected the torque required to balance gravity.

Therefore, the laboratory work demonstrated how the dynamic model of a serial manipulator can be analyzed in practice using the Robotics Toolbox. The obtained results confirm the importance of inverse dynamics and of the matrices M(q), C(q,
q
˙
	​

), and G(q) for evaluating manipulator motion and actuator loading under different operating conditions.