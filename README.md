 # 🔴  Atividade - DevSecOps - Projeto Final AWS


## 🟢 Proposta de Migração para AWS – Fast Engineering S/A

### Empresa executora: TI SOLUÇÕES INCRÍVEIS

# 1. Contexto do Projeto

### A *Fast Engineering S/A* enfrenta um crescimento acelerado em seu e-commerce, causando limitações na infraestrutura atual. A demanda por acessos e compras aumentou significativamente, tornando necessário um ambiente mais escalável, seguro e de alta disponibilidade.

### Diante desse cenário, a melhor solução é migrar a aplicação para a AWS seguindo um processo em duas fases:

_ _ _ _ _
###  Fase 1 
 >**Lift-and-Shift (As-Is):**
 >>Migração rápida da infraestrutura atual para a AWS, garantindo continuidade operacional sem grandes mudanças.
### Fase 2
>**Modernização:**
>> Após a migração, otimizar a infraestrutura para Kubernetes e implementar melhores práticas em Cloud AWS.

_ _ _ _ _
_ _ _ _ _
# 🔵 Diagrama da Infraestrutura atual da empresa *Fast Engineering S/A*

![Imagem diagrama atual da infraestrutura da empresa](img/img-dg-atual.png)

## Fase 1: Lift-and-Shift – Migração As-Is
 Nosso foco nesta etapa é garantir uma transição rápida e segura da aplicação para a AWS, utilizando os serviços 

**AWS MGN (AWS Application Migration Service)**.
   > Para replicação de servidores 

**AWS DMS (Database Migration Service)**.
   > Para migração de banco de dados

# 2. Escopo Detalhado da Migração As-Is

## 2.1. Atividades Necessárias
Para realizar a migração Lift-and-Shift, seguiremos estas etapas:

### Mapeamento da Infraestrutura Atual:
- **Servidor Frontend** (React)
- **Servidor Backend** (3 APIs, Ngnix)
- **Servidor de Banco de Dados** (MySQL)

### Configuração da AWS:
- Criar ambiente na AWS para replicação e testes.

- Configurar **AWS MGN** (Application Migration Service) para replicação contínua dos servidores, de maneira econômica.

 - Configurar **AWS DMS** para migração do banco de dados, minimizando o tempo de inatividade e garantindo a integridade dos dados durante a migração.

- Ajustar permissões e regras de segurança.

### Replicação de Dados e Testes:
- Instalar o **AWS MGN Agent** nos servidores locais para replicação.
- Utilizar o **AWS DMS** para migrar o banco de dados do ambiente local para a AWS, com a replicação contínua dos dados.
- Criar máquinas **EC2** espelhando a infraestrutura atual.
- Testar a aplicação na AWS antes da migração final.

### Cutover (Troca para Produção):
- Redirecionar tráfego para a infraestrutura na AWS.
- Desativar os servidores antigos após validação.

## 2.2. Ferramentas Utilizadas


- AWS EC2 para servidores.
- Amazon RDS para banco de dados.
- AWS Elastic Load Balancer (ELB) para balanceamento de carga.
- Amazon MGN para Migração de dados
- Amazon DMS para migração de banco de dados.


---

# 2.3  Controle de Segurança Básico para a Migração

A migração será realizada com o seguinte controle de segurança básico para garantir a proteção da infraestrutura:


##  A VPC de Staging

-  Criar um ambiente temporário com uma subnet pública para hospedar o servidor de replicação. Esse servidor recebe os dados do ambiente local por meio do AWS Replication Agent.


##  VPC (Virtual Private Cloud)
- Criar uma **VPC isolada**, com subnets públicas e privadas, para garantir que a rede da AWS esteja isolada e protegida.

##  Security Groups
- Configuração de **Security Groups** para permitir o tráfego de rede apenas entre os recursos autorizados, como servidores backend, frontend e banco de dados.

- Grupos de segurança incluindo as portas 443 (HTTPS), 1500 (MGN), (3306) MySQL

# 3. Processo de Backup

Embora a migração **Lift-and-Shift** seja realizada rapidamente, a segurança dos dados será priorizada com um processo de backup :




### 4. Custo Estimado na AWS

Abaixo estão os serviços que serão utilizados para migrar e hospedar sua aplicação na AWS, com uma estimativa de custos mensais:

![Imagemde estimativade custo migração infra para  aws ](img/img-custos-migração.png)

---

### **Total Estimado dos Custos Mensais**

   Custo Total Mensal: $936.41 USD.


---

# 🟢 **Atividades Necessárias para a Modernização**

A modernização envolve transformar a infraestrutura já migrada para uma arquitetura mais escalável, eficiente e automatizada. As atividades para essa modernização incluem:

## 1. Transformação da Aplicação em Containers
- **Dockerizar a aplicação** para que ela seja executada em pods no **Amazon EKS**.

## 2. Implantação no Kubernetes
- Configuração do cluster **Amazon EKS** para orquestrar containers.
- Criação dos **Deployments** no Kubernetes para a aplicação, garantindo alta disponibilidade e escalabilidade.

## 3. Configuração de Auto Scaling e Load Balancer
- Definir políticas de **Auto Scaling** para as instâncias EC2 dos nós do Kubernetes (EKS) com base na carga.
- Configuração do **Load Balancer** para distribuir o tráfego entre os pods de forma eficiente.

## 4. Ajustes nas Subnets
- Ajustar a configuração de subnets públicas para os nós EKS e subnets privadas para o banco de dados **RDS MySQL**.

## 5. Configuração de Rede e Segurança
- Configuração de **Security Groups** e **NACLs** para garantir uma comunicação segura entre os componentes da infraestrutura.
- Implementação de **AWS WAF** para proteger a aplicação contra ataques.

## 6. Monitoramento e Logs
- Implementação do **AWS CloudWatch** para monitoramento de logs, métricas e eventos da infraestrutura.

## 7. Configuração de Backup e Recuperação
- Implementação de backups regulares para o banco de dados **RDS MySQL** e arquivos estáticos em **S3**.

---



---

# 🔵 Diagrama da Infraestrutura na AWS

Aqui está o diagrama básico da infraestrutura modernizada na AWS:

![Imagem diagrama atual da infraestrutura da empresa](img/img-dg-modernizado.png)

# Descrição do Fluxo

- **Acesso dos Usuários**: Os usuários acessam a aplicação pela internet.
- **Filtragem de Tráfego**: O tráfego é filtrado pelo AWS WAF e distribuído via Amazon CloudFront.
- **Balanceamento de Carga**: O Load Balancer distribui o tráfego para o Amazon EKS.
- **Dentro da VPC**:
  - **Subnets Públicas**: Contêm os nós EC2 do Amazon EKS.
  - **Subnets Privadas**: Contêm o RDS MySQL e grupos de Auto Scaling.
- **Auto Scaling**: O Auto Scaling Group ajusta a quantidade de instâncias EC2 dos nós Kubernetes conforme a demanda.
- **IAM**: Gerencia o acesso a recursos na AWS.
- **Amazon S3**: Armazena arquivos estáticos e backups.
- **Amazon CloudWatch**: Coleta logs, métricas e eventos da infraestrutura.
---

# Requisitos de Segurança

- **AWS IAM**: Gerenciamento de permissões, garantindo que cada serviço tenha apenas o acesso necessário.
- **AWS WAF**: Proteção contra ataques à aplicação, como SQL Injection e Cross-Site Scripting (XSS).
- **Security Groups e NACLs**: Controle de tráfego entre as subnets públicas e privadas, além do tráfego interno da VPC.
- **Criptografia**: Todos os dados em trânsito e em repouso são criptografados, tanto no RDS MySQL quanto no S3.
- **CloudWatch**: Monitoramento de logs para detectar e alertar sobre comportamentos suspeitos ou falhas de segurança.
- **CloudFront**: Proteção adicional para os recursos estáticos, além de fornecer uma camada extra de segurança e desempenho.
---

# Processo de Backup

1. **RDS MySQL**:
   - Backup automático diário utilizando RDS snapshots.
   - Backups manuais serão feitos conforme a necessidade.
2. **Amazon S3**:
   - Armazenamento de backups de arquivos estáticos e logs.
3. **Amazon CloudWatch Logs**:
   - Monitoramento contínuo e armazenamento de logs para auditoria e recuperação de falhas.
4. **AWS Backup**:
   - Ferramenta para automação do backup de recursos em toda a infraestrutura, incluindo RDS e EFS (se necessário).

---

# Ferramentas Utilizadas

As ferramentas específicas para a modernização são:


# Custo da Infraestrutura na AWS (AWS Calculator)

---

# Conclusão

A modernização para Kubernetes na AWS com Amazon EKS, RDS MySQL e CloudWatch permitirá que a Fast Engineering S/A escale sua infraestrutura de maneira eficiente, segura e com alta disponibilidade. Com a utilização de auto scaling, load balancers e ferramentas de segurança como AWS WAF e IAM, a infraestrutura estará preparada para suportar um tráfego maior, com resiliência e flexibilidade.

Além disso, o monitoramento em tempo real através do CloudWatch, o uso de backups automáticos e criação de snapshots do RDS garantirão que a infraestrutura seja bem mantida, segura e capaz de se recuperar rapidamente de falhas, mantendo a continuidade operacional sem interrupções.
