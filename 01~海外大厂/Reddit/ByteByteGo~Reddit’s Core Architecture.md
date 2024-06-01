# Reddit’s Core Architecture

This information is based on research from many Reddit engineering blogs. But since architecture is ever-evolving, things might have changed in some aspects.

![Reddit’s Core Architecture](https://ngte-superbed.oss-cn-beijing.aliyuncs.com/uPic/qcAsqIzVPGzN.png)

The main points of Reddit’s architecture are as follows:

1. Reddit uses a Content Delivery Network (CDN) from Fastly as a front for the application
2. Reddit started using jQuery in early 2009. Later on, they started using Typescript and have now moved to modern Node.js frameworks. Over the years, Reddit has also built mobile apps for Android and iOS.
3. Within the application stack, the load balancer sits in front and routes incoming requests to the appropriate services.
4. Reddit started as a Python-based monolithic application but has since started moving to microservices built using Go.
5. Reddit heavily uses GraphQL for its API layer. In early 2021, they started moving to GraphQL Federation, which is a way to combine multiple smaller GraphQL APIs known as Domain Graph Services (DGS). In 2022, the GraphQL team at Reddit added several new Go subgraphs for core Reddit entities thereby splitting the GraphQL monolith.
6. From a data storage point of view, Reddit relies on Postgres for its core data model. To reduce the load on the database, they use memcached in front of Postgres. Also, they use Cassandra quite heavily for new features mainly because of its resiliency and availability properties.
7. To support data replication and maintain cache consistency, Reddit uses Debezium to run a Change Data Capture process.
8. Expensive operations such as a user voting or submitting a link are deferred to an async job queue via RabbitMQ and processed by job workers. For content safety checks and moderation, they use Kafka to transfer data in real-time to run rules over them.
9. Reddit uses AWS and Kubernetes as the hosting platform for its various apps and internal services.
10. For deployment and infrastructure, they use Spinnaker, Drone CI, and Terraform.
