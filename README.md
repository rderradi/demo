Getting Started
---------------
This is a demo project for education/training purposes of DevOps. All the services used below are in the Cloud to facilitate the understanding.
The architecture uses microservices and containerization.

[![Pipeline](https://github.com/fvilarinho/demo/actions/workflows/pipeline.yml/badge.svg?branch=master)](https://github.com/fvilarinho/demo/actions/workflows/pipeline.yml)

The pipeline uses [`GitHub Actions`](https://github.com/features/actions) that contains a pipeline with 4 phases described below:

### 1. Compile, Build and Test
All commands of this phase are defined in `build.sh` file. 
It checks if there are no compile/build errors.
The tools used are:
- [`Gradle`](https://www.gradle.org) - Tool to automate the build of the code.

Environments variables needed in this phase:
- `GITHUB_TOKEN`: API Key used by Sonar client to communicate with GitHub.
- `SONAR_TOKEN`: API Key used by Sonar client to store the generated analysis.

### 2. Packaging
All commands of this phase are defined in `package.sh` file.
It encapsulates all binaries in a Docker image.
Once the code and libraries were checked, it's time build the package to be used in the next phases.
The tools/services used are:
- [`Docker Compose`](https://docs.docker.com/compose) - Tool to build the images.

### 3. Publishing
All commands of this phase are defined in `publish.sh` file.
It publishes the package in the Docker registry (GitHub Packages).
The tools/services used are:
- [`Docker Compose`](https://docs.docker.com/compose) - Tool to push the images into the Docker registry.
- [`GitHub Packages`](https://github.com/features/packages) - Docker registry where the images are stored.

Environments variables needed in this phase:
- `DOCKER_REGISTRY_USER`: Username of the Docker registry.
- `DOCKER_REGISTRY_PASSWORD`: Password of the Docker registry.

### 4. Deploy
All commands of this phase are defined in `deploy.sh` file.
It deploys the package in a K3S (Kubernetes) multi-cloud cluster.
The tools/services used are:
- [`kubectl`](https://kubernetes.io/docs/reference/kubectl/overview/) - Kubernetes Orchestration tool. 
- [`Portainer`](https://portainer.io) - Kubernetes Orchestration Portal.
- [`Linode`](https://www.linode.com) - Cloud (Newark/USA) where the cluster manager is installed.
- [`DigitalOcean`](https://www.digitalocean.com) - Cloud (Frankfurt/Germany) where the cluster worker is installed.

Comments
--------
### If any phase got errors or violations, the pipeline will stop.
### All environments variables must also have a secret with the same name. 
### You can define the secret in the repository settings. 
### DON'T EXPOSE OR COMMIT ANY SECRET IN THE PROJECT.

Architecture
------------
The application uses:
- [`Java 11`](https://www.oracle.com/br/java/technologies/javase-jdk11-downloads.html) - Programming Language.
- [`Spring Boot 2.5.4`](https://spring.io) - Development Framework.
- [`Gradle 6.8.3`](https://www.gradle.org) - Automation build tool.
- [`Mockito 3`](https://site.mockito.org/) - Test framework.
- [`JUnit 5`](https://junit.org/junit5/) - Test framework.
- [`MariaDB`](https://mariadb.com/) - Database server.
- [`NGINX 1.18`](https://www.nginx.com/****) - Web server.
- [`Docker 20.10.8`](https://www.docker.com) - Containerization tool.
- [`K3S 1.21.4`](https://k3s.io/) - Containerization tool.

For further documentation please check the documentation of each tool/service.

How to install
--------------
1. Linux operating system.
2. You need an IDE such as [IntelliJ](https://www.jetbrains.com/pt-br/idea).
3. You need an account in the following services:
`GitHub, Linode, DigitalOcean`.
4. You need to set the environment variables described above in you system.
5. The API Keys for each service must be defined in the UI of each service. Please refer the service documentation.
6. Fork this project from GitHub.
7. Import the project in IDE.
8. Commit some changes in the code and follow the execution of the pipeline in GitHub.

How to run locally
------------------
1. In the project directory, execute the scripts below:
`./build.sh; ./package.sh; docker-compose up`
2. Remember to rename the packages to use your repository id in all YAML and SH files.

How to run in the cloud
-----------------------
1. First, you need to create to find a cloud provider with VPS service (Virtual Private Server).
2. After you provision the VPS and log into, you need to create a Kubernetes cluster using [`k3s`](https://k3s.io). Follow the instructions of the website.
3. Then, install the [`Portainer`](https://portainer.io) to facilitate the deployment. Follow the instructions of the website.
4. Once Portainer is running, just create the namespace and the applications on the cluster.

Other Resources
----------------
- [Official Gradle documentation](https://docs.gradle.org)
- [Spring Boot Gradle Plugin Reference Guide](https://docs.spring.io/spring-boot/docs/2.4.4/gradle-plugin/reference/html/)
- [Spring Web](https://docs.spring.io/spring-boot/docs/2.5.4/reference/htmlsingle/#boot-features-developing-web-applications)
- [Spring Data JPA](https://docs.spring.io/spring-boot/docs/2.5.4/reference/htmlsingle/#boot-features-jpa-and-spring-data)
- [Serving Web Content with Spring MVC](https://spring.io/guides/gs/serving-web-content/)
- [Accessing Data with JPA](https://spring.io/guides/gs/acce****ssing-data-jpa/)

All opinions and standard described here are my own.

That's it! Now enjoy and have fun!

Contact
-------
- LinkedIn: https://www.linkedin.com/in/fvilarinho
- e-Mail: fvilarinho@gmail.com