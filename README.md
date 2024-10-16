### Nginx lab inside k8s

0. A K8s cluster is required. For this lab, I used microk8s.
1. Install microk8s
2. Start microk8s and enable ingress addon
```
microk8s start
microk8s enable ingress
```
3. Deploy the resources (*)
```
cat deployment-nginx.yaml | sed s+{{path}}+$(pwd)+g | kubectl apply -f -
k apply -f service-nginx.yaml
k apply -f ingress-nginx.yaml
```
4. Go to localhost with your browser, you should see the contents of index.html

#### TODO:
- Create a pipeline to build the backend and push it to a container registry
```
docker build . -t node-express-server
docker run -p 1111:7777 -d node-express-server
docker run -p 2222:7777 -d node-express-server
docker run -p 2222:7777 -d node-express-server
docker run -p 2222:7777 -d node-express-server
```
- Create deployments or pods for 4 different node-express-server applications and expose them on different ports.
- Modify the nginx.conf file to serve the backend.
- Verify that everything is working well

#### Disclamer:
This environment is for laboratory purposes only. It is obviously useless in k8s, since everything is done automatically under the hood through ingress-controller, ingress, and services.

(*) Although hostPath is not suggested, we used it in this lab. Since the absolute path is required, we do a sed on the fly to set the correct value in every env. You can change it manually.