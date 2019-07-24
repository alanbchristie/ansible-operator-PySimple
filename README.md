# Ansible Operator for PySimple
Minimal files to form a functional operator. In this early version
we just introduce the conventional `build` and `deploy` directories.
There should be much more for testing but, for now, this is all we need.

Our operator logic is encoded in a separate Ansible Role that's
installed from [Ansible Galaxy] during the build. This way we keep our
application logic and operator implementation separate.
 
The documentation for the [Ansible SDK] has plenty of information on
building and deploying operators.  

First, build and push the operator: -

    $ docker build -t alanbchristie/operator-pysimple -f build/Dockerfile .
    $ docker push alanbchristie/operator-pysimple

---

[ansible galaxy]: https://galaxy.ansible.com/alanbchristie/pysimple
[ansible sdk]: https://github.com/operator-framework/operator-sdk/blob/master/doc/ansible/user-guide.md
