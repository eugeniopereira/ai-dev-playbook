# Dashboard de Métricas - Setup Rápido

**Tempo de setup**: 30 minutos  
**Ferramenta**: Google Sheets (gratuito, colaborativo)  
**Owner**: Tech Lead

---

## 🚀 Setup em 5 Passos

### Passo 1: Criar Google Sheet (5 min)

1. Acesse [Google Sheets](https://sheets.google.com)
2. Crie novo sheet: "AI Dev Metrics - 2026"
3. Compartilhe com o time (view access)
4. Tech Lead tem edit access

### Passo 2: Criar Abas (10 min)

**Aba 1: Commits**
```
Colunas:
A: Data (DD/MM/YYYY)
B: Desenvolvedor
C: Tipo Código (AI / Traditional)
D: Ferramenta (Claude / Copilot / Gemini / Manual / N/A)
E: LOC Adicionadas
F: LOC Removidas
G: Arquivos Modificados
H: Issue/Task ID
I: Complexidade (Small / Medium / Large)
```

**Aba 2: Pull Requests**
```
Colunas:
A: PR Number
B: Desenvolvedor
C: Tipo Código (AI / Traditional)
D: Ferramenta
E: Data Opened
F: Data Merged
G: Time to Merge (horas) [=F-E em horas]
H: Rejeitado? (Sim / Não)
I: Motivo Rejeição
J: Security Scan (Pass / Fail / N/A)
K: Peer Reviews (#)
```

**Aba 3: Bugs**
```
Colunas:
A: Bug ID
B: PR Origin (link)
C: Fase Detecção (Review / QA / Production)
D: Severidade (Critical / High / Medium / Low)
E: Tipo Código (AI / Traditional)
F: Data Encontrado
G: Data Corrigido
H: MTTR (horas) [=G-F]
I: Root Cause
```

**Aba 4: Security**
```
Colunas:
A: Data
B: PR Number
C: Tipo Código (AI / Traditional)
D: Ferramenta IA
E: Critical (#)
F: High (#)
G: Medium (#)
H: Low (#)
I: Fonte Detecção (CI/CD / Manual / Production)
J: Status (Open / Fixed)
K: Time to Fix (horas)
```

**Aba 5: Satisfação**
```
Colunas:
A: Mês
B: Desenvolvedor
C: NPS Score (0-10)
D: Horas Economizadas (self-report)
E: Feedback Positivo (texto)
F: Feedback Negativo (texto)
G: Sugestão de Melhoria (texto)
```

**Aba 6: Summary (Dashboard Visual)**
- Deixar em branco por enquanto
- Vamos popular com gráficos no Passo 4

### Passo 3: Popular Dados Iniciais (5 min)

**Na aba "Commits"**, adicionar commits da última semana:

Exemplo:
```
27/05/2026 | Alice | AI | Claude | 150 | 20 | 3 | TASK-123 | Small
27/05/2026 | Bob | Traditional | N/A | 80 | 10 | 2 | TASK-124 | Medium
```

**Na aba "Pull Requests"**, adicionar PRs recentes:

Exemplo:
```
42 | Alice | AI | Claude | 27/05/2026 10:00 | 27/05/2026 14:00 | 4 | Não | - | Pass | 2
```

**Objetivo**: Ter pelo menos 5-10 linhas de dados de exemplo para testar fórmulas

### Passo 4: Criar Gráficos (10 min)

**Na aba "Summary"**, criar:

**Gráfico 1: Commits AI vs. Traditional (Por Semana)**
```
Tipo: Stacked Bar Chart
Dados: Aba "Commits", colunas A (Data) e C (Tipo Código)
Agregação: Count por semana
```

**Gráfico 2: Defect Density Trend**
```
Tipo: Line Chart
Eixo X: Semana
Eixo Y: Bugs / 1000 LOC
Duas linhas: AI vs. Traditional

Fórmula (na Summary):
=SUMIF(Bugs!E:E,"AI",Bugs!A:A) / (SUMIF(Commits!C:C,"AI",Commits!E:E)/1000)
```

**Gráfico 3: Security Findings (Trend)**
```
Tipo: Stacked Area Chart
Eixo X: Semana
Eixo Y: Count
Áreas: Critical, High, Medium, Low
```

**Gráfico 4: NPS Trend**
```
Tipo: Line Chart
Eixo X: Mês
Eixo Y: NPS Score
Linha única com target line em 70
```

**Gráfico 5: Time to Merge (AI vs. Traditional)**
```
Tipo: Box Plot ou Column Chart (median)
Comparar: AI vs. Traditional
Métrica: Median time to merge
```

### Passo 5: Automatizar Coleta (Opcional - 30 min extra)

**Script Python** (salvar como `scripts/export-to-sheets.py`):

```python
#!/usr/bin/env python3
"""
Exporta métricas do Git para Google Sheets
Requer: gspread, oauth2client

Setup:
pip install gspread oauth2client
"""

import gspread
from oauth2client.service_account import ServiceAccountCredentials
from datetime import datetime
import subprocess
import re

# Configurar credenciais (ver docs Google Sheets API)
scope = ['https://spreadsheets.google.com/feeds', 'https://www.googleapis.com/auth/drive']
creds = ServiceAccountCredentials.from_json_keyfile_name('credentials.json', scope)
client = gspread.authorize(creds)

# Abrir sheet
sheet = client.open("AI Dev Metrics - 2026").worksheet("Commits")

def get_commits_last_week():
    """Extrai commits da última semana"""
    cmd = 'git log --since="1 week ago" --pretty=format:"%ad|%an|%s" --date=short'
    output = subprocess.check_output(cmd, shell=True).decode('utf-8')
    
    commits = []
    for line in output.split('\n'):
        if not line:
            continue
        
        date, author, message = line.split('|')
        
        # Detectar se é código IA
        is_ai = bool(re.search(r'(Claude|Copilot|Gemini)', message, re.I))
        tipo = "AI" if is_ai else "Traditional"
        
        # Detectar ferramenta
        if 'Claude' in message:
            tool = "Claude"
        elif 'Copilot' in message:
            tool = "Copilot"
        elif 'Gemini' in message:
            tool = "Gemini"
        else:
            tool = "N/A"
        
        # LOC (simplified - usar git diff para precisão)
        loc_added = 0  # TODO: calcular com git diff
        
        commits.append([date, author, tipo, tool, loc_added, 0, 0, "", ""])
    
    return commits

def export_to_sheet():
    """Exporta dados para Google Sheets"""
    commits = get_commits_last_week()
    
    # Append rows
    for commit in commits:
        sheet.append_row(commit)
    
    print(f"✅ Exported {len(commits)} commits to Google Sheets")

if __name__ == "__main__":
    export_to_sheet()
```

**Agendar coleta semanal** (cron):
```bash
# crontab -e
0 9 * * 5 cd /opt/iplanrio/apps/ai-dev-playbook && python3 scripts/export-to-sheets.py
```

---

## 📊 Template de Coleta Semanal (Manual)

**Tempo**: 15 minutos toda sexta-feira

### Friday Standup Script

**1. Coletar commits (5 min)**

```bash
# Commits da última semana
git log --since="1 week ago" --oneline | wc -l

# Commits com IA
git log --since="1 week ago" --grep="Claude\|Copilot\|Gemini" --oneline | wc -l

# Por desenvolvedor
git shortlog --since="1 week ago" -sn
```

**Preencher aba "Commits"** com dados principais

**2. Revisar PRs (5 min)**

- Abrir GitHub/GitLab
- Listar PRs merged esta semana
- Anotar: número, autor, tempo de merge, rejeitado?
- **Preencher aba "Pull Requests"**

**3. Checar Security (2 min)**

- Revisar logs do CI/CD
- Contar findings por severidade
- **Preencher aba "Security"**

**4. Atualizar gráficos (2 min)**

- Abrir aba "Summary"
- Verificar se gráficos atualizaram automaticamente
- Se não, refresh manual

**5. Share com time (1 min)**

```
Slack post:
📊 Métricas da Semana 22

Commits: 35 (60% com IA)
PRs: 8 merged, 1 rejeitado
Security: 0 critical, 2 medium (fixed)
Time to merge (median): 6h

Dashboard: [link]
```

---

## 🎯 Interpretando o Dashboard

### ✅ Sinais Positivos

```
✅ Commits com IA aumentando semanalmente
✅ Defect density (AI) <= defect density (traditional)
✅ Security findings diminuindo
✅ Time to merge reduzindo
✅ NPS subindo
```

**Ação**: Celebrar! Compartilhar wins.

### ⚠️ Sinais de Atenção

```
⚠️ Defect density (AI) > tradicional por 2+ semanas
⚠️ Rejection rate (AI) > 30%
⚠️ Security critical findings > 0
⚠️ Time to merge aumentando
⚠️ NPS estável ou caindo
```

**Ação**: 
1. Investigar causa raiz
2. Retrospectiva focada
3. Ajustar metodologia/training

### 🚨 Sinais Críticos

```
🚨 Bugs críticos em produção (AI)
🚨 Security incident
🚨 NPS < 30 por 2+ meses
🚨 Adoption rate caindo
🚨 Time está resistindo ativamente
```

**Ação**:
1. Reunião de emergência
2. Pausar expansão
3. Root cause analysis
4. Plano de correção
5. Considerar pivotar ou pausar programa

---

## 📈 Dashboards Avançados (Fase 2)

**Quando tiver 8+ semanas de dados**, considerar:

### Opção 1: Metabase (Open Source)
- Queries SQL direto no banco
- Dashboards interativos
- Alertas automáticos

### Opção 2: Grafana + BigQuery
- Ingerir dados no BigQuery
- Visualizações avançadas
- Integração com alerting

### Opção 3: Ferramenta comercial
- DataDog
- New Relic
- Amplitude

**Decisão**: Validar ROI antes de investir em ferramenta paga

---

## 🔧 Troubleshooting

### "Gráficos não atualizam"

**Causa**: Dados em formato inconsistente  
**Solução**: Validar formato de datas, números sem texto

### "Muitos dados para preencher manualmente"

**Causa**: Falta automação  
**Solução**: Implementar script Python (Passo 5)

### "Time não olha dashboard"

**Causa**: Não está visível/relevante  
**Solução**:
- Apresentar em retrospectivas
- Slack bot com summary semanal
- TV/monitor com dashboard

### "Não sei o que significa métrica X"

**Causa**: Falta documentação  
**Solução**: Consultar [metricas-baseline.md](metricas-baseline.md)

---

## 📞 Próximos Passos

Após setup:
1. ✅ Coletar dados por 2 semanas (baseline)
2. ✅ Apresentar dashboard para time (10 min)
3. ✅ Ajustar baseado em feedback
4. ✅ Automatizar o que for repetitivo
5. ✅ Revisar semanalmente

**Link do Sheet**: [adicionar aqui após criar]  
**Owner**: Tech Lead  
**Atualização**: Sexta-feira 9h

---

**Setup completo? ✅ Próximo: Começar Semana 1 da Fase 0!**
