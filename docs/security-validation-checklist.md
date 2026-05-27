# Security Validation Checklist - Código Gerado por IA

**Versão**: 1.0  
**Data**: 27 de maio de 2026  
**Objetivo**: Garantir que código gerado por IA não introduza vulnerabilidades de segurança

---

## 📋 Checklist Obrigatório para Code Review

### Antes de Aprovar PR com Código IA

**Todo código gerado ou assistido por IA DEVE passar por esta validação:**

#### 🔴 Crítico (Bloqueante)

- [ ] **Secrets Detection**
  - Sem API keys, tokens, passwords hard-coded
  - Sem credenciais em comentários ou strings
  - Variáveis sensíveis usando environment variables
  - Verificado com TruffleHog/GitLeaks

- [ ] **Injection Vulnerabilities**
  - SQL queries usando prepared statements (não string concatenation)
  - Inputs do usuário sempre validados e sanitizados
  - Sem `eval()`, `exec()`, ou similar em Python/JavaScript
  - Sem command injection (shell commands com user input)

- [ ] **Authentication & Authorization**
  - Endpoints protegidos com autenticação adequada
  - Validação de permissões antes de operações sensíveis
  - Sem bypass de autenticação (ex: comments como `// TODO: add auth`)
  - JWT/tokens validados corretamente

- [ ] **Data Exposure**
  - Sem logging de dados sensíveis (PII, credentials)
  - Responses de API não expõem informações internas
  - Stack traces não vazam para produção
  - Sem informações de debug em produção

#### 🟡 Alto (Importante)

- [ ] **Error Handling**
  - Erros tratados adequadamente (sem bare `except:` em Python)
  - Mensagens de erro não revelam detalhes do sistema
  - Fallbacks seguros em caso de falha
  - Logging de erros sem expor dados sensíveis

- [ ] **Input Validation**
  - Todos os inputs validados (tipo, tamanho, formato)
  - Whitelist preferível a blacklist
  - Validação tanto no frontend quanto backend
  - Sem confiança cega em dados externos

- [ ] **Path Traversal**
  - File paths validados (sem `../` ou absolute paths não sanitizados)
  - Upload de arquivos restrito a tipos permitidos
  - File operations com permissões adequadas
  - Sem acesso direto a filesystem baseado em user input

- [ ] **CORS & Headers**
  - CORS configurado corretamente (não `*` em produção)
  - Security headers presentes (CSP, X-Frame-Options, etc.)
  - Cookies com flags adequados (HttpOnly, Secure, SameSite)

#### 🟢 Médio (Recomendado)

- [ ] **Dependencies**
  - Bibliotecas sem vulnerabilidades conhecidas (CVE check)
  - Versões atualizadas e mantidas
  - Licenças compatíveis com projeto
  - Sem dependências desnecessárias

- [ ] **Code Quality**
  - Complexidade ciclomática <= 15 por função
  - Sem código duplicado extensivamente
  - Funções com responsabilidade única
  - Nomes descritivos (não genéricos gerados por IA)

- [ ] **Testing**
  - Unit tests para lógica crítica
  - Security test cases (negative tests)
  - Edge cases cobertos
  - Cobertura >= 80% para código novo

---

## 🚨 Red Flags - Parar Imediatamente

**Se encontrar qualquer um desses, REJEITAR PR e escalar:**

### 🔴 Gravíssimo

```python
# ❌ NUNCA ACEITAR
password = "admin123"  # Hard-coded credential
api_key = "sk-abc123..."  # API key exposta

# ❌ SQL Injection
query = f"SELECT * FROM users WHERE id = {user_input}"

# ❌ Command Injection  
os.system(f"rm -rf {user_provided_path}")

# ❌ Path Traversal
open(f"/var/data/{user_file_name}")  # sem validação

# ❌ Eval/Exec
eval(user_input)  # Arbitrary code execution
```

### 🟡 Muito Suspeito

```python
# ⚠️ Revisar com atenção
try:
    dangerous_operation()
except:
    pass  # Bare except silenciando tudo

# ⚠️ Authentication bypass
# if user.is_authenticated():  # Comentado "temporariamente"
process_sensitive_data()

# ⚠️ Logging sensível
logger.info(f"User {username} logged in with password {password}")

# ⚠️ CORS permissivo
@app.route('/api/data')
@cross_origin(origins="*")  # Aceita qualquer origem
```

### 🟢 Atenção

```python
# ⚠️ Pode ser OK mas validar
import pickle  # Deserialization risk
import yaml.unsafe_load  # YAML bomb risk

# Regex complexo (DoS potential)
re.match(r'(a+)+', user_input)

# Sem rate limiting em endpoint público
@app.route('/api/expensive-operation')
def expensive():
    # Pode ser abusado
```

---

## 🔍 Como Validar na Prática

### 1. Automated Checks (CI/CD)

```bash
# Deve rodar automaticamente no PR
✅ TruffleHog (secrets)
✅ Semgrep (SAST)
✅ GitLeaks (credentials)
✅ Dependency scanning
```

**Se falhar**: Não prosseguir até corrigir

### 2. Manual Review (Code Reviewer)

**Tempo estimado**: 5-10 minutos extras por PR com IA

**Foco em**:
1. Lógica de autenticação/autorização
2. Tratamento de inputs externos
3. Queries de banco de dados
4. File operations
5. Logging/error handling

**Perguntas chave**:
- [ ] "O que acontece se input for malicioso?"
- [ ] "Esse endpoint precisa de auth?"
- [ ] "Dados sensíveis estão sendo expostos?"
- [ ] "Erro aqui pode vazar informação?"

### 3. Security Champion Review (Código crítico)

**Quando necessário**:
- Mudanças em autenticação/autorização
- Novos endpoints de API pública
- Operações com dados sensíveis (PII, financeiro)
- Integrações com serviços externos

**Processo**:
1. Tag Security Champion no PR
2. Review focado em segurança
3. Aprovação explícita antes de merge

---

## 📊 Tracking de Issues

### Se Encontrar Vulnerabilidade

**1. Classificar Severidade**

| Severidade | Critério | Exemplo |
|------------|----------|---------|
| **Critical** | Exploração direta, acesso não autorizado | Hard-coded admin password |
| **High** | Risco alto de exploração, impacto significativo | SQL injection em endpoint público |
| **Medium** | Exploração difícil ou impacto limitado | Logging de dados não sensíveis |
| **Low** | Teórico ou impacto mínimo | Complexity alta, sem risco direto |

**2. Reportar**

```markdown
## 🚨 Security Issue Found

**Severidade**: [Critical/High/Medium/Low]

**Tipo**: [SQL Injection / Hard-coded Secret / etc]

**Localização**: 
- Arquivo: `path/to/file.py`
- Linha: 42

**Descrição**:
[O que está errado]

**Impacto**:
[O que pode acontecer]

**Correção Sugerida**:
[Como corrigir]

**Prazo**: 
- Critical: 24h
- High: 3 dias
- Medium: 1 semana
- Low: Próximo sprint
```

**3. Escalar se Necessário**

- **Critical/High**: Notificar Tech Lead + Security Champion imediatamente
- **Medium/Low**: Criar issue e trackear normalmente

---

## 🎓 Training Resources

### Para Revisar Código IA

**Leitura obrigatória** (30 min):
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [Common Weakness Enumeration (CWE) Top 25](https://cwe.mitre.org/top25/)

**Hands-on** (1 hora):
- [OWASP WebGoat](https://owasp.org/www-project-webgoat/) - Prática de vulnerabilidades

**Reference**:
- Apêndice A - Prompts Avançados (seção Security)
- Este checklist (bookmark!)

### Casos Reais Internos

**Manter atualizado com exemplos encontrados:**

#### Caso 1: [Data] - Hard-coded API Key
- **O que**: Claude Code gerou `api_key = "sk-..."`
- **Detecção**: TruffleHog no CI/CD
- **Impacto**: Bloqueado antes de merge ✅
- **Lição**: Sempre validar variáveis de ambiente

[Adicionar novos casos conforme encontrados]

---

## ✅ Approval Checklist

**Antes de aprovar PR com código IA:**

```markdown
## Security Review - PR #XXX

Reviewer: [seu nome]
Data: [data]

### Automated Checks
- [ ] CI/CD security scan passou
- [ ] Sem vulnerabilidades críticas/high
- [ ] Dependency check OK

### Manual Review
- [ ] Checklist de segurança aplicado
- [ ] Nenhum red flag encontrado
- [ ] Inputs validados adequadamente
- [ ] Autenticação/autorização correta
- [ ] Sem exposição de dados sensíveis

### Testing
- [ ] Security test cases existem
- [ ] Negative tests incluídos
- [ ] Cobertura >= 80%

### Decision
- [x] ✅ Aprovado para merge
- [ ] ⚠️ Aprovado com ressalvas (comentar)
- [ ] ❌ Mudanças necessárias

Comentários adicionais:
[se houver]
```

---

## 🔄 Processo de Exception

**Quando permitido pular checklist:**

### Cenários Válidos
1. **Protótipo em branch temporária** (não vai para produção)
2. **Código de teste** (não executado em prod)
3. **Documentação/Markdown** (sem código executável)

### Processo de Exceção

```markdown
1. Abrir issue: "Security Exception Request - [motivo]"
2. Justificativa técnica detalhada
3. Aprovação de 2 tech leads
4. Prazo para regularização (max 1 sprint)
5. Tag no PR: `security-exception`
6. Tracking até resolução
```

**Nunca permitido**:
- ❌ Código em produção
- ❌ Endpoints públicos
- ❌ Operações com dados sensíveis

---

## 📈 Métricas

**Tracking mensal (para melhoria contínua):**

```markdown
## Security Metrics - [Mês/Ano]

### Vulnerabilities Found
- Critical: X
- High: Y
- Medium: Z
- Low: W

### By Source
- AI-generated code: X%
- Traditional code: Y%

### Detection
- Automated (CI/CD): X%
- Manual review: Y%
- Production (FAIL): Z% (target: 0%)

### Resolution Time
- Median: X hours
- p95: Y hours
- Target: < 24h for Critical

### False Positives
- Rate: X% (target: < 5%)
- Top causes: [lista]
```

---

## 🔧 Troubleshooting

### "Security scan está bloqueando tudo!"

**Problema**: Muitos falsos positivos  
**Solução**:
1. Revisar regras do Semgrep
2. Adicionar exceções documentadas (`.semgrep.yml`)
3. Ajustar sensitivity do TruffleHog
4. Documentar padrões legítimos

### "Não sei se isso é vulnerabilidade"

**Solução**:
1. Consultar [CWE Database](https://cwe.mitre.org/)
2. Perguntar no #security-champions
3. Quando em dúvida, escalar (melhor safe que sorry)

### "Correção vai quebrar funcionalidade"

**Solução**:
1. Não é trade-off - segurança não é negociável
2. Encontrar solução que seja segura E funcional
3. Se necessário, pair programming com Security Champion
4. Nunca: "vamos aceitar por enquanto"

---

## 📞 Contatos

**Security Champion**: [nome] - Slack: @security-champion  
**Tech Lead**: [nome] - Slack: @tech-lead  
**Canal**: #security-issues  

**Emergência de segurança**: [processo de incident response]

---

## 🔄 Review deste Checklist

**Frequência**: Mensal  
**Owner**: Security Champion  
**Processo**:
1. Revisar casos encontrados no mês
2. Atualizar red flags se necessário
3. Adicionar novos exemplos
4. Socializar mudanças com time

**Última revisão**: 27/05/2026  
**Próxima revisão**: 27/06/2026  
**Versão**: 1.0
