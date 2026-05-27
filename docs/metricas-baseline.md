# Métricas Baseline - Desenvolvimento com IA

**Versão**: 1.0  
**Data de início**: 27 de maio de 2026  
**Objetivo**: Estabelecer linha de base para medir impacto de IA no desenvolvimento

---

## 📊 Métricas Primárias

### 1. Defect Density (Bugs por 1000 LOC)

**Definição**: Número de bugs encontrados por 1000 linhas de código

**Como medir**:
```
Defect Density = (Total de Bugs / Total LOC) × 1000
```

**Separar**:
- Código IA-assisted
- Código tradicional

**Fases de detecção**:
- Code review
- QA/Testing
- Produção (CRITICAL)

**Coleta**:
```markdown
| Data | Tipo Código | LOC | Bugs (Review) | Bugs (QA) | Bugs (Prod) | Density |
|------|-------------|-----|---------------|-----------|-------------|---------|
| 27/05| AI          | 500 | 2             | 1         | 0           | 6.0     |
| 27/05| Traditional | 300 | 1             | 0         | 0           | 3.3     |
```

**Target**: 
- Redução de 30% em 6 meses
- Bugs em produção = 0

---

### 2. Code Review Rejection Rate

**Definição**: Percentual de PRs que precisam de correções antes de aprovação

**Como medir**:
```
Rejection Rate = (PRs Rejeitados / Total PRs) × 100%
```

**O que conta como "rejeitado"**:
- PR recebe "Request Changes"
- Comentários de bloqueio (não minor suggestions)
- Security scan falha

**Separar**:
- PRs com código IA
- PRs tradicionais

**Coleta**:
```markdown
| Semana | Total PRs | PRs AI | Rejeitados AI | Rate AI | Rejeitados Trad | Rate Trad |
|--------|-----------|--------|---------------|---------|-----------------|-----------|
| 1      | 10        | 4      | 1             | 25%     | 1               | 16.7%     |
```

**Target**:
- Rate de código IA <= código tradicional
- Absoluto: < 20%

---

### 3. Security Findings (Vulnerabilidades por Commit)

**Definição**: Número de vulnerabilidades de segurança encontradas

**Como medir**:

Por severidade:
- **Critical**: Exploração direta, acesso não autorizado
- **High**: Alto risco, impacto significativo
- **Medium**: Risco moderado
- **Low**: Teórico ou impacto mínimo

**Separar**:
- Código IA vs. tradicional
- Detectado por: CI/CD vs. Manual vs. Produção

**Coleta**:
```markdown
| Data | Tipo | Critical | High | Medium | Low | Detecção | Status |
|------|------|----------|------|--------|-----|----------|--------|
| 27/05| AI   | 0        | 1    | 2      | 3   | CI/CD    | Fixed  |
| 28/05| Trad | 0        | 0    | 1      | 1   | Manual   | Fixed  |
```

**Target**:
- Critical/High em produção = 0
- Detection por CI/CD > 90%
- Mean time to fix < 24h (Critical)

---

### 4. Time to First Working Solution

**Definição**: Tempo desde início até PR aprovado e merged

**Como medir**:
```
Time = (Merge timestamp - First commit timestamp)
```

**Fases**:
1. Implementation time (first commit → PR opened)
2. Review time (PR opened → approved)
3. Fixes time (changes requested → re-approved)

**Separar**:
- Tarefas com IA vs. tradicionais
- Por complexidade (Small/Medium/Large)

**Coleta**:
```markdown
| Task ID | Complexidade | Com IA? | Impl (h) | Review (h) | Fixes (h) | Total (h) |
|---------|--------------|---------|----------|------------|-----------|-----------|
| TASK-1  | Small        | Sim     | 2        | 0.5        | 0.5       | 3         |
| TASK-2  | Medium       | Não     | 8        | 1          | 2         | 11        |
```

**Comparar**:
- Mediana e p95 (mais robusto que média)
- IA vs. tradicional por complexidade

**Target**:
- Redução de 25% no p95
- Review time não aumentar (IA não adiciona overhead)

---

### 5. Test Coverage Delta

**Definição**: Variação na cobertura de testes

**Como medir**:
```
Coverage Delta = Coverage After - Coverage Before
```

**Separar**:
- Testes gerados por IA
- Testes escritos manualmente

**Qualidade dos testes**:
- Mutation score (se possível)
- Assertions per test
- Edge cases cobertos

**Coleta**:
```markdown
| PR | Tipo Código | LOC Added | Coverage Before | Coverage After | Delta | Testes IA? |
|----|-------------|-----------|-----------------|----------------|-------|------------|
| 1  | AI          | 200       | 75%             | 82%            | +7pp  | Sim        |
| 2  | Traditional | 150       | 75%             | 78%            | +3pp  | Não        |
```

**Target**:
- Coverage >= 80% para código novo
- Delta sempre positivo (nunca diminuir)
- Testes IA com qualidade igual/superior a manuais

---

## 📈 Métricas Secundárias

### 6. Developer Satisfaction (NPS)

**Definição**: Net Promoter Score para uso de IA

**Pergunta mensal**:
> "Em uma escala de 0-10, o quanto você recomendaria o uso de IA no desenvolvimento para um colega?"

**Cálculo**:
```
NPS = % Promotores (9-10) - % Detratores (0-6)
```

**Coleta**:
```markdown
| Mês | Respondentes | Promotores | Neutros | Detratores | NPS  |
|-----|--------------|------------|---------|------------|------|
| Jun | 8            | 4 (50%)    | 2 (25%) | 2 (25%)    | +25  |
```

**Target**:
- Mês 1: Baseline (qualquer valor)
- Mês 3: NPS >= 50
- Mês 6: NPS >= 70

**Acompanhar**:
- Perguntas abertas (o que funciona / o que frustra)
- Criar action items para top 3 frustrações

---

### 7. Time Saved (Self-Reported)

**Definição**: Tempo que devs estimam ter economizado com IA

**Coleta semanal** (friday standup):
> "Quanto tempo você economizou usando IA esta semana?"

**Formato**:
```markdown
| Dev   | Semana | Horas Economizadas | Caso Destaque |
|-------|--------|--------------------|---------------|
| Alice | 22     | 4h                 | Debug complexo reduziu de 6h → 2h |
| Bob   | 22     | 2h                 | Geração de testes |
```

**Cuidados**:
- Percepção != realidade (complementar com métricas objetivas)
- Útil para identificar casos de sucesso
- Não usar como métrica única de ROI

**Target**:
- Baseline: 0-2h/dev/semana (primeiras semanas)
- Mês 3: 4-6h/dev/semana
- Mês 6: 6-8h/dev/semana

---

### 8. AI Tool Usage

**Definição**: Frequência de uso das ferramentas IA

**Coleta automática** (via commits):
```bash
# Contar commits com tags IA
git log --since="1 week ago" | grep -c "Claude\|Copilot\|Gemini"
```

**Separar por ferramenta**:
```markdown
| Semana | Total Commits | Claude | Copilot | Gemini | Tradicional | % IA |
|--------|---------------|--------|---------|--------|-------------|------|
| 22     | 50            | 15     | 10      | 5      | 20          | 60%  |
```

**Tracking**:
- Adoption rate (% de commits com IA)
- Distribuição por ferramenta
- Quais devs usam vs. não usam

**Target**:
- Mês 1: 30% adoption
- Mês 3: 60% adoption
- Mês 6: 80% adoption (não forçar 100%, permitir flexibilidade)

---

## 🎯 Métricas de Processo

### 9. Pipeline Performance

**Definição**: Tempo e taxa de sucesso do CI/CD

**Métricas**:
```markdown
| Métrica | Valor | Target |
|---------|-------|--------|
| Tempo médio de pipeline | 4.2 min | < 5 min |
| Taxa de sucesso first-time | 85% | > 80% |
| False positives (security) | 8% | < 5% |
| Blocked PRs (legítimos) | 2 | 0 |
```

**Tracking**:
- Se pipeline fica muito lento, devs vão contornar
- Se muitos falsos positivos, vão ignorar
- Balance: rigor vs. developer experience

---

### 10. Documentation Quality

**Definição**: Documentação está atualizada e útil?

**Avaliação qualitativa trimestral**:
```markdown
| Documento | Última Atualização | Útil? | Action Needed |
|-----------|-------------------|-------|---------------|
| CLAUDE.md | 27/05/2026        | ✅    | -             |
| Apêndice A| 15/04/2026        | ⚠️    | Atualizar exemplos |
```

**Indicadores**:
- Documentos desatualizados (> 3 meses sem review)
- Perguntas repetidas no Slack (doc não está clara)
- PRs rejeitados por não seguir doc (doc não está visível)

**Target**:
- 100% docs atualizados trimestralmente
- < 5 perguntas repetidas/mês

---

## 📅 Calendário de Coleta

### Diário
- ✅ Pipeline metrics (automático)
- ✅ Security findings (automático via CI/CD)

### Semanal (Friday standup - 15 min)
- ✅ Commit counts (AI vs. tradicional)
- ✅ Time saved (self-reported)
- ✅ Quick wins da semana
- ✅ Blockers/frustrations

### Mensal (última sexta - 1h)
- ✅ Developer satisfaction survey
- ✅ Consolidar defect density
- ✅ Review de todos os security findings
- ✅ Atualizar dashboard

### Trimestral (ou ao final de cada fase)
- ✅ Relatório executivo completo
- ✅ Retrospectiva de metodologia
- ✅ Review de documentação
- ✅ Ajustes em métricas (se necessário)

---

## 📊 Dashboard (Template)

### Google Sheets Structure

**Sheet 1: Commits**
```
| Data | Dev | Tipo Código | Ferramenta | LOC | Arquivo | Issue |
```

**Sheet 2: PRs**
```
| PR # | Dev | Tipo | Opened | Merged | Time (h) | Rejected? | Reason |
```

**Sheet 3: Bugs**
```
| Bug ID | PR Origin | Fase Detecção | Severidade | Fixed Date | MTTR (h) |
```

**Sheet 4: Security**
```
| Date | Tipo Código | Critical | High | Medium | Low | Source | Status |
```

**Sheet 5: Surveys**
```
| Mês | Dev | NPS Score | Time Saved | Feedback Positivo | Feedback Negativo |
```

**Sheet 6: Summary (automático)**
```
Gráficos:
- Defect density trend (AI vs. Traditional)
- Time to merge (AI vs. Traditional)
- Security findings por semana
- NPS trend
- Adoption rate
```

---

## 🔄 Processo de Coleta

### Responsável: Tech Lead

**Tempo necessário**:
- Diário: 0 min (automático)
- Semanal: 15 min (compilar dados)
- Mensal: 1 hora (survey + análise)
- Trimestral: 4 horas (relatório)

**Ferramentas**:
```bash
# Script de coleta semanal
./scripts/collect-weekly-metrics.sh

# Gera:
# - Commit counts por tipo
# - PR statistics
# - Security findings summary
# - Exporta para Google Sheets
```

---

## 🎯 Como Usar Essas Métricas

### ✅ Bom Uso

1. **Identificar tendências**
   - "Defect density está aumentando → investigar"
   - "Time to merge diminuiu 20% → ótimo sinal"

2. **Validar hipóteses**
   - "IA ajuda em X mas não em Y → ajustar uso"
   - "Templates melhorados reduziram rejeição → manter"

3. **Tomar decisões**
   - "Security findings altos → reforçar training"
   - "NPS baixo → retrospectiva focada"

4. **Comunicar valor**
   - Relatórios executivos
   - Business case para investimento
   - Celebrar wins

### ❌ Mau Uso

1. **Comparar desenvolvedores**
   - ❌ "Alice tem menos bugs que Bob"
   - Métricas são para melhorar processo, não ranquear pessoas

2. **Otimizar métrica errada**
   - ❌ Aumentar velocidade diminuindo qualidade
   - ❌ Reduzir rejection rate aprovando tudo

3. **Ignorar contexto**
   - Complexidade das tarefas varia
   - Times diferentes têm baselines diferentes

4. **Micro-management**
   - ❌ "Por que você demorou X horas?"
   - Foco em tendências, não em eventos isolados

---

## 📈 Baseline vs. Target (6 meses)

| Métrica | Baseline (Mês 0) | Target (Mês 6) | Como Medir Sucesso |
|---------|------------------|----------------|-------------------|
| **Defect Density** | 5.0 bugs/1000 LOC | 3.5 (-30%) | ✅ Se redução >= 30% |
| **Security Critical** | Baseline | 0 em prod | ✅ Se zero incidentes |
| **Time to Merge (p95)** | 48h | 36h (-25%) | ✅ Se redução >= 20% |
| **Test Coverage** | 70% | 80% (+10pp) | ✅ Se >= 80% |
| **NPS** | TBD | >= 70 | ✅ Se >= 70 |
| **Adoption Rate** | TBD | 80% | ✅ Se >= 75% |
| **CI/CD Success** | TBD | > 85% | ✅ Se > 85% |
| **False Positives** | TBD | < 5% | ✅ Se < 5% |

**Como validar sucesso do programa**:
- ✅ 80%+ das métricas atingiram target
- ✅ Nenhuma métrica piorou significativamente
- ✅ ROI positivo (economizamos mais do que investimos)
- ✅ Time satisfeito (NPS alto)

---

## 🔧 Troubleshooting

### "Não tenho tempo para coletar métricas"

**Solução**:
- Automatize o máximo possível (scripts, CI/CD)
- Coleta semanal em 15min (não diária manual)
- Delegue: cada dev reporta próprios dados

### "Métricas não mostram melhoria"

**Solução**:
- Normal nas primeiras 4-6 semanas (curva de aprendizado)
- Se após 3 meses sem melhoria: retrospectiva profunda
- Possíveis causas: metodologia errada, ferramentas inadequadas, falta de training

### "Dados estão inconsistentes"

**Solução**:
- Definir processo claro de coleta
- Validar dados semanalmente
- Corrigir inconsistências imediatamente
- Documentar edge cases

### "Dashboard não está sendo usado"

**Solução**:
- Apresentar em standups/retrospectivas
- Tornar visível (monitor, Slack bot)
- Mostrar insights acionáveis (não só números)

---

## 📞 Suporte

**Dúvidas sobre métricas**: @tech-lead no Slack  
**Issues com coleta**: Abrir issue no GitHub  
**Sugestões de novas métricas**: #ai-dev-playbook

---

## 🔄 Revisão deste Documento

**Frequência**: Trimestral  
**Próxima revisão**: 27/08/2026  
**Owner**: Tech Lead

**Changelog**:
- 27/05/2026: v1.0 - Baseline definido
