# AWS EC2 – Implantação de Servidor Web e Gerenciamento de Infraestrutura

## 1. Visão Geral do Projeto.

Este projeto apresenta a implantação e o gerenciamento de uma instância Amazon EC2 utilizando os serviços da AWS.

O laboratório aborda a criação de um servidor virtual, instalação automatizada de um servidor web, configuração de segurança de rede, monitoramento da infraestrutura, dimensionamento de recursos e proteção da instância.

**Objetivo:** desenvolver conhecimentos práticos sobre infraestrutura em nuvem, redes, segurança e gerenciamento de recursos computacionais utilizando a AWS.

## 2. Serviços e Tecnologias Utilizados

- **Amazon EC2:** criação e gerenciamento de servidores virtuais.
- **Amazon VPC:** ambiente de rede virtual utilizado para implantação da instância.
- **Security Groups:** controle do tráfego de entrada e saída.
- **Amazon EBS:** armazenamento em bloco associado à instância.
- **Amazon CloudWatch:** monitoramento de métricas da instância.
- **Amazon Linux 2023:** sistema operacional do servidor.
- **Apache HTTP Server:** serviço responsável pela hospedagem da página web.
- **User Data:** automação da instalação e configuração do servidor.
- **Bash:** execução de comandos para configuração do ambiente.

## 3. Etapas de Implementação

### 3.1. Criação da Instância EC2

- Criação de uma instância EC2 utilizando Amazon Linux 2023.
- Seleção do tipo de instância t3.micro.
- Configuração da instância dentro de uma VPC.
- Criação de um Security Group.
- Ativação da proteção contra encerramento acidental (Termination Protection).
- Configuração de um volume EBS de 8 GiB.

**Evidência – Instância EC2 criada:**

<img width="1460" height="327" alt="image" src="https://github.com/user-attachments/assets/78457c14-5bb7-4d9c-b6d8-0e66fdf1b02a" />
<img width="1541" height="364" alt="image" src="https://github.com/user-attachments/assets/059e61ed-798b-41ca-bd4d-0175386737a4" />
<img width="776" height="193" alt="image" src="https://github.com/user-attachments/assets/5f82fe07-51bb-48e9-ad18-62c738c2f102" />

<img width="1648" height="354" alt="image" src="https://github.com/user-attachments/assets/a9f61656-dcf1-4580-ad65-279ba994f283" />



### 3.2. Instalação Automatizada do Servidor Web

Foi utilizado o recurso User Data do EC2 para automatizar a instalação e configuração do servidor Apache.

```bash
#!/bin/bash
yum -y install httpd
systemctl enable httpd
systemctl start httpd
echo '<html><h1>Hello From Your Web Server!</h1></html>' > /var/www/html/index.html
```

O script executa automaticamente:

- Instalação do servidor Apache.
- Configuração para iniciar automaticamente junto com o sistema.
- Inicialização do serviço web.
- Criação de uma página HTML simples.

- ###. Captura de tela da Instância>

- <img width="1425" height="816" alt="image" src="https://github.com/user-attachments/assets/f3599dd4-99a7-4dc4-ae85-3b7dd5c87c29" />


### 3.3. Configuração de Segurança de Rede

Foi realizada a configuração do Security Group para controlar o tráfego de entrada da instância.

- Bloqueio inicial do tráfego HTTP.
- Criação de uma regra de entrada para HTTP na porta 80.
- Liberação de acesso a partir de qualquer endereço IPv4.
- Teste de acesso ao servidor web por meio do endereço IPv4 público.

**Evidência – Configuração do Security Group:**
<img width="1694" height="652" alt="image" src="https://github.com/user-attachments/assets/c4f78c9b-6137-4767-8066-d0e86bcef75f" />


### 3.4. Teste de Acesso ao Servidor Web

Após liberar o tráfego HTTP no Security Group, foi realizado o teste de acesso ao servidor Apache por meio do navegador.

A página apresentou a mensagem:

**Hello From Your Web Server!**

**Evidência – Página web hospedada na EC2:**

<img width="1819" height="989" alt="image" src="https://github.com/user-attachments/assets/d6dd7991-949c-4b32-91a1-3b69afa7a561" />


### 3.5. Monitoramento da Instância

Foram explorados os recursos de monitoramento disponíveis na AWS:

- Verificação do status da instância.
- Verificação de acessibilidade do sistema.
- Verificação de acessibilidade da instância.
- Análise de métricas pelo Amazon CloudWatch.
- Captura de tela da instância para auxiliar na solução de problemas.

**Evidência – Monitoramento da instância:**

<img width="1690" height="686" alt="image" src="https://github.com/user-attachments/assets/85c42659-dd20-4704-9d45-a0395d66f8c6" />


### 3.6. Dimensionamento da Infraestrutura (Scaling)

Foi realizado o redimensionamento dos recursos computacionais e de armazenamento.

| Recurso | Configuração inicial | Configuração final |
|---|---|---|
| Tipo de instância | t3.micro | t3.small |
| Volume EBS | 8 GiB | 10 GiB |

A instância foi interrompida antes da alteração do tipo de máquina e reiniciada após as modificações.
<img width="1702" height="512" alt="image" src="https://github.com/user-attachments/assets/740d4db0-2aab-460b-8973-ce561e3823f4" />


**Evidência – Redimensionamento da instância:**

<img width="1246" height="765" alt="image" src="https://github.com/user-attachments/assets/f1c5463e-9eec-46c4-b5ac-b04450f1cc25" />

<img width="782" height="404" alt="image" src="https://github.com/user-attachments/assets/d9b9f82e-099c-4e0b-8ce2-2c1815addcc0" />



### 3.7. Teste de Proteção contra Encerramento

Foi realizado um teste da funcionalidade Termination Protection.

Inicialmente, foi tentado encerrar a instância com a proteção ativada, e a solicitação foi bloqueada pela AWS.

Em seguida, a proteção foi desativada e a instância foi encerrada com sucesso.
<img width="616" height="291" alt="image" src="https://github.com/user-attachments/assets/db2fb588-0e70-4614-b0a8-521a74ae28d1" />
<img width="447" height="264" alt="image" src="https://github.com/user-attachments/assets/d54bb635-f308-4231-886c-dfc478961970" />
<img width="304" height="143" alt="image" src="https://github.com/user-attachments/assets/2b96e41e-aadc-46c8-9bfe-797a9b98a5be" />


