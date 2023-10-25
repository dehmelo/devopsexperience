# Ansible - Do Zero à Automação - DevOps Experience

### Requisitos:

Será necessário instalar [Vagrant](https://www.vagrantup.com/) e o [VirtualBox](https://www.virtualbox.org/), para utilizar o repositório para o provisionamento das máquinas.

Também poderá ser instalado o [git](https://git-scm.com/), para realizar o clone do repositório a partir de seu terminal, para usuários de Windows recomendo [https://gitforwindows.org/](https://gitforwindows.org/). Outra opção: [Chocolatey Community](https://community.chocolatey.org/)

Nome            | vCPUs | Memoria RAM | IP             | S.O.         
----------------|:-----:|:-----------:|:--------------:|:---------------:
devops   | 1     | 2048MB      | 192.168.57.100 | debian/bullseye64
lab1     | 1     | 512MB      | 192.168.57.101 | debian/bookworm64
lab2     | 1     | 512MB      | 192.168.57.102 | debian/bookworm64



Após as instalações das ferramentas, através do **Vagrant** serão criadas as máquinas virtuais no **VirtualBox** de forma automatizada, seguindo as instruções da configuração do Vagrantfile. O **Vagrant** é utilizado para criar e gerenciar as máquinas de uma maneira simples e automática.

Clone o repositório em algum diretório da sua máquina e inicie as VMs:

```bash
git clone https://github.com/dehmelo/devopsexperience.git
cd devopsexperience/labs
vagrant up
```

As máquinas serão provisionadas, este processo leva alguns minutos e depende da sua velocidade de conexão com a internet e recursos de sua máquina.

### Comandos Principais:

Para listar as máquinas:

```bash
vagrant status
```

Para entrar em uma máquina:

```bash
vagrant ssh devops
```

Para iniciar as máquinas:

```bash
vagrant up
```

Para iniciar somente uma máquina:

```bash
vagrant up devops
```

Para desligar as máquinas:

```bash
vagrant halt
```

Para deletar uma máquina:

```bash
vagrant destroy lab1
```

## labs

O arquivo [Vagrantfile](https://github.com/dehmelo/devopsexperience/labs/Vagrantfile), descreve quais e como serão criadas as VMS no VirtualBox (para mais informações consulte a doc do [Vagrant](https://developer.hashicorp.com/vagrant/docs)).

O provisionamento será feito pelo Ansible, os arquivos estão presentes em `provision`, onde o [devops.yml](https://github.com/dehmelo/devopsexperience/labs/provision/devops.yml) será executado na VM **devops** e o [lab.yml](https://github.com/dehmelo/devopsexperience/labs/provision/lab.yml) será executado nas VMs **lab1** e **lab2**. 

O arquivo `ansible.cfg` define que alguns avisos serão ocultos. 

Em `files` está presente o *par de chaves* que será copiado para todas as máquinas durante o provisionamento, para ser possível o fácil acesso (após clonar o repo, no conteúdo de `files`, pode ser adicionado suas chaves pessoais para facilitar o acesso às VMs).

Na máquina `devops` será instalado, através da playbook de provisionamento, o Rundeck, para realizar o acesso ao seu painel digite no navegador de sua preferência, o IP da VM na porta 4440. Desta forma: `192.168.57.100:4440`


## ansible_projects

> Para esta etapa é necessário estar up o ambiente presente em [labs](https://github.com/dehmelo/devopsexperience/labs)

Na pasta [ansible_projects](https://github.com/dehmelo/devopsexperience/ansible_projects) contém um inventário que está mapeado dois grupos com duas VMs que estão presente no [Vagrantfile](https://github.com/dehmelo/devopsexperience/labs/Vagrantfile), são as VMs `lab1` e `lab2`.

O arquivo `ansible.cfg` define o local do inventário e o local das roles e oculta um possível aviso de depreciação.


Para rodar a [playbook](https://github.com/dehmelo/devopsexperience/ansible_projects/playbook.yml) nos hosts mapeados (garanta que as VMs estejam ligadas), abra o seu terminal, acesse a pasta clonada, entre na pasta `ansible_projects` e execute: 
```bash
ansible-playbook playbook.yml
```

Após a execução da playbook será possível acessar os seguintes endereços:

`http://192.168.57.101:8080/` - Interface do WordPress disponível para configuração básica, executada em contêiner.

`http://192.168.57.102:80/` - Interface Web com mensagem gerada a partir da configuração do Apache.


Created by: Déborah Melo
