# Mentalize

O erro comum ao se utilizar IA como ferramenta de desenvolvimento é tentar “ensinar a ferramenta”. O ganho real vem de **padronizar o uso da IA como parte do fluxo de engenharia**, não como algo ad-hoc.

---

A proposta a seguir, sem ser presunçoso, é uma metodologia operacional, quase como um “playbook de engenharia assistida por IA”.

# 1. Princípio base: IA como *copiloto determinístico*, não como oráculo

Se você não controlar o *input*, a saída será inconsistente.

Então o seu time precisa trabalhar com:

* prompts estruturados
* contexto mínimo obrigatório
* validação sistemática da resposta

Isso transforma IA de “chat” em **ferramenta de engenharia reproduzível**.

---

# 2. Estrutura de uso no dia a dia (workflow)

## 🔹 Etapa 1 — Formulação do problema (obrigatória)

Antes de perguntar à IA, o dev deve estruturar:

```
Contexto:
- Stack (Java 17, Quarkus, Spring, etc.)
- Tipo de problema (bug, performance, design, integração)

Entrada:
- Código relevante
- Erro/log

Saída esperada:
- O que exatamente ele quer (ex: corrigir erro, otimizar, refatorar)
```

👉 Isso sozinho já melhora drasticamente a qualidade.

---

## 🔹 Etapa 2 — Uso dirigido da IA (3 modos)

Padronize 3 tipos de interação:

### 1. Debug assistido

Para erros

Prompt padrão:

> “Analise esse erro considerando Java + [framework]. Explique a causa raiz e proponha correção com código.”

---

### 2. Code review automático

Antes de PR

Prompt:

> “Faça review desse código considerando boas práticas Java, concorrência, performance e legibilidade.”

---

### 3. Design / arquitetura

Para decisões maiores

Prompt:

> “Compare abordagens para [problema], considerando trade-offs em produção.”

---

## 🔹 Etapa 3 — Validação obrigatória

Regra simples para o time:

> “Nada vindo da IA entra no código sem validação humana”

Checklist:

* Compila?
* Faz sentido com o contexto do sistema?
* Não inventou API?
* Não quebrou padrão interno?

---

# 3. Introduzir “templates de prompt” (isso escala muito)

Você pode criar um pequeno catálogo interno:

### Exemplo — Template de bug

```
Você é um especialista em Java.

Contexto:
- Framework: Quarkus
- Ambiente: Docker / OpenShift

Erro:
<stacktrace>

Código:
<trecho>

Objetivo:
Identificar causa raiz e propor correção objetiva.
```

👉 Isso reduz variabilidade entre devs.

---

# 4. Casos de uso que mais geram ganho (priorize esses)

Para um time Java, foque onde ROI é alto:

### ✔ Debug de erro (principal)

Stacktrace + contexto → ganho imediato

### ✔ Refatoração

* transformar código legado
* aplicar clean code
* melhorar legibilidade

### ✔ Testes automatizados

Gerar:

* unit tests
* mocks
* cenários de borda

### ✔ Integrações

* REST clients
* parsing
* configuração de libs

---

# 5. O que NÃO incentivar (importante)

Você precisa evitar esses anti-patterns:

❌ “Gera um sistema completo”
❌ Copiar código sem entender
❌ Usar IA como substituto de debugging real
❌ Perguntas vagas (“não está funcionando”)

---

# 6. Modelo de maturidade do time

Pode-se evoluir o time em 3 níveis:

### 🟢 Nível 1 — Assistido

* usa IA para debug e dúvidas
* ainda dependente

### 🟡 Nível 2 — Produtivo

* usa IA para acelerar tarefas repetitivas
* já estrutura prompts

### 🔵 Nível 3 — Engenheiro com IA

* usa IA para design, análise e decisão
* sabe validar criticamente

👉 O objetivo aqui é levar o time pelo menos até o nível 2.

---

# 7. Como implementar isso na prática (sem fricção)

Sugestão direta:

### Semana 1

* Apresentar os 3 modos de uso
* Mostrar exemplos reais seus

### Semana 2

* Criar templates internos
* Incentivar uso em tarefas reais

### Semana 3+

* Code review passa a aceitar “uso de IA” como parte do processo
* Compartilhar prompts bons entre o time

---

# 8. O papel do líder

Não precisamos que todos virem experts.

O líder deve:

* definir padrão mínimo
* evitar uso caótico
* garantir qualidade

Na prática, o líder vira um **“orquestrador de produtividade assistida”**

---

# 9. Ajuste fino para o contexto

Considerando que já trabalhamos com:

* microsserviços
* APIs
* IA (Gemini, etc.)

Podemos evoluir isso depois para:

* geração de contratos de API
* análise automática de logs
* apoio em troubleshooting distribuído

---
