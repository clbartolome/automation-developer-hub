# automation-developer-hub

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