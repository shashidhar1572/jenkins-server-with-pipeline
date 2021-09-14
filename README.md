This repo is for Jenkins server helm and example pipeline

prerequisite: aws cli, helm v3.6.3 and kubectl 

step 1: generate kubeconfig with aws-cli 

aws eks --region us-east-1 update-kubeconfig --name test-sha

* create a namespace for jenkins\
#kubectl create namespace jenkins

step 2: 
* add jenkins public helm repo\
#helm repo add jenkins https://charts.jenkins.io

* update helm repo\
#helm repo update

* provision Jenkins controller on default namespaces with below command as helm release_name\
#helm install jenkins-controller-v1 jenkins/jenkins -f jenkins-server-values.yaml -n jenkins

* wait for Jenkins pods to avilable/running
#kubectl get pods -n jenkins

* Get your 'admin' user password by running:\
#kubectl exec --namespace jenkins -it svc/jenkins-controller-v1 -c jenkins -- /bin/cat /run/secrets/chart-admin-password && echo
* Get the Jenkins URL to visit by running these commands in the same shell:
#kubectl --namespace jenkins port-forward svc/jenkins-controller-v1 8080:8080
#echo http://127.0.0.1:8080



