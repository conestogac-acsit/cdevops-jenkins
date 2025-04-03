# Jenkins on Kubernetes

This repository contains Ansible playbooks to deploy and remove Jenkins on a Kubernetes cluster.

## Prerequisites

- Docker installed and running
- Ansible installed
- Kubernetes cluster running

## Checking Prerequisites

1. Check if Docker is running:
   ```
   docker ps
   ```

2. Check if Ansible is installed:
   ```
   ansible-playbook --version
   ```
   
   If not installed, run:
   ```
   bash <(curl -Ls https://raw.githubusercontent.com/conestogac-acsit/cdevops-bootstrap/refs/heads/main/bootstrap.sh)
   ```

3. Check if Kubernetes cluster is running:
   ```
   kubectl get ns default
   ```
   
   If not running, install a Kubernetes cluster:
   ```
   bash <(curl -Ls https://raw.githubusercontent.com//conestogac-acsit/cdevops-bootstrap/refs/heads/main/k8s.sh)
   ```

## Deploying Jenkins

To deploy Jenkins on your Kubernetes cluster:

```
ansible-playbook up.yaml
```

After deployment, you can access Jenkins through the ngrok ingress. Get the ingress URL with:

```
kubectl get ingress -n jenkins
```

## Initial Jenkins Setup

1. Get the initial admin password:
   ```
   kubectl exec -it $(kubectl get pods -n jenkins -l app=jenkins -o jsonpath='{.items[0].metadata.name}') -n jenkins -- cat /var/jenkins_home/secrets/initialAdminPassword
   ```

2. Navigate to your Jenkins URL and enter the initial admin password
3. Install suggested plugins
4. Create your first admin user
5. Configure Jenkins URL

## Removing Jenkins

To remove Jenkins from your Kubernetes cluster:

```
ansible-playbook down.yaml
```

## GitHub and Gitea Integration

Follow the tutorial at [Jenkins Python App Tutorial](https://www.jenkins.io/doc/tutorials/build-a-python-app-with-pyinstaller/) to:

1. Create a Python application with a Jenkinsfile
2. Push to GitHub and configure webhooks
3. Push to Gitea and configure webhooks
