---
name: plan
description: Gera plano de implementação para qualquer app do projeto (api/web/worker/agent)
---

# Plan - Gerador de Plano de Implementação

Gera planos de implementação contextualizados para as aplicações do projeto Danfe AI.

## Uso

```bash
/plan <app> "<descrição_do_jira>" [<logs_opcional>]
```

**Apps disponíveis:**
- `api` - FastAPI backend (GCP)
- `web` - Next.js frontend (GCP)
- `worker` - Worker assíncrono (GCP)
- `agent` - Vertex AI agent

## Exemplos

```bash
# Exemplo sem logs (apenas descrição do Jira)
/plan api "DANFEAI-127: Implementar novo endpoint de relatórios"
/plan web "DANFEAI-128: Adicionar página de configurações do usuário"

# Exemplo com logs (quando há erro para investigar)
/plan api "DANFEAI-123: Erro ao processar DANFE" "KeyError: 'itens' at line 45"
/plan web "DANFEAI-124: Erro na autenticação MSAL" "MSAL error: invalid_token"
/plan worker "DANFEAI-125: Callback timeout" "TimeoutError no processamento"
/plan agent "DANFEAI-126: JSON parsing falhou" "Gemini retornou texto malformado"
```

---

## Prompt de Execução

Ao receber os argumentos, execute:

1. **Identifique a aplicação** do primeiro argumento (api/web/worker/agent)

2. **Carregue os contextos relevantes:**
   - **Raiz do projeto**: `CLAUDE.md` (sempre)
   - **App-specific CLAUDE.md** (se existir):
     - `api/` → não tem CLAUDE.md próprio, usa raiz
     - `web/` → não tem CLAUDE.md próprio, usa raiz
     - `app-danfe-worker/CLAUDE.md`
     - `app-danfe-agent/CLAUDE.md`
   - **AI Context** (se existir):
     - `api/docs/ai-context.md`
     - `web/docs/ai-context.md` ou `web/ai-context.md`
     - `app-danfe-worker/docs/ai-context.md` ou `app-danfe-worker/ai-context.md`
     - `app-danfe-agent/docs/ai-context.md` ou `app-danfe-agent/ai-context.md`

3. **Execute o prompt:**

---

Seja um dev fullstack senior especializado em {app}.

**Contextos do projeto carregados:**
- CLAUDE.md (raiz)
- {app-specific CLAUDE.md se existir}
- {ai-context.md se existir}

**Problema (Jira):**
{descrição_do_jira}

**Logs/Contexto Técnico:**
{logs se existir}

**Gere um plano de implementação seguindo as premissas:**

1. **Quebrar a solução em passos técnicos pequenos**
   - Cada passo deve ser atômico e testável
   - Indicar arquivos/funções afetados
   
2. **Identificar dependências entre passos**
   - Mapear ordem de execução
   - Destacar pontos de bloqueio
   
3. **Identificar riscos**
   - Riscos técnicos (breaking changes, performance)
   - Riscos de integração (API, banco, serviços externos)
   - Riscos de segurança
   
4. **Estimar esforço**
   - Baixo: < 2 horas
   - Médio: 2-8 horas
   - Alto: > 8 horas

**Formato de saída esperado:**

```markdown
## Resumo
[Breve explicação da solução]

## Passos de Implementação

### 1. [Nome do passo] - Esforço: [Baixo/Médio/Alto]
- **Arquivos afetados**: `path/to/file.py:linha`
- **Descrição**: [O que fazer]
- **Dependências**: [Lista de outros passos ou nenhuma]
- **Riscos**: [Lista de riscos ou nenhum]

### 2. [Próximo passo]
...

## Considerações Finais
- Pontos de atenção
- Testes necessários
- Rollback strategy (se aplicável)
```

---
