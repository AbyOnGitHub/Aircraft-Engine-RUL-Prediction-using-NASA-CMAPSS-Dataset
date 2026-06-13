# Aircraft-Engine-RUL-Prediction-using-NASA-CMAPSS-Dataset

CMAPSS (Commerical Modular Aero-Propulsion System Simulation) is a software built by NASA to carry out simulations on jet engines. It typically simulates engines in the 90,000 Lb thrust category (Engines GE90s, Rolls-Royce Trent XWBs used in Boeing 777 family and Airbus A350). The dataset prepared tested the Remaining Useful Life (RUL) of modern turbofan engines. An engine was tested under variable conditions with certain degradation like High Pressure Compressor Degradation, Fan Degradation until failure. The aim was to see whether it could be detected when an engine might fail solely using sensor data while it was in running condition. 

The dataset consited 4 .txt training data files - FD001, FD002, FD003, FD004 and 4 .txt testing data files respectively. The true RULs for testing data were provided in separate files. Details of the data are as follows:

Data Set: FD001
Train trjectories: 100
Test trajectories: 100
Conditions: ONE (Sea Level)
Fault Modes: ONE (HPC Degradation)

Data Set: FD002
Train trjectories: 260
Test trajectories: 259
Conditions: SIX 
Fault Modes: ONE (HPC Degradation)

Data Set: FD003
Train trjectories: 100
Test trajectories: 100
Conditions: ONE (Sea Level)
Fault Modes: TWO (HPC Degradation, Fan Degradation)

Data Set: FD004
Train trjectories: 248
Test trajectories: 249
Conditions: SIX 
Fault Modes: TWO (HPC Degradation, Fan Degradation)

Experimental Scenario

Data sets consists of multiple multivariate time series. Each data set is further divided into training and test subsets. Each time series is from a different engine – i.e., the data can be considered to be from a fleet of engines of the same type. Each engine starts with different degrees of initial wear and manufacturing variation which is unknown to the user. This wear and variation is considered normal, i.e., it is not considered a fault condition. There are three operational settings that have a substantial effect on engine performance. These settings are also included in the data. The data is contaminated with sensor noise.

The engine is operating normally at the start of each time series, and develops a fault at some point during the series. In the training set, the fault grows in magnitude until system failure. In the test set, the time series ends some time prior to system failure. The objective of the competition is to predict the number of remaining operational cycles before failure in the test set, i.e., the number of operational cycles after the last cycle that the engine will continue to operate. Also provided a vector of true Remaining Useful Life (RUL) values for the test data.

The data are provided as a zip-compressed text file with 26 columns of numbers, separated by spaces. Each row is a snapshot of data taken during a single operational cycle, each column is a different variable. The columns correspond to:
1)	unit number
2)	time, in cycles
3)	operational setting 1
4)	operational setting 2
5)	operational setting 3
6)	sensor measurement  1
7)	sensor measurement  2
...
26)	sensor measurement  26


Reference: A. Saxena, K. Goebel, D. Simon, and N. Eklund, “Damage Propagation Modeling for Aircraft Engine Run-to-Failure Simulation”, in the Proceedings of the Ist International Conference on Prognostics and Health Management (PHM08), Denver CO, Oct 2008.

Data Cleaning Process:
The datasets provided by NASA were simple .txt files with no column headers, no comma separation and only blank spaces.
With reference to the research paper “Damage Propagation Modeling for Aircraft Engine Run-to-Failure Simulation” the column headers were added and the white spaces were handled in a Pandas dataframe. 

Columns that showed no standard deviation to negligible deviation were dropped. These were either controlled measurements that were kept intentionally constant while taking readings or just ambient data. 

RUL was computed slightly differently as a result of Currect Cycle/Maximum Cycles
Columns that showed least correlation with this were further dropped. 

Model Training:

1) XGBoost:
   Mean Squared Error (MSE): 0.0057
Root Mean Squared Error (RMSE): 0.0752
R-squared (R2) Score: 0.9005
Official PHM08 Challenge Score (Adjusted): 113183.5133

Average Fleet Correlation Score on TEST Data: 0.9688

2) Random Forest Regressor:
Mean Squared Error (MSE): 0.0051
Root Mean Squared Error (RMSE): 0.0716
R-squared (R2) Score: 0.9098
Official PHM08 Challenge Score (Adjusted): 107207.4460
Average Fleet Correlation Score on TEST Data (Random Forest): 0.9724
