##	Crime in Vancouver

In this project, we collected crime data records from the Vancouver Open Data Catalogue as instructed by Kaggle.
Th dataset can be forund here: https://www.kaggle.com/wosaku/crime-in-vancouver/data

The original data has 530,652 records from 2003-01-01 to 2017-07-13 with the following features:

#### Data Schema:

Columns:
TYPE, YEAR, MONTH, DAY, HOUR, MINUTE, HUNDRED_BLOCK, NEIGHBOURHOOD, X, Y, LATITUDE, LONGITUDE.

The record consists of 9 different types of crimes in 24 neighborhoods and 21193 street names. 

In this project we train different classifiers on the crime data to identify crimes relating to collisions (Vehicle Collision or Pedestrian Struck with Fatality or Injury) only. 

#### Initial Data Analysis:

**data_analysis.py**

This files provides all the necessary functions to generate initial results from the dataset.

Running the analysis function inside data_analysis.py generates the different types of columns and the different types of criminal activities reported.



#### Data preprocessing
From the 530652 records, we identified 22141 records that are related to collision. We randomly selected 27859 records to create a training set with 50000 records.

The processed data set has the following features:
	
	-	Neighborhood: 0 to 23
	-	Latitude: 49.200896849999999 to 49.31334872
	-	Longitude: -123.223955 to -123.02328940000001
	-	Year: 2003 to 2017
	- 	Month: 1 to 12
	- 	Hour: 0 to 23
	- 	Minute: 0 to 59
	- 	Day of Week: 0 to 6
	- 	Day of Month: 1 to 31

#### Code (Python files)
	- common.py
		main system file that handles packages, logging and debugging purposes
	- process.py
		preprocesses the raw data file and creates a csv with the relevant features for training, validation and testing
	- mapper.py
		since we have mapped some of the string features into integers, the mapper file preserves these features as a csv to be later used for data visualization
	- data_analysis.py
		computes statistics and generates plots for raw and processed data
	- logistic_regression.py
		runs logistic regression


##### How to Run Code
	- Download crime.csv dataset from https://www.kaggle.com/wosaku/crime-in-vancouver/downloads/crime.csv and place it in raw_data folder.
	- Fork or download zip file from this repository.
	- Run all code from the root directory with subdirectories for code and raw_data
	- First run the process.py on the original crime.csv data set in raw_data folder
	- Once process.py is completed, run mapper.py to create a map between the raw data set and features.
	- Run any other ML technique file.


##### Results for Milestone 1
	Logistic Regression
		- Avg accuracy: 0.601822160415
		- Area under roc curve: 0.70335792905

	Decision Tree
		- Train Accuracy ::  0.9437
		- Test Accuracy  ::  0.87695
		-- 10-fold cross-validation --
		- mean: 0.876 (std: 0.007)

##### Results for Milestone 2

	Gaussian Process Classifier
		Running on a complete dataset takes ~10-15 mins

		kernel = gp.kernels.ConstantKernel() + \
				gp.kernels.Matern(length_scale=2, nu=3/2) + \
				gp.kernels.WhiteKernel(noise_level=1)

		Accuracy: 82.30% with entire dataset

		kernel = gp.kernels.RBF(np.ones((X.shape[1], 1))) \
				 * gp.kernels.ConstantKernel() \
			     + gp.kernels.WhiteKernel()	

		Accuracy: 66.00% with 1000 data points


	Support Vector Machines
	        We have used an RBF kernel as well as a linear kernel
		
		RBF Kernel (Max iterations=1000, degree=2):
		- Test Accuracy  ::   0.60577
		-- 10-fold cross-validation --
		- Avg Accuracy: 0.5357
		
		Linear Kernel (Max iterations=auto)
		- Test Accuracy  :: 0.61814764783
		-- 10-fold cross-validation --
		- Avg Accuracy: 0.60192104452 