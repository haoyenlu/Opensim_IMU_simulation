# Using Opensim to synthesize IMU data from stroke patient's full-body kinematic data

This project explored OpenSim python API to simluate stroke patient motion and synthesizing IMU data. 

The dataset used in this project can be downloaded from here:
https://figshare.com/articles/dataset/A_dataset_of_overground_walking_full-body_kinematics_and_kinetics_in_individuals_with_Parkinson_s_disease/14896881

## Opensim Model

In this project, I provided two model for IMU simulation: **gait2392** and **FullBodyModel**

- **gait2392** is the model provided from official opensim repository but it only contains lower body part and body (no shoulder, arm, and hand)
- **FullBodyModel** is a full body model contains all the important body structure.

FullBodyModel allows us to synthesize IMU data for upper body part but it contains more noise and abnormal magnitude peak. gait2392 has less noise but only for synthesizing IMU of lower body part.


## Pipeline

The pipeline to synthesize IMU data follows:
1. Transform static and trial C3D file to TRC (Opensim Marker file) file given the model type (fullbodymodel or gait2392)
2. Create Opensim Model with markers renamed to the TRC file
3. Scale the model using subject age, height, weight data
4. Append virtual IMU to the model
5. Use Opensim InverseKinematicTool to calculate inverse kinematic of the model using the trial marker TRC file
6. Use Opensim MocoInverse to calculate the solution for virtual IMU signal with the result from inverse kinematic tool
7. Get the IMU signal from the Opensim Table data structure



## Simulation Example
### Inverse Kinematic Result
<p align="middle">
<video src="https://github.com/user-attachments/assets/48dfdba9-0303-45d6-aa2d-d4ce15f02ab4">
</p>
  
### IMU  Signal

<p float="left" align="middle">
  <img src="https://github.com/user-attachments/assets/3ed53104-4c9f-4f29-9046-378aa426b82c" width=40% height=50%>
  <img src="https://github.com/user-attachments/assets/9b0b1cb7-c6ff-4017-a4df-22e0bd461521" width=40% height=50%>
</p>



## Reference:
Shida TKF, Costa TM, de Oliveira CEN, de Castro Treza R, Hondo SM, Los Angeles E, Bernardo C, Dos Santos de Oliveira L, de Jesus Carvalho M, Coelho DB. A public data set of walking full-body kinematics and kinetics in individuals with Parkinson's disease. Front Neurosci. 2023 Feb 16;17:992585. doi: 10.3389/fnins.2023.992585. PMID: 36875659; PMCID: PMC9978741.
