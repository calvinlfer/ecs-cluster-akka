# ECS Cluster for Akka

This project provides a CloudFormation template which deploys an ECS Cluster which can be used to deploy 
Clustered Akka applications.

# What does it create?

### Container Instances
We create an auto-scaling group that launches ECS Container instances

### Application Load Balancer
We create a single application load balancer for our cluster. The idea is that
each service running in the cluster will leverage path or host based routing with its own Target Group.

Please refer to this AWS Blog [post](https://aws.amazon.com/blogs/devops/introducing-application-load-balancer-unlocking-and-optimizing-architectures/) for more information about this architecture
![Application Load Balancer](![Task Definition Alt](images/Task Definition Alt.png))

#### Security

The template gives you the option of using an SSL certificate on your ALB to securely serve traffic.

It also provides the option to make the ALB `internet-facing` or `internal`

### Scaling Policies and Alarms

We set up scaling policies and alarms to trigger scaling actions on our ECS Cluster

The scaling of the cluster is done using cluster level Memory Reservation metrics


In addition to the above major components, the necessary glue components such as Security Groups
are also created to restrict traffic to the Load Balancer and Container Instances.

# What Makes this Cluster suitable for Clustered Akka Applications?

This cluster comes with [Docker Mirror](https://github.com/LoyaltyOne/docker-mirror) installed on every Container Instance.

Docker Mirror enables nodes in the Akka Cluster to advertise themselves at the correct address for cluster communication.

Please see the following post for a detailed walkthrough of deploying an Akka Cluster on ECS.

TODO: Add blog link

