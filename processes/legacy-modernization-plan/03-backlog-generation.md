# Backlog Generation Process

## Objetivo

Transformar o conhecimento arquitetural e funcional descoberto no sistema legado em um backlog estruturado de modernização, evolução ou reengenharia.

O objetivo desta etapa é gerar artefatos utilizáveis para:

* planejamento técnico
* modernização incremental
* decomposição de iniciativas
* priorização
* planejamento de roadmap
* definição de entregas
* gestão de risco
* refinamento técnico-funcional

---

# Escopo

Este processo deve gerar:

* epics
* user stories
* iniciativas técnicas
* melhorias arquiteturais
* backlog incremental
* dependências
* riscos
* critérios de aceite
* estratégias de modernização

---

# Entradas Esperadas

## Obrigatórias

* `architecture-context.md`
* `functional-map.md`

## Opcionais

* Jira
* requisitos de negócio
* restrições organizacionais
* roadmap estratégico
* limitações operacionais
* informações de equipe
* prioridades executivas
* SLAs
* restrições regulatórias

---

# Pré-Requisitos

* Arquitetura identificada
* Fluxos principais documentados
* Funcionalidades principais identificadas
* Dependências críticas conhecidas

---

# Princípios do Processo

## 1. Modernização incremental

Priorizar:

* evolução gradual
* desacoplamento incremental
* entregas pequenas
* redução contínua de risco

Evitar:

* big bang rewrite
* reescrita completa sem necessidade
* substituição integral prematura

---

## 2. Backlog baseado em evidências

Toda história deve possuir rastreabilidade para:

* fluxo funcional
* componente arquitetural
* regra de negócio
* risco identificado
* limitação observada

---

## 3. Separar negócio de infraestrutura

O backlog deve diferenciar:

* funcionalidades de negócio
* melhorias técnicas
* débitos técnicos
* observabilidade
* segurança
* automação
* infraestrutura

---

## 4. Priorizar redução de risco

A priorização deve considerar:

* criticidade operacional
* acoplamento
* obsolescência
* ausência de testes
* dependências externas
* impacto organizacional

---

## 5. Evitar over-engineering

Não criar:

* abstrações desnecessárias
* microsserviços artificiais
* refatorações sem benefício mensurável
* backlog excessivamente especulativo

---

# Workflow

## Etapa 1 — Identificação de Iniciativas

### Objetivo

Identificar grandes áreas de modernização.

### Atividades

* Agrupar funcionalidades relacionadas
* Agrupar módulos relacionados
* Detectar áreas críticas
* Detectar oportunidades de desacoplamento
* Detectar modernizações necessárias

### Exemplos

* modernização de autenticação
* desacoplamento de integração
* observabilidade
* migração de runtime
* modernização frontend
* melhoria de processamento batch

### Artefatos Gerados

* Lista de iniciativas
* Macro backlog

---

## Etapa 2 — Geração de Epics

### Objetivo

Transformar iniciativas em épicos organizáveis.

### Atividades

* Definir objetivo do epic
* Identificar impacto
* Identificar dependências
* Identificar riscos
* Identificar áreas afetadas

### Artefatos Gerados

* Lista de epics
* Dependências entre epics

---

## Etapa 3 — Geração de User Stories

### Objetivo

Decompor épicos em entregas executáveis.

### Atividades

* Criar histórias pequenas
* Garantir independência parcial
* Garantir rastreabilidade
* Definir valor técnico ou funcional
* Definir critérios de aceite

### Tipos de histórias

* funcional
* técnica
* arquitetura
* segurança
* observabilidade
* testes
* infraestrutura

### Artefatos Gerados

* User stories
* Critérios de aceite

---

## Etapa 4 — Identificação de Dependências

### Objetivo

Mapear dependências técnicas e organizacionais.

### Atividades

* Detectar dependências entre histórias
* Detectar bloqueios
* Detectar dependências externas
* Detectar integrações críticas
* Detectar restrições operacionais

### Artefatos Gerados

* Mapa de dependências
* Histórias bloqueadoras

---

## Etapa 5 — Classificação de Complexidade

### Objetivo

Classificar o esforço relativo das histórias.

### Atividades

* Avaliar impacto técnico
* Avaliar acoplamento
* Avaliar risco
* Avaliar desconhecimento
* Avaliar impacto operacional

### Escalas sugeridas

* XS
* S
* M
* L
* XL

ou

* Baixa
* Média
* Alta

### Artefatos Gerados

* Estimativa relativa
* Complexidade

---

## Etapa 6 — Identificação de Riscos

### Objetivo

Associar riscos às iniciativas.

### Atividades

* Detectar riscos técnicos
* Detectar riscos operacionais
* Detectar riscos de integração
* Detectar riscos organizacionais
* Detectar riscos de rollout

### Artefatos Gerados

* Matriz de riscos
* Riscos críticos

---

## Etapa 7 — Estratégia de Modernização

### Objetivo

Definir abordagem evolutiva recomendada.

### Atividades

* Identificar quick wins
* Identificar desacoplamentos prioritários
* Identificar áreas críticas
* Detectar oportunidades de paralelismo
* Detectar riscos de big bang

### Estratégias possíveis

* strangler fig
* modularização incremental
* coexistência legado + novo
* modernização parcial
* migração gradual

### Artefatos Gerados

* Estratégia recomendada
* Sequência evolutiva

---

# Confidence Levels

## HIGH

Itens baseados diretamente em:

* componentes identificados
* integrações observadas
* funcionalidades explícitas

## MEDIUM

Itens inferidos a partir de:

* padrões arquiteturais
* comportamento funcional
* débitos técnicos

## LOW

Itens altamente heurísticos:

* estimativas
* priorização executiva
* roadmap organizacional
* dependências humanas

---

# Artefato de Saída Esperado

O processo deve gerar:

`modernization-backlog.md`

---

# Estrutura Esperada do Artefato

```md id="djlwmv"
# Modernization Backlog

## Executive Summary

## Modernization Initiatives

### Epic
- Objetivo
- Riscos
- Dependências
- Prioridade

### User Stories
- História
- Critérios de aceite
- Complexidade
- Dependências
- Riscos

## Technical Improvements

## Architectural Improvements

## Security Improvements

## Observability Improvements

## Suggested Prioritization

## Quick Wins

## Risks

## Confidence Assessment
```

---

# Critérios de Qualidade

O processo será considerado adequado quando:

* backlog rastreável ao legado
* histórias pequenas e compreensíveis
* riscos identificados
* dependências mapeadas
* iniciativas coerentes
* critérios de aceite definidos
* modernização incremental priorizada

---

# Limitações Conhecidas

Este processo pode apresentar limitações em:

* ausência de contexto organizacional
* regras não identificadas
* dependências humanas ocultas
* backlog excessivamente técnico
* priorização artificial
* estimativas imprecisas

---

# Revisão Humana Recomendada

Os seguintes pontos devem ser revisados manualmente:

* priorização
* estimativas
* estratégia de modernização
* riscos críticos
* dependências organizacionais
* impacto operacional
* alinhamento com negócio

---

# Ferramentas Compatíveis

Este processo pode ser executado utilizando:

* Claude Code
* Cursor IDE
* ChatGPT
* Gemini
* Copilot
* MCPs especializados

A ferramenta utilizada não altera:

* workflow
* critérios
* artefatos esperados
* responsabilidades de revisão

---

# Próxima Etapa

Após concluir este processo, iniciar:

`04-roadmap-generation.md`
