# Functional Discovery Process

## Objetivo

Descobrir e documentar o comportamento funcional de um sistema legado através da análise assistida por IA do código-fonte, arquitetura identificada, fluxos de execução, integrações e persistência.

O objetivo desta etapa é transformar evidências técnicas em conhecimento funcional utilizável para:

* modernização de sistemas
* entendimento de domínio
* geração de backlog
* análise de impacto
* decomposição de funcionalidades
* descoberta de regras de negócio
* documentação funcional

---

# Escopo

Este processo deve identificar:

* capacidades funcionais
* fluxos de negócio
* regras de negócio implícitas
* atores do sistema
* integrações funcionais
* jornadas operacionais
* entidades de domínio
* side effects
* dependências funcionais
* funcionalidades críticas
* funcionalidades obsoletas
* lacunas de conhecimento

---

# Entradas Esperadas

## Obrigatórias

* Código-fonte
* Artefato gerado em:

  * `01-architecture-discovery.md`
  * `architecture-context.md`

## Opcionais

* Logs
* Tickets/Jira
* Banco de dados
* APIs
* Swagger/OpenAPI
* Documentação funcional antiga
* Fluxos operacionais
* Screenshots
* Telas do sistema
* Relatos de usuários

---

# Pré-Requisitos

* Arquitetura minimamente identificada
* Stack conhecida
* Módulos identificados
* Principais integrações conhecidas

---

# Princípios do Processo

## 1. Funcionalidade emerge do comportamento

A descoberta funcional deve priorizar:

* fluxo executado
* regras observadas
* persistência
* integrações
* efeitos colaterais

e não apenas nomes de classes ou arquivos.

---

## 2. Regras de negócio podem estar dispersas

Assumir que sistemas legados podem distribuir regras em:

* controllers
* services
* queries SQL
* procedures
* jobs
* validações
* integrações externas
* frontend
* banco de dados

---

## 3. Diferenciar evidência de inferência

Toda funcionalidade identificada deve indicar:

* evidência encontrada
* origem da inferência
* confidence level

---

## 4. Priorizar fluxos reais

Priorizar:

* fluxos efetivamente utilizados
* regras implementadas
* integrações reais

em vez de:

* intenções arquiteturais
* funcionalidades parcialmente implementadas
* código morto

---

## 5. Descoberta funcional é probabilística

A IA pode:

* inferir incorretamente
* unir fluxos independentes
* omitir regras implícitas
* interpretar incorretamente nomenclaturas

Todo output deve ser revisável.

---

# Workflow

## Etapa 1 — Identificação de Capacidades Funcionais

### Objetivo

Identificar quais capacidades de negócio o sistema oferece.

### Atividades

* Identificar funcionalidades principais
* Identificar módulos funcionais
* Identificar operações críticas
* Detectar funcionalidades administrativas
* Detectar funcionalidades batch
* Detectar automações

### Exemplos

* emissão de DANFE
* autenticação
* gestão documental
* processamento de pagamentos
* workflow operacional
* processamento de arquivos
* integração com SUS

### Artefatos Gerados

* Lista de capacidades
* Inventário funcional

---

## Etapa 2 — Descoberta de Fluxos de Negócio

### Objetivo

Mapear os fluxos executados pelo sistema.

### Atividades

* Identificar entrypoints
* Seguir fluxo de execução
* Identificar decisões condicionais
* Detectar regras de validação
* Detectar side effects
* Detectar persistência envolvida
* Detectar integrações acionadas

### Artefatos Gerados

* Fluxos funcionais
* Sequência operacional textual
* Dependências funcionais

---

## Etapa 3 — Descoberta de Regras de Negócio

### Objetivo

Inferir regras de negócio implementadas no sistema.

### Atividades

* Detectar validações
* Detectar restrições
* Detectar regras condicionais
* Detectar cálculos
* Detectar políticas
* Detectar regras temporais
* Detectar regras distribuídas

### Exemplos

* validações fiscais
* regras SUS
* regras tributárias
* controle de status
* workflows de aprovação

### Artefatos Gerados

* Catálogo de regras
* Regras críticas
* Regras implícitas

---

## Etapa 4 — Descoberta de Entidades de Domínio

### Objetivo

Identificar entidades funcionais relevantes.

### Atividades

* Identificar entidades persistidas
* Detectar DTOs
* Detectar aggregates
* Detectar objetos de negócio
* Detectar relacionamentos

### Artefatos Gerados

* Modelo conceitual
* Entidades principais
* Relacionamentos

---

## Etapa 5 — Descoberta de Atores e Perfis

### Objetivo

Identificar usuários, sistemas consumidores e perfis envolvidos.

### Atividades

* Detectar autenticação
* Detectar perfis
* Detectar permissões
* Detectar integrações consumidoras
* Detectar automações externas

### Artefatos Gerados

* Lista de atores
* Perfis operacionais
* Dependências externas

---

## Etapa 6 — Descoberta de Funcionalidades Críticas

### Objetivo

Identificar funcionalidades com maior impacto operacional.

### Atividades

* Detectar fluxos centrais
* Detectar funcionalidades com múltiplas integrações
* Detectar funcionalidades sensíveis
* Detectar riscos operacionais
* Detectar pontos únicos de falha

### Artefatos Gerados

* Inventário crítico
* Priorização funcional
* Dependências críticas

---

## Etapa 7 — Descoberta de Lacunas

### Objetivo

Identificar limitações e incertezas da descoberta funcional.

### Atividades

* Detectar funcionalidades incompletas
* Detectar código morto
* Detectar fluxos não compreendidos
* Detectar ausência de contexto
* Detectar inferências frágeis

### Artefatos Gerados

* Lista de lacunas
* Hipóteses pendentes
* Necessidades de validação humana

---

# Confidence Levels

## HIGH

Informações observáveis diretamente:

* endpoints
* jobs
* tabelas
* integrações
* fluxos explícitos

## MEDIUM

Inferências baseadas em evidências indiretas:

* regras de negócio
* responsabilidades
* capacidades funcionais

## LOW

Inferências heurísticas:

* intenção original
* comportamento operacional completo
* regras externas ao código
* fluxos dependentes de contexto humano

---

# Artefato de Saída Esperado

O processo deve gerar:

`functional-map.md`

---

# Estrutura Esperada do Artefato

```md id="ulq0nq"
# Functional Map

## System Purpose
## Functional Capabilities
## Main Business Flows
## Actors
## Business Rules
## Domain Entities
## Integrations
## Critical Functionalities
## Side Effects
## Operational Dependencies
## Risks
## Functional Gaps
## Confidence Assessment
```

---

# Critérios de Qualidade

O processo será considerado adequado quando:

* funcionalidades principais identificadas
* fluxos principais documentados
* regras críticas mapeadas
* integrações funcionais identificadas
* atores identificados
* side effects relevantes registrados
* lacunas documentadas
* confidence levels atribuídos

---

# Limitações Conhecidas

Este processo pode apresentar limitações em:

* regras implementadas fora do código
* lógica distribuída em banco
* sistemas altamente acoplados
* código morto não identificado
* nomenclaturas inconsistentes
* dependências organizacionais implícitas

---

# Revisão Humana Recomendada

Os seguintes pontos devem ser revisados manualmente:

* regras críticas de negócio
* fluxos financeiros/fiscais
* inferências de domínio
* funcionalidades classificadas como críticas
* hipóteses com confidence LOW

---

# Ferramentas Compatíveis

Este processo pode ser executado utilizando:

* Claude Code
* Cursor IDE
* ChatGPT
* Gemini
* Copilot
* MCPs especializados
* ferramentas de análise estática

A ferramenta utilizada não altera:

* workflow
* critérios
* artefatos esperados
* responsabilidades de revisão

---

# Próxima Etapa

Após concluir este processo, iniciar:

`03-backlog-generation.md`
