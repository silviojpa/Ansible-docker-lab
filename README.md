# Laboratório de Estudos Ansible com Docker

Este projeto cria um ambiente de laboratório local para estudar e praticar Ansible. Ele utiliza Docker e Docker Compose para provisionar rapidamente "nós" (servidores em containers) que podem ser gerenciados pelo Ansible a partir da máquina host.

## Tecnologias Utilizadas
* Ansible
* Docker
* Docker Compose
* Ubuntu (como base para os nós e para o host)

## Estrutura do Projeto

ansible-docker-lab/
├── .gitignore
├── README.md
├── ansible.cfg
├── docker-compose.yml
├── inventory.ini
├── docker/
│   └── Dockerfile
└── playbooks/
└── install_htop.yml

## Como Usar

1.  **Clone o Repositório:**
    ```bash
    git clone [https://github.com/SEU-USUARIO/ansible-docker-lab.git](https://github.com/SEU-USUARIO/ansible-docker-lab.git)
    cd ansible-docker-lab
    ```

2.  **Suba o Ambiente Docker:**
    ```bash
    docker-compose up -d
    ```

3.  **Atualize o Inventário:**
    Obtenha os endereços IP dos containers com os comandos abaixo e atualize o arquivo `inventory.ini` com os IPs corretos.
    ```bash
    # Obter IP do node1
    docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ansible-node1

    # Obter IP do node2
    docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ansible-node2
    ```

4.  **Teste a Conexão Ansible:**
    ```bash
    ansible all -m ping
    ```
    Você deve receber uma resposta `SUCCESS` de ambos os nós.

5.  **Execute o Playbook de Exemplo:**
    ```bash
    ansible-playbook playbooks/install_htop.yml
    ```

## Comandos Úteis

* **Ver containers em execução:** `docker-compose ps`
* **Derrubar o ambiente:** `docker-compose down`
* **Acessar um container:** `docker exec -it ansible-node1 bash`

