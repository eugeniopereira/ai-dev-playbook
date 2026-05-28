# Guia Prático: Modernização de Legados com IA

> **Objetivo**: Transformar sistemas legados em backlog e roadmap executável usando IA como amplificador cognitivo.

---

## 📋 Visão Geral do Processo

```
1. Architecture Discovery    →  architecture-context.md
2. Functional Discovery      →  functional-map.md
3. Backlog Generation        →  modernization-backlog.md
4. Roadmap Generation        →  modernization-roadmap.md
```

**Tempo estimado**: 2-4 horas para sistemas de médio porte  
**Pré-requisito**: Acesso ao código-fonte do sistema legado

---

## 🎯 Etapa 1: Architecture Discovery

### Objetivo
Mapear a arquitetura técnica do sistema legado.

### Prompt Pronto

```markdown
Você é um arquiteto de software especializado em análise de sistemas legados.

Analise este projeto e gere um documento `architecture-context.md` seguindo a estrutura:

# Architecture Context

## System Overview
- Nome e propósito do sistema
- Tipo de aplicação (monólito/microserviços/outro)

## Technology Stack
- Linguagens
- Frameworks principais
- Bibliotecas críticas
- Versões

## Runtime Environment
- Servidor de aplicação
- Container/orquestração
- Build system

## Modules and Components
- Estrutura de módulos
- Responsabilidades
- Boundaries identificados

## Persistence Layer
- Bancos de dados
- ORMs
- Estratégias de acesso a dados

## Integrations
- APIs externas
- Mensageria
- Serviços consumidos
- Protocolos (REST/SOAP/gRPC)

## Infrastructure
- Deploy
- CI/CD
- Observabilidade (logs/traces/métricas)

## Security
- Autenticação
- Autorização
- Gestão de secrets

## Technical Risks
- Dependências obsoletas
- Pontos únicos de falha
- Acoplamentos críticos

## Technical Debt
- Código obsoleto
- Ausência de testes
- Problemas arquiteturais

## Architectural Patterns
- Padrões identificados
- Inconsistências

## Constraints
- Limitações técnicas
- Restrições operacionais

## Confidence Assessment
Para cada seção, indique:
- HIGH: evidência direta no código
- MEDIUM: inferência com evidências indiretas
- LOW: hipótese

---

**Importante**:
- Cite arquivos específicos como evidência
- Diferencie observação de inferência
- Documente lacunas de conhecimento
```

### ✅ Checklist de Validação

- [ ] Stack tecnológica identificada
- [ ] Principais módulos mapeados
- [ ] Integrações externas documentadas
- [ ] Banco de dados identificado
- [ ] Riscos técnicos listados
- [ ] Confidence levels atribuídos

---

## 🔍 Etapa 2: Functional Discovery

### Objetivo
Descobrir comportamento funcional e regras de negócio.

### Prompt Pronto

```markdown
Você é um analista de negócio especializado em engenharia reversa funcional.

Usando o `architecture-context.md` gerado anteriormente e o código-fonte, 
gere um documento `functional-map.md` seguindo a estrutura:

# Functional Map

## System Purpose
- Propósito principal do sistema
- Problema que resolve

## Functional Capabilities
- Principais funcionalidades
- Capacidades de negócio oferecidas
- Agrupamento por domínio

## Main Business Flows
Para cada fluxo principal:
- Nome do fluxo
- Entrypoint (controller/endpoint/job)
- Sequência de execução
- Decisões condicionais
- Side effects
- Integrações acionadas

## Actors
- Usuários/perfis
- Sistemas consumidores
- Automações

## Business Rules
- Validações
- Restrições
- Cálculos
- Políticas
- Regras temporais
- Regras distribuídas (código + banco + integrações)

## Domain Entities
- Entidades principais
- Relacionamentos
- Aggregates

## Integrations
- Integrações funcionais
- Propósito de cada integração
- Fluxo de dados

## Critical Functionalities
- Funcionalidades com maior impacto operacional
- Justificativa da criticidade

## Side Effects
- Persistência
- Notificações
- Integrações assíncronas
- Jobs disparados

## Operational Dependencies
- Dependências organizacionais
- Processos manuais
- Regras fora do código

## Risks
- Funcionalidades sem testes
- Lógica crítica acoplada
- Regras não documentadas

## Functional Gaps
- Fluxos não compreendidos
- Código morto suspeito
- Funcionalidades incompletas
- Necessidade de validação humana

## Confidence Assessment
Para cada seção, indique:
- HIGH: endpoints/jobs/queries observáveis
- MEDIUM: regras de negócio inferidas
- LOW: comportamento dependente de contexto organizacional

---

**Importante**:
- Priorize fluxos reais sobre código morto
- Diferencie fato de hipótese
- Documente incertezas
- Indique necessidade de validação com especialistas
```

### ✅ Checklist de Validação

- [ ] Principais funcionalidades listadas
- [ ] Fluxos críticos documentados
- [ ] Regras de negócio identificadas
- [ ] Atores mapeados
- [ ] Integrações funcionais documentadas
- [ ] Lacunas registradas

---

## 📦 Etapa 3: Backlog Generation

### Objetivo
Transformar descoberta em backlog executável.

### Prompt Pronto

```markdown
Você é um Product Owner técnico especializado em modernização de sistemas legados.

Usando `architecture-context.md` e `functional-map.md`, 
gere um documento `modernization-backlog.md` seguindo a estrutura:

# Modernization Backlog

## Executive Summary
- Principais iniciativas
- Esforço estimado (alto nível)
- Riscos principais

## Modernization Initiatives

Para cada iniciativa:
- Nome e objetivo
- Funcionalidades/módulos afetados
- Riscos
- Dependências
- Benefícios esperados

## Epics

Para cada epic:

### [EPIC-XXX] Nome do Epic

**Objetivo**: descrição clara

**Impacto**: 
- Operacional
- Técnico
- Organizacional

**Riscos**:
- Lista de riscos

**Dependências**:
- Outros epics
- Dependências externas

**Áreas Afetadas**:
- Módulos/componentes

## User Stories

Para cada história:

**[STORY-XXX] Nome da História**

**Como** [ator]  
**Quero** [ação]  
**Para** [benefício]

**Tipo**: [funcional|técnica|arquitetura|segurança|observabilidade|teste]

**Critérios de Aceite**:
- [ ] Critério 1
- [ ] Critério 2

**Complexidade**: [XS|S|M|L|XL]

**Dependências**: [lista]

**Riscos**: [lista]

**Rastreabilidade**:
- Fluxo funcional: [referência ao functional-map]
- Componente: [referência ao architecture-context]

## Technical Improvements
- Débitos técnicos priorizados
- Melhorias de performance
- Atualização de dependências

## Architectural Improvements
- Desacoplamentos
- Modularização
- Refatorações estruturais

## Security Improvements
- Vulnerabilidades conhecidas
- Melhorias de autenticação/autorização
- Gestão de secrets

## Observability Improvements
- Logging
- Tracing
- Métricas
- Alertas

## Suggested Prioritization

**Quick Wins** (alto valor, baixo esforço):
- Lista

**Crítico** (alto risco se não feito):
- Lista

**Estruturante** (habilita outras iniciativas):
- Lista

## Quick Wins
- Melhorias de rápido retorno
- Baixo risco
- Alto impacto percebido

## Risks
- Riscos técnicos
- Riscos operacionais
- Riscos organizacionais

## Confidence Assessment
- Estimativas: LOW (revisão humana necessária)
- Priorização: LOW (validar com negócio)
- Complexidade: MEDIUM

---

**Importante**:
- Histórias pequenas e independentes
- Rastreabilidade aos artefatos anteriores
- Priorize modernização incremental
- Evite big bang rewrites
- Indique necessidade de refinamento
```

### ✅ Checklist de Validação

- [ ] Epics definidos com objetivos claros
- [ ] User stories com critérios de aceite
- [ ] Dependências mapeadas
- [ ] Complexidade estimada (relativa)
- [ ] Quick wins identificados
- [ ] Riscos documentados

---

## 🗺️ Etapa 4: Roadmap Generation

### Objetivo
Organizar backlog em roadmap incremental executável, **considerando uso de IA para acelerar implementação**.

### Prompt Pronto

```markdown
Você é um Engineering Manager especializado em planejamento de modernizações graduais com uso de IA.

**Premissa importante**: O time utilizará ferramentas de IA (Claude Code, Cursor, etc.) para 
acelerar codificação, testes e refatorações. Isso muda a viabilidade de algumas tarefas.

Usando `architecture-context.md`, `functional-map.md` e `modernization-backlog.md`,
gere um documento `modernization-roadmap.md` seguindo a estrutura:

# Modernization Roadmap

## Executive Summary
- Estratégia de modernização
- Duração estimada (ondas)
- Marcos principais
- Riscos executivos

## Modernization Strategy

**Abordagem escolhida**:
- [ ] Strangler Fig Pattern
- [ ] Modularização incremental
- [ ] Coexistência legado + novo
- [ ] Modernização parcial
- [ ] Migração gradual

**Justificativa**: [explicar escolha]

**Uso de IA na implementação**:
- Ferramentas: [Claude Code, Cursor, etc.]
- Aceleração esperada: 25-35% do tempo total
- Onde IA ajuda: codificação, testes, refatorações, observabilidade
- Onde IA NÃO ajuda: aprovações, reuniões, dependências externas

## Prioritization Rationale

**Critérios de priorização** (recalibrados com IA):
1. Redução de risco operacional
2. Desacoplamento
3. Observabilidade (antes "muito caro", com IA viável)
4. Qualidade técnica (testes, documentação)
5. Quick wins (redefinidos com IA)
6. Habilitadores estruturantes

**Como IA muda priorização**:
- Tarefas "muito caras" sobem na fila (testes, observabilidade)
- Refatorações estruturais viram mais viáveis
- Menos trade-off entre velocidade e qualidade

## Modernization Waves

### Wave 1: Estabilização + Qualidade (mais densa com IA)
**Duração estimada**: [X sprints]

**Objetivos**:
- Reduzir risco operacional
- Aumentar visibilidade
- Estabelecer qualidade técnica desde o início
- Preparar base para modernização

**Entregas** (mais ambiciosas com IA):
- [EPIC-XXX] Testes automatizados abrangentes
- [EPIC-YYY] Observabilidade completa (logs + métricas + traces)
- [STORY-XXX] Refatorações para testabilidade
- [STORY-YYY] Documentação atualizada
- ...

**Onde IA acelera esta wave**:
- Geração de testes: ~50% mais rápido
- Implementação de observabilidade: ~35% mais rápido
- Refatorações: ~40% mais rápido
- Documentação: ~50% mais rápido

**Aceleração esperada da wave**: ~30%

**Riscos**:
- Lista de riscos

**Dependências**:
- Dependências organizacionais

**Critério de sucesso**:
- Suite de testes com cobertura >70%
- Observabilidade completa implantada
- Riscos críticos mitigados

---

### Wave 2: Desacoplamento + Refatoração Estrutural
**Duração estimada**: [Y sprints]

**Objetivos**:
- Desacoplar integrações críticas
- Refatorar módulos monolíticos
- Preparar para migração

**Entregas**:
- [EPIC-XXX] Extração de interfaces
- [EPIC-YYY] Criação de adapters/facades
- [STORY-XXX] Refatorações estruturais
- ...

**Onde IA acelera esta wave**:
- Extração de interfaces: ~40% mais rápido
- Criação de adapters: ~35% mais rápido
- Refatorações estruturais: ~40% mais rápido

**Aceleração esperada da wave**: ~35%

**Riscos**: [lista]

**Dependências**: [lista]

---

### Wave 3: Migração + Modernização
**Duração estimada**: [Z sprints]

**Objetivos**:
- Migrar framework/runtime
- Reescrever componentes críticos
- Finalizar modernização

**Entregas**:
- [EPIC-XXX] Migração de framework
- [EPIC-YYY] Reescrita de componentes
- [STORY-XXX] Atualização de dependências
- ...

**Onde IA acelera esta wave**:
- Migração de framework: ~40% mais rápido
- Reescrita de componentes: ~35% mais rápido
- Atualização de dependências: ~30% mais rápido

**Aceleração esperada da wave**: ~40%

**Riscos**: [lista]

**Dependências**: [lista]

## Simplified Sprint Planning

### Sprint 1
**Foco**: [tema]
**Histórias**:
- [STORY-XXX] - Complexidade: M
- [STORY-YYY] - Complexidade: S

**Riscos**: [lista]

### Sprint 2
[mesma estrutura]

### Sprint 3
[mesma estrutura]

## Quick Wins

**Quick wins tradicionais** (ainda válidos):
- Sprint 1: [STORY-XXX] - [benefício]
- Sprint 2: [STORY-YYY] - [benefício]

**Quick wins viabilizados por IA** (antes "muito caros"):
- Sprint 1: Adicionar testes automatizados para módulo crítico (antes: 2 semanas, com IA: 3-4 dias)
- Sprint 2: Implementar observabilidade completa (antes: 1-2 semanas, com IA: 2-3 dias)
- Sprint 3: Refatorar módulo legado + testes (antes: 3 semanas, com IA: 1.5 semanas)

## Critical Risks

**Riscos gerais**:

**Risco 1**: [descrição]
- Probabilidade: [Alta|Média|Baixa]
- Impacto: [Alto|Médio|Baixo]
- Mitigação: [estratégia]

**Riscos relacionados ao uso de IA**:

**Risco: Ferramentas de IA indisponíveis**:
- Probabilidade: Baixa-Média
- Impacto: Médio (reduz aceleração esperada)
- Mitigação: ter plano B sem IA, não depender 100%

**Risco: Código gerado sem validação adequada**:
- Probabilidade: Média
- Impacto: Alto (débito técnico)
- Mitigação: code review obrigatório, testes automatizados

## Organizational Dependencies

**Infraestrutura**:
- [dependência] - necessário em [wave/sprint]

**Equipes externas**:
- [time] - para [atividade]

**Aprovações**:
- [stakeholder] - para [decisão]

## Rollout Strategy

**Estratégia de deploy**:
- Feature toggles
- Blue/green
- Canary releases
- Rollback plan

**Convivência legado + novo**:
- Período: [duração]
- Critérios de migração completa

## Mitigation Strategy

**Validação contínua**:
- Testes automatizados
- Monitoramento de métricas
- Smoke tests
- Rollback imediato se [condição]

## Executive Milestones

**M1**: Observabilidade + Testes implantados - Sprint [X]  
**M2**: Integração crítica desacoplada - Sprint [Y]  
**M3**: Runtime modernizado - Sprint [Z]  
**M4**: Migração completa - Sprint [W]

## AI Acceleration Impact

**Resumo de aceleração esperada**:

| Tipo de tarefa | Aceleração | Impacto no roadmap |
|----------------|------------|-------------------|
| Codificação pura | 1.8x - 2x | Módulos reescritos mais rápido |
| Testes unitários | 1.8x - 2x | Cobertura completa viável |
| Refatorações | 1.5x - 1.8x | Refatorações estruturais viáveis |
| Observabilidade | 1.8x - 2x | Implementação completa desde Wave 1 |
| Documentação | 2x | Documentação contínua viável |
| **Aprovações** | **1x** | Não acelera - manter realista |
| **Reuniões** | **1x** | Não acelera - manter realista |
| **Dependências externas** | **1x** | Não acelera - manter realista |

**Aceleração média geral do roadmap**: 25-35%

**Tarefas mais aceleradas** (priorizar):
1. Criação de suites de testes (~50% economia)
2. Implementação de observabilidade (~40% economia)
3. Refatorações estruturais (~35% economia)
4. Migração entre frameworks (~40% economia)

**Tarefas não aceleradas** (manter prazo realista):
1. Aprovações organizacionais
2. Reuniões de alinhamento
3. Dependências de infraestrutura
4. Validação com especialistas de negócio
5. Homologação e deploy

## Confidence Assessment

**Roadmap**: LOW (tratar como hipótese evolutiva)  
**Priorização**: MEDIUM (validar continuamente)  
**Estimativas**: LOW (refinar a cada sprint)  
**Aceleração por IA**: MEDIUM (monitorar velocity real)

---

**Importante**:
- Roadmap é adaptativo, não rígido
- Discovery é contínua
- Prioridades podem mudar
- Validar suposições de capacidade do time
- Revisar roadmap a cada onda
- **Monitorar se aceleração por IA está sendo atingida**
- **Ajustar estimativas se velocity divergir do esperado**
- **Code review continua obrigatório mesmo com IA**
```

### ✅ Checklist de Validação

- [ ] Ondas de modernização definidas
- [ ] Quick wins priorizados (incluindo viabilizados por IA)
- [ ] Dependências organizacionais mapeadas
- [ ] Estratégia de rollout definida
- [ ] Marcos executivos claros
- [ ] Riscos críticos com mitigação
- [ ] **Aceleração por IA considerada nas estimativas**
- [ ] **Identificado onde IA acelera e onde não acelera**
- [ ] **Roadmap mais ambicioso em qualidade (testes/observabilidade)**
- [ ] **Validado que ondas não estão conservadoras demais**

---

## 🎓 Dicas de Uso

### 1. Ferramentas Compatíveis
- **Claude Code** (recomendado para projetos locais)
- **Cursor IDE**
- **ChatGPT**
- **Gemini**
- **Copilot**

### 2. Contexto Adicional Recomendado

Sempre que possível, inclua no prompt:

```markdown
**Contexto organizacional**:
- Tamanho do time: [X devs]
- Ferramentas de IA que serão usadas: [Claude Code, Cursor, etc.]
- Restrições conhecidas: [lista]
- Prioridades estratégicas: [lista]
- Janelas de deploy: [periodicidade]
```

### 2.1. Como IA Muda o Roadmap

**Roadmap tradicional** (conservador):
- Wave 1: Apenas estabilização básica
- Evita testes/observabilidade ("muito caro")
- Refatorações mínimas

**Roadmap com IA** (mais ambicioso):
- Wave 1: Estabilização + testes + observabilidade completa
- Inclui qualidade técnica desde o início
- Refatorações estruturais viáveis

**Por quê?**
- Testes custam ~50% menos tempo com IA
- Observabilidade custa ~40% menos tempo
- Refatorações são ~35% mais rápidas

**Resultado**: menos trade-off entre velocidade e qualidade

### 3. Validação Humana Obrigatória

**Nunca confie 100% nos artefatos gerados**. Revisão crítica necessária em:

- ✅ Regras de negócio críticas
- ✅ Estimativas de esforço
- ✅ Priorização executiva
- ✅ Riscos operacionais
- ✅ Dependências organizacionais
- ✅ Decisões arquiteturais

### 4. Iteração Contínua

O processo **NÃO é one-shot**:

1. Gere os artefatos
2. Valide com o time
3. Refine com feedback
4. Atualize conforme execução
5. Repita discovery conforme necessário

### 5. Níveis de Confiança

Use como guia de revisão:

| Confidence | O que significa | Ação |
|------------|-----------------|------|
| **HIGH** | Evidência direta no código | Pode confiar, mas valide críticos |
| **MEDIUM** | Inferência razoável | Revisão recomendada |
| **LOW** | Hipótese ou estimativa | Revisão obrigatória |

---

## ⚠️ Limitações Conhecidas

A IA pode:
- ❌ Inferir funcionalidades inexistentes
- ❌ Unir fluxos independentes
- ❌ Gerar estimativas imprecisas
- ❌ Sugerir over-engineering
- ❌ Omitir regras fora do código

**Sempre valide com conhecimento organizacional e testes reais**.

---

## 📚 Artefatos Gerados

Ao final, você terá:

```
architecture-context.md      ← Visão técnica
functional-map.md            ← Visão funcional
modernization-backlog.md     ← Backlog executável
modernization-roadmap.md     ← Roadmap incremental
```

---

## 🚀 Próximos Passos

Após concluir os 4 artefatos:

1. **Validar com stakeholders**
   - Arquitetura: time técnico
   - Funcional: PO + especialistas de negócio
   - Backlog: PO + time
   - Roadmap: liderança técnica + executiva

2. **Refinar e adaptar**
   - Ajustar priorização
   - Corrigir inferências incorretas
   - Adicionar contexto organizacional

3. **Iniciar execução incremental**
   - Começar pelos quick wins
   - Validar hipóteses
   - Adaptar roadmap conforme aprendizado

4. **Discovery contínua**
   - Atualizar artefatos
   - Documentar novas descobertas
   - Refinar backlog

---

## 📖 Referências

- [orchestration.md](orchestration.md) - Filosofia e governança do processo
- [01-architecture-discovery.md](01-architecture-discovery.md) - Detalhamento técnico
- [02-functional-discovery.md](02-functional-discovery.md) - Detalhamento funcional
- [03-backlog-generation.md](03-backlog-generation.md) - Detalhamento de backlog
- [04-roadmap-generation.md](04-roadmap-generation.md) - Detalhamento de roadmap

---

**Versão**: 0.1  
**Última atualização**: 2026-05-28
