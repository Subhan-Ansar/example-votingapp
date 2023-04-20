# Kubernetes Application Developer CKAD
Commands for CKAD
first visit abd login for account on Docker Play ground:

https://labs.play-with-k8s.com/


This is a sandbox environment. Using personal credentials 
is HIGHLY! discouraged. Any consequences of doing so, are 
completely the user's responsibilites.
You can bootstrap a cluster as follows:

1. Initializes cluster master node:
kubeadm init --apiserver-advertise-address $(hostname -i) --pod-network-cidr 10.5.0.0/16

2. Initialize cluster networking:
kubectl apply -f https://raw.githubusercontent.com/cloudnativelabs/kube-router/master/daemonset/kubeadm-kuberouter.yaml

3. (Optional) Create an nginx deployment:
kubectl apply -f https://raw.githubusercontent.com/kubernetes/website/master/content/en/examples/application/nginx-app.yaml
The PWK team.

# Link Nodes

to link the nodes to the master node you will have to copy paste the join token received by running the above command 1. 
the token will be in the following format: 
paste the token to your worker nodes instances:

kubeadm join 192.168.0.13:6443 --token 5qr462.2nxuvoens0qshotv \
--discovery-token-ca-cert-hash sha256:fa73ddad326e09b4a2d6dc8787b54bd52d78ffbcb02c4f9674dfd22853ad5641

# Lets gets started and check the nodes or linked as worker or not run the following command

kubectl get nodes 

# create a nginx container and check for pods creation

kubectl run nginx --image=nginx

kubectl get pods

kubectl describe pod nginx

# Commands and arguments

docker run ubuntu sleep 5

# to clone with github repos

git clone [url address]

#listing the items in the repos

ls


#create a file

cat > name.properties

#check file data

cat name.properties

#edit data in file 

vi name.properties


#open the folder
cd example-voting-app-kubernetes-v2


# above files are the files for CKAD course

kubectl create -f

#pick each file and create deployments
# this command will pick each file in the folder/repos and create them 

kubectl create -f . 

#to check process of creation
kubectl get all


#configmaps:

  #imperative: 

      #literals
          kubectl create configmap \
            config-name --from-literal=key=value

          kubectl create configmap \
            app-config --from-literal=APP_COLOR=pink \
              --from-literal=APP_MODE=prod
      #files
          kubectl create configmap \
            app-config --from-file=app_config.properties


  #decalartive:
          kubectl create -f 

# get configmaps 

kubectl get configmaps

kubectl describe configmaps

# Secrets

# imperative Secrets:
#literals:
kubectl create secret generic \
secret-name --from-literal=key=value

kubectl create secret generic \
app-secret --from-literal=DB_Host=mysql \
--from-literal=DB_User=mysql \
--from-literal=DB_Password=password 

kubectl create secret generic \
secret-name --from-file=app_secret.properties

# encode values:
echo -n 'value'|base64

# get secrets
kubectl get secrets

kubectl describe secrets

kubectl get secret app-secret -o yml


# decode values in secrets:
echo -n 'hashedvalue'"|base64 --decode


# secrets in docker
  docker run ubuntu sleep 3600
  ps aux

  docker run --user=1001 ubuntu sleep 3600

  ps aux

  docker run --cap-add MAC_ADMIN ubuntu



# Serviceaccounts

kubectl create serviceaccount dashboard-sa

kubectl get serviceaccount

kubectl describe serviceaccount dashboard-sa

kubectl describe secret token

kubectl get pod my-kubernetes-dashboard
automountServiceAccountToken: false




kubectl exec -it my-kubernetes-dashboard ls /var/run/secrets/kubernetes.io/serviceaccount

kubectl exec -it my-kubernetes-dashboard cat /var/run/secrets/kubernetes.io/serviceaccount/token

kubectl get pods


docker run nginx

docker ps -a

# Logs and Debugg
kubectl create –f event-simulator.yml

kubectl logs –f event-simulator-pod
kubectl logs –f event-simulator-pod event-simulator

# Pod Design
kubectl get pods --selector app=App1

kubectl create –f deployment-definition.yml
kubectl get deployments
kubectl get replicasets
kubectl get pods
kubectl get all

# Roll out and update

kubectl rollout status deployment/myapp-deployment

kubectl rollout history deployment/myapp-deployment

kubectl rollout apply --filename=deployment-definition.yml --record
kubectl set image deployment/myapp-deployment \ nginx=nginx:1.9.1

kubectl rollout undo deployment/myapp-deployment








