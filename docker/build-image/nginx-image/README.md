- [Build Image: nginx-image](#build-image-nginx-image)
- [Nginx image](#nginx-image)
- [Running](#running)
  - [Reference](#reference)

# Build Image: nginx-image

In this demo/lab/exercise we will see how to build custom image using nginx base image that we can deploy in  our k8s cluster to test our `kubectl port-forward` feature. As part of the exercise will expose our web-server to listen on port 80 and 8080.

# Nginx image

Our nginx image listens on port 80 and 8080. So need to replace the default configuration file with our.
- Content to be served is stored inside `/usr/share/nginx/html`.
- Configuration files go in `/etc/nginx` 
- Don't forget to replace default nginx configuration. (`/etc/nginx/conf.d/default.conf`)

# Running 

- Build the image.  
```console
$ docker build -t muse-sisay/web-server .
```
the image is tagged as `muse-sisay/web-server`. If you want to access this image inside your minikube cluster run `eval $(minikube docker-env)` before building the image. It will build the image in your kubernetes cluster.

- Run image/pod
```console
$ docker run -d --name=webserver -p 80:80 -p 8080:8080 muse-sisay/webserver
$ kubectl run -d --image=muse-sisay/webserver -p 8000:80 -p 8080:8080 webserver
```
The docker container exposes port 80 and 8080 on the local machine. To access the ports published by the pod you need to create a service or you can use port-forward.

- Use kubectl port forward feature to reach the pod
```console
$ kubectl port-forward webserver 30301:8080
```

## Reference
- Use nginx base image to build custom images. [Nginx Documentation](https://www.nginx.com/blog/deploying-nginx-nginx-plus-docker/) [Docker Documentation](https://www.docker.com/blog/how-to-use-the-official-nginx-docker-image/)