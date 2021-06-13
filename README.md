# Lab 9

In this lab, we will consider new methods for the solution of an ODE initial value problem. The example this time will be a relativistic oscillator. The mass of the oscillator depends on its velocity, thus will change during an oscillation.

In appropriately chosen units, the Hamiltonian becomes
<p align="center">
<img src="stuffy_stuff/p3.png" width="150">
</p>
where p is the momentum and q is the position. Thus, the Hamiltonian equations of motion are
<p align="center">
<img src="stuffy_stuff/ode2.png" width="150">
</p>


Because the motion is nonlinear, the period of the oscillation will depend on the initial amplitude **q(t=0) = q<sub>0</sub>**. This is what we would like to study by numerically solving the equations of motion. You will implement three different methods that you need to compare. Thus, see that you save your results from the three methods into different files.

----

#### Try No. 1: Forward Euler


Our first approach is to use our old (but untrusty) friend *forward Euler* integration, for which we obtain:
<p align="center">
<img src="stuffy_stuff/fwdEuler.png" width="200">
</p>

Although we already have a feeling, that this is no good, implement a program that uses this method to integrate from *t=0* to *t=20* in 50 steps. Let *q0 = 1* and *p0 = 0*. Output all the values (i.e. time, q<sub>n</sub>, p<sub>n</sub>), together with the Hamiltonian after every time step. Have a look in GNUplot what the result looks like.

_Hint_: There is no need for arrays here. You can immediately print the values to the console and redirect to a file, or write into a file directly.  


#### Try No. 2: Symplectic Euler

The symplectic Euler method is new, but only a mash-up of known methods. Our system of ODEs has the form

<p align="center">
<img src="stuffy_stuff/symplEuler1.png" width="75">
</p>

and the idea of the symplectic Euler method is to treat one variable explicitly (i.e. via Euler forward), and the other one implicitly (i.e. via Euler backward). We choose to treat *q* implicitly. This gives:

<p align="center">
<img src="stuffy_stuff/symplEuler2.png" width="250">
</p>

Apply this to our problem and find the equations you have to implement. Make the according changes to your program. Compare your new solution to the one for Euler forward, in particular check out what happened to the Hamiltonian.

#### Try No. 3: Störmer-Verlet

The Störmer-Verlet algorithm is a widely used explicit method for molecular dynamics and there are many ways to motivate this method. We motivate the algorithm in the following way:
1. Advance *q* by half a time step using the current value of
2. Advance *p* by a full step using the intermediate value of *q* from step 1.
3. Advance *q* by another half time step, but now use *p* from step 2.

In formulas:

<p align="center">
<img src="stuffy_stuff/stoermer.png" width="250">
</p>

Change your implementation to this algorithm and check again the Hamiltonian.
