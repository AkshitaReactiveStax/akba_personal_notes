
## Commands
oc login --token=sha256~NMDLK-Xn_WQ6j56VnFP7LSvJ4y8eZOVxyYt9tihjLJY --server=https://api.rm3.7wse.p1.openshiftapps.com:6443


### Use this token directly against the API

curl -H "Authorization: Bearer sha256~NMDLK-Xn_WQ6j56VnFP7LSvJ4y8eZOVxyYt9tihjLJY" "https://api.rm3.7wse.p1.openshiftapps.com:6443/apis/user.openshift.io/v1/users/~"



 oc project akshita2002bajaj15-dev

 oc get pods 

 oc get pod parksmap-1-585br -o yaml

 oc get services

 oc get service parksmap -o yaml

 oc describe service parksmap

-- deployment config(dc)
 oc get dc

-- replication controller(rc)
 oc get rc

 --scaling the application
 oc scale --replicas=2 dc/parksmap

 oc get endpoints parksmap

 oc delete pod parksmap-1-2fp7t && oc get pods

 oc expose service parksmap

 oc get route 

 --logging
 oc logs pod-name
kubectl logs pod-name


 OpenShift API handles this cleanly:
When you run:

     oc logs parksmap-web-12345-abcde


--You’re actually calling OpenShift API.

--OpenShift API talks to Docker daemon (or CRI-O).

--Docker provides the log stream from STDOUT/STDERR.

--You see all your container logs directly.

👉 This is why OpenShift requires applications to log to STDOUT




### to redeploy the application ->

topology -> actions drop-down -> start rollout




### connecting to a container ->

Now you can establish a remote shell session into the pod by using the pod name:


oc rsh parksmap-2-mcjsw

ls /

exit 

oc exec parksmap-2-dhuad -- ls -l /parksmap.jar


oc rsh parksmap-2-mcjsw whoami


oc get builds 


oc delete buildconfig nationalparks-git

oc delete builds nationalpa
rks-git-1


### S2I (Source 2 Image) build  
 oc new-app registry.access.redhat.com/ubi8/openjdk-11~https://github.com/openshift-roadshow/nationalparks.git

oc set triggers dc nationalparks --manual -n workshop


oc whoami --show-server


oc create -f https://raw.githubusercontent.com/openshift-roadshow/nationalparks/master/pipeline/nationalparks-pipeline-all-vfs.yaml -n akshita2002bajaj15-dev


oc get tasks -n akshita2002bajaj15-dev

# Continuous Integration and Pipelines

In this lab you will learn about pipelines and how to configure a pipeline in OpenShift so that it will take care of the application lifecycle.

A continuous delivery (CD) pipeline is an automated expression of your process for getting software from version control right through to your users and customers. Every change to your software (committed in source control) goes through a complex process on its way to being released. This process involves building the software in a reliable and repeatable manner, as well as progressing the built software (called a "build") through multiple stages of testing and deployment.

OpenShift Pipelines is a cloud-native, continuous integration and delivery (CI/CD) solution for building pipelines using [Tekton](https://tekton.dev/). Tekton is a flexible, Kubernetes-native, open-source CI/CD framework that enables automating deployments across multiple platforms (Kubernetes, serverless, VMs, etc) by abstracting away the underlying details.




`Pipeline` is a user-defined model of a CD pipeline. A Pipeline’s code defines your entire build process, which typically includes stages for building an application, testing it and then delivering it.

A `Task` and a `ClusterTask` contain some step to be executed. **ClusterTasks** are available to all user within a cluster where OpenShift Pipelines has been installed, while **Tasks** can be custom.

This pipeline has 4 Tasks defined:

- **git clone**: this is a `ClusterTask` that will clone our source repository for nationalparks and store it to a `Workspace` `app-source` which will use the PVC created for it `app-source-workspace`
    
- **build-and-test**: will build and test our Java application using `maven` `ClusterTask`
    
- **build-image**: will build an image using a binary file as input in OpenShift. The build will use the .jar file that was created and a custom Task for it `s2i-java11-binary`
    
- **redeploy**: it will deploy the created image on OpenShift using the DeploymentConfig named `nationalparks` we created in the previous lab, using the custom Task `redeploy`

 