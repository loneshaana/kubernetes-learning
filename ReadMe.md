## Learning Kubernates

### what is kubernates?

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

---
## <span style="color:blue;">Kubernetes Overview</span>

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

        1.The Big Picture 
        2.Controller/Manager 
        3. Scheduler 
        4. Node 
        5. Pod 
        6. Api Service

---
## <span style="color:blue;">Benefits and Use Cases</span>

    1. why do we need kubernetes
        Key Container Benefits
            Accelerate Developer On-boarding
            Eliminate App Conflicts
            Environment Consistency
            Ship Software Faster
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

---
## <span style="color:blue;">Kubectl Commands</span>

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

---
## <span style="color:blue;">Pod</span>

    Pod core concepts
    Creating a pod
    kubectl and pods
    yaml fundamentals

---
### <span style="color:blue;">Pod core concepts</span>

    A pod is the basic execution unit of a kubernnetes application-the smallest and simplest unit in the kubernetes object model that you create or deploy.

    Pods run containers
    Environment for containers
    organize applications "parts" into pods(server, caching, api's, database etc)

    Pod IP , memory , volumes , etc, shared accross containers
    pods live and die but never come back to life


    Master node is gonna schedule pods on the  node(worker node)
    our pods can be horizontally scales as well , we can create replica of them and
    kubernates can load balance between those

    if pods goes sick, kubernates monitors that and replaces with  healthy one

    Pods within the node have  the unique ip address and this by defaul will 
    have cluster ips , and then the containers within pod will have their unique ports

    Pod containers have the same loopback network interface
    container processes need to bind to different ports within a pod

    Pods do  not span nodes

---
### <span style="color:blue;">Creating a pod</span>

    1. kubectl run [podname] --image=nginx:alpine 2. kubectl get pods 3. kibectl get all

    As a pod is broguht to life it will get cluster ip address
    kubectl port-forward [name-of-pod] 8080:80 => externalPort:internalPort

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

---
### <span style="color:blue;">Pod Health</span>
    A probe is a diagnostic perfomed periodically by kubelet on a container

    Liveness Probe : liveness probes can be used to determine if a pod is healthy and running as expected

    Readiness Probe: Readiness probes can be used to determine if a pod should receive requests, failed pods containers are recreated by default (restartPolicy defaults to always) when should container receive traffic

    ExecAction - Executes an action inside the container

    TCPSocketAction - TCp check against the containers IP addres on a specified port# kubernetes-learning

---
### <span style="color:blue;">Creating Deployments</span>

    Deployments core concepts
    Creating a deployment
    kubectl and deployments
    Deployment options

    Deployments core concepts:
    A replicaSet is a declarative way to manage pods.
    A deployment is a declarative way to manage pods using a ReplicaSet.
    Deployments and replicaSets ensure pods saty running and can be used to scale pods

    The Role of Replicasets
    ReplicaSets act as a pod controller - Self-healing mechanism - Ensure the requested number of pods are avaiable - provide fault-tolerance - can be used to scale pords - Relies on a pod template - No need to create pods directly - used by deployments

        A deployment manages pods:
            - pods are managed using replicaSets
            - scales replicaSets , which scale pods
            - supports zero-downtime updates by creating and destroying replicaSets
            - provides rollback functionality
            - creates a unique label that is assigned to the replicaSet and generated pods
            - YAML for deployment is very similar to a YAML for replicaSet
                - one difference is a kind property
