# automation-developer-hub

Repository with a collection development and lifecycle with OpenShift DevTools

> [!IMPORTANT]  
> Last tested versions: 
> - OpenShift: 4.18.4
> - OpenShift GitOps: 1.15.1
> - OpenShift Pipelines: 1.17.1 
> - OpenShift DevSpaces: 3.18.1
> - AAP: 2.5


## Requirements

- Install **OpenShift GitOps** operator (default config)
- Install **OpenShift Pipelines** operator (default config)
- Install **OpenShift DevSpaces** operator (default config)
- Install **Ansible Automation Platform** operator (default config)



## Install

- Open a terminal

- Login into OpenShift

- Access installation->ansible-navigator: `cd installation/ansible-navigator`

- Create environment vars for configuration:

```sh
export OPENSHIFT_TOKEN=$(oc whoami --show-token)
export CLUSTER_DOMAIN=$(oc whoami --show-server | sed 's~https://api\.~~' | sed 's~:.*~~')
```

- Run installation:

```sh
ansible-navigator run ../install.yaml -m stdout \
    -e "ocp_host=$CLUSTER_DOMAIN" \
    -e "api_token=$OPENSHIFT_TOKEN"
```


## SetUp

- Environment:
    - Create a project named: `ansible-dev`
    - Install openshift-pipelines
    - Install devspaces and create a che instance in `ansible-dev` namespace

- Clone and create demo branch
```sh
cd /tmp
git clone git@github.com:zaskan/ansible-devspaces-demo.git
cd ansible-devspaces-demo
git checkout -b live-demo
git push --set-upstream origin live-demo
```

- Create resources
```sh
cd /<demo-code>
oc project ansible-dev
oc adm policy add-cluster-role-to-user cluster-reader system:serviceaccount:ansible-dev:pipeline

oc create secret generic ci-config --from-literal=GITHUB_TOKEN=<token>

oc apply -f tekton

oc expose svc el-sample-collection-ci
oc get route 
```

- Create a webhook in github pointing to previously created route

- Cleanup demo branch
```sh
cd /tmp/ansible-devspaces-demo
git checkout main
git branch -D live-demo
git push origin --delete live-demo
rm -rf /tmp/ansible-devspaces-demo
```