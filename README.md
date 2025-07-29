# DESAFIO-FINAL--MODULO-1-CYBERSEC
# Análise de Segurança de Rede Corporativa Simulada


# Projeto Técnico: Mapeamento de Rede Corporativa (Docker)

Este repositório contém o projeto técnico realizado como parte da Trilha de Formação em Cibersegurança – Módulo 1.

## 📄 Conteúdo

- Relatório técnico final (PDF)
- Evidências de exploração e enumeração
- Diagrama da rede corporativa simulada
- Plano de ação baseado no princípio 80/20

## 🛠️ Ferramentas utilizadas

- Kali Linux (nmap, rustscan,)
- Docker para ambiente simulado
- Canva (diagrama)

Este repositório contém o relatório de uma análise  de um ambiente de rede corporativo, focado na identificação de ativos, serviços expostos e potenciais vulnerabilidades. O objetivo é orientar a tomada de decisões para o reforço da segurança da informação na organização.



## 🚀 Sumário Executivo

Este relatório apresenta uma análise detalhada do ambiente de rede corporativo simulado, segmentado em três sub-redes principais: **infraestrutura (infra_net)**, **corporativa (corp_net)** e **convidados (guest_net)**.

**Pontos-chave identificados:**
* A **sub-rede de infraestrutura** concentra servidores críticos (FTP, MySQL e Samba) com serviços expostos nas portas 21, 3306, 139 e 445, demandando atenção prioritária.
* A **sub-rede corporativa** demonstrou um bom nível de segurança, com estações de trabalho protegidas e sem serviços acessíveis externamente, mas o roteador merece atenção contínua.
* A **sub-rede de convidados** possui poucos ativos, mas com serviços abertos, indicando a necessidade de controle mais rigoroso de acessos.

A principal vulnerabilidade identificada está na exposição de serviços da infraestrutura. O plano de ação adota o princípio 80/20, priorizando medidas de alto impacto e rápida implementação.



## 🎯 Objetivo e Escopo da A Ação

O objetivo foi realizar o mapeamento completo da rede corporativa simulada, identificando ativos, serviços expostos e potenciais vulnerabilidades que possam comprometer a segurança da informação.

**Sub-redes Analisadas:**
* `infra_net` (10.10.30.0/24) – Servidores de serviços críticos (FTP, MySQL, Samba).
* `corp_net` (10.10.10.0/24) – Estações de trabalho e roteador da empresa.
* `guest_net` (10.10.50.0/24) – Dispositivos de convidados e visitantes.

**Metodologia Utilizada:**
* **Reconhecimento Ativo:** Varredura com Nmap e Rustscan (TCP/UDP).
* **Enumeração de Serviços:** Busca por FTP, MySQL, Samba e HTTP.
* **Inventário de Ativos:** Organização por sub-redes.
* **Diagnóstico de Exposição:** Com base nos serviços inseguros ou expostos.
* **Plano de Ação:** Com foco em priorização 80/20.


## 🌐 Topologia e Inventário da Rede

### Diagrama de Topologia de Rede

**Nota:** Para uma versão visualmente mais elaborada, consulte a imagem do diagrama na seção de [Anexos e Evidências](#-anexos-e-evidências)



### Inventário de Ativos

**Sub-rede: corp_net (10.10.10.0/24)**



| IP           | Hostname        | Serviço Detectado | Sistema Operacional |
| :----------- | :-------------- | :---------------- | :------------------ |
| 10.10.10.1   | Gateway/Router  | Nenhum (fechado)  | Desconhecido        |
| 10.10.10.10  | WS_001          | SSH, HTTP         | Provável Linux      |
| 10.10.10.101 | WS_002          | HTTP              | Desconhecido        |
| 10.10.10.127 | WS_003          | HTTP              | Desconhecido        |
| 10.10.10.222 | WS_004          | HTTP              | Desconhecido        |



**Sub-rede: guest_net (10.10.50.0/24)**

| IP           | Hostname       | Serviço Detectado | Sistema Operacional |
| :----------- | :------------  | :---------------- | :------------------ |
| 10.10.50.1   | Gateway/Router | Nenhum (fechado)  | Desconhecido        |
| 10.10.50.10  | Device_01      | HTTP              | Desconhecido        |
| 10.10.50.11  | Device_02      | HTTP              | Desconhecido        |
| 10.10.50.12  | Device_03      | HTTP              | Desconhecido        |



**Sub-rede: infra_net (10.10.30.0/24)**
 
 
| IP             | Hostname       | Serviço Detectado | Sistema Operacional |                                  |
| :-----------   | :------------- |: ---------------- | :------------------ | :------------------------------|  
| 10.10.30.10    | FTP Server     | FTP               | Provável Linux      | Porta 21 aberta, sugere acesso |  |  anônimo          
| 10.10.30.11    | MySQL Server   | MySQL             | Desconhecido        | Versão 8.0.42 detectada, porta |  3306 aberta      |
| 10.10.30.15    | Samba Server   | Samba (SMB)       | Desconhecido        | Portas SMB abertas (139, 445),  ]|  SMBv2/SMBv3      |



## ⚠️ Diagnóstico de Exposição e Riscos


Esta seção detalha os principais pontos de atenção observados na rede simulada, com foco em exposição de serviços, fragilidades de configuração e potenciais vetores de risco:

1.  **Serviços Críticos Acessíveis na Infraestrutura:** Serviços como FTP, MySQL e SMB identificados com configurações padrão que representam risco de exploração.
2.  **Segmentação Lógica Insuficiente entre Sub-redes:** Falta de controle efetivo de comunicação (e.g., firewalls ou ACLs) entre as sub-redes, permitindo movimentação lateral.
3.  **Políticas de Acesso Insuficientes:** Ausência de autenticação robusta ou controle refinado de permissões nos serviços, como SMB sem assinatura obrigatória de mensagens.
4.  **Ausência de Monitoramento e Backup Visível:** Indica falta de políticas de auditoria e contingência para resposta a incidentes.

**Resumo de Riscos por Prioridade:**

| Sub-rede    | Nível de Exposição | Prioridade de Ação |
| :---------- | :----------------- | :----------------- |
| infra_net   | Alto               | Alta               |
| corp_net    | Moderado           | Monitoramento      |
| guest_net   | Moderado           | Atenção contínua   |



## ✅ Recomendações Técnicas e Estratégicas


* **Segmentação de Rede:** Implementar regras de firewall rígidas (ACLs) entre as sub-redes.
* **Monitoramento Ativo:** Implementar um sistema de monitoramento de logs (SIEM) e configurar alertas.
* **Controle de Acesso em Serviços Críticos:** Configurar autenticação forte (senhas complexas, MFA) e limitar IPs de origem. Desativar acesso anônimo e impor assinatura SMB.
* **Atualização e Hardening de Sistemas:** Gerenciamento de patches e vulnerabilidades; aplicar hardening de segurança.
* **Gerenciamento de Firewall:** Revisar e otimizar regras de firewall de borda e internas.
* **Contingência e Auditoria:** Implementar solução de backup validada e rotinas de auditoria.



## 📈 Plano de Ação Prioritário (80/20)


Para uma rápida melhoria na segurança, adotamos o princípio 80/20:

| Fase | Ação                                                 | Impacto | Esforço | Prazo Estimado |
| :--- | :--------------------------------------------------- | :------ | :------ | :------------- |
| 1    | Desabilitar acessos anônimos em FTP e Samba; impor autenticação. | Alto    | Baixo   | 1 semana       |
| 1    | Configurar autenticação forte no banco MySQL.        | Alto    | Baixo   | 1 semana       |
| 2    | Implantar sistema de monitoramento e alertas em tempo real (SIEM). | Médio   | Médio   | 2 semanas      |
| 2    | Reforçar segmentação e regras de firewall entre sub-redes. | Médio   | Médio   | 2 semanas      |
| 3    | Capacitar equipe em segurança e resposta a incidentes (procedimentos e ferramentas). | Médio   | Médio   | 3 semanas      |



## 📂 Anexos e Evidências



* **Diagrama de Topologia Ilustrado:**
    * Anexo Diagrama

* **+Evidências**
    * Anexos
