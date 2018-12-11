# PID Autoscaling Strava's Linkerd Service Mesh Using Prometheus Data
J Evans, Strava @jayeve6 (twitter)

## What is a PID controller?
Proportional Integral Derivative

A controller is any algorithm designed to maintain desired state.

e.g.

setpoint: maintain 80% cpu_util

Process variable: cpu_util

Error: diff between what we want and what we observe

Control variable: what we can change

## PID autoscaling at Strava
 [ this entire portion was done via graphics ]