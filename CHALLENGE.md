# Process & Steps
1. Draw basic architecture diagram: What will the application Pod contain? Koitlin app and what kind of database container? = SQLite
2. App needs to be scalable, no mention of statelful or statelessness -> Choose Deployment
3. Add Service object
4. Add HPA for scalability
5. Try to setup basic Kotlin app with DB (fail due to some errors)
6. Just use sample app spring-petclinic by building it locally and copying over the war file so that Docker/Helm work can continue
7. Simply copy over the war file into a Docker image and push it to my public DockerHub account for easy testing 
8. Create a simple Helm Deployment template and test the installation of the chart and if it creates a running Pod
9. Extend the Helm templates to also include a Service object and a Prometheus ServiceMonitor object
10. Debug and fix several minor issues with the template syntax, container args etc
11. Add a ArgoCD ApplicationSet relase manifest and test it

# References:
- https://kotlinlang.org/docs/jvm-spring-boot-restful.html#next-step
- https://dev.to/gateixeira/deploying-a-spring-boot-kotlin-app-on-kubernetes-with-docker-and-helm-589p
- https://github.com/spring-petclinic/spring-petclinic-kotlin/blob/master/Dockerfile
- https://dev.to/scaledynamics/deploy-a-spring-boot-kotlin-application-with-docker-4do3

# Problems: 
- Spent a lot of time figuring out why the docker image I built locally on my Mac wouldn't run on a Kubernetes cluster. After trying several permutations and combinations and digging deep inside the system, found out that my Mac M1 was building the image for the arm64 system and not amd64. Fixed by using the `docker build --platform=linux/amd64` flag.
- Scope of the task is quite big. Had to decide where to draw the line in terms of having a multi-layer Docker image that also complies and build the code, adding a helm AlertConfig/PrometheusRule template that can add a feature toggle to enable or disable Prometheus alerts, adding a Github Actions pipeline to demonstrate the CI/CD pipeline etc.
 
# Potential Questions for Discussion
1. What kind of a flow is being used for development? Feature branches, trunk-based?
2. Information on which Ports will be exposed for metrics, API, etc?
3. What other apps can potentially use this setup in the future?
4. What kind of database is required, how exactly does the initialisation of the database take place?
5. What kind of alerts are desired, what kind of metrics should be exposed?
6. What other components would be involved in the app that uses this setup? What auxillary services would the app communicate with?
7. How does the existing Monitoring setup work? In order to design the Prometheus Alerts and Service Monitors
8. Where will the app be deployed? How many clusters? How would different deployments differ from each other and in what way? How often would the releases take place 
