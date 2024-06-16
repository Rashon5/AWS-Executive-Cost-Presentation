# Executive Cost Presentation with AWS

![Executive Presentation](https://i.imgur.com/RWpv0Wq.jpeg)
![Infrastructure](https://i.imgur.com/uLA0hcG.png)

## Project Description
In this AWS project, we will need to make an executive presentation to managers and stakeholders to give an idea of the prospective cost of migrating to the cloud from an on-premises data center environment using AWS Pricing Calculator.

Each environment used will have application servers, load balancers, block storage, NFS storage, and Oracle databases.

We will need to estimate how much it would cost for the environment to be migrated to have an idea of return on investment. If decided upon, the company would be in it for the 3-year long haul.

## Video Implementation: 
[![YouTube](https://img.youtube.com/vi/L9v8r0fxlek/0.jpg)](https://www.youtube.com/watch?v=L9v8r0fxlek)

### Part 1: Calculating EC2 (Production Stage and Development/Testing)
We’ll continue to reference the picture above. We’ll start by creating the EC2 Production environment.

Navigate to [AWS Pricing Calculator](https://calculator.aws/#/) in order to access the AWS Pricing Calculator and click on ‘Create estimate’.

In ‘Find service’ search for Amazon EC2 and click on Configure ![EC2 Configure](https://i.imgur.com/DJkAKHk.png)

Once in Configure we will keep the same Region consistent for each one of these services we configure.
As we reference the picture at the top we will need to configure 2 EC2 configurations shown below as well:

#### EC2 (Production)
- 5 Instances
- 8 vCPUs 16GB RAM
- 2TB Block Storage (EBS)

#### EC2 (Stage Development/Testing)
- 5 Instances (3 Stage + 2 Development/Testing)
- 1.5TB Block Storage (1TB Stage + 500GB Development/Testing)

Starting with the EC2 Production configuration give this a Description to differentiate all the estimates created. Choose a region that will stay static for each configuration we’ll keep it at US East (Ohio). ![Region](https://i.imgur.com/0H27WWY.png)

Scroll down to where it says ‘Number of instances’ of which we want 5 then in the ‘EC2 Instance (709)’ area specify the number of vCPUs and Memory (GB) required which in this case is 8 vCPUs and 16GB RAM. Once done we can see what is recommended. ![vCPUs and Memory](https://i.imgur.com/Y5v0gWu.png)

The ‘c6a.2xlarge’ instance gives us the desired vCPUs and Memory needed with more network speed than the ‘t4g.2xlarge’ instance with more memory. If network performance isn’t a bottleneck we could opt to go for the cheaper version with more memory but we’ll settle with the ‘c6a.2xlarge’ instance.

Down to ‘Payment options’ we will stick with the Compute Savings Plan the whole way where taking on the 3-year reservation term will result in more savings as well as if we pay some money upfront. In this case we’ll stick with no upfront. ![Payment Options](https://i.imgur.com/s5ekzLL.png)

Down to Amazon Elastic Block Store (EBS) set Storage for each EC2 instance to ‘General Purpose SSD (gp2) and since 2TB of block storage is needed total across 5 instances we can set the Storage amount to 400GB (400GB * 5 Instances = 2TB) ![EBS](https://i.imgur.com/RlBN91n.png)

Once that’s done click on the yellow button ‘Save and add service’.

Create another EC2 configuration for ‘EC2 Stage Dev/Testing.’ Since the same number of vCPUs and RAM is needed for both Stage and Development/Testing we will combine these. Set it up like so below:

#### EC2 (Stage - Dev/Test)
- Instances: 5 (3 Stage + 2 Dev/Test)
- 4 vCPUs 8GB RAM - t4g.xlarge
- Compute Savings Plan 3 Year No upfront
- 300GB SSD gp2 (1TB + 500GB = 1.5TB)

### Part 2: Calculating Elastic Load Balancers
Next find the Elastic Load Balancing service by typing ELB and ‘Configure’. Keep ‘Application Load Balancer’ checked and increase the number of load balancers to 3.

When getting to ‘Load Balancer Capacity Units (LCUs)’ set ‘Processed bytes (EC2 Instances and IP addresses as targets)’ to 2GB per hour and set the value to 100 for ‘Average number of requests per second per ALB’ and ‘Average number of rule evaluations per request.’ Save and add service. ![ELB](https://i.imgur.com/tod2NHB.png)

### Part 3: Calculating EFS
Search for the EFS service and Configure. Set the ‘Desired Storage Capacity’ to 1750GB per month and then save and add. That combines the NFS storage shown for Production Stage and Development/Testing (1TB + 500GB + 250GB = 1.75TB/1750GB) ![EFS](https://i.imgur.com/0n8XfLg.png)

### Part 4: Calculating RDS for Oracle
We’ll need to do this three different times: one for Production, one for Stage, and one for Development/Testing to use RDS to house Oracle databases. For the Production databases, we’ll need to have 2 instances with at least 38 vCPUs and 156GB RAM and 3TB total storage.

Search for ‘RDS for Oracle’ and Configure. Set the RDS for Oracle instances to 2. The db.m5.12xlarge instance gives us 48 vCPUs and 192GB RAM which is closest to what we need. The db.m6i.12xlarge does the same thing and is slightly cheaper. Both instances would need to be researched to check the pros and cons.

In Storage set the Storage amount to 1500GB (3TB / 2 Instances) and the Backup Storage to 3000GB. ![RDS Storage](https://i.imgur.com/L8G797m.png) ![Backup Storage](https://i.imgur.com/ojKy4Vo.png)

Repeat the same procedure for the Stage and Development/Testing RDS for Oracle instances.

### Part 5: Adding Support Plan
On the Add service page click the yellow ‘View summary’ button to see the current progress and overview of services that were added to the estimate. Support service will now have to be added. Click on the yellow ‘Add service’ button. ![Support Plan](https://i.imgur.com/lkwenr6.png)

On this page, it will ask for ‘Technical support levels’ and ‘Technical support response time.’ The former asks what level of accessibility is required. The latter asks what is the maximum allowable response time after reaching out for support. We will select the choices that give us the fastest response times which will lead us into choosing the ‘Enterprise support plan.’ After selection click on ‘Add to my estimate.’

### Part 6: Presentation of Cost Analysis
Now that we have our estimate we want to externally analyze it in order to get a breakdown of our potential costs from each individual service. Click on ‘Export’ and download the CSV of the estimate. The repository has a PowerPoint at [___ExecutiveCostPresentationwithAWS.pptx](https://github.com/Rashon5/AWS-Executive-Cost-Presentation/blob/main/___ExecutiveCostPresentationwithAWS.pptx) which will have the template of how we’ll display those costs.

Open the downloaded CSV and the columns to look for are Service, Monthly, and First 12 months. We want to format those cells to show them as dollar values and see what our cost will be. ![CSV](https://i.imgur.com/mEbVpgb.png)

Navigate to the PowerPoint and on the second slide click on the pie graph go up to ‘Chart Design’ and click on ‘Edit data’ to adjust the data. ![Chart Design](https://i.imgur.com/hWp09NO.png)

Now we can copy and paste the monthly cost from the CSV into the small spreadsheet within PowerPoint after clicking on ‘Edit data.’ ![Edit Data](https://i.imgur.com/oJKcJL2.png)

Once done the pie graph will update and don’t forget to manually edit the total. For slide 3 in the PowerPoint do the same for the ‘First 12 months’ column on the CSV and have it reflect on that slide. ![First 12 months](https://i.imgur.com/i6340C7.png)

There it is! Now upon the presentation, your management will know the cost to migrate to the AWS cloud along with adjustments and compromises that they might want to do. Since the Enterprise support plan is quite expensive that’s where the adjustments may be made.
