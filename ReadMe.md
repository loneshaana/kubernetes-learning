1. Learning Kubernates

what is kubernates?
    
TODO:
    Kubernates from a developer perspective
    Creating Pods
    Creating Deployments
    Creating Services
    Understanding Storage Options
    Creating ConfigMaps and Secrets
    Putting it all Together


Kubernetes Overview
The Big picture
Benefits and use case
Running kubernates locally
Getting started with kubectl
Web UI dashboard


1. Kubernetes Overview

Kubernetes(k8s) is an open source system for automating deployment, scaling and management of containerized systems

    Package up an app and let something else manage it for us

    Not worry about management of containers
    eliminate single point of failure
    scale containers
    update container without bringing down the application
    have robest networking 


    Kubernetes acts and orchastrator of nodes
    
    1. Service Discovery/ Load Balancing
    2. Storage Orchestration
    3. Automate Rollouts/ Rollbacks
    4. Self Healing
    5. Secret and configuration Management
    6. ConfigMaps
    7. Horizontal Scaling


The Big Picture
    1. Controller/Manager
    2. Scheduler
    3. Node
    4. Pod
    5. Api Service


Benefits and Use Cases
1. why do we need kubernets

    Key Container Benefits
    1. Accelerate Developer On-boarding
    2. Eliminate App Conflicts
    3. Environment Consistency
    4. Ship Software Faster

    Orchestrate Container
    Zero-Downtime Deployments
    Self Healing
    Scale Containers
    Emulate Production Locally
    Move From Docker Compose to kubernetes
    Create an end-to-end testing environment
    Ensure Application scales properly
    Ensure secrets/config are working properly
    performance testing scenarios
    workload scenarios(ci/cd)





kubectl
    kubectl version
    kubectl cluster-info
    kubectl get all
    kubectl run [container-name] --image [image-name]
    kubectl port-forward [pod] [ports]
    kubectl expose ...
    kubectl create [resource]
    kubectl apply [resource]
    
    
    
    kubectl describe secret -n kube-system




POD
    Pod core concepts
    Creating a pod
    kubectl and pods
    yaml fundamentals



Pod core concepts
     A pod is the basic execution unit of a kubernnetes application-the smallest and simplest unit in the kubernetes object model that you create or deploy.


     Pod run containers
     Environment for containers
     organize applications "parts" into pods(server, caching, api's, database etc)

     Pod IP , memory , volumes , etc, shared accross containers
     pods live and die but never come back to life


     Master node is gonna schedule pods on the  node(worker node)
     our pods can be horizontally scales as well , we can create replica of them and 
     kubernates can load balance between those

     if pods goes sick, kubernates monitors that and replaces with  healthy one


     pods within the node have  the unique ip address and this by defaul will have cluster ips , and then the containers within pod will have their unique ports

    Pod containers have the same loopback network interface
    container processes need to bind to different ports within a pod

    Pods do  not span nodes


Creating  a pod:
    1. kubectl run [podname] --image=nginx:alpine
    2. kubectl get pods
    3. kibectl get all

As a pod is broguht to life it will get cluster ip address
    kubectl port-forward [name-of-pod] 8080:80   => externalPort:internalPort

    kubectl delete pod [name-of-pod]

    #  Delete deployment
    kubectl delete deployment [name-of-deployment]

    k get services


    Perform a trial , create and also validate the yaml
    kubectl create -f file.pod.yml --dry-run --validate=true

    Create a pod from yaml
    will error if pod already exists
    kubectl create -f file.pod.yml


    Alternate way to create and apply changes to a pod from YAML
    kubectl apply -f file.pod.yml


    #use --save-config when you want to use
    #kubectl apply in the future

    kubectl create -f file.pod.yml --save-config( save current properties in the resource configuration)


    kubectl delete -f file.pod.yml


POD Health
 A probe is a diagnostic perfomed periodically by kubelet on a container

 Liveness Probe   : liveness probes can be used to determine if a pod is healthy and     running as expected


 Readiness Probe: Readiness probes can be used to determine if a pod should receive requests, failed pods containers are recreated by default (restartPolicy defaults to always) when should container  receive traffic



 ExecAction - Executes an action inside the container

 TCPSocketAction - TCp check against the containers IP addres on a specified port# kubernetes-learning
