---
name: commit-message
description: Gera mensagem de commit baseada nas mudanças staged seguindo convenções do projeto
user-invocable: true
---

# Commit Message - Gerador de Mensagens de Commit

Analisa mudanças staged e gera mensagem de commit seguindo convenções do projeto Danfe AI.

## Uso

```bash
/commit-message
```

Sem argumentos - analisa automaticamente as mudanças staged e a branch atual.

## Exemplos

```bash
# Gerar mensagem para mudanças staged
/commit-message

# Depois de revisar a mensagem gerada, pode commitar com:
# git commit -m "mensagem gerada"
```

---

## Prompt de Execução

Você é um desenvolvedor sênior especializado em criar mensagens de commit claras e descritivas.

### 1. Analise o estado atual do git

Execute os seguintes comandos em paralelo:
- `git branch --show-current` - Para extrair código da issue e tipo
- `git status --short` - Para ver arquivos staged
- `git diff --cached` - Para ver mudanças staged em detalhe
- `git log -1 --oneline` - Para ver estilo do último commit

### 2. Extraia informações da branch

**Formato esperado**: `<ISSUE-CODE>/<type>/<description>`

Exemplos:
- `DANFEAI-164/refactor/mensagem-de-retorno-no-bloqueio`
- `DANFEAI-26/feat/autenticacao-google`
- `DANFEAI-27/fix/validacao-cpf`

**Tipos válidos**:
- `feat`: Nova funcionalidade
- `fix`: Correção de bug
- `refactor`: Refatoração de código
- `chore`: Tarefas rotineiras (atualizações de dependências)
- `docs`: Mudanças em documentação

### 3. Analise as mudanças

**Identifique**:
- Escopo principal (api, web, worker, agent, config, tests, etc)
- Natureza da mudança (o que foi feito)
- Propósito da mudança (por que foi feito)
- Arquivos críticos modificados

**Diretrizes de análise**:
- Foque no "WHY" e no "WHAT", não no "HOW"
- Mudanças em múltiplos escopos devem ser descritas no body
- Se há apenas mudanças triviais (formatação), mencione explicitamente
- Para refactoring, mencione o objetivo (performance, legibilidade, etc)

### 4. Gere a mensagem de commit

**Formato**:
```
<type>(<scope>): <description>

[body opcional - detalhes adicionais se necessário]
[body opcional - múltiplas linhas se mudanças complexas]

Gerado com assistência de: <Claude/Copilot/Gemini/etc>
Validação: <security scan status, peer reviews>

[ISSUE-CODE se extraído da branch]
Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>
```

**Regras para a primeira linha** (`<type>(<scope>): <description>`):
- Máximo 72 caracteres
- `type` deve ser um dos tipos válidos (feat, fix, refactor, chore, docs)
- `scope` é opcional, use quando aplicável (api, web, config, tests, etc)
- `description` em português, imperativo, minúsculo, sem ponto final
- Seja específico mas conciso

**Regras para o body** (opcional):
- Use quando precisar explicar contexto adicional
- Explique O QUE e POR QUE, não como
- Pode ter múltiplas linhas
- Deixe linha em branco antes do footer

**Regras para o footer**:
- **IMPORTANTE**: Se código foi gerado/assistido por IA, inclua linha:
  `Gerado com assistência de: [Claude/Copilot/Gemini]`
- **IMPORTANTE**: Inclua status de validação:
  `Validação: Security scan passed, 2 peer reviews`
- Sempre inclua `Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>`
- Se branch tem código de issue (ex: DANFEAI-164), inclua antes do Co-Authored-By
- Formato do issue: `[ISSUE-CODE]` ou `Refs: ISSUE-CODE`

### 5. Exemplos de mensagens bem formatadas

**Exemplo 1 - Feature simples**:
```
feat(api): adiciona endpoint para gerar URLs assinadas em lote

Gerado com assistência de: Claude Code
Validação: Security scan passed, 2 peer reviews

DANFEAI-123
Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>
```

**Exemplo 2 - Refactoring com contexto**:
```
refactor(api): torna mensagens de erro 503 configuráveis via env vars

Adiciona variáveis OVERLOAD_MESSAGES, OVERLOAD_RETRY_MINUTES e
OVERLOAD_RETRY_SECONDS para permitir customização das mensagens
de sobrecarga sem precisar alterar código.

Remove cálculo dinâmico de retry que não era mais utilizado.

Gerado com assistência de: Claude Code
Validação: Security scan passed, SonarQube quality gate OK, 2 peer reviews

DANFEAI-164
Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>
```

**Exemplo 3 - Fix de bug**:
```
fix(api): corrige validação de CPF em formulário de cadastro

Adiciona regex correto para validar formato XX.XXX.XXX-XX
e verificação de dígitos verificadores.

DANFEAI-27
Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>
```

**Exemplo 4 - Chore**:
```
chore(api): atualiza dependências de segurança

Atualiza SQLAlchemy 2.0.23 -> 2.0.25 e Pydantic 2.5.0 -> 2.6.1
para corrigir vulnerabilidades reportadas pelo Dependabot.

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>
```

**Exemplo 5 - Docs**:
```
docs(api): adiciona documentação de variáveis de ambiente

Documenta OVERLOAD_MESSAGES e retry configs no env.example
com exemplos de uso e valores padrão.

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>
```

### 6. Formato de saída

Apresente a mensagem gerada da seguinte forma:

```markdown
## 📝 Mensagem de commit sugerida

\`\`\`
[mensagem completa aqui]
\`\`\`

---

**Resumo das mudanças**:
- [Lista de arquivos/mudanças principais]

**Para commitar**:
\`\`\`bash
git commit -m "$(cat <<'EOF'
[mensagem completa aqui]
EOF
)"
\`\`\`
```

### 7. Validações importantes

**SEMPRE verifique**:
- Há mudanças staged? Se não, avise o usuário
- A mensagem não ultrapassa 72 caracteres na primeira linha?
- O tipo é válido (feat, fix, refactor, chore, docs)?
- Está em português (exceto palavras técnicas)?
- Inclui Co-Authored-By?
- Se há código de issue na branch, está incluído no footer?

**NUNCA**:
- Gere mensagens genéricas ("atualiza código", "faz mudanças")
- Use gerúndio ("atualizando", "fazendo")
- Coloque ponto final na primeira linha
- Escreva mensagens muito longas sem body
- Esqueça o Co-Authored-By

---

## Anti-patterns a evitar

❌ `update: changes stuff` (muito genérico, em inglês)
❌ `feat: atualizando o endpoint.` (gerúndio, ponto final)
❌ `refactor(api): refatora o código do endpoint de GCS para melhorar a organização` (> 72 chars)
❌ Mensagem sem Co-Authored-By
❌ Mensagem sem contexto quando há refactoring complexo

✅ `feat(api): adiciona suporte a upload em lote`
✅ `refactor(config): torna mensagens de erro configuráveis`
✅ `fix(auth): corrige validação de token expirado`
