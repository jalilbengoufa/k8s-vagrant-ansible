# k8s-vagrant-ansible

- Install vagrant, ansible, kubectl and virtualbox in your local env.

- To start the cluster run `vagrant up` (change N in Vagranfile for the number of nodes needed)

#### Set remote access from local env

- run `scp -r vagrant@192.168.50.10:/home/vagrant/.kube/config .`  (use `vagrant` as password, this will copy config file to your local env )

- run `KUBECONFIG=~/.kube/config:$PWD/config kubectl config view --flatten > ~/.kube/config` (merge current config file with the one we copied from cluster)

#### Testing cluster hello-node

- Run deployment hello-node `kubectl create deployment hello-node --image=gcr.io/hello-minikube-zero-install/hello-node` 

- Run service hello-node `kubectl apply -f hello-node-service.yaml`

- Verify  deployments, pods and services with `kubectl get deployments` , `kubectl get pods` and ` kubectl get rs`

- Copy the pods name example: `hello-node-78cd77d68f-sqc2p`

- forward port 8080 to localhost with `kubectl port-forward hello-node-78cd77d68f-sqc2p 8080:8080`

- Test the app hello-node with `curl http://localhost:8080` should see the output `Hello World!`