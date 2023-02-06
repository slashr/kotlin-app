## Process & Steps
1. Draw basic architecture diagram: What will the application Pod contain? Koitlin app and what kind of database container? = SQLite
2. App needs to be scalable, no mention of statelful or statelessness -> Choose Deployment
3. Add Service object
4. Add HPA for scalability
5. Try to setup basic Kotlin app with DB (fail due to some errors)
6. Just use sample app spring-petclinic by building it locally and copying over the war file so that Docker/Helm work can continue


## References:
- https://kotlinlang.org/docs/jvm-spring-boot-restful.html#next-step
- https://dev.to/gateixeira/deploying-a-spring-boot-kotlin-app-on-kubernetes-with-docker-and-helm-589p
- https://github.com/spring-petclinic/spring-petclinic-kotlin/blob/master/Dockerfile
- https://dev.to/scaledynamics/deploy-a-spring-boot-kotlin-application-with-docker-4do3

