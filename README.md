# glue_project - STEDI-Human-Balance

## Project Overview

### Project Introduction

In this project, we aim to build a data lakehouse solution for the STEDI team, specifically focusing on sensor data to train a machine learning model. The STEDI Step Trainer, equipped with sensors, aims to train users in balance exercises while collecting data to enhance a machine-learning algorithm for step detection. The project also involves a companion mobile app that collects customer data and interacts with the device sensors.

### Project Details

The hardware STEDI Step Trainer collects data through motion sensors, and the companion mobile app collects data using a mobile phone accelerometer. The objective is to use this motion sensor data to train a machine learning model capable of real-time step detection. Privacy is a primary concern, and only data from customers who have agreed to share their information for research purposes should be used in the training data.

### Project Summary

As a data engineer on the STEDI Step Trainer team, the goal is to extract data from the Step Trainer sensors and the mobile app, curate this data into a data lakehouse solution on AWS, allowing Data Scientists to train the machine learning model.

## Project Data

### Customer Records

**Data Source:** [Customer Record](https://github.com/HiteshBhagwani/glue_project/tree/d4eee3c9d953a28a8151743e2f06291f04e7b3b4/Data/customer/landing)

**Fields:**

-   serialnumber
-   sharewithpublicasofdate
-   birthday
-   registrationdate
-   sharewithresearchasofdate
-   customername
-   email
-   lastupdatedate
-   phone
-   sharewithfriendsasofdate

### Step Trainer Records

**Data Source:** [Step Trainer Records](https://github.com/HiteshBhagwani/glue_project/tree/d4eee3c9d953a28a8151743e2f06291f04e7b3b4/Data/step_trainer/landing)

**Fields:**

-   sensorReadingTime
-   serialNumber
-   distanceFromObject

### Accelerometer Records

**Data Source:** [Accelerometer Records](https://github.com/HiteshBhagwani/glue_project/tree/d4eee3c9d953a28a8151743e2f06291f04e7b3b4/Data/accelerometer/landing)

**Fields:**

-   timeStamp
-   user
-   x
-   y
-   z

## Implementation

### Landing Zone

**Glue Tables SQL DDL**:

 -   [customer_landing.sql](https://github.com/HiteshBhagwani/glue_project/blob/d4eee3c9d953a28a8151743e2f06291f04e7b3b4/scripts/customer_landing.sql)
 -   [accelerometer_landing.sql](https://github.com/HiteshBhagwani/glue_project/blob/d4eee3c9d953a28a8151743e2f06291f04e7b3b4/scripts/accelerometer_landing.sql)
 -  [step_trainer_landing.sql](https://github.com/HiteshBhagwani/glue_project/blob/d4eee3c9d953a28a8151743e2f06291f04e7b3b4/scripts/step_trainer_landing.sql)

**Athena Landing Zone Data Query**

 - `customer_landing` table:
![customer_landing](https://github.com/HiteshBhagwani/glue_project/blob/d4eee3c9d953a28a8151743e2f06291f04e7b3b4/images/customer_landing.jpg)

 - `accelerometer_landing` table:
![accelerometer_landing](https://github.com/HiteshBhagwani/glue_project/blob/d4eee3c9d953a28a8151743e2f06291f04e7b3b4/images/accelerometer_landing.jpg)

### Trusted Zone

**Glue job scripts**:

-   [customer_landing_to_trusted.py](https://github.com/HiteshBhagwani/glue_project/blob/d4eee3c9d953a28a8151743e2f06291f04e7b3b4/scripts/customer_landing_to_trusted.py)
-   [accelerometer_landing_to_trusted_zone.py](https://github.com/HiteshBhagwani/glue_project/blob/d4eee3c9d953a28a8151743e2f06291f04e7b3b4/scripts/accelerometer_landing_to_trusted.py)

**Athena Trusted Zone Data Query**
 - `customer_trusted` table:
![customer_trusted](https://github.com/HiteshBhagwani/glue_project/blob/d4eee3c9d953a28a8151743e2f06291f04e7b3b4/images/customer_trusted.jpg)

 - `accelerometer_trusted` table:
![accelerometer_trusted](https://github.com/HiteshBhagwani/glue_project/blob/d4eee3c9d953a28a8151743e2f06291f04e7b3b4/images/accelerometer_trusted.jpg)

## Curated Zone

**Glue job scripts**:
- [customer_trusted_to_curated.py](https://github.com/HiteshBhagwani/glue_project/blob/d4eee3c9d953a28a8151743e2f06291f04e7b3b4/scripts/customer_trusted_to_curated.py)
- [machine_learning_curated.py](https://github.com/HiteshBhagwani/glue_project/blob/d4eee3c9d953a28a8151743e2f06291f04e7b3b4/scripts/machine_learning_curated.py)

**Athena Curated Zone Data Query**
- `machine_learning_curated` table:
![machine_learning_curated](https://github.com/HiteshBhagwani/glue_project/blob/d4eee3c9d953a28a8151743e2f06291f04e7b3b4/images/machine_learning_curated.jpg)
