# AWS-RDS-Setup
 # AWS RDS Setup and Access
 ## How to Setup AWS RDS and Access it
 ## Architecture


 ## Step 1: Create an RDS DB Instance
 # Prerequisite
 Before starting this step, you need to have a VPC that contains both public subnets with corresponding Security Groups.
 Also, make sure that the Security Group that will be used also contains the Inbound rule for port 3306 which is the port for MySQL Database.
 - On VPC > Security Group
 - Select the Security Group that you will use for this exercise
 - On the tab **Inbound Rules** add new rule for **Custom TCP Rule**, **Port Range** is **3306**, **Source** is **Anywhere**. Then, **Save**. This new Inbound Rule will be create
 ![SG_MySQL](https://user-images.githubusercontent.com/57285863/70044255-50b37b80-15c2-11ea-982d-6d971b39aa39.png)

 # Launching a MySQL DB Instance
 1. On AWS Management Console, open Amazon RDS Console: https://console.aws.amazon.com/rds/.
 2. From navigation pane choose **Databases** > **Create database**
 ![createDB1](https://user-images.githubusercontent.com/57285863/69810032-50df0000-11eb-11ea-8361-3f7ed54547aa.png)"
 3. Choose **Standard Create** > **MySQL**
 ![createDB2](https://user-images.githubusercontent.com/57285863/69810533-6acd1280-11ec-11ea-8eb0-6b180cba16b6.png)
 4. For **Templates** section, choose **Free tier**
 5. For **Settings** section, configure as followed:
    - **DB instance identifier**: tutorial-db-instance
    - **Master username**: admin
    - **Auto generate a password**: Disable this option
    - **Master password**: choose password then retype the same password to confirm
![createDB3](https://user-images.githubusercontent.com/57285863/69810966-5a696780-11ed-11ea-8da9-f2929aa1e80b.png)
6. In **DB Instance Size**, set these values:
   - DB instance performance type: Burstable
   - DB instance class: db.t2.micro
![DBcreateNew2](https://user-images.githubusercontent.com/57285863/70054100-24eec080-15d7-11ea-90a0-df26377c9a5b.png)
7. In the **Storage** and **Availability & Durability** section, use the default values
8. In the **Connectivity** section, open the **Additional connectivity configuration** and set these values:
   - **Virtual Private Cloud (VPC)**: choose an existing VPC that you created before with public subnets or creating new one. For this workshop, you need to be able to access the database publicly therefore make sure to have the internet connection on your security group
   **Important Note**: The VPC must have subnets in different Availability Zone
   - **Subnet group**: the DB subnet group of the chosen VPC
   - **Publicly Access**: Yes
   - **VPC Security Group**: Choose an existing VPC Security Group that is configured for the private access (such as the security group of the Jump Box Web Server workshop). Remove other security groups, such as the default security group, by choosing the **X** associated with each.
   - **Availability Zone**: No Preference
   - **Database port**: 3306
![DBcreateNew1](https://user-images.githubusercontent.com/57285863/70053964-e0fbbb80-15d6-11ea-8d7b-92a1bac5bf0c.png)
![DBcreateNew3](https://user-images.githubusercontent.com/57285863/70054038-04266b00-15d7-11ea-9e1a-a0c3de546871.png)
9. Open **Additional Configuration**, enter sample for **Initial database name**. Then keep the rest of the configuraton default.
10. If you get an error that the database cannot be created because your VPC chosen doesn't support DNS/Hostname resolution, please follow these steps:
   - Go to VPC page and select the VPC that you used. Then, Actions > Edit DNS resolution
   - Make sure **DNS resolution** is Enable
![EditDNSresol](https://user-images.githubusercontent.com/57285863/70037898-9fa7e380-15b7-11ea-860c-ddf2b9a9447c.png)
   - Then, Actions > Edit DNS Hostnames, make sure **DNS hostname** is Enable
![EditDNShostname](https://user-images.githubusercontent.com/57285863/70038015-dbdb4400-15b7-11ea-858f-cb87e8fbd2f7.png)
11. Choose **Create database** to create your Amazon RDS MySQL DB instance. The new DB will appear on the **Databases** list with the status **Creating**
12. Wait until your new database is completely finished (status is "Available") creating before connecting to it.
13. Click on the newly created database to get the following details for connection:
   - **Endpoint**: in this exercise, **tutorial-db-instance.cmwix84nntpy.us-east-1.rds.amazonaws.com**
   - **Port**: 3306
![newDB](https://user-images.githubusercontent.com/57285863/70038549-b569d880-15b8-11ea-9369-79b9d4fab28f.png)
![Dbdetails](https://user-images.githubusercontent.com/57285863/70038437-82bfe000-15b8-11ea-9c36-742dfa5464d1.png)

## Step 2: Test the connection to the new AWS RDS Database using MySQL Workbench
1. Download MySQL Workbench from: https://www.mysql.com/products/workbench/
![MySQLWorkbench1](https://user-images.githubusercontent.com/57285863/70038728-08439000-15b9-11ea-9728-9cc451d7eda3.png)
2. Install MySQL Workbench on your local computer.
3. Launch MySQL Workbench > Welcome page > Click the **+** sign next to **MySQL Connections**
4. On the **Setup New Conection** window, enter the following details:
   - **Connection Name**: choose any name that corresponds to the exercise, for example **AWS RDS DB Connect**
   - **Hostname**: enter the Endpoint details of the AWS RDS DB from step above, for example **tutorial-db-instance.cmwix84nntpy.us-east-1.rds.amazonaws.com**
   - **Port**: enter port **3306** for MySQL DB connection
   - **Username**: enter the **Master username** from above step, in this case, **admin**
   - **Password**: click on Store in Vault and enter the password for DB from above step
   - Then click **Test Connection**
![MySQLWorkbench2](https://user-images.githubusercontent.com/57285863/70039628-8bb1b100-15ba-11ea-94a9-a291860e2611.png)
5. You should get the message **Successfully made the MySQL connection** message which indicates that you can successfully connect to the AWS RDS Database.
![DBConnectSuccess](https://user-images.githubusercontent.com/57285863/70044441-ab4cd780-15c2-11ea-807f-c2b81cdb18c3.png)
6. From here, you can work on your database hosted on AWS RDS.
![MySQLWorkbench4](https://user-images.githubusercontent.com/57285863/70044572-e949fb80-15c2-11ea-864c-5cc4db93eaa8.png)

## Step 3: Connect to the AWS RDS Database using Python
1. For this step you can either create a new Linux instance on AWS and run the python commands there. Or you can also do this on your local PC.
2. Open jupyter notebook or any Python terminal
3. Enter the following script in the jupyter notebook
> **_NOTE:_** 
> # Install pymysql package 
> pip install pymysql


