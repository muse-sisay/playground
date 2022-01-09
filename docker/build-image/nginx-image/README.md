# Build Image: nginx-image

In this demo/lab/exercise we will see how to build custom image using nginx base image that we can deploy in  our k8s cluster to test our `kubectl port-forward` feature. As part of the exercise will expose our web-server to listen on port 80 and 8080.

# Nginx image
- Content is stored inside `/usr/share/nginx/html`.
- Configuration files go in `/etc/nginx` 
- Don't forget to replace default nginx configuration. (`/etc/nginx/conf.d/default.conf`)

# Running 

- To build the image:
```console
docker build -t muse-sisay/web-server .
```
the image is tagged as `muse-sisay/web-server`

- Run image
```console
docker run -d --name=webserver -p 80:80 -p 8080:8080 muse-sisay/webserver
```
The container exposes port 80 and 8080 on the local machine.

## Reference
- Use nginx base image to build custom images. [Nginx Documentation](https://www.nginx.com/blog/deploying-nginx-nginx-plus-docker/) [Docker Documentation](https://www.docker.com/blog/how-to-use-the-official-nginx-docker-image/)