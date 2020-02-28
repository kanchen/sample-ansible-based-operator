# sample-ansible-based-operator
This project contains a sample operator developed by using the [Ansible][ansibl_too] option of the operator-sdk[operator_sdk_tool]

## Ansible-based operator-sdk

Based on [Ansible User's Guide for Operator SDK][ansibl_operator_user_guide]
the prerequisites to use the operator-sdk


- [git][git_tool]
- [go][go_tool] version v1.12+.
- [mercurial][mercurial_tool] version 3.9+
- [docker][docker_tool] version 17.03+.
- [kubectl][kubectl_tool] version v1.11.3+.
- Access to a Kubernetes v1.11.3+ cluster.

The Dockerfile.go can be used to create an docker image with the tools installed

Use the following to create a docker image:

```sh
$ docker build -t kanchen/operator-sdk:0.0.1 -f ./Dockerfile.go
```

Use the following to use the image:

```sh
$ run -it -v /var/run/docker.sock:/var/run/docker.sock kchen/operator-sdk:0.0.1 /bin/sh
```

[ansibl_too]: https://github.com/operator-framework/operator-sdk/blob/master/doc/ansible/user-guide.md 
[ansibl_operator_user_guide]: https://github.com/operator-framework/operator-sdk/blob/master/doc/ansible/user-guide.md 
[operator_sdk_tool]: https://github.com/operator-framework/operator-sdk
[operator_sdk_user_guide]: https://github.com/operator-framework/operator-sdk/blob/master/doc/user-guide.md ,
[openshift_ansible_based_operators]: https://docs.openshift.com/container-platform/4.1/applications/operator_sdk/osdk-ansible.html
[git_tool]:https://git-scm.com/downloads
[mercurial_tool]:https://www.mercurial-scm.org/downloads
[go_tool]:https://golang.org/dl/
[docker_tool]:https://docs.docker.com/install/
