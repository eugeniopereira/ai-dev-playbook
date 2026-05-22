---
name: plan-review
description: Revisa e refina plano de implementação proposto
---

# Review - Revisor de Plano de Implementação

Revisa e refina planos de implementação considerando padrões do projeto, simplicidade e segurança.

## Uso

```bash
/plan-review [<app>]
```

**Argumento opcional:**
- `<app>`: api, web, worker ou agent (para carregar contextos específicos)
- Se omitido, tenta inferir do plano na conversa

## Exemplos

```bash
# Revisar o plano atual (infere app automaticamente)
/plan-review

# Revisar com contexto específico de app
/plan-review api
/plan-review worker
```

---

## Prompt de Execução

Ao receber a solicitação de revisão:

1. **Identifique o plano na conversa atual** que precisa ser revisado

2. **Identifique a aplicação** (do argumento ou do plano)

3. **Carregue os contextos relevantes:**
   - `CLAUDE.md` (raiz)
   - `{app}/CLAUDE.md` (se existir)
   - `{app}/docs/ai-context.md` (se existir)

4. **Execute o prompt:**

---

Seja um arquiteto de software sênior e code reviewer.

**Contextos do projeto carregados:**
- CLAUDE.md (raiz)
- {app-specific CLAUDE.md se existir}
- {ai-context.md se existir}

**Plano a ser revisado:**
{plano_da_conversa}

**Revise o plano proposto considerando:**

1. **Padrões do projeto**
   - Está seguindo as convenções de código estabelecidas?
   - Usa as ferramentas e bibliotecas corretas do stack?
   - Respeita a arquitetura atual?
   - Segue as práticas de git workflow (branch naming, commits)?

2. **Simplicidade da solução**
   - Há passos desnecessários ou redundantes?
   - A solução está over-engineered?
   - Pode ser simplificada sem perder qualidade?
   - Está criando abstrações prematuras?
   - Há dependências desnecessárias sendo adicionadas?

3. **Possíveis falhas**
   - Identifique edge cases não considerados
   - Verifique tratamento de erros
   - Avalie impacto em funcionalidades existentes
   - Considere cenários de rollback
   - Valide integração com serviços externos (SharePoint, GCS, Azure AD, etc)
   - Verifique segurança (CORS, autenticação, validação de entrada)

4. **Testes e validação**
   - Os passos incluem testes adequados?
   - É possível validar cada passo isoladamente?
   - Faltam testes de integração críticos?

**Formato de saída esperado:**

```markdown
## 📋 Análise do Plano Original

### ✅ Pontos Fortes
- [Lista do que está bom no plano]

### ⚠️ Problemas Identificados
- [Lista de problemas, anti-patterns, riscos]

### 💡 Sugestões de Melhoria
- [Melhorias específicas com justificativa]

---

## 🎯 Plano Revisado

### Resumo
[Versão refinada do resumo]

### Passos de Implementação

#### 1. [Nome do passo] - Esforço: [Baixo/Médio/Alto]
- **Arquivos afetados**: `path/to/file.py:linha`
- **Descrição**: [O que fazer - versão simplificada/ajustada]
- **Dependências**: [Lista de outros passos ou nenhuma]
- **Riscos mitigados**: [Como os riscos foram endereçados]
- **Testes**: [Testes específicos para este passo]

#### 2. [Próximo passo]
...

### Considerações Finais
- Pontos de atenção
- Estratégia de rollback
- Validação pós-deploy

---

## 📊 Resumo de Mudanças

- **Passos removidos**: [Lista e justificativa]
- **Passos adicionados**: [Lista e justificativa]
- **Passos modificados**: [Lista e justificativa]
- **Estimativa de esforço**: [Original] → [Revisada]
```

---
