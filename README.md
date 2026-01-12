# automation-developer-hub

Repository with a collection development and lifecycle with OpenShift DevTools

> [!IMPORTANT]  
> Last tested versions: 
> - OpenShift: 4.18.4
> - OpenShift GitOps: 1.15.1
> - OpenShift Pipelines: 1.17.1 
> - OpenShift DevSpaces: 3.18.1
> - AAP: 2.5


## Pre-Requisites

- Install **OpenShift GitOps** operator (default config)
- Install **OpenShift Pipelines** operator (default config)
- Install **OpenShift DevSpaces** operator (default config) and create an instance of eclipse che
- Install **Ansible Automation Platform** operator (default config)
- Build Ansible Execution Environment Manually:

```sh
cd installation/ansible-navigator
ansible-builder build -t custom-ee:latest
```

- Fork repository `https://github.com/zaskan/ansible-devspaces-demo` and generate a token so demo resources can perform actions on it with following permissions:
  - Contents (RW) 
  - Webhooks (RW) 
  - Pull requests (RW)

## Install

- Open a terminal

- Login into OpenShift

- Access installation->ansible-navigator: `cd installation/ansible-navigator`

- Create environment vars for configuration (**update token**):

```sh
export OPENSHIFT_TOKEN=$(oc whoami --show-token)
export CLUSTER_DOMAIN=$(oc whoami --show-server | sed 's~https://api\.~~' | sed 's~:.*~~')
export GITHUB_USER=<user>
export GITHUB_TOKEN=<token>
export GITHUB_BRANCH=<branch name to be used during demo (will be created and deleted automatically)>
```

- Run installation:

```sh
ansible-navigator run ../install.yaml -m stdout \
    -e "ocp_host=$CLUSTER_DOMAIN" \
    -e "api_token=$OPENSHIFT_TOKEN" \
    -e "github_user=$GITHUB_USER" \
    -e "github_token=$GITHUB_TOKEN" \
    -e "github_branch=$GITHUB_BRANCH"
```



