# Architecture Discovery Process

## Objetivo

Descobrir e documentar a arquitetura técnica de um sistema legado através da análise assistida por IA do código-fonte, arquivos de configuração, estrutura do projeto, dependências e integrações.

O objetivo desta etapa é criar uma visão arquitetural suficientemente confiável para suportar:

* descoberta funcional
* análise de impacto
* modernização
* planejamento técnico
* geração de backlog
* definição de roadmap

---

# Escopo

Este processo deve identificar:

* stack tecnológica
* frameworks e bibliotecas
* módulos e componentes
* integrações externas
* persistência de dados
* padrões arquiteturais
* mecanismos de autenticação
* infraestrutura e deploy
* riscos técnicos
* dependências críticas
* sinais de débito técnico

---

# Entradas Esperadas

## Obrigatórias

* Código-fonte do projeto
* Estrutura de diretórios
* Arquivos de build/dependências
* Arquivos de configuração

## Opcionais

* Logs de execução
* Dockerfiles
* Arquivos Kubernetes/OpenShift
* Scripts CI/CD
* Documentação existente
* Banco de dados
* Diagramas antigos
* Tickets/Jira
* README

---

# Pré-Requisitos

* Acesso de leitura ao projeto
* Capacidade de indexação/análise do código
* Ferramenta de IA configurada
* Contexto organizacional disponível (quando existir)

---

# Princípios do Processo

## 1. Descoberta antes de inferência

Priorizar evidências observáveis no código antes de inferir comportamentos arquiteturais.

## 2. Evidência explícita

Toda conclusão arquitetural deve indicar:

* evidência encontrada
* arquivo de origem
* nível de confiança

## 3. Separação entre fato e hipótese

O processo deve diferenciar claramente:

* observações concretas
* inferências
* hipóteses arquiteturais

## 4. Arquitetura real vs arquitetura ideal

Documentar:

* arquitetura efetivamente implementada
* inconsistências
* desvios de padrão
* acoplamentos indevidos

## 5. Neutralidade tecnológica

O processo deve funcionar independentemente de:

* IDE
* modelo de IA
* fornecedor
* ferramenta específica

---

# Workflow

## Etapa 1 — Identificação Tecnológica

### Objetivo

Identificar stack principal do sistema.

### Atividades

* Detectar linguagens
* Detectar frameworks
* Detectar build system
* Detectar runtime
* Detectar servidor de aplicação
* Detectar containers
* Detectar orquestração

### Exemplos

* JBoss AS
* Spring
* FastAPI
* Django
* PHP
* Node.js
* OpenShift
* Docker
* Kubernetes

### Artefatos Gerados

* Stack inventory
* Runtime inventory

---

## Etapa 2 — Descoberta Estrutural

### Objetivo

Mapear a organização estrutural do sistema.

### Atividades

* Identificar módulos
* Identificar boundaries
* Identificar camadas
* Identificar responsabilidades
* Detectar monólito vs microsserviços
* Detectar compartilhamento indevido

### Artefatos Gerados

* Mapa estrutural
* Diagrama lógico textual
* Relação entre módulos

---

## Etapa 3 — Descoberta de Persistência

### Objetivo

Identificar mecanismos de persistência e fluxo de dados.

### Atividades

* Identificar bancos
* Identificar ORMs
* Identificar queries
* Detectar acesso direto ao banco
* Detectar stored procedures
* Detectar acoplamentos de persistência

### Artefatos Gerados

* Mapa de persistência
* Dependências de dados
* Riscos de acoplamento

---

## Etapa 4 — Descoberta de Integrações

### Objetivo

Mapear integrações externas e dependências organizacionais.

### Atividades

* Identificar APIs
* Identificar mensageria
* Identificar serviços externos
* Detectar autenticação/autorização
* Detectar integrações síncronas e assíncronas

### Exemplos

* SharePoint
* Azure AD
* Gemini
* GCS
* RabbitMQ
* Kafka
* SMTP
* REST
* SOAP

### Artefatos Gerados

* Mapa de integrações
* Dependências externas
* Fluxos de comunicação

---

## Etapa 5 — Descoberta de Infraestrutura

### Objetivo

Identificar características operacionais e de deploy.

### Atividades

* Identificar pipelines CI/CD
* Identificar infraestrutura alvo
* Identificar configuração de ambientes
* Identificar variáveis sensíveis
* Detectar observabilidade
* Detectar logging
* Detectar tracing
* Detectar monitoramento

### Artefatos Gerados

* Contexto operacional
* Dependências de infraestrutura
* Riscos operacionais

---

## Etapa 6 — Descoberta de Débito Técnico

### Objetivo

Identificar riscos técnicos e limitações estruturais.

### Atividades

* Detectar código obsoleto
* Detectar dependências vulneráveis
* Detectar acoplamento excessivo
* Detectar baixa modularidade
* Detectar ausência de testes
* Detectar riscos de performance
* Detectar riscos de segurança

### Artefatos Gerados

* Inventário de riscos
* Débitos técnicos
* Limitações arquiteturais

---

# Confidence Levels

## HIGH

Informações diretamente observáveis:

* frameworks
* dependências
* estrutura
* containers
* runtime

## MEDIUM

Inferências com evidências indiretas:

* boundaries
* padrões arquiteturais
* responsabilidades

## LOW

Inferências heurísticas:

* decisões arquiteturais históricas
* motivações
* intenções de design

---

# Artefato de Saída Esperado

O processo deve gerar:

`architecture-context.md`

---

# Estrutura Esperada do Artefato

```md
# Architecture Context

## System Overview
## Technology Stack
## Runtime Environment
## Modules and Components
## Persistence Layer
## Integrations
## Infrastructure
## Security
## Observability
## Technical Risks
## Technical Debt
## Architectural Patterns
## Constraints
## Confidence Assessment
```

---

# Critérios de Qualidade

O processo será considerado adequado quando:

* Stack principal identificada
* Principais integrações mapeadas
* Persistência identificada
* Runtime identificado
* Principais módulos identificados
* Dependências externas documentadas
* Riscos técnicos registrados
* Confidence level atribuído

---

# Limitações Conhecidas

Este processo pode apresentar limitações em:

* sistemas sem build funcional
* código parcialmente disponível
* lógica altamente dinâmica
* configurações externas não versionadas
* integrações implícitas
* regras distribuídas em banco

---

# Revisão Humana Recomendada

Os seguintes pontos devem ser revisados manualmente:

* inferências arquiteturais
* boundaries de domínio
* integrações críticas
* riscos classificados como HIGH impact
* hipóteses sem evidência suficiente

---

# Ferramentas Compatíveis

Este processo pode ser executado utilizando:

* Claude Code
* Cursor IDE
* ChatGPT
* Gemini
* Copilot
* MCPs especializados
* análise estática tradicional

A ferramenta utilizada não altera:

* workflow
* critérios
* artefatos esperados
* responsabilidades de revisão

---

# Próxima Etapa

Após concluir este processo, iniciar:

`02-functional-discovery.md`
