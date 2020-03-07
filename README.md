# sample-ansible-based-operator
This project contains a sample operator developed by using the [Ansible][ansibl_too] option of the [operator-sdk][operator_sdk_tool]

## Ansible-based operator-sdk

Based on [Ansible User's Guide for Operator SDK][ansibl_operator_user_guide]
the prerequisites to use the operator-sdk

- [git][git_tool]
- [docker][docker_tool] version 17.03+.
- [kubectl][kubectl_tool] version v1.9.0+.
- [ansible][ansible_tool] version v2.6.0+
- [ansible-runner][ansible_runner_tool] version v1.1.0+
- [ansible-runner-http][ansible_runner_http_plugin] version v1.0.0+
- [go][go_tool] version v1.13+. (Optional if you aren't installing from source)

## Build the operator
Use the docker image build from [github.com/kanchen/operator-sdk](https://github.com/kanchen/operator-sdk)

```sh
$ docker run -it -v /var/run/docker.sock:/var/run/docker.sock kchen/ansible-operator-sdk:0.0.1 /bin/sh
```

## Run the operator

Once inside the ansible-operator-sdk interative session, check out [sample-ansible-based-operator](https://github.com/kanchen/sample-ansible-based-operator)

```
$git clone https://github.com/kanchen/sample-ansible-based-operator.git
$cd sample-ansible-based-operator
```

Deploy the CRD:

```sh
$ kubectl create -f deploy/crds/web.globalinfotek.com_nginxes_crd.yaml
```

Build the nginx-operator image and push it to a registry:
```
$ operator-sdk build docker.io/kchen/nginx-operator:v0.0.1
$ docker push docker.io/kchen/nginx-operator:v0.0.1
```

Deploy the nginx-operator:

```sh
$ kubectl create -f deploy/service_account.yaml
$ kubectl create -f deploy/role.yaml
$ kubectl create -f deploy/role_binding.yaml
$ kubectl create -f deploy/operator.yaml
```

Verify that the memcached-operator is up and running:

```sh
$ kubectl get deployment
NAME                     DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
nginx-operator           1         1         1            1           1m
```
Create a Nginx CR

Modify `deploy/crds/web.globalinfotek.com_v1alpha1_nginx_cr.yaml` as shown:

```sh
$ cat deploy/crds/web.globalinfotek.com_v1alpha1_nginx_cr.yaml
apiVersion: web.globalinfotek.com/v1alpha1
kind: Nginx
metadata:
  name: test-nginx
spec:
  image: docker.io/nginx
  tag: 1.17.8
  replicas: 3
  node_port: 30001

$ kubectl apply -f deploy/crds/web.globalinfotek.com_v1alpha1_nginx_cr.yaml
```

Ensure that the nginx-operator creates the deployment for the CR:

```sh
$ kubectl get deployment
NAME                     DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
nginx-operator           1         1         1            1           2m
test-nginx               3         3         3            3           1m
```


[ansibl_too]: https://github.com/operator-framework/operator-sdk/blob/master/doc/ansible/user-guide.md
[ansibl_operator_user_guide]: https://github.com/operator-framework/operator-sdk/blob/master/doc/ansible/user-guide.md
[operator_sdk_tool]: https://github.com/operator-framework/operator-sdk
[operator_sdk_user_guide]: https://github.com/operator-framework/operator-sdk/blob/master/doc/user-guide.md
[openshift_ansible_based_operators]: https://docs.openshift.com/container-platform/4.1/applications/operator_sdk/osdk-ansible.html
[git_tool]:https://git-scm.com/downloads
[go_tool]:https://golang.org/dl/
[docker_tool]:https://docs.docker.com/install/
[ansible_tool]:https://docs.ansible.com/ansible/latest/index.html
[ansible_runner_tool]:https://ansible-runner.readthedocs.io/en/latest/install.html
[ansible_runner_http_plugin]:https://github.com/ansible/ansible-runner-http
[ansible_runner_http_installation]: https://pypi.org/project/ansible-runner-http/#files

