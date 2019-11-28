# AWS-RDS-Setup
 # AWS RDS Setup and Access
 ## How to Setup AWS RDS and Access it
 ## Architecture


 ## Step 1: Create an RDS DB Instance
 # Prerequisite
 Before starting this step, you need to have a VPC that contains both public and private subnets with corresponding Security Groups.

 # Launching a MySQL DB Instance
 1. On AWS Management Console, open Amazon RDS Console: https://console.aws.amazon.com/rds/.
 2. From navigation pane choose **Databases** > **Create database**
 ![createDB1](https://user-images.githubusercontent.com/57285863/69810032-50df0000-11eb-11ea-8361-3f7ed54547aa.png)"
 3. Choose **Standard Create** > **MySQL**
 ![createDB2](https://user-images.githubusercontent.com/57285863/69810533-6acd1280-11ec-11ea-8eb0-6b180cba16b6.png)
 4. For **Templates** section, choose **Dev/Test**
 5. For **Settings** section, configure as followed:
    - **DB instance identifier**: tutorial-db-instance
    - **Master username**: tutorial_user
    - **Auto generate a password**: Disable this option
    - **Master password**: choose password then retype the same password to confirm
![createDB3](https://user-images.githubusercontent.com/57285863/69810966-5a696780-11ed-11ea-8da9-f2929aa1e80b.png)
6. In **DB Instance Size**, set these values:
   - DB instance performance type: Burstable
   - DB instance class: db.t2.small
![createDB4](https://user-images.githubusercontent.com/57285863/69811172-cb108400-11ed-11ea-956a-4cd99495bdf9.png)
7. In the **Storage** and **Availability & Durability** section, use the default values
8. In the **Connectivity** section, open the **Additional connectivity configuration** and set these values:
   - **Virtual Private Cloud (VPC)**: choose an existing VPC that you created before with both public and private subnets
   **Important Note**: The VPC must have subnets in different Availability Zone
   - **Subnet group**: the DB subnet group of the chosen VPC
   - **Publicly Access**: Yes
   - **VPC Security Group**: Choose an existing VPC Security Group that is configured for the private access (such as the security group of the Jump Box Web Server workshop). Remove other security groups, such as the default security group, by choosing the **X** associated with each.
   - **Availability Zone**: No Preference
   - **Database port**: 3306
![createDB5](https://user-images.githubusercontent.com/57285863/69813065-bfbf5780-11f1-11ea-866a-b7407f843593.png)
![createDB6](https://user-images.githubusercontent.com/57285863/69813092-ce0d7380-11f1-11ea-9ec7-db1579e403a6.png)
9. Open **Additional Configuration**, enter sample for **Initial database name**. Then keep the rest of the configuraton default.
10. Choose **Create database** to create your Amazon RDS MySQL DB instance. The new DB will appear on the **Databases** list with the status **Creating**

## Step 2: Create an EC2 Instance and Install a Web Server




