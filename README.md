#Create-react-app, Docker and K8s

1. Dockerize the app
We run this command to create a docker image:
`docker build -t my-react-app .`

2. Connect to a Kubernetes cluster
Open your Docker Desktop preferences and switch to your Kubernetes tab. Enable Kubernetes support here. It automatically creates a cluster for you.

Once it is running, connect to it with kubectl

`kubectl config use-context docker-desktop`

3. Upload the Docker image to your container registry
Create local registry with this command:
`docker run -d -p 5000:5000 --restart=always --name registry registry:2`

To upload our Docker image, we have to tag it with the hostname and port of our registry:
`docker tag my-react-app localhost:5000/my-react-app`

And then we push the image to our Docker registry:
`docker push localhost:5000/my-react-app`

4. Deploy the React application
To deploy your application to Kubernetes with:
`kubectl apply -f deployment.yaml`

`kubectl apply -f service.yaml`

For check status:
`kubectl get pods`
`kubectl get deployment`
`kubectl get service`

If everything went right, you should be able to go to http://localhost:31000 and see your react app, now served from a Kubernetes cluster

https://koala42.com/create-a-react-app-in-kubernetes/