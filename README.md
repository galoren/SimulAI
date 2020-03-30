# SimulAI
SimulAI: Computer-Vision Aided Experimental \&amp; Simulated Hydrodynamic Instabilities Analysis
In fluid dynamics, one of the most important research fields is hydrodynamic instabilities and their evolution in different flow regimes. The investigation of said instabilities is concerned with the highly non-linear dynamics. Currently, three main methods are used for the understanding of such phenomenon - namely analytical models, experiments and simulations - and all of them are primarily investigated and correlated using human expertise. In this work we claim and demonstrate that a major portion of this research effort could and should be analysed using recent breakthrough advancements in the field of Computer Vision with Deep Learning (CVDL or Deep Computer-Vision). Specifically, we target and evaluate specific state-of-the-art techniques - such as Image Retrieval, Template Matching, Parameters Regression and Spatiotemporal Prediction - for the quantitative and qualitative benefits they provide. In order to do so we focus in this research on one of the most representative instabilities, the Rayleigh-Taylor one, simulate its behaviour and create an open-sourced state-of-the-art annotated database RayleAI. Finally, we use adjusted experimental results and novel physical loss methodologies to validate the correspondence of the predicted results to actual physical reality to prove the models correctness.
The techniques which were developed and proved in this work can be served as essential tools for physicists in the field of hydrodynamics for investigating a variety of physical systems, and also could be used via Transfer Learning to other instabilities research. A part of the techniques can be easily applied on already exist simulation results. All models as well as the data-set that was created for this work are availbe in this repository

# RayleAI Database
The first model is the state-of-the-art database - RayleAI. The database contains thresholded images from a simulation of a simple single-mode RTI perturbation with a resolution of 64x128 cells, 2.7cm in x axis and 5.4cm in y axis, while each fluid follows the equation of state of an ideal gas. The simulation input consists of three free parameters: Atwood number, gravity and the amplitude of the perturbation. The database contains of 101,250 images produced by 1350 different simulations (75 frames each) with unique pair of the free parameters. The format of the repository is built upon directories, each represents a simulation execution with the directory name indicating the parameters of the execution.
| Parameter | From | To  | Stride |           
|---------- | ---- | --- | ------ |
| Atwood    | 0.02 | 0.5 | 0.02   | 
| Gravity   | 600  | 800 | 25     |
| Amplitude | 0.1  | 0.5 | 0.1    |
| X         | 2.7  | 2.7 | 0      |
| Y         | 5.4  | 5.4 | 0      |
