# Ansible - Udemy

## Seção 1: Introdução

1. Introdução ao Ansible
    - Introdução ao que aprenderemos durante o curso, comandos e conceitos sobre o Ansible.
    - Repositório do curso <https://gitlab.com/treinamentos1/ansible>
    - O que é o Ansible: Uma ferramenta de automação e gerenciamento de configurações. 
    - Porque o Ansible:
        - É livre e de código aberto;
        - Curva rápida de aprendizado;
        - Automatização em menos tempo;
        - Entrega completa em minutos;
        - Gerenciamento simples;
        - Sem necessidade de agentes (SSH);
        - Indempotência:
            - É a propriedade que algumas operações têm de poderem ser aplicadas várias vezes sem que o valor do resultado se altere após a aplicação inicial. Em resumo, será executado apenas se houver necessidade.
            ![image1](img/image1.png)
    - Administração do Ansible:
    ![image2](img/image2.png)
        - Arquivos:
            - **Inventário:**  Arquivo que descreve as máquinas a serem acessadas pelo Ansible e suas particularidades.
            - **Modulos:** pequenos programas utilizados para realizar tarefas de automação no nó destino.
            - **Playbooks:** UM arquivo escrito em linguagem YAML com configuração simples, reutilizável e repetível.
            - **ad-hoc:** Quando utilizamos o Ansible para uma tarefa única, por exemplo: desligar, reiniciar, enviar um arquivo, inserimos um módulo diretamente da linha de comando. Já para comandos mais complexos, é necessário usar um Ansible Playbook.

## Seção 2: Criando laboratório

2. Instalação das ferramentas
    - Como utilizo Windows, tentarei reproduzir o laboratório totalmente em nuvem, instalei um Debian para ser servidor do Ansible, e irei instalar VMs lá para dar continuidade. Optei por ser assim porque não tem Ansible para Windows.
    - Virtualbox -> OK
    - Visual Code -> OK
    - Vagrant -> OK
    - Git -> OK
    - Ansible -> OK

3. Criando máquinas virtuais
    - Criei 4 vms no GCP, 2 com Ubuntu e 2 com centOS

4. Formas de acessar as VMs
    - Nesta aula o instrutor deu algumas dicas com a utilização do vagrant para laboratório em Virtualbox

5. Instalação do Ansible
    - Utilização do Ubuntu como server do Ansible

6. Criar o arquivo de inventário personalizado
    - Criando um arquivo dentro do server
    - `ansible -i hosts IP -k -m ping`
    - (A sessão ssh de uma VM para outra dura apenas 5 min)

7. Melhorando o arquivo de inventário
    - Adicionando nome aos servidores
    - `NOMEMAQUINA ansible_ssh_host=IPMAQUINA`
    - Adicionando um grupo de servidores
    - ```
        [GRUPO]
        SERVIDORES
      ```
    - Adicionando subgrupos de servidores
    - ```
        [GRUPO:children]
        SUBGRUPO1
        SUBGRUPO2
      ```
    - Adicionando usuário e senha para servidores
    - ```
        [GRUPO:vars]
        ansible_ssh_user=USUARIO ansible_ssh_pass=SENHA
      ```

8. Criando chave ssh e configurando
    - Adicionando chave privada no arquivo de configuração do ansible
    - `private_key_file=CAMINHODOARQUIVO`
    
9. Transferindo o Inventário para o arquivo padrão
    - No inicio do curso foi criado um arquivo com o nome `hosts`.
    - Nesse vídeo o instrutor mostra como colocar no arquivo padrão do ansible sem colocar o `-i ARQUIVO`, porém na instalação do Ansible não colocou os arquivos padrões que normalmente ficam em `/etc/ansible/`.

## Ad-hoc

10. Ad-hoc
    - O que significa Ad-hoc: Ad hoc significa “para esta finalidade", “para isso” ou "para este efeito". É uma expressão latina, geralmente usada para informar que determinado acontecimento tem caráter temporário e que se destina para aquele fim específico.
    - Um exame ad hoc, um método ad hoc, um cargo ou uma função ad hoc, são exemplos que definem a criação de algo provisório, que vai atender apenas determinado propósito.
    - ADHOC no Ansible, São comandos executados diretamente na linha de comando com a instrução que deseja, vamos supor que você precise dar um start/stop/restart em um serviço em uma série de servidores, ou você precise saber quais servidores estão com a configuração X, ou ver espaço em disco, memória, ou talvez você queira instalar um pacote, enfim são N possibilidades, mais você só quer fazer isso em um dado momento e não necessariamente guardar essa configuração em playbook.
    Parametro | Descrição
    :---------|:---------
    -i| Apresentar a localização do inventário
    -u | Apresentar o usuário que executará o comando
    -k | Solicitar a senha do usuário.
    -m | Módulo que será utilizado.
    -b | Substituir para o usuário root caso precisar.
    -a | argumento do módulo.



