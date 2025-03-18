### Kubernetes Lab 001

First we builded our app: 

    docker build -t kub-first-app

Checking our minikube app with:

    minikube status

After ensuring our minikube is running, we can create a deployment object with the image we just created but here is the thing, we cant give our local image to the cluster, therefor we need to upload our image to docker hub and then give to cluster:

Send image to docker hub:

    docker tag kub-first-app mandalina/kub-lab-001

    docker push mandalina/kub-lab-001

Now our image in our remote repository, now we can proceed:


    kubectl create deployment first-app --image=kub-mandalina/kub-lab-001

If we want to see our deployments, we can use:

    kubectl get deployments

If we want to see our pods, we can use:

    kubectl get pods


# 

If we want to see our pods and deployments inside our cluster, we can use minikube's dashboard like this:

    minikube dashboard

And if we click on the given ip, we can see information about our cluster:


![alt text](image.png)

Using "Service" object:

    kubectl  expose deployment first-app --type=NodePort --port=8080

And then we can see our services with:

    kubectl get services

Since we are using minikube for our demo lab, we have to use this code in order to check if our pods is working how we want it:

    minikube service first-app