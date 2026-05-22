---
name: pr-description
description: Gera descrição de PR no arquivo pr-description.md baseado no template e diferenças entre branches
user-invocable: true
---

# PR Description - Gerador de Descrição de Pull Request

Analisa diferenças entre branches e gera descrição de PR seguindo o template do projeto.

## Uso

```bash
/pr-description <branch_origem> <branch_destino>
```

**Parâmetros**:
- `branch_origem`: Branch com as mudanças (ex: `DANFEIA-164/refactor/mensagem-de-retorno-no-bloqueio`)
- `branch_destino`: Branch de destino do PR (ex: `develop`, `staging`, `master`)

## Exemplos

```bash
# Gerar PR description para merge de feature em develop
/pr-description DANFEIA-164/refactor/mensagem-de-retorno-no-bloqueio develop

# Gerar PR description para merge de develop em staging
/pr-description develop staging

# Gerar PR description para release (staging -> master)
/pr-description staging master
```

---

## Prompt de Execução

Você é um desenvolvedor sênior especializado em documentar mudanças e criar descrições claras de Pull Requests.

### 1. Valide os argumentos

Se `$ARGUMENTS` estiver vazio ou incompleto:
- Mostre erro explicativo
- Exemplo de uso correto
- Pare a execução

Extraia `branch_origem` e `branch_destino` de `$ARGUMENTS`.

### 2. Analise as diferenças entre branches

Execute os seguintes comandos em paralelo:

```bash
# Commits entre as branches
git log --oneline --no-merges ${branch_destino}..${branch_origem}

# Estatísticas de arquivos modificados
git diff --stat ${branch_destino}...${branch_origem}

# Lista de arquivos modificados (resumida)
git diff --name-only ${branch_destino}...${branch_origem}

# Verificar se branch_origem existe
git rev-parse --verify ${branch_origem}

# Verificar se branch_destino existe
git rev-parse --verify ${branch_destino}
```

### 3. Extraia informações da branch origem

**Se branch_origem segue padrão** `<ISSUE-CODE>/<type>/<description>`:
- Extraia código da issue (ex: `DANFEIA-164`)
- Extraia tipo (feat, fix, refactor, chore, docs)
- Use para título do PR

**Tipos de PR**:
- **Feature branch → develop**: `[ISSUE-CODE] tipo: descrição`
- **develop → staging**: `merge: develop -> staging`
- **staging → master**: `release: [version] - descrição`

### 4. Gere o conteúdo da descrição

Use o template como base e preencha com informações inteligentes:

**Estrutura**:
```markdown
<!-- Título sugerido: [extraído da análise] -->

## 📋 Resumo

[Resumo baseado nos commits e arquivos modificados]

## 📝 Changelog

[Lista de mudanças principais com checkboxes]

## 🧪 Como Testar

### Pré-requisitos
- [Pré-requisitos identificados nas mudanças]

### Passos para teste
1. [Passos baseados no tipo de mudança]
2.
3.

### Resultado esperado
[Comportamento esperado baseado nas mudanças]

---

### ✅ Checklist
- [ ] Código segue os padrões do projeto
- [ ] Testes foram executados e estão passando
- [ ] Documentação foi atualizada (se necessário)
- [ ] Variáveis de ambiente foram configuradas (se necessário)
- [ ] Migrations foram criadas (se necessário)
```

### 5. Diretrizes para geração

**Resumo**:
- 2-3 parágrafos máximo
- Foco no "O QUE" e "POR QUE"
- Mencione objetivo principal da mudança
- Para merge de branches (develop→staging), resuma features incluídas

**Changelog**:
- Liste mudanças principais (5-10 itens)
- Agrupe por escopo quando possível (api, web, config, tests)
- Use checkboxes `- [ ]`
- Seja específico mas conciso
- Formato: `- [ ] <escopo>: descrição da mudança`

**Como Testar**:
- **Pré-requisitos**: Identifique de arquivos modificados
  - Novos env vars? Liste-os
  - Migrations? Mencione `alembic upgrade head`
  - Dependências? Mencione `pip install` ou `pnpm install`
  
- **Passos para teste**: Baseie-se no tipo de mudança
  - Feature: Como usar a nova funcionalidade
  - Fix: Como reproduzir o bug e validar correção
  - Refactor: Como validar que comportamento não mudou
  
- **Resultado esperado**: Seja claro e objetivo

**Checklist**:
- Mantenha itens padrão do template
- Marque itens óbvios se aplicável (ex: migrations se há arquivo alembic)

### 6. Análise de arquivos modificados

**Identifique automaticamente**:
- **Migrations**: Arquivos em `api/alembic/versions/` → Checklist: migrations
- **Env vars**: Mudanças em `env.example` ou `.env.example` → Pré-requisitos + Checklist
- **Dependências**: Mudanças em `requirements.txt`, `package.json`, `pyproject.toml` → Pré-requisitos
- **Testes**: Arquivos em `tests/` ou `__tests__/` → Mencione em changelog
- **Docs**: Arquivos `.md` → Checklist: documentação
- **Config**: `config.py`, `settings.py` → Mencione env vars

### 7. Exemplos de descrições geradas

**Exemplo 1 - Feature simples**:
```markdown
<!-- Título sugerido: [DANFEIA-164] refactor: torna mensagens de erro 503 configuráveis -->

## 📋 Resumo

Refatora sistema de mensagens de erro HTTP 503 (sobrecarga) para permitir
customização via variáveis de ambiente. Isso facilita ajustes de mensagens
sem precisar alterar código ou fazer deploy.

## 📝 Changelog

- [ ] api: adiciona variáveis OVERLOAD_MESSAGES, OVERLOAD_RETRY_MINUTES/SECONDS
- [ ] api: remove cálculo dinâmico de retry não utilizado
- [ ] config: adiciona validators com fallback para valores padrão
- [ ] tests: adiciona testes unitários em test_config.py (5 casos)
- [ ] tests: valida retry delay no teste de integração
- [ ] docs: documenta novas env vars no env.example

## 🧪 Como Testar

### Pré-requisitos
- [ ] Configurar variáveis no .env local (ou testar valores padrão)

### Passos para teste
1. Defina `MAX_FILES_IN_PROCESSING=0` no .env da API
2. Acesse Swagger em http://localhost:8000/docs
3. Execute endpoint `/api/v2/gcs/generate-signed-urls-batch`
4. Valide resposta 503 com mensagens customizadas no campo `error.messages`
5. Valide `retryDelay.minutes` e `retryDelay.seconds`

### Resultado esperado
Erro 503 retorna mensagens configuráveis e tempo de retry fixo baseado
nas variáveis de ambiente (ou valores padrão se não configuradas).

---

### ✅ Checklist
- [ ] Código segue os padrões do projeto
- [ ] Testes foram executados e estão passando
- [ ] Documentação foi atualizada (env.example)
- [x] Variáveis de ambiente foram configuradas (OVERLOAD_MESSAGES, OVERLOAD_RETRY_*)
- [ ] Migrations foram criadas (não aplicável)
```

**Exemplo 2 - Merge develop → staging**:
```markdown
<!-- Título sugerido: merge: develop -> staging -->

## 📋 Resumo

Merge de develop para staging incluindo 3 features e 2 bug fixes
desenvolvidos nas últimas 2 semanas.

Features principais:
- Configuração de mensagens de erro 503
- Novo endpoint de relatórios mensais
- Integração com sistema de notificações

## 📝 Changelog

- [ ] api: mensagens de erro 503 configuráveis (DANFEIA-164)
- [ ] api: endpoint de relatórios mensais (DANFEIA-170)
- [ ] api: integração com sistema de notificações (DANFEIA-172)
- [ ] api: corrige timeout em processamento em lote (DANFEIA-168)
- [ ] web: corrige validação de datas no formulário (DANFEIA-171)

## 🧪 Como Testar

### Pré-requisitos
- [ ] Database atualizada com migrations
- [ ] Variáveis de ambiente configuradas

### Passos para teste
1. Executar migrations: `cd api && alembic upgrade head`
2. Reiniciar API e Web
3. Testar cada feature listada no changelog
4. Validar que bugs foram corrigidos

### Resultado esperado
Todas as features funcionando corretamente em staging sem regressões.

---

### ✅ Checklist
- [ ] Código segue os padrões do projeto
- [ ] Testes foram executados e estão passando
- [ ] Documentação foi atualizada (se necessário)
- [ ] Variáveis de ambiente foram configuradas (se necessário)
- [ ] Migrations foram criadas (se aplicável)
```

### 8. Escrita do arquivo

**Após gerar o conteúdo**:
1. Escreva em `pr-description.md` na raiz do projeto
2. Confirme para o usuário:
   - Arquivo criado/atualizado
   - Título sugerido para o PR
   - Resumo rápido (1 linha)
   - Próximos passos

### 9. Formato de saída

```markdown
## ✅ Descrição de PR gerada

**Arquivo**: `pr-description.md` (raiz do projeto)

**Título sugerido para o PR**:
```
[título extraído]
```

**Resumo rápido**:
[1 linha resumindo as mudanças]

**Próximos passos**:
1. Revise o conteúdo gerado em `pr-description.md`
2. Ajuste se necessário
3. Crie o PR e copie o conteúdo do arquivo para a descrição

---

**Preview do conteúdo**:
[Primeiras linhas do arquivo gerado]
```

### 10. Validações importantes

**SEMPRE verifique**:
- Branches existem no repositório?
- Há commits entre as branches?
- Arquivos foram modificados?
- Template existe em `.github/pull_request_template.md`?

**NUNCA**:
- Gere descrições genéricas sem contexto
- Liste todos os arquivos modificados (resuma)
- Copie commits literalmente (interprete e agrupe)
- Esqueça de marcar checkboxes relevantes

---

## Tratamento de erros

**Se branch não existe**:
```
❌ Erro: Branch '${branch}' não existe

Branches disponíveis:
[listar branches principais]

Uso correto:
/pr-description <branch_origem> <branch_destino>
```

**Se não há diferenças**:
```
⚠️ Nenhuma diferença encontrada entre '${branch_origem}' e '${branch_destino}'

Possíveis causas:
- Branches já estão sincronizadas
- Branch origem está atrás da destino
- Verifique se as branches estão corretas
```

**Se faltam argumentos**:
```
❌ Erro: Argumentos insuficientes

Uso:
/pr-description <branch_origem> <branch_destino>

Exemplo:
/pr-description DANFEIA-164/refactor/mensagem develop
```
