# Ansible - Fullcycle

## Seção 1: Iniciando com Ansible

1. Boas vindas
    - Apresentando o curso sobre Ansible

2. Ansible Vs. Terraform
    - A principal diferença entre os 2 é que com o Terraform você provisiona a infraestrutura, por exemplo, cria uma instância em uma Cloud qualquer e com o Ansible você configura ela com o que quiser, por exemplo instalando um Nginx ou simplesmente criando um usuário no Linux.
    - Ambos conseguem provisionar ambiente e configurações, porém um é melhor em uma coisa e o outro é melhor em outra.

3. Rodando primeiro ping
    - criando o arquivo de inventário e adicionando localhost
    - `ansible -i inventory all -m ping` *utilizando primeiro módulo, rodando um ping*

4. Configurando um servidor Ansible no Ubuntu com Docker
    - Criando Dockerfile para subir um container com o Ansible
    - Criando o Docker-compose para subir o container do Ansible Server

5. Configurando nodes e configurando chaves
    - Efetuada configuração de mais um container com Ubuntu e feito a troca de chaves ssh para conexão entre o Server e o Node1
    - `ssh-keygen`
    - `ssh-copy-id root@node1`
    - `ansible -i inventory all -m shell -a 'uptime'`

6. Executando primeiros comandos (Ad-hoc)
    - `ansible -i inventory all -m apt -a "update_cache=yes name=git state=present"` *instalando o git nos nodes*
    - `ansible -i hosts all -m git -a "repo=LINKREPOSITORIO dest=/root/NOMEDIRETORIO/"` *fazendo clone de um repositório utilizando o modulo git do Ansible*
    - `ansible -i inventory node1 -m setup` *módulo para visualizar todas as informações a máquina remota*
    - `ansible -i inventory node1 -m shell -a "ls -la"` *executando um comando shell na máquina remota*

## Seção 2: Trabalhando com Playbooks

7. Criando maquina na nuvem
    - Já tenho algumas maquina na GCP

8. Pingando maquinas criadas
    - Segui esse tutorial para realizar o inventório automático no GCP <https://devopscube.com/ansible-dymanic-inventry-google-cloud/>
    - Criei a chave publica no servidor docker na minha maquina
    - configurei o gcloud no container e configurei meu projeto
    - coloquei a chave publica criada no arquivo `/HOME/USUARIOGOOGLE/.ssh/authorized_keys`
    - maquina centos precisa desabilitar o selinux `setenforce 0`

9. Iniciando com Playbooks
    - Instalanda ferramentas, utilizando módulo `apt` e iniciando serviço com o módulo `service` (diretório `Fullcycle/Docker/playbook.yaml`)

10. Trabalhando com Ansible Galaxy
    - Iniciando a arvore de diretório com o comando `ansible-galaxy init NOMEDAPASTA` (diretório `Fullcycle/Docker/roles/install_nginx/*`)

11. Instalando docker usando ansible role
    - Colocando o passo a passo de instalação do Docker nas tasks. (diretório `Fullcycle/Docker/roles/main.yaml`)
    - `ansible-playbook roles/main.yaml` *rodando o playbook dentro de `roles`*

12. Instalando o docker-compose
    - Adicionando a task de instalação do docker-compose

13. Inicializando o docker-swarm
    - Inicializando o docker swarm, criado uma nova role somente para o "manager" do swarm.

14. Realizando join no Manager
    - Consegui realizar o join das máquina no manager, criei um novo arquivo de inventário chamado `gcp-inventory.yaml`
    - Com o comando `ansible-inventory --list` trago todos os dados inventário realizados de forma automática pela integração com o GCP, peguei as máquinas e inseri no inventário para poder utilizar algumas váriaveis que não estava conseguindo obter.
    - Inseri a instalação do componente `docker` na role `install_docker`

15. Fazendo deploy da stack
    - 


