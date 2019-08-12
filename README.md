# Ansible Operator for PySimple

[![Build Status](https://travis-ci.org/alanbchristie/ansible-operator-PySimple.svg?branch=master)](https://travis-ci.org/alanbchristie/ansible-operator-PySimple)

Minimal files to form a functional operator. In this early version
we just introduce the conventional `build` and `deploy` directories.
There should be much more for testing but, for now, this is all we need.

Our operator logic is encoded in a separate Ansible Role that's
installed from [Ansible Galaxy] during the build. This way we keep our
application logic and operator implementation separate.
 
The documentation for the [Ansible SDK] has plenty of information on
building and deploying operators, what follows is a summary of what you can
find there.  

First, build and push the operator: -

    $ docker build -t alanbchristie/operator-pysimple . \
        -f build/Dockerfile \
        --no-cache
    $ docker push alanbchristie/operator-pysimple

## Deploying (Kubernetes/OpenShift)

>   If deploying to OpenShift you shoud just beed to replate `kubectl`
    with `oc` in the following commands. In fact I think `oc` can
    also deploy to Kubernetes.

Deploy the CRD: -

    $ kubectl create -f deploy/crds/pysimple_v1_pysimple_crd.yaml

Create and move to a new namespace: -

    $ kubectl create -f deploy/namespace.yaml
    $ kubectl config set-context --current --namespace=pysimple
    
Deploy the operator: -

    $ kubectl create -f deploy/service_account.yaml
    $ kubectl create -f deploy/role.yaml
    $ kubectl create -f deploy/role_binding.yaml
    $ kubectl create -f deploy/operator.yaml

Deploy the app: -

    $ kubectl apply -f deploy/crds/pysimple_v1_pysimple_cr_1.yaml

Un-deploy (which simply sets the role's `state` variable to `absent`): -

    $ kubectl apply -f deploy/crds/pysimple_v1_pysimple_cr_absent.yaml

---

[ansible galaxy]: https://galaxy.ansible.com/alanbchristie/pysimple
[ansible sdk]: https://github.com/operator-framework/operator-sdk/blob/master/doc/ansible/user-guide.md
