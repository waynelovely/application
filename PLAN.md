Terraform will be used to establish the AWS infrastructure including:

* an AWS VPC for the resources to live in so the components can communicate with one another
* HTTP and HTTPS load balancers to injest traffic
* AWS ECR to house Docker images of the application
* AWS Fargate to control the autoscaling of the backing EC2 instances which will run the application

Circle CI will be used to establish a hook into the Github repository.

When a commit is push to the repository, Circle CI will run a script to package
the code and update the docker image in AWS ECR.

AWS Fargate will detect this and will launch new EC2 instances to run the update 
application while phasing out traffic to the old instances.
