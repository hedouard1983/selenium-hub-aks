# Selenium Grid Deployment on Azure Kubernetes Service (AKS)

This guide will walk you through deploying a Selenium Grid to Azure Kubernetes Service (AKS). This includes setting up a Selenium Hub and nodes for Chrome, Firefox, and Edge.

## Prerequisites

- An active Azure account
- Azure CLI installed and configured
- Kubernetes CLI (kubectl) installed and configured
- A running AKS cluster

## Repository Structure

```
/deployments
selenium-hub-deployment.yaml # Deployment file for Selenium Hub
selenium-node-chrome-deployment.yaml # Deployment file for Selenium Chrome Node
selenium-node-firefox-deployment.yaml # Deployment file for Selenium Firefox Node
selenium-node-edge-deployment.yaml # Deployment file for Selenium Edge Node
/services
selenium-hub-svc.yaml # Service file for Selenium Hub
```

## Deployment Steps

1. **Clone the Repository**

   ```bash
   git clone https://github.com/<your-github-username>/selenium-grid-aks.git
   cd selenium-grid-aks
```
Create the Selenium Hub

Deploy the Selenium Hub to your AKS cluster:
kubectl apply -f deployments/selenium-hub-deployment.yaml
kubectl apply -f services/selenium-hub-svc.yaml
```
Create the Selenium Hub

Deploy the Selenium Hub to your AKS cluster:

bash
Copy code
kubectl apply -f deployments/selenium-hub-deployment.yaml
kubectl apply -f services/selenium-hub-svc.yaml
Deploy Selenium Nodes

Deploy each type of Selenium Node (Chrome, Firefox, and Edge):

bash
Copy code
kubectl apply -f deployments/selenium-node-chrome-deployment.yaml
kubectl apply -f deployments/selenium-node-firefox-deployment.yaml
kubectl apply -f deployments/selenium-node-edge-deployment.yaml
Verify the Deployments

Check that all pods are running:

bash
Copy code
kubectl get pods
You should see the Selenium Hub and nodes listed as running.

Access the Selenium Grid Console

Find the external IP of the Selenium Hub:

bash
Copy code
kubectl get svc selenium-hub
Open a web browser and navigate to http://<EXTERNAL-IP>:4444/ui/index.html to access the Selenium Grid Console.

Scaling
To scale the number of nodes for a particular browser:

bash
Copy code
kubectl scale deployment selenium-node-chrome --replicas=<number-of-replicas>
Replace <number-of-replicas> with the desired number of nodes.

Updating
To update your Selenium Nodes or Hub with a new Docker image:

Update the Docker image tag in the respective YAML file.

Apply the changes:

bash
Copy code
kubectl apply -f deployments/selenium-node-chrome-deployment.yaml
Troubleshooting
Ensure that AKS has enough resources to run the desired number of nodes.

Check the pod logs if any pod is not in the Running state:

bash
Copy code
kubectl logs <pod-name>
```