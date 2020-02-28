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

Use the docker image build from [github.com/kanchen/operator-sdk](https://github.com/kanchen/operator-sdk)

```sh
$ docker run -it -v /var/run/docker.sock:/var/run/docker.sock kchen/ansible-operator-sdk:0.0.1 /bin/sh
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

