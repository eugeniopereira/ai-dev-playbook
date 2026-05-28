# Roadmap Generation Process

## Objetivo

Transformar o backlog de modernização em um roadmap incremental, executável e gerenciável, considerando restrições técnicas, organizacionais e **uso de ferramentas de IA para acelerar implementação**.

O objetivo desta etapa é organizar a evolução do sistema legado em uma sequência sustentável de entregas para suportar:

* modernização gradual
* gestão de risco
* planejamento executivo
* planejamento de sprints
* coordenação organizacional
* previsibilidade
* priorização evolutiva
* **aproveitamento estratégico de IA para acelerar entregas**

---

# Escopo

Este processo deve gerar:

* roadmap incremental
* agrupamento de entregas
* sequência evolutiva
* ondas de modernização
* planejamento simplificado de sprints
* priorização
* dependências organizacionais
* identificação de quick wins
* estratégia de rollout
* marcos executivos

---

# Entradas Esperadas

## Obrigatórias

* `architecture-context.md`
* `functional-map.md`
* `modernization-backlog.md`

## Opcionais

* capacidade do time
* quantidade de equipes
* ferramentas de IA disponíveis (Claude Code, Cursor, etc.)
* restrições organizacionais
* janelas de deploy
* calendário operacional
* roadmap corporativo
* SLAs
* orçamento
* prioridades estratégicas

---

# Pré-Requisitos

* backlog estruturado
* dependências identificadas
* funcionalidades críticas identificadas
* riscos principais identificados

---

# Princípios do Processo

## 1. Roadmap é adaptativo

O roadmap deve ser tratado como:

* hipótese evolutiva
* planejamento iterativo
* instrumento de coordenação

e não:

* cronograma rígido
* previsão absoluta
* contrato imutável

---

## 2. Priorizar redução progressiva de risco

Priorizar:

* desacoplamento
* observabilidade
* testes
* estabilização
* automação
* redução de dependências críticas

antes de:

* reescritas massivas sem validação
* expansões prematuras

**Nota sobre IA**: Com ferramentas de IA, refatorações estruturais e testes se tornam menos custosos. O roadmap pode ser mais ambicioso em qualidade técnica.

---

## 2.1. Aproveitar estrategicamente o uso de IA

**Com IA, o roadmap pode incluir**:

* Testes automatizados abrangentes (antes "não tinha tempo")
* Observabilidade completa desde Wave 1
* Refatorações estruturais mais profundas
* Modernizações mais ambiciosas no mesmo período

**Onde IA acelera**:

* Geração de testes: ~50% mais rápido
* Refatorações: ~40% mais rápido
* Implementação de observabilidade: ~35% mais rápido
* Migração entre frameworks: ~40% mais rápido

**Onde IA NÃO acelera** (manter no roadmap com prazo realista):

* Aprovações organizacionais
* Reuniões e alinhamentos
* Dependências de infra/outras equipes
* Validação de regras de negócio
* Deploy e homologação

**Impacto no roadmap**:

* Aceleração média: 25-35% do tempo total
* Permite incluir mais melhorias estruturais
* Reduz trade-off entre velocidade e qualidade

---

## 3. Entregas pequenas e verificáveis

Priorizar:

* incrementos pequenos
* validação contínua
* rollback simples
* aprendizado progressivo

Evitar:

* ondas gigantes de mudança
* dependências excessivas
* sprints artificialmente grandes

---

## 4. Modernização contínua

Assumir que:

* discovery continuará ocorrendo
* backlog mudará
* riscos surgirão
* prioridades evoluirão

O roadmap deve acomodar descoberta contínua.

---

## 5. Evitar roadmaps fictícios

Não assumir:

* capacidade ideal
* ausência de incidentes
* conhecimento completo do legado
* disponibilidade perfeita de equipe
* ausência de dependências humanas

---

# Workflow

## Etapa 1 — Classificação Estratégica do Backlog

### Objetivo

Classificar iniciativas por criticidade e impacto, **considerando o que IA acelera**.

### Atividades

* Identificar quick wins (redefinidos com IA disponível)
* Identificar riscos críticos
* Identificar dependências bloqueadoras
* Identificar iniciativas estruturantes
* Identificar melhorias de baixo risco
* **Identificar tarefas que IA acelera significativamente**
* **Identificar tarefas que IA NÃO acelera**

### Critérios sugeridos

* impacto operacional
* redução de risco
* desacoplamento
* facilidade de entrega (recalibrada com IA)
* criticidade organizacional
* **potencial de aceleração por IA**

### Exemplos de reclassificação com IA

**Quick wins tradicionais** (sem IA):
- Adicionar logs básicos
- Documentar APIs existentes
- Pequenas correções de bugs

**Quick wins com IA** (mais ambiciosos):
- Adicionar testes automatizados abrangentes
- Implementar observabilidade completa (logs + métricas + traces)
- Refatorar módulo crítico + testes
- Migrar dependências obsoletas

**Alta complexidade sem IA** → **Média complexidade com IA**:
- Criação de suite de testes
- Extração de interfaces
- Refatorações estruturais

### Artefatos Gerados

* Priorização estratégica (com IA considerada)
* Agrupamento inicial
* Mapeamento de aceleração por IA

---

## Etapa 2 — Definição de Ondas de Modernização

### Objetivo

Organizar iniciativas em ondas evolutivas, **aproveitando aceleração por IA**.

### Atividades

* Agrupar entregas relacionadas
* Minimizar dependências cruzadas
* Definir sequência evolutiva
* **Combinar estabilização + qualidade (viável com IA)**
* Organizar rollout incremental
* **Incluir melhorias estruturais desde cedo**

### Exemplos de ondas (roadmap tradicional)

* Wave 1: estabilização básica
* Wave 2: observabilidade
* Wave 3: desacoplamento
* Wave 4: modernização incremental

### Exemplos de ondas (roadmap com IA - mais ambicioso)

* Wave 1: estabilização + observabilidade + testes
* Wave 2: desacoplamento + refatoração estrutural
* Wave 3: modernização incremental + migração de runtime

**Por que ondas com IA podem ser mais densas?**

Com IA, tarefas que antes eram "ou/ou" viram "e/e":
- Antes: "vamos estabilizar OU adicionar testes"
- Com IA: "vamos estabilizar E adicionar testes E observabilidade"

### Estratégia por onda

**Wave 1 (Estabilização + Fundação)**:
- Testes automatizados (IA gera rapidamente)
- Observabilidade completa (logs + métricas + traces)
- Refatorações para testabilidade
- Aceleração esperada: ~30%

**Wave 2 (Desacoplamento + Modernização)**:
- Extração de interfaces
- Criação de adapters/facades
- Refatorações estruturais
- Aceleração esperada: ~35%

**Wave 3 (Migração + Evolução)**:
- Migração de framework/runtime
- Reescrita de componentes
- Atualização de dependências
- Aceleração esperada: ~40%

### Artefatos Gerados

* Ondas de modernização (com IA considerada)
* Sequência macro
* Estimativa de aceleração por onda

---

## Etapa 3 — Planejamento Simplificado de Sprints

### Objetivo

Criar uma visão executável inicial.

### Atividades

* Distribuir histórias
* Balancear complexidade
* Evitar excesso de dependências
* Separar entregas críticas
* Organizar capacidade incremental

### Diretrizes

* evitar sprints excessivamente grandes
* evitar dependências críticas no mesmo sprint
* priorizar validação contínua

### Artefatos Gerados

* Planejamento simplificado
* Sequência de sprints

---

## Etapa 4 — Identificação de Marcos Executivos

### Objetivo

Definir pontos relevantes de acompanhamento organizacional.

### Atividades

* Identificar entregas estratégicas
* Identificar marcos técnicos
* Identificar marcos operacionais
* Identificar pontos de validação

### Exemplos

* migração concluída
* observabilidade implantada
* integração desacoplada
* runtime modernizado

### Artefatos Gerados

* Marcos executivos
* Pontos de controle

---

## Etapa 5 — Identificação de Dependências Organizacionais

### Objetivo

Detectar fatores externos que impactam a execução.

### Atividades

* Detectar dependências entre equipes
* Detectar aprovações necessárias
* Detectar restrições operacionais
* Detectar dependências de infraestrutura
* Detectar dependências regulatórias

### Artefatos Gerados

* Dependências organizacionais
* Restrições externas

---

## Etapa 6 — Estratégia de Rollout e Mitigação

### Objetivo

Definir abordagem segura de evolução.

### Atividades

* Definir entregas progressivas
* Definir rollback simplificado
* Definir validações incrementais
* Definir convivência legado + novo
* Identificar riscos de rollout

### Estratégias possíveis

* strangler fig
* feature toggle
* blue/green
* coexistência parcial
* migração gradual

### Artefatos Gerados

* Estratégia de rollout
* Estratégia de mitigação

---

## Etapa 7 — Revisão de Sustentabilidade

### Objetivo

Validar se o roadmap é operacionalmente sustentável.

### Atividades

* Avaliar carga organizacional
* Avaliar risco acumulado
* Avaliar dependências excessivas
* Avaliar complexidade por sprint
* Avaliar fragilidade operacional

### Artefatos Gerados

* Ajustes do roadmap
* Riscos de execução

---

# Confidence Levels

## HIGH

Itens baseados em:

* backlog explícito
* dependências observáveis
* capacidades conhecidas

## MEDIUM

Itens inferidos a partir de:

* priorização
* agrupamentos
* estratégia evolutiva

## LOW

Itens altamente heurísticos:

* estimativas temporais
* capacidade organizacional
* velocidade do time
* cronogramas rígidos

---

# Artefato de Saída Esperado

O processo deve gerar:

`modernization-roadmap.md`

---

# Estrutura Esperada do Artefato

```md id="rqpt7h"
# Modernization Roadmap

## Executive Summary

## Modernization Strategy
- Abordagem escolhida (strangler fig, coexistência, etc.)
- Uso de IA na implementação
- Aceleração esperada

## Prioritization Rationale
- Critérios de priorização
- Impacto do uso de IA nas prioridades

## Modernization Waves

### Wave 1
- Objetivos
- Entregas
- Onde IA acelera
- Aceleração esperada (%)
- Riscos
- Dependências

### Wave 2
...

## Simplified Sprint Planning

### Sprint 1
- Histórias
- Complexidade
- Uso de IA previsto

### Sprint 2
### Sprint 3

## Quick Wins
- Quick wins tradicionais
- Quick wins viabilizados por IA

## Critical Risks
- Riscos gerais
- Riscos relacionados ao uso de IA

## Organizational Dependencies

## Rollout Strategy

## Mitigation Strategy

## Executive Milestones

## AI Acceleration Impact
- Tarefas mais aceleradas
- Tarefas não aceleradas
- Aceleração geral esperada

## Confidence Assessment
```

---

# Critérios de Qualidade

O processo será considerado adequado quando:

* roadmap incremental definido
* dependências principais mapeadas
* quick wins identificados (incluindo viabilizados por IA)
* riscos principais registrados
* backlog organizado progressivamente
* estratégia de rollout definida
* roadmap executável de forma plausível
* **aceleração por IA considerada nas estimativas**
* **identificado onde IA acelera e onde não acelera**

---

# Como IA Muda o Roadmap

## Mudanças Estratégicas

**Sem IA** (roadmap conservador):
- Priorizar quick wins superficiais
- Postergar testes para "quando tiver tempo"
- Evitar refatorações grandes (muito custo)
- Observabilidade mínima
- Modernizações pequenas e graduais

**Com IA** (roadmap mais ambicioso):
- Incluir testes desde Wave 1
- Implementar observabilidade completa cedo
- Fazer refatorações estruturais profundas
- Modernizações mais ousadas no mesmo período
- Menos trade-off entre velocidade e qualidade

## Impacto nas Ondas

**Wave 1** tradicionalmente:
- Apenas estabilização básica
- Alguns logs

**Wave 1 com IA**:
- Estabilização + testes automatizados completos
- Observabilidade completa (logs + métricas + traces)
- Refatorações para testabilidade
- Documentação atualizada

**Por quê?** IA reduz custo de testes/observabilidade em ~50%.

## Recalibração de Complexidade

Com IA, a complexidade muda:

| Tarefa | Complexidade SEM IA | Complexidade COM IA |
|--------|---------------------|---------------------|
| Criar suite de testes | Alta | Média |
| Implementar observabilidade | Alta | Média |
| Refatoração estrutural | Alta | Média-Alta |
| Extração de interfaces | Média-Alta | Média |
| Migração de framework | Alta | Média-Alta |
| Documentação | Média | Baixa |

**Resultado**: tarefas "muito caras" viram viáveis.

## Mudança de Priorização

**Critérios tradicionais**:
1. Valor de negócio
2. Risco
3. Esforço técnico ← IA muda isso

**Com IA, repriorizar**:
- Itens que antes eram "muito caros" sobem na fila
- Testes deixam de ser "nice to have" e viram prioridade
- Qualidade técnica vira mais alcançável

## Impacto na Velocidade

**Aceleração não é uniforme**:

| Tipo de tarefa | Aceleração esperada |
|----------------|---------------------|
| Codificação pura | 1.8x - 2x |
| Testes unitários | 1.8x - 2x |
| Refatorações | 1.5x - 1.8x |
| Observabilidade | 1.8x - 2x |
| Documentação | 2x |
| **Aprovações** | **1x (não acelera)** |
| **Reuniões** | **1x (não acelera)** |
| **Dependências externas** | **1x (não acelera)** |

**Aceleração média geral**: 25-35% do tempo total

## Estratégia de Roadmap com IA

**Recomendações**:

1. **Wave 1 mais densa**: inclua testes + observabilidade juntos
2. **Refatorações mais ousadas**: com IA, são menos arriscadas
3. **Menos "dívida técnica planejada"**: não precisa adiar qualidade
4. **Marcos mais frequentes**: entregas menores e mais rápidas
5. **Documentação contínua**: com IA, custa pouco

**Evitar**:

- Assumir 10x de aceleração (irreal)
- Ignorar que aprovações não aceleram
- Eliminar code review
- Confiar cegamente em código gerado

---

# Limitações Conhecidas

Este processo pode apresentar limitações em:

* ausência de informações organizacionais
* capacidade real desconhecida
* dependências humanas ocultas
* descoberta contínua do legado
* backlog incompleto
* estimativas heurísticas

---

# Revisão Humana Recomendada

Os seguintes pontos devem ser revisados manualmente:

* capacidade do time
* cronogramas
* priorização
* dependências organizacionais
* riscos críticos
* estratégia executiva
* restrições operacionais

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

# Resultado Esperado da Pipeline

Ao concluir este processo, a pipeline de modernização deve produzir:

* contexto arquitetural
* mapa funcional
* backlog estruturado
* roadmap incremental
* visão executiva de modernização

---

# Próximos Processos Recomendados

Após concluir este processo, recomenda-se criar processos adicionais para:

* implementation-planning
* impact-analysis
* architecture-review
* modernization-governance
* delivery-validation
* ai-assisted-code-review
