# A CloudFormation Solution

## The Launch Order & Main Resources Created

### 1. vpc.yml

- A VPC with 2 public-private subnet pair in 2 AZ
- Internet Gateway and NAT Gateway
- Route Tables
- A Security Group

## 2. autoscaling-group.yml

- An Auto Scaling Group
- A Target Group for the Load Balancer which will be created in the loadBalancer template

## 3. pipeline-ec2.yml

- A CodePipeline which connects to GitHub
- An S3 bucket to store the built artifact
- A CodeDeploy Application and Deployment Group

## 4. loadBalancer.yml

- A Load Balancer
- A Listener Rule pointing to the Target Group created in the previous template
- A Security Group

## 5. pipeline-s3-cloudfront.yml

- A CodePipeline which connects to GitHub
- A CodeBuild Project with a buildspec which does cache invalidation for CloudFront
- An S3 bucket to store the built artifact
- An S3 bucket to host the website
- A CloudFront with 2 Origins: S3 (website host) and the Load Balancer
- A Record Set

## Solution Highlights

- Deploy an app on an Auto Scaling Group (EC2 instances). Created a Target Group and a Load Balancer for the Auto Scaling Group to direct traffic from CloudFront
- Deploy an app on an S3 bucket
- Continuous delivery: deploy CodePipelines listening to the lastest GitHub commits
- Deploy a CloudFront to distribute the traffic

## References

- Stelligent https://github.com/stelligent/cloudformation_templates/blob/master/labs/spa/pipeline.yml
- How to continuously deploy a static website in style using GitHub and AWS 
  https://medium.com/@kyle.galbraith/how-to-continuously-deploy-a-static-website-in-style-using-github-and-aws-3df7ecb58d9c
- How to Easily Boost the Delivery of Static Websites in AWS
  https://blog.kylegalbraith.com/2018/09/16/how-to-easily-boost-the-delivery-of-static-websites-in-aws/
- AWS official docs
