# Structure
### app - Application code and Dockerfile
- This contains the application code which can build locally using gradlew. 
- JAR/WAR artifacts are stored in app/build/libs. 
- For simplicity sake, the Dockerfile only creates a lightweight container that simply runs the JAR artifact. Due to time constraints, I didn't work on using Docker to also build the artifact 

### helm - Helm templates for creating the various Kubernetes resources
- Contains the bare minimum templates for creating k8s resources that can fulfil the Task requirements
- Contains an envs directory which subsequently consists of the three environments described in the challenge along with their respective values.yaml files

### argo - ArgoCD Manifest file specifially ArgoCD ApplicationSet
- The ApplicationSet creates separate Applications based on the number of directories inside /helm/envs- The type of [Generator](https://argocd-applicationset.readthedocs.io/en/stable/Generators-Git/) used is the Git Directories generator which creates unique Applications for each directory found in the specified path. 
- This approach simplifies the requirement of having multiple releases corresponding to each environment. 

# How-To
### Building the Docker image & pushing to your own registry
1. cd app
2. docker build . -t your-private-registry-url:tag
3. docker push your-private-registry-url

### Modifying Configuration using the Helm chart
1. cd helm
2. Inside values.yaml, change the value of `app.image.name` and `app.image.tag` to use your own private Docker image 
3. Similary, change the value of the `dbInitApp.enabled` to true and set appropriate values for the image and command if you want to initialise the database.

# Notes
1. The `helm/templates/prometheus-service-monitory.yaml` can be used to monitor the health of the app and extend to also include custom metrics
