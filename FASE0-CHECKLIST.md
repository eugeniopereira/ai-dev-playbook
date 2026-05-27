# ✅ FASE 0: Checklist de Execução

**Objetivo**: Implementar controles mínimos de segurança  
**Prazo**: 2 semanas  
**Status**: 🟡 Em Progresso

---

## 📅 SEMANA 1: Security Quick Wins

### Segunda-feira (4 horas) - DIA 1 🔴 HOJE

#### Manhã (2 horas)

- [ ] **Setup Security Scanning no CI/CD** (1 hora)
  ```bash
  # 1. Criar diretório
  mkdir -p .github/workflows
  
  # 2. Arquivo já criado em:
  # .github/workflows/ai-code-security.yml
  
  # 3. Commit e push
  git add .github/workflows/ai-code-security.yml
  git commit -m "ci: adiciona security scanning para código IA
  
  Implementa validação automática com:
  - TruffleHog (secrets)
  - Semgrep (SAST)
  - GitLeaks (credentials)
  
  Fase 0 - Fundação Crítica
  Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"
  
  git push origin main
  
  # 4. Verificar no GitHub Actions
  # Abrir: https://github.com/<seu-repo>/actions
  ```
  
  **Validação**: Workflow aparece no GitHub Actions ✅
  
  **Troubleshooting**:
  - Se não aparecer: verificar sintaxe YAML
  - Se falhar: revisar logs do workflow

- [ ] **Criar Security Validation Checklist** (30 min)
  ```bash
  # Arquivo já criado em:
  # docs/security-validation-checklist.md
  
  # Commit
  git add docs/security-validation-checklist.md
  git commit -m "docs: adiciona checklist de validação de segurança
  
  Checklist obrigatório para code review de código IA.
  Inclui red flags, processo de validação e tracking.
  
  Fase 0 - Fundação Crítica
  Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"
  
  git push origin main
  ```
  
  **Validação**: Documento acessível e lido pelo time ✅

- [ ] **Atualizar Skill commit-message** (30 min)
  ```bash
  # Arquivo já atualizado em:
  # skill/commit-message/SKILL.md
  
  # Agora inclui tags de rastreabilidade:
  # "Gerado com assistência de: Claude/Copilot/Gemini"
  # "Validação: Security scan passed, X peer reviews"
  
  # Commit
  git add skill/commit-message/SKILL.md
  git commit -m "feat(skill): adiciona rastreabilidade de código IA
  
  Atualiza skill commit-message para incluir:
  - Tag de ferramenta IA utilizada
  - Status de validação de segurança
  - Permite tracking de código IA vs tradicional
  
  Gerado com assistência de: Claude Code
  Validação: Manual review
  
  Fase 0 - Fundação Crítica
  Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"
  
  git push origin main
  ```
  
  **Validação**: Skill atualizada e documentada ✅

#### Tarde (2 horas)

- [ ] **Definir Métricas Baseline** (1 hora)
  ```bash
  # Arquivo já criado em:
  # docs/metricas-baseline.md
  
  # Commit
  git add docs/metricas-baseline.md
  git commit -m "docs: define métricas baseline para desenvolvimento com IA
  
  Estabelece 10 métricas primárias e secundárias:
  - Defect density
  - Code review rejection rate
  - Security findings
  - Time to first working solution
  - Test coverage delta
  - Developer satisfaction (NPS)
  
  Fase 0 - Fundação Crítica
  Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"
  
  git push origin main
  ```
  
  **Validação**: Métricas definidas e socializadas ✅

- [ ] **Setup Dashboard Inicial** (1 hora)
  ```bash
  # Arquivo já criado em:
  # docs/dashboard-setup.md
  
  # Commit
  git add docs/dashboard-setup.md
  git commit -m "docs: adiciona guia de setup do dashboard de métricas
  
  Instruções para criar dashboard em Google Sheets.
  Inclui estrutura de abas, fórmulas e gráficos.
  
  Fase 0 - Fundação Crítica
  Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"
  
  git push origin main
  
  # Agora executar setup real:
  # 1. Criar Google Sheet "AI Dev Metrics - 2026"
  # 2. Seguir instruções em docs/dashboard-setup.md
  # 3. Compartilhar com time
  ```
  
  **Validação**: Google Sheet criado e compartilhado ✅

#### Fim do Dia 1

**Checkpoint**:
- [ ] 4 documentos criados e commitados
- [ ] CI/CD rodando (mesmo que sem PRs ainda)
- [ ] Dashboard criado (pode estar vazio)
- [ ] Time informado das mudanças

**Comunicar no Slack**:
```
🚀 Fase 0 - Dia 1 Completo

Implementado hoje:
✅ Security scanning automático no CI/CD
✅ Checklist de validação de segurança
✅ Tags de rastreabilidade em commits
✅ Métricas baseline definidas
✅ Dashboard inicial configurado

Próximos passos:
- Terça: Testar security scan em PRs reais
- Quarta: Ajustar falsos positivos
- Quinta: Training do time

Docs: [link do repo]
Dashboard: [link do Google Sheet]
```

---

### Terça-feira (2 horas)

- [ ] **Testar Security Scan em PRs Reais** (1.5 horas)
  
  **Ação**:
  1. Pegar 2-3 PRs recentes ou criar PR de teste
  2. Verificar se workflow roda automaticamente
  3. Analisar resultados
  4. Documentar falsos positivos (se houver)
  
  **Criar PR de Teste**:
  ```bash
  # Branch de teste
  git checkout -b test/security-scan
  
  # Adicionar código de teste com vulnerabilidade proposital
  echo "api_key = 'sk-test123456789'" > test_security.py
  
  # Commit
  git add test_security.py
  git commit -m "test: validar security scan
  
  PR de teste para validar funcionamento do security scanning.
  Contém vulnerabilidade proposital (hard-coded key).
  
  Gerado com assistência de: Claude Code
  
  Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"
  
  # Push
  git push origin test/security-scan
  
  # Criar PR no GitHub/GitLab
  # Verificar se workflow detecta a vulnerabilidade
  ```
  
  **Validação**:
  - [ ] Workflow roda automaticamente
  - [ ] Vulnerabilidade é detectada (TruffleHog)
  - [ ] PR é bloqueado ou comentado
  - [ ] Mensagem de erro é clara

- [ ] **Documentar Resultados** (30 min)
  
  Criar arquivo `docs/fase0-teste-security.md`:
  ```markdown
  # Teste de Security Scanning - Fase 0
  
  Data: [data]
  
  ## PRs Testados
  1. PR #X - [descrição]
     - Vulnerabilidade encontrada: [sim/não]
     - Tipo: [secrets/SAST/credentials]
     - Ação tomada: [bloqueado/warning]
  
  ## Falsos Positivos
  - [Se houver, listar]
  
  ## Ajustes Necessários
  - [Lista de ajustes]
  
  ## Decisão
  ✅ Security scan está funcionando
  ⚠️ Ajustes necessários antes de Semana 2
  ```

---

### Quarta-feira (3 horas)

- [ ] **Ajustar Falsos Positivos** (2 horas)
  
  **Se encontrou falsos positivos ontem:**
  
  1. Identificar padrões comuns
  2. Criar arquivo de configuração:
  
  ```yaml
  # .semgrep.yml (exemplo)
  rules:
    - id: exclude-test-files
      patterns:
        - pattern-not-inside: |
            test_*.py
      message: Ignorar arquivos de teste
  ```
  
  3. Adicionar whitelist ao TruffleHog:
  ```yaml
  # .trufflehog.yml
  allow:
    - 'test_*'  # Ignorar arquivos de teste
    - '*.example'  # Ignorar arquivos de exemplo
  ```
  
  4. Testar novamente com PR de ontem
  5. Validar que falsos positivos sumiram

- [ ] **Documentar Configurações** (1 hora)
  
  Atualizar `docs/security-validation-checklist.md`:
  ```markdown
  ## Configurações de Exceção
  
  ### Arquivos Ignorados
  - `test_*.py` - Arquivos de teste (podem ter mocks)
  - `*.example` - Exemplos de configuração
  
  ### Padrões Permitidos
  - API keys em comentários de docs
  - Fake credentials em testes
  
  Revisão: Mensal
  ```

---

### Quinta-feira (2 horas)

- [ ] **Training do Time** (2 horas)
  
  **Preparação** (30 min antes):
  ```bash
  # Criar apresentação (slides ou doc)
  # - Por que security scanning?
  # - Como funciona o CI/CD?
  # - O que fazer quando bloqueia?
  # - Demo do checklist
  ```
  
  **Sessão de Training**:
  
  **Agenda** (2 horas):
  
  1. **Contexto** (15 min)
     - Por que Fase 0?
     - Dados da literatura (29% hard-coded credentials)
     - Nosso objetivo
  
  2. **Como Funciona** (30 min)
     - Demo do CI/CD ao vivo
     - Mostrar PR sendo bloqueado
     - Interpretar logs
     - Corrigir vulnerabilidade
  
  3. **Security Checklist** (30 min)
     - Walkthrough do checklist
     - Red flags principais
     - Quando escalar
  
  4. **Hands-on** (30 min)
     - Pair programming
     - Cada dev cria PR de teste
     - Valida que entendeu
  
  5. **Q&A** (15 min)
  
  **Entregáveis**:
  - [ ] Gravação da sessão
  - [ ] Slides compartilhados
  - [ ] Quiz de validação (80% para passar)

- [ ] **Quiz de Validação** (Google Forms)
  
  **Perguntas** (10 questões, 5 min):
  
  1. O que o TruffleHog detecta?
     - [ ] Bugs
     - [x] Secrets/credentials
     - [ ] Performance issues
  
  2. Quando um PR deve ser bloqueado?
     - [x] Critical/High vulnerabilidade
     - [ ] Medium vulnerabilidade
     - [ ] Qualquer vulnerabilidade
  
  3. O que fazer se security scan falhar?
     - [ ] Fazer merge mesmo assim
     - [x] Corrigir vulnerabilidade
     - [ ] Desabilitar scan
  
  [... 7 perguntas mais]
  
  **Validação**: 100% do time com 80%+ de acerto

---

### Sexta-feira (1 hora)

- [ ] **Retrospectiva de Segurança - Semana 1** (1 hora)
  
  **Reunião obrigatória com todo o time**
  
  **Agenda**:
  
  1. **Review de PRs** (20 min)
     - Listar todos os PRs da semana
     - Quantos foram bloqueados?
     - Vulnerabilidades encontradas?
     - Alguma passou despercebida?
  
  2. **Feedback do Time** (20 min)
     - O que funcionou bem?
     - O que frustrou?
     - Scan está muito lento?
     - Muitos falsos positivos?
  
  3. **Ajustes para Semana 2** (15 min)
     - Lista de melhorias
     - Responsáveis
     - Prioridade
  
  4. **Gate Decision** (5 min)
     - ✅ Prosseguir para Semana 2?
     - ⚠️ Ajustar mais 1 semana?
     - ❌ Re-avaliar abordagem?
  
  **Gate Criteria**:
  - [ ] CI/CD rodando em 100% dos PRs
  - [ ] Zero vulnerabilidades críticas não detectadas
  - [ ] 100% do time treinado (quiz 80%+)
  - [ ] Checklist de segurança em uso
  - [ ] Máximo 5% falsos positivos

---

## 📅 SEMANA 2: Baseline de Métricas

### Segunda-feira (1 hora)

- [ ] **Coletar Primeira Semana de Dados** (1 hora)
  
  **Manualmente no Google Sheet**:
  
  1. **Aba Commits**:
     ```bash
     # Extrair dados da última semana
     git log --since="1 week ago" --pretty=format:"%ad|%an|%s" --date=short
     
     # Para cada commit:
     # - Data
     # - Dev
     # - Tipo (AI se menciona Claude/Copilot/Gemini)
     # - Ferramenta
     # - LOC (git diff --shortstat)
     ```
  
  2. **Aba PRs**:
     - Listar PRs merged
     - Calcular time to merge
     - Marcar rejeitados
  
  3. **Aba Security**:
     - Revisar logs do CI/CD
     - Contar findings por severidade
     - Status de correção

---

### Terça-Quarta-Quinta (Coleta Contínua)

- [ ] **Monitorar Métricas Diariamente** (15 min/dia)
  
  **Checklist diário**:
  - [ ] Revisar security findings do dia
  - [ ] Validar que PRs estão passando por scan
  - [ ] Documentar edge cases
  - [ ] Ajustar configurações se necessário

---

### Sexta-feira (2 horas)

- [ ] **Compilar Baseline** (1 hora)
  
  **Criar arquivo** `reports/baseline-semana1-2.md`:
  
  ```markdown
  # Baseline - Semanas 1-2 (Fase 0)
  
  Período: 27/05/2026 - 07/06/2026
  
  ## Dados Coletados
  
  ### Commits
  - Total: X
  - Com IA: Y (Z%)
  - Tradicional: W
  
  ### PRs
  - Total merged: X
  - Rejection rate: Y%
  - Time to merge (median): Z horas
  
  ### Security
  - Critical: X (target: 0)
  - High: Y
  - Medium: Z
  - False positive rate: W% (target: <5%)
  
  ### Bugs
  - Total: X
  - Em produção: Y (target: 0)
  - Defect density: Z bugs/1000 LOC
  
  ## Baseline Estabelecido ✅
  
  Valores de referência para comparação nos próximos 6 meses.
  ```

- [ ] **Retrospectiva Final da Fase 0** (1 hora)
  
  **Reunião com todo o time**
  
  **Objetivo**: Decidir se avança para Fase 1
  
  **Perguntas**:
  1. Security scan está funcionando de forma confiável?
  2. Time está confortável com checklist?
  3. Métricas estão sendo coletadas?
  4. Algum blocker crítico?
  
  **Gate Criteria da Fase 0**:
  - [ ] CI/CD rodando security scan em 100% dos PRs
  - [ ] Checklist de segurança documentado e socializado
  - [ ] Rastreabilidade de commits IA implementada
  - [ ] Baseline de métricas definida e coleta iniciada
  - [ ] **Zero vulnerabilidades críticas em código IA atual**
  
  **Decisão**:
  - ✅ **Avançar para Fase 1** (se todos os critérios OK)
  - ⚠️ **Ajustar mais 1 semana** (se algum critério faltando)
  - ❌ **Re-avaliar abordagem** (se problemas fundamentais)

---

## 📊 Dashboard de Progresso

### Status da Fase 0

```
Semana 1: Security Quick Wins
[████████░░] 80% - Em andamento

- Segunda (Dia 1):     [████████████] 100% ✅
- Terça:               [░░░░░░░░░░░░]   0% 📅 Próximo
- Quarta:              [░░░░░░░░░░░░]   0%
- Quinta:              [░░░░░░░░░░░░]   0%
- Sexta:               [░░░░░░░░░░░░]   0%

Semana 2: Baseline de Métricas
[░░░░░░░░░░] 0%

- Segunda:             [░░░░░░░░░░░░]   0%
- Terça-Quinta:        [░░░░░░░░░░░░]   0%
- Sexta:               [░░░░░░░░░░░░]   0%
```

---

## 🎯 Objetivos da Fase 0 (Resumo)

### O Que Implementamos

1. ✅ **Security Scanning Automático**
   - TruffleHog, Semgrep, GitLeaks
   - Roda em todo PR
   - Bloqueia vulnerabilidades críticas

2. ✅ **Security Validation Checklist**
   - Red flags documentados
   - Processo de code review
   - Escalação de incidentes

3. ✅ **Rastreabilidade de Código IA**
   - Tags em commits
   - Permite análise futura
   - Separação AI vs. tradicional

4. ✅ **Baseline de Métricas**
   - 10 métricas definidas
   - Dashboard configurado
   - Coleta iniciada

5. ✅ **Training do Time**
   - 100% treinados
   - Quiz validado
   - Confortáveis com processo

### Por Que Isso Importa

**Sem Fase 0**:
- ❌ Código IA pode ter vulnerabilidades
- ❌ Sem forma de medir impacto
- ❌ Sem rastreabilidade
- ❌ Time despreparado

**Com Fase 0**:
- ✅ Vulnerabilidades bloqueadas antes de produção
- ✅ Métricas para validar ROI
- ✅ Rastreabilidade total
- ✅ Time preparado e confiante

---

## 📞 Suporte Durante Fase 0

### Problemas Comuns

**"CI/CD não está rodando"**
- Verificar sintaxe do YAML
- Validar permissões do GitHub Actions
- Consultar logs

**"Muitos falsos positivos"**
- Normal nas primeiras semanas
- Ajustar configurações (Quarta-feira)
- Documentar exceções

**"Time está resistindo"**
- Explicar o "por quê" (dados da literatura)
- Mostrar quick wins
- Dar voz às preocupações

**"Não tenho tempo para coletar métricas"**
- Semana 1: Manual é OK (investimento inicial)
- Semana 2: Começar a automatizar
- Fase 2: Totalmente automatizado

### Contatos

**Tech Lead**: [seu contato]  
**Canal Slack**: #fase0-security  
**Issues**: GitHub Issues com tag `fase0`

---

## ✅ Checklist Final - Pronto para Fase 1?

### Antes de avançar, validar:

**Técnico**:
- [ ] Security scan rodando 100%
- [ ] Zero vulnerabilidades críticas
- [ ] Falsos positivos < 5%
- [ ] Dashboard funcionando

**Processo**:
- [ ] Checklist documentado
- [ ] Time treinado (100%)
- [ ] Rastreabilidade implementada
- [ ] Baseline coletado (2 semanas)

**Pessoas**:
- [ ] Time confortável com processo
- [ ] Nenhuma resistência forte
- [ ] Comunicação clara estabelecida
- [ ] Ownership definido (Tech Lead)

**Decisão**:
- [ ] ✅ **SIM - Avançar para Fase 1** (Quality Gates)
- [ ] ⚠️ **AJUSTAR - Mais 1 semana de Fase 0**
- [ ] ❌ **PAUSAR - Re-avaliar abordagem**

---

**Fase 0 é a FUNDAÇÃO. Não pule etapas. Melhor fazer bem feito que rápido.**

**Próximo**: [FASE1-CHECKLIST.md](FASE1-CHECKLIST.md) (criar quando Fase 0 completa)

---

**Última atualização**: 27/05/2026  
**Status**: 🟡 Dia 1 Completo - Continuando...
