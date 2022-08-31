# circle-ci-project
A piece of code to test ci/cd process in circle ci platform <link>https://circleci.com/</link>

# What you have in this project's repository?
  - A Dockerfile, this file make a container with our app, in this case is just nginx service
  - ./circleci/config.yml: This file save the workflow, with steps to make de pull, tag and push image to dockerhub (<link>https://hub.docker.com/repository/docker/adriandockerimg/circle-ci-test</link>, install applications (kubectl and gettext-base) and finally, run a .sh code to exec the deploy's file (from template) and create the service.
  - ./circleci/deploy/ci-deploy.sh: The ci-deploy.sh file run a script to replace enviroment var and generate a new deployment file to exec.
  - ./circleci/kube: Here we have two files:
      - deployment.yml.template: Save the code to run a deploy, it's a template because the ci-deploy.sh file run a script to replace enviroment var and generate a new file to exec.
      - service.yaml: It's a NodePort services to route throght my application
      
# Information to know
 - The infrastructure was make with Terraform <link>https://www.terraform.io/</link>, and the code is available in <link>https://github.com/dislepsia/kubernetes</link>, folder number 14.
    - A cluster, a node, a load balancer, a deploy (with one replica) and finally the service was create how infrastructure as code in a Terraform
 - Is necesary create a github project and bind with circleci platform. Here we have 3 tokens to create:
    - Project Token: Its works like a var.circleci_token
    - Account Token: Its works like a provider.circleci.token
      - Data extra: The provider.circleci.organization question its about name account in GitHub, in my case its dislepsia.
    - And the last one is necesary create a API Access Token in Digital Ocean <link>https://www.digitalocean.com/</link>
      - It's works like a var.digitalocean_token
