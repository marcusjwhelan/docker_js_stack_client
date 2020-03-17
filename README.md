Build docker file to run

```bash
 docker build -t react-prod-tag .  
 # run dockerfile
 docker run -p 80:80 react-prod-tag
 ```

 Build and run dev
 ```bash
 # --no-cache optional after build if errors
 docker build -f Dockerfile.dev -t react-dev-tag . 
 # run dev container
 docker run -v ${PWD}:/var/www -v /var/www/node_modules -p 8080:8080 -ti --rm --name dev-react-name react-dev-tag
 # visit localhost 8080 to view live reloading :D
 ```

 # Push to docker hub
Docker hub pro tip - to release several tags for the same build
```bash
docker tag local-image:tagname new-repo:tagname
docker push new-repo:tagname
```
1. First create repo in docker hub {{docker-js-stack-client}}
2. build
```bash
docker build -t mjwrazor/docker-js-stack-client:v0.1.0 .
```

3. push
```bash
docker push mjwrazor/docker-js-stack-client:v0.1.0  
```

## Test kubernetes deployment.yml

```bash
kubectl apply --validate=true --dry-run=true -f deployment.yaml
kubeclt apply --validate=true -f deployment.yaml
kubectl get services
```

Should get localhost for external IP and be able to go to localhost and get a web simple web page.

Shut down test
```bash
kubectl delete deploy/client svc/client
```

# Setting up CircleCI
Make sure you have circleci account and you have connected it with github. 

Make a circleCi directory and the config file
```bash
mkdir .circleci
cd .circleci
touch config.yml
cd ..
```

Set up config.yml with the basic docker hub build context for latest and tags. Commit to git and then in circleCi select project and "Set Up Project"

Then go to settings and add environment variables DOCKERHUB_USERNAME & DOCKERHUB_PASS which should then map correctly into the config.yml for circleci.

Once this is done git push and circleci will build the image and push to docker hub.

To push a specific tag. Create a release with a tag. Or tag a commit.