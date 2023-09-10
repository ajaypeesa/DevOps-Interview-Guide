# Kubernetes Architecture Interview Questions for DevOps

## 1. **Describe the main components of Kubernetes architecture.**

- **Answer**: 
  - **Control Plane (Master) Components**: These make global decisions about the cluster (e.g., scheduling). Key components include:
    - **kube-apiserver**: Serves the Kubernetes API and is the entry point for commands.
    - **etcd**: Consistent and highly-available key-value store for all cluster data.
    - **kube-scheduler**: Watches for newly created pods and assigns them to nodes.
    - **kube-controller-manager**: Regulates controllers that handle different aspects of the cluster.
    - **cloud-controller-manager**: Interacts with underlying cloud providers.
  - **Node Components**: These run on every node and maintain running pods.
    - **kubelet**: Ensures the containers are running in a pod.
    - **kube-proxy**: Maintains network rules for pod communication.
    - **Container runtime**: Software responsible for running containers (e.g., Docker, containerd).

## 2. **What role does `etcd` play in Kubernetes?**

- **Answer**: `etcd` is a consistent and highly-available key-value store used as Kubernetes' backing store for all cluster data. It stores the configuration data of the cluster, representing the overall state of the cluster at any given point in time.

## 3. **How does the `kube-scheduler` decide where to place a pod?**

- **Answer**: The `kube-scheduler` ranks available nodes for the pod and places it on the best one based on multiple criteria, such as resource requirements, hardware/software/policy constraints, affinity and anti-affinity specifications, and more.

## 4. **Explain the role of a `kubelet` on a node.**

- **Answer**: `kubelet` is an agent that runs on each node in the cluster. It ensures that containers are running in a Pod. It takes a set of PodSpecs (provided as `.yaml` files) and ensures the described containers are running and healthy.

## 5. **Describe the purpose of `kube-proxy` in the Kubernetes architecture.**

- **Answer**: `kube-proxy` is a network proxy that runs on each node in the cluster. It maintains network rules for Pod communication, allowing communication inside or outside of the cluster.

## 6. **How does Kubernetes achieve high availability?**

- **Answer**: Kubernetes achieves HA by:
  - Running multiple replicas of the control plane components across different nodes.
  - Using services like `etcd` in a distributed mode.
  - Using a load balancer to distribute traffic to API servers.
  - Replicating application pods across different nodes.

## 7. **What's the difference between a `Controller` and an `Operator` in Kubernetes?**

- **Answer**: 
  - **Controller**: It's a loop that drives the current state towards the desired state in Kubernetes. Controllers handle different aspects like nodes, endpoints, etc.
  - **Operator**: It's a method of packaging, deploying, and managing a Kubernetes application. Operators use the Kubernetes' extensibility to handle the entire lifecycle of complex applications.

## 8. **How do `DaemonSets` differ from `Deployments` and `StatefulSets`?**

- **Answer**:
  - **DaemonSet**: Ensures a copy of a pod runs across all (or some) nodes in the cluster.
  - **Deployment**: Manages stateless applications, maintaining a specified number of pod replicas.
  - **StatefulSet**: Manages stateful applications, ensuring a specific ordering and uniqueness to pods.

## 9. **What is the role of the `Namespace` in Kubernetes architecture?**

- **Answer**: Namespaces are a way to divide cluster resources between multiple users or teams. They provide a scope for names and can be used to allocate resources and set access controls on parts of the cluster.

## 10. **How does Kubernetes handle storage orchestration?**

- **Answer**: Kubernetes uses `Persistent Volumes (PV)` and `Persistent Volume Claims (PVC)` for storage orchestration. PVs are cluster-wide resources that abstract the underlying storage infrastructure, while PVCs are requests for those resources. Storage can be automatically provisioned using StorageClasses.

- These questions probe into the architectural understanding of Kubernetes. A candidate's answers will give insights into their depth of experience and knowledge regarding Kubernetes' workings, especially from an architectural viewpoint.

---
# Kubernetes Interview Questions for DevOps

## 1. **What is Kubernetes, and why is it used?**

- **Answer**: Kubernetes is an open-source platform designed to automate deploying, scaling, and operating containerized applications. It groups containers into logical units for easy management and discovery.

## 2. **Explain the difference between a pod, a deployment, and a service in Kubernetes.**

- **Answer**:
  - **Pod**: The smallest deployable unit in Kubernetes that can hold one or multiple containers.
  - **Deployment**: Manages the desired state for Pods. It ensures that the specified number of pod replicas are maintained. If a Pod fails, the Deployment will recreate it.
  - **Service**: A Kubernetes resource that provides a stable endpoint to communicate with a set of Pods, abstracting the dynamic nature of Pods.

## 3. **How does Kubernetes handle scalability?**

- **Answer**: Kubernetes scales applications using `ReplicaSets` or `Deployments`. You can specify the number of pod replicas, and Kubernetes will ensure that the specified number of replicas are maintained.

## 4. **Describe ConfigMaps and Secrets in Kubernetes. How do they differ?**

- **Answer**: 
  - **ConfigMap**: Allows configuration data to be decoupled from application artifacts. Useful for non-sensitive configuration.
  - **Secret**: Similar to ConfigMap but meant for storing sensitive data like passwords and API keys. Secrets are stored encoded but not encrypted.

## 5. **What is a Kubernetes Ingress?**

- **Answer**: An Ingress is an API object that manages external access to the services in a cluster, typically HTTP/HTTPS. It can provide load balancing, SSL termination, and name-based virtual hosting.

## 6. **How do you monitor applications in Kubernetes?**

- **Answer**: Common tools include Prometheus for metrics collection and Grafana for visualization. Additionally, you might use logging solutions like the ELK stack (Elasticsearch, Logstash, Kibana) or EFK (Elasticsearch, Fluentd, Kibana).

## 7. **Explain the concept of 'desired state' in Kubernetes.**

- **Answer**: Kubernetes works on a declarative model where you provide the 'desired state' of your application or infrastructure in a YAML or JSON configuration file. Kubernetes then works to ensure the actual state matches the desired state.

## 8. **How does Kubernetes handle failures or crashes?**

- **Answer**: If a node fails, the Replication Controller ensures that the designated number of pod replicas are maintained, creating new pods on other nodes if necessary. For node failures, the K8s control plane will reschedule the pods to healthy nodes.

## 9. **What are Helm charts in Kubernetes?**

- **Answer**: Helm is a package manager for Kubernetes. Helm charts are pre-configured Kubernetes resource packages. They allow developers to define, install, and upgrade even the most complex Kubernetes applications.

## 10. **How do you secure a Kubernetes cluster?**

- **Answer**: 
  - Use Role-Based Access Control (RBAC) to restrict access.
  - Enable Network Policies for pod-to-pod communication.
  - Use a private image registry and scan images for vulnerabilities.
  - Rotate credentials regularly and use tools like HashiCorp Vault for secret management.
  - Ensure API server, kubelet, and etcd are properly secured.



These questions provide a foundation to assess the understanding and experience of candidates with Kubernetes in a DevOps context. Depending on the depth needed, interviewers can further delve into topics or introduce more advanced concepts such as Custom Resource Definitions, Operators, StatefulSets, and more.

---

# Kubernetes Networking and Security Interview Questions for DevOps

## Networking:

## 1. **How does networking function in Kubernetes?**
- **Answer**:
  - Kubernetes uses a flat network model, where each Pod gets its own IP address, ensuring the Pods can communicate without NAT.
  - `kube-proxy` on each node handles some of the internal routing and services help in directing the traffic.

## 2. **What is the difference between a `ClusterIP`, `NodePort`, and `LoadBalancer` service?**
- **Answer**:
  - **ClusterIP**: Default K8s service; exposes the service on a cluster-internal IP.
  - **NodePort**: Exposes the service on each Node's IP at a static port.
  - **LoadBalancer**: Provisions an external IP to act as a load balancer for the service.

## 3. **How do network policies work in Kubernetes?**
- **Answer**:
  - Network policies are crucial for controlling the communication between Pods. By default, Pods can communicate with all other Pods. With network policies, you can enforce whitelist-based rules for Pod communications.

## 4. **Describe the role of Ingress in Kubernetes.**
- **Answer**:
  - Ingress is an API object that manages external access to services within a cluster, typically HTTP. It can provide load balancing, SSL termination, and name-based virtual hosting.

## 5. **What are `CNI` plugins in Kubernetes? Name a few.**
- **Answer**:
  - `CNI` stands for Container Network Interface. They are plugins that assist in setting up networking for the Pods. Examples: Calico, Flannel, Weave Net.

## Security:

## 6. **Explain Kubernetes RBAC.**
- **Answer**:
  - Role-Based Access Control (RBAC) is a method to manage permissions around Kubernetes API requests. Users can define roles with specific permissions and bind those roles to users/groups.

## 7. **What are Kubernetes Secrets? How do they differ from ConfigMaps?**
- **Answer**:
  - Secrets are objects that let you store and manage sensitive information, like passwords, OAuth tokens, and ssh keys. Unlike ConfigMaps which hold configuration data, Secrets are specifically meant for confidential data.

## 8. **How can you securely store and manage secrets in Kubernetes?**
- **Answer**:
  - Besides using Kubernetes' native Secrets, you can use third-party tools like HashiCorp Vault or encrypted storage solutions. Additionally, integrating with KMS solutions provided by cloud providers can enhance secret management.

## 9. **Describe Pod Security Policies (PSP) in Kubernetes.**
- **Answer**:
  - PSPs are cluster-level resources that control the conditions a pod must adhere to in order to be accepted into the system. They define a set of conditions that a pod must run with in order to be accepted into the system.

## 10. **What is a Service Account in Kubernetes? How is it different from a regular user?**
- **Answer**:
  - Service Accounts are meant for processes that run in pods, whereas regular users are for humans. Service Accounts are tied to a set of credentials stored as Secrets, automatically created by Kubernetes, and are attached to pods to interact with the Kubernetes API.

- These questions test the depth of a candidate's experience with Kubernetes networking and security. The responses will offer insights into their familiarity with best practices and advanced concepts in Kubernetes network and security management.

---

# Kubernetes Cheat Sheet

## Basic Commands:

- **Get Information**
  - `kubectl get nodes`: List all nodes.
  - `kubectl get pods`: List all pods in the current namespace.
  - `kubectl get services`: List all services in the current namespace.
  - `kubectl get deployments`: List all deployments in the current namespace.
  - `kubectl get namespaces`: List all namespaces.

- **Describe Resource**
  - `kubectl describe <resource-type> <resource-name>`: Describe a specific resource.

- **Logs & Monitoring**
  - `kubectl logs <pod-name>`: Get logs from a pod.
  - `kubectl top pod`: Display metrics for pods.
  - `kubectl top nodes`: Display metrics for nodes.

## Configuration:

- **Create & Apply**
  - `kubectl create -f <filename>.yaml`: Create a resource from a YAML file.
  - `kubectl apply -f <filename>.yaml`: Apply changes to a resource from a YAML file.

- **Delete**
  - `kubectl delete -f <filename>.yaml`: Delete a resource defined in a YAML file.
  - `kubectl delete <resource-type> <resource-name>`: Delete a specific resource.

## Debugging:

- **Access Shell Inside Pod**
  - `kubectl exec -it <pod-name> -- /bin/sh`: Access shell inside a running pod.

- **Port Forwarding**
  - `kubectl port-forward <pod-name> <local-port>:<pod-port>`: Forward a local port to a port in the pod.

## Cluster Management:

- **Configuration**
  - `kubectl config view`: View Kubernetes configuration.
  - `kubectl config use-context <context-name>`: Switch to a different cluster context.

- **Cluster Info**
  - `kubectl cluster-info`: Display information about the current cluster.

## Advanced:

- **Rolling Update**
  - `kubectl rollout status deployment/<deployment-name>`: View the status of a deployment.
  - `kubectl rollout undo deployment/<deployment-name>`: Rollback a deployment.

- **Autoscaling**
  - `kubectl autoscale deployment <deployment-name> --min=<min-pods> --max=<max-pods> --cpu-percent=<cpu-usage-percentage>`: Auto scale pods in a deployment.

- **Labels & Selectors**
  - `kubectl get pods --selector=<label-key>=<label-value>`: List pods with a specific label.

- **Namespace**
  - `kubectl get pods --namespace=<namespace-name>`: List pods in a specific namespace.

This is a fundamental Kubernetes cheat sheet. For in-depth operations, consider referring to the [official Kubernetes documentation](https://kubernetes.io/docs/).

---