# AWS Cloud Foundations

## Visão Geral
Este repositório contém o resumo do curso AWS Cloud Foundations, cobrindo desde os conceitos básicos de computação em nuvem até segurança, custos e infraestrutura da AWS.

---

<details>
<summary>Conceitos e Infraestrutura Global</summary>

A AWS é uma plataforma de computação em nuvem que oferece serviços sob demanda para construir e escalar aplicações sem precisar gerenciar servidores físicos.

Infraestrutura Global:
- Regiões: áreas geográficas independentes.
- Zonas de disponibilidade (AZs): data centers isolados dentro de uma região.
- Edge locations: pontos de presença usados para entregar conteúdo com menor latência.

Principais vantagens:
- Escalabilidade e flexibilidade.
- Alta disponibilidade e redundância.
- Pagamento conforme o uso.
- Redução de custos e tempo de implantação.

</details>

---

<details>
<summary>Computação na Nuvem (EC2, Lambda, Containers)</summary>

A AWS oferece recursos de computação escaláveis e configuráveis para diferentes tipos de aplicações.

Amazon EC2:
- Permite criar máquinas virtuais configuráveis.
- Tipos de instância: general purpose, compute optimized, memory optimized, storage optimized e accelerated computing.
- Suporte a auto scaling e balanceamento de carga (ELB).

AWS Lambda:
- Executa código sob demanda sem precisar de servidor.
- Cobrança por tempo de execução.
- Boa opção para arquiteturas baseadas em eventos e microserviços.

Containers:
- Amazon ECS: orquestração nativa da AWS.
- Amazon EKS: orquestração Kubernetes gerenciada.
Ambos ajudam a implantar e escalar containers com mais facilidade.

</details>

---

<details>
<summary>Armazenamento e Bancos de Dados</summary>

Serviços de armazenamento:
- Amazon S3: armazenamento de objetos, com várias classes (Standard, Intelligent-Tiering, Glacier, Deep Archive).
- Amazon EBS: armazenamento em blocos ligado a instâncias EC2, com snapshots e criptografia.
- Amazon EFS: sistema de arquivos elástico e compartilhado.
- Amazon FSx: sistemas otimizados como Windows, Lustre, NetApp e ZFS.

Serviços de banco de dados:

| Tipo | Serviço | Uso principal |
|------|----------|---------------|
| Relacional | RDS, Aurora, Redshift | Aplicações empresariais, ERP, BI |
| Chave-valor | DynamoDB | Alta escala e baixa latência |
| Documento | DocumentDB | Armazenamento de JSON |
| Gráfico | Neptune | Redes sociais, fraudes |
| Tempo real | Timestream | IoT e métricas temporais |
| Ledger | QLDB | Registros auditáveis |
| In-memory | ElastiCache, MemoryDB | Cache e resposta rápida |
| Wide column | Keyspaces | Grandes volumes de dados |

</details>

---

<details>
<summary>Rede e Comunicação (VPC, Route 53, ELB)</summary>

Amazon VPC:
- Cria redes privadas dentro da nuvem.
- Controle sobre IPs, sub-redes e roteamento.

Amazon Route 53:
- Serviço de DNS escalável e disponível.
- Faz registro de domínios, roteamento e checagem de integridade.

Elastic Load Balancing (ELB):
- Distribui o tráfego entre várias instâncias EC2.
- Melhora a disponibilidade e reduz falhas.

Esses serviços formam a base de uma comunicação segura e escalável na AWS.

</details>

---

<details>
<summary>Segurança e Modelo de Responsabilidade Compartilhada</summary>

O modelo de responsabilidade compartilhada define o que é função da AWS e o que é função do cliente.

| AWS - Security of the Cloud | Cliente - Security in the Cloud |
|-----------------------------|--------------------------------|
| Proteção da infraestrutura física e lógica | Configuração e controle de acesso |
| Hardware, software e rede | Gerenciamento de usuários e chaves |
| Regiões e data centers | Criptografia, firewalls e sistemas operacionais |

Serviços de segurança:
- IAM: controle de usuários e permissões.
- KMS: gerenciamento de chaves criptográficas.
- AWS Shield: proteção contra ataques DDoS.
- AWS Artifact: relatórios de conformidade.

Áreas principais:
1. Identidade e acesso  
2. Proteção de rede e aplicações  
3. Criptografia de dados  
4. Detecção de ameaças  
5. Conformidade e auditoria

</details>

---

<details>
<summary>AWS Trusted Advisor</summary>

Ferramenta que fornece recomendações automáticas baseadas nas boas práticas da AWS.

| Categoria | Função |
|------------|--------|
| Custo | Identifica recursos ociosos e reduz gastos. |
| Desempenho | Otimiza uso de recursos e latência. |
| Segurança | Corrige permissões e falhas de configuração. |
| Tolerância a falhas | Melhora a resiliência e recuperação. |
| Limites de serviço | Alerta sobre uso próximo dos limites. |

</details>

---

<details>
<summary>Precificação e Custos</summary>

Princípios de precificação:
1. Pague apenas pelo que usar.  
2. Pague menos com reserva (1 a 3 anos).  
3. Descontos por volume de uso.  
4. Preços menores à medida que a AWS cresce.

Modelos de compra de EC2:

| Tipo | Descrição | Uso indicado |
|------|------------|---------------|
| On-demand | Pagamento por hora ou segundo. | Cargas imprevisíveis. |
| Reserved / Savings Plans | Até 75% de desconto com uso contínuo. | Aplicações estáveis. |
| Spot instances | Até 90% de desconto em capacidade ociosa. | Processos flexíveis. |

AWS Free Tier:
- Always Free: serviços permanentes.  
- 12 Months Free: EC2, S3 e RDS gratuitos por um ano.  
- Free Trials: testes temporários.

Cloud Financial Management:
Ferramentas para acompanhar e otimizar custos:
- Monitoramento em tempo real.
- Alertas de orçamento.
- Relatórios de uso.

</details>

---

## Conclusão Geral

A AWS oferece uma plataforma completa para computação em nuvem com serviços diversos em computação, armazenamento, rede, segurança e banco de dados.

Tem um modelo baseado em escalabilidade, disponibilidade e custo variável e é uma das soluções mais eficientes do mercado.

Entender a infraestrutura, o modelo de responsabilidade compartilhada e as estratégias de otimização de custos é essencial para conseguir fazer uso dessas tecnologias corretamente como desenvolvedor.
