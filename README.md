# CarND-Controls-MPC
Self-Driving Car Engineer Nanodegree Program

# Dependencies

* make >= 4.1(mac, linux), 3.81(Windows)              
* gcc/g++ >= 5.4       
* uWebSockets
* Eigen
* Ipopt and CppAD

# The Model

I used geometry and basic physics to build a vehicle model. The specific formula is as follows
$$
\large x_{t+1} = x_t + v_t cos(\psi_t) * dt
$$

$$
\large y_{t+1} = y_t + v_t sin(\psi_t) * dt
$$

$$
\large \psi_{t+1} = \psi_t + \frac {v_t} { L_f} \delta * dt
$$

$$
\large v_{t+1} = v_t + a_t * dt
$$

$$
cte_{t+1} = y_t - f(x_t) + (v_t * sin(e\psi_t) * dt)
$$

$$
e\psi_{t+1} = \psi_t - \psi{des}_t + (\frac{v_t} { L_f} * \delta_t * dt)
$$

# Timestep Length and Elapsed Duration (N & dt)

I tried different length and elapsed Duration combinations,then observe their performance.

In order to ensure that the model can predict a certain accuracy,I find N*dt must be in a certain range.

I thind 0.75 < N*dt < 1.25 is better.I try N =20,dt=0.05 and N=10,dt=0.1.They are doing well.

# Polynomial Fitting and MPC Preprocessing

I converted the coordinate system to the car as the origin,and the x-axis is the direction in which the vehicle travels.This means the car's px = 0, py = 0, and psi = 0.

# Model Predictive Control with Latency

In order to handle the latency, the input is controlled in advance. That is to say, when the time t is, I use the control input at t+t. In this case, it was a t time advance. the advance can offset the latency.