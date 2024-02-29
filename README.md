## Домашнее задание к занятию «Jenkins» - Вдовин Вадим

### Подготовка к выполнению

1. Создать два VM: для jenkins-master и jenkins-agent.

![1](https://github.com/V4d1M63/devops-netology/assets/130470784/bac4d8b9-0559-441f-9f08-1c356c0a6c5c)

2. Установить Jenkins при помощи playbook.

<details>
<summary>ansible-playbook</summary>

┌──(root㉿kali)-[/home/…/lesson/devops-netology/09-ci-04-jenkins/infrastructure]
└─# ansible-playbook -i inventory/cicd/hosts.yml site.yml

PLAY [Preapre all hosts] ***************************************************************************************************************************************

TASK [Gathering Facts] *****************************************************************************************************************************************
ok: [jenkins-master-01]
ok: [jenkins-agent-01]

TASK [Create group] ********************************************************************************************************************************************
ok: [jenkins-master-01]
ok: [jenkins-agent-01]

TASK [Create user] *********************************************************************************************************************************************
ok: [jenkins-master-01]
ok: [jenkins-agent-01]

TASK [Install JDK] *********************************************************************************************************************************************
changed: [jenkins-master-01]
changed: [jenkins-agent-01]

PLAY [Get Jenkins master installed] ****************************************************************************************************************************

TASK [Gathering Facts] *****************************************************************************************************************************************
ok: [jenkins-master-01]

TASK [Get repo Jenkins] ****************************************************************************************************************************************
changed: [jenkins-master-01]

TASK [Add Jenkins key] *****************************************************************************************************************************************
changed: [jenkins-master-01]

TASK [Install epel-release] ************************************************************************************************************************************
changed: [jenkins-master-01]

TASK [Install Jenkins and requirements] ************************************************************************************************************************
changed: [jenkins-master-01]

TASK [Ensure jenkins agents are present in known_hosts file] ***************************************************************************************************
# 158.160.75.107:22 SSH-2.0-OpenSSH_7.4
# 158.160.75.107:22 SSH-2.0-OpenSSH_7.4
# 158.160.75.107:22 SSH-2.0-OpenSSH_7.4
# 158.160.75.107:22 SSH-2.0-OpenSSH_7.4
# 158.160.75.107:22 SSH-2.0-OpenSSH_7.4

changed: [jenkins-master-01] => (item=je
changed: [jenkins-master-01] => (item=jenkins-agent-01)
[WARNING]: Module remote_tmp /home/jenkins/.ansible/tmp did not exist and was created with a mode of 0700, this may cause issues when running as another user.
To avoid this, create the remote_tmp dir with the correct permissions manually

TASK [Start Jenkins] *******************************************************************************************************************************************
changed: [jenkins-master-01]

PLAY [Prepare jenkins agent] ***********************************************************************************************************************************

TASK [Gathering Facts] *****************************************************************************************************************************************
ok: [jenkins-agent-01]

TASK [Add master publickey into authorized_key] ****************************************************************************************************************
changed: [jenkins-agent-01]

TASK [Create agent_dir] ****************************************************************************************************************************************
changed: [jenkins-agent-01]

TASK [Add docker repo] *****************************************************************************************************************************************
changed: [jenkins-agent-01]

TASK [Install some required] ***********************************************************************************************************************************
changed: [jenkins-agent-01]

TASK [Update pip] **********************************************************************************************************************************************
changed: [jenkins-agent-01]

TASK [Install Ansible] *****************************************************************************************************************************************
changed: [jenkins-agent-01]

TASK [Reinstall Selinux] ***************************************************************************************************************************************
changed: [jenkins-agent-01]

TASK [Add local to PATH] ***************************************************************************************************************************************
changed: [jenkins-agent-01]

TASK [Create docker group] *************************************************************************************************************************************
ok: [jenkins-agent-01]

TASK [Add jenkinsuser to dockergroup] **************************************************************************************************************************
changed: [jenkins-agent-01]

TASK [Restart docker] ******************************************************************************************************************************************
changed: [jenkins-agent-01]

TASK [Install agent.jar] ***************************************************************************************************************************************
changed: [jenkins-agent-01]

PLAY RECAP *****************************************************************************************************************************************************
jenkins-agent-01           : ok=17   changed=12   unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
jenkins-master-01          : ok=11   changed=7    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0 

</details>

3. Запустить и проверить работоспособность.
4. Сделать первоначальную настройку.

![2](https://github.com/V4d1M63/devops-netology/assets/130470784/bc8ef639-f7de-418d-af20-c79f321c3560)

### Основная часть

1. Сделать Freestyle Job, который будет запускать molecule test из любого вашего репозитория с ролью.

<details>
<summary>Freestyle Job</summary>

![09-ci-04-jenkins-4](https://github.com/V4d1M63/devops-netology/assets/130470784/c558e979-c424-4310-9aa2-d9868c74d4ec)
![09-ci-04-jenkins-5](https://github.com/V4d1M63/devops-netology/assets/130470784/fd2138b5-828a-4cfe-926a-cf548bdcab0c)
![09-ci-04-jenkins-6](https://github.com/V4d1M63/devops-netology/assets/130470784/dff022c9-998d-4692-a0b1-3e37764f009b)

</details>

2. Сделать Declarative Pipeline Job, который будет запускать molecule test из любого вашего репозитория с ролью.

<details>
<summary>Declarative Pipeline Job</summary>

![09-ci-04-jenkins-8](https://github.com/V4d1M63/devops-netology/assets/130470784/99d4416b-9ff3-40e1-98a1-6906f633a3ad)
![09-ci-04-jenkins-10](https://github.com/V4d1M63/devops-netology/assets/130470784/cc1eac27-f1c0-49e2-beb9-e512f3df1beb)

</details>

3. Перенести Declarative Pipeline в репозиторий в файл Jenkinsfile.

4. Создать Multibranch Pipeline на запуск Jenkinsfile из репозитория.

![3](https://github.com/V4d1M63/devops-netology/assets/130470784/b5fe59c1-73b3-414f-984b-b7b1d068299e)
![4](https://github.com/V4d1M63/devops-netology/assets/130470784/44a3ab62-b8d4-4b33-a126-66a1ccb77773)
![5](https://github.com/V4d1M63/devops-netology/assets/130470784/521076d7-8313-449c-9276-acd9adfc1872)

5. Создать Scripted Pipeline, наполнить его скриптом из pipeline.
![6](https://github.com/V4d1M63/devops-netology/assets/130470784/38f295f5-13ae-4095-9024-0d550c2b9500)
![7](https://github.com/V4d1M63/devops-netology/assets/130470784/40694c95-948e-4675-9df8-e4a808f6b34e)

6. Внести необходимые изменения, чтобы Pipeline запускал ansible-playbook без флагов --check --diff, если не установлен параметр при запуске джобы (prod_run = True). По умолчанию параметр имеет значение False и запускает прогон с флагами --check --diff.
![8](https://github.com/V4d1M63/devops-netology/assets/130470784/3670f79f-5ee3-468d-ad6a-7f0131cf591a)

```
node("linux"){
    parameters {
        booleanParam(name: "prod_run", defaultValue: false)
    }
    stage("Git checkout"){
        git credentialsId: 'git', url: 'git@github.com:aragastmatb/example-playbook.git'
    }
    stage('preparation for run playbook') {
        sh 'sudo mkdir -p /opt/jdk/openjdk-11'
    }
    stage("Run playbook"){
        if (params.prod_run){
            sh 'ansible-playbook site.yml -i inventory/prod.yml'
        }
        else{
            sh 'ansible-playbook site.yml -i inventory/prod.yml --check --diff'
        }

    }
}
```

7. Проверить работоспособность, исправить ошибки, исправленный Pipeline вложить в репозиторий в файл ScriptedJenkinsfile.

![9](https://github.com/V4d1M63/devops-netology/assets/130470784/62585f51-f4f6-429b-a0f9-043291f5d745)

