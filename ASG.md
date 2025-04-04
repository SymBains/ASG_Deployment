**Step 1: Create a Launch Template**

- Go to the EC2 Dashboard in the AWS Management Console.
- Click on Launch Templates → Create Launch Template.
- Enter a name and optional description.
- Under AMI, select your image
- Choose an instance type (e.g., t2.micro).
- Under Key Pair, select an existing one or create a new SSH key.
- Configure Security Group
- In User Data, enter your startup script

```bash
!/bin/bash
sleep 20
cd /home/ubuntu
cd Sparta-Test-App/app
pm2 start app.js
```

Click Create Launch Template.

**Step 2: Configure an Auto Scaling Group**

- Go to Auto Scaling Groups → Create Auto Scaling Group.
- Enter a name and choose the Launch Template created earlier.

![ASG Setup Screenshot](Images/Screenshot%202025-04-04%20at%2014.56.24.png)

- Select Availiability Zones

![Screenshot](Images/Screenshot%202025-04-04%20at%2014.57.00.png)

- Attach to a new Load Balancer with these settings

![Screenshot](Images/Screenshot%202025-04-04%20at%2014.57.33.png)

- Set target group name and turn on health checks

![Screenshot](Images/Screenshot%202025-04-04%20at%2014.58.12.png)

- Configure Desired Capacity:

![Screenshot](Images/Screenshot%202025-04-04%20at%2014.59.08.png)

- Set up Scaling Policies:
    - Target Tracking → CPU Utilization 50%.

![Screenshot](Images/Screenshot%202025-04-04%20at%2014.59.26.png)

- Click Create Auto Scaling Group.

**Step 4: Verify Deployment**

- Check the Auto Scaling Group for launched instances.
- Verify that instances register in the Target Group.
- Access the app using the Load Balancer DNS name.

![Screenshot](Images/Screenshot%202025-04-04%20at%2015.13.12.png)

**Deleting**

- Delete in this order:
  - Delete LB
  - Delete TG
  - Delete ASG