## To use

You need to have a recent version of docker running on your laptop which you can download from [here](https://download.docker.com/mac/stable/Docker.dmg).

```bash
# Clone the repo
$ git clone https://github.com/sakiv/concourse-workshop.git

# Run docker-compose
$ cd concourse-workshop; docker-compose up

# Visit localhost:8080 and download the fly binary which will be used to interact with concourse

# Move the file to your path and make it executable:
$ sudo mv ~/Downloads/fly /usr/local/bin/fly; chmod 0755 /usr/local/bin/fly

# Authenticate the cli with concourse
$ fly login -t local-main -n main -c http://localhost:8080

# Set and unpause the first pipeline
$ fly set-pipeline -t local-main -p autoscaler -c autoscaler1.yml
$ fly -t local-main unpause-pipeline -p autoscaler

# Use autoscaler2.yml to update the pipeline
$ fly set-pipeline -t local-main -p autoscaler -c autoscaler2.yml

# Hijacking the job we just added
# (it needs to have run at least once)
$ fly -t local-main hijack -j autoscaler/deploy-preview
