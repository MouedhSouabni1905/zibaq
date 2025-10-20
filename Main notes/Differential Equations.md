**Tags:** [[Maths]] [[Analysis]]

Differential equations describe **change** not amounts. Solving differential equations is basically figuring out what a function is, based on information about its rate of change. Often when solving differential equations, you will need to find functions whose derivatives and/or higher order derivatives are represented in terms of that function itself (meaning that function is the variable).

Imagine a vector with 2 coordinates. Both coordinates are a function of time. The derivative of that vector is its rate of change, and a new vector. The first vector determines the rate of change of both coordinates (which are functions) through time, and the second in turn determines the rate of change of that. The differential equation is a function of that second vector.

Any system of ordinary differential equations can be described with a vector field. The intuition behind the computation of solutions to differential equations is mainly based on the thought of looking at small regions is space around a fixed point and asking whether the flow tend to contract or expand.

In the context of Ordinary Differential Equations (ODEs), a "phase plane" is a graphical tool used to visualize the behavior of solutions to a system of ODEs. For a two-dimensional system, the phase plane is a plot where the axes represent the two state variables, and the solutions are represented as trajectories or curves in this plane.
# Ordinary Differential equations
They take only one input (variable) which is most often "time".

# Partial Differential equations
Functions that take multiple inputs. Thought of as involving a whole **continuum** of values changing with time.

# Computation
The basic idea is to simulate these equations but instead of taking infinitesimally small steps like in theory, we take finite steps based on the current vector for a small time step.  When done repeatedly, the final destination of this operation is the approximation of the result we're looking for (which is the goal of solving problems using numerical methods as opposed to analytical methods).