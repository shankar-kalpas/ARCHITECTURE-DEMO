# System Architecture Overview

In this document, we'll provide an overview of the recommended system architecture for your applications, considering scalability, security, and performance considerations.

# AWS Service Pricing (Estimates)

Here are rough estimates for AWS services used in the architecture:

## Application Components

### Frontend
- The frontend is hosted on AWS Elastic Beanstalk, There is no additional charge for AWS Elastic Beanstalk. Avg: $15 per month. You only pay for what you use, as you use it.
  - Pricing details: [Elastic Beanstalk Pricing](https://aws.amazon.com/elasticbeanstalk/pricing/)

### Backend
- The backend runs on Amazon EC2 instances, with the cost depending on the instance type and usage Avg: $16 per month. 
  - Pricing details: [EC2 Pricing](https://aws.amazon.com/ec2/pricing/)

### Admin Dashboard
- The admin dashboard is hosted on Elastic Beanstalk, with similar costs to the frontend.

### WordPress
- Your WordPress instance on EC2 might cost around $12 per month, but it varies based on instance type and usage.
  - Pricing details: [EC2 Pricing](https://aws.amazon.com/ec2/pricing/)

### DataBase
- AWS RDS automated backups for the MySQL database cost around $25  per month, or we can use the seperate EC2 for the data base which cost $12  per month,.

### Containers
- Docker container costs are associated with the EC2 instances they run on.

## AWS Architecture Diagram (Simplified)


```plaintext
+----------------+       +----------------+        +----------------+
|   Elastic      | ----> |   Amazon RDS   |        |   EC2 (Node.js |
| Beanstalk      |       | (MySQL Database|        |    Backend)    |
| (Next.js Front |       |    Instance)   |        +----------------+
|   End & Admin  |       +----------------+
|    Dashboard)  |       /                \
+----------------+      /                  \
     |                 V                    V
     |        +----------------+    +----------------+
     |        | Self-hosted    |    | Self-hosted    |
     |        | Email Service  |    | SMS Provider   |
     |        |  (Docker)      |    |  (Docker)      |
     |        +----------------+    +----------------+
     |                 \                 /
     |                  \               /
     |                   \             /
     |                    +-----------+
     |                    |   EC2     |
     |                    | (WordPress)|
     |                    +-----------+

```

1. **Regular Backups**
   - Utilize AWS RDS automated backups for the MySQL database.
   - Schedule snapshots for the EC2 instance hosting WordPress.
   - Implement container backup strategies for Docker containers.

2. **Redundancy**
   - Deploy resources across multiple Availability Zones (AZs) for high availability.

## Scaling to 2000 Users Concurrently (Simplified)

1. **Auto-Scaling**
   - Configure auto-scaling for the AWS Elastic Beanstalk environment based on traffic patterns.
   - Manually scale EC2 instances for the backend as needed.

2. **Load Balancing**
   - Implement AWS Elastic Load Balancing (ELB) to distribute traffic for the frontend and admin dashboard.

## Testing Process (Simplified)

- Define a comprehensive testing process that covers unit testing, integration testing, load testing, and security testing.
- Utilize tools and services like Jest, Mocha, Postman, and JMeter based on your specific needs and codebase size.

# Simplified Load Testing Tools

Below is a list of load testing tools along with brief descriptions and pricing information:

1. **Apache JMeter**
   - *Description*: Open-source load testing tool for performance and functional testing.
   - *Pricing*: Free and open-source.

2. **Locust**
   - *Description*: Open-source Python-based load testing tool with code-based test scenarios.
   - *Pricing*: Free and open-source.

3. **Gatling**
   - *Description*: Open-source and scriptable load testing tool in Scala.
   - *Pricing*: Free and open-source.

4. **k6**
   - *Description*: Open-source load testing tool scriptable in JavaScript.
   - *Pricing*: Offers free and paid plans. Pricing details can be found on their [Pricing page](https://k6.io/pricing).

5. **Loader.io**
   - *Description*: Cloud-based load testing platform with free and paid plans.
   - *Pricing*: Pricing details available on the [Loader.io Pricing page](https://loader.io/pricing).


