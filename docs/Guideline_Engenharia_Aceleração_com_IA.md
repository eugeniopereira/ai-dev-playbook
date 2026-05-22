# Guideline de Uso de IA no Desenvolvimento Java

## Objetivo

Estabelecer um guideline oficial para uso de ferramentas de IA no ciclo de desenvolvimento, garantindo aumento de produtividade com controle de qualidade e previsibilidade.

---

# 1. Escopo

Este guideline define:

* Como utilizar IA no dia a dia de desenvolvimento
* Padrões mínimos obrigatórios
* Boas e más práticas
* Estrutura de evolução contínua

---

# 2. Princípios Fundamentais

## 2.1 IA como ferramenta de engenharia

* IA é um **copiloto técnico**
* Não substitui análise humana

## 2.2 Responsabilidade do desenvolvedor

* Todo código gerado é responsabilidade de quem o utiliza

## 2.3 Determinismo operacional

* Uso deve ser baseado em **prompts estruturados e reproduzíveis**

---

# 3. Fluxo Operacional Obrigatório

## 3.1 Estruturação do problema

Antes de usar IA, o desenvolvedor deve definir:

* Stack (Java 17, Quarkus, Spring, etc.)
* Tipo de problema (bug, melhoria, design)
* Código relevante
* Logs/erros completos
* Objetivo claro

---

## 3.2 Modos de uso permitidos

### 3.2.1 Debug Assistido

Uso para análise de erros e falhas

### 3.2.2 Code Review Assistido

Uso para revisão técnica antes de PR

### 3.2.3 Refatoração

Uso para melhoria de código existente

### 3.2.4 Design / Arquitetura

Uso para comparação de abordagens

---

## 3.3 Validação obrigatória

Nenhum código gerado por IA deve ser utilizado sem validação.

Checklist mínimo:

* [ ] Compila corretamente
* [ ] Não utiliza APIs inexistentes
* [ ] Está aderente ao padrão do projeto
* [ ] Resolve o problema proposto

---

# 4. Templates Oficiais de Prompt

## 4.1 Debug

```
Você é um especialista em Java.

Contexto:
- Framework: <framework>
- Ambiente: <ambiente>

Erro:
<stacktrace>

Código:
<trecho>

Objetivo:
Identificar causa raiz e propor correção objetiva.
```

---

## 4.2 Code Review

```
Analise o código abaixo considerando:
- Boas práticas Java
- Performance
- Concorrência
- Legibilidade

Código:
<trecho>
```

---

## 4.3 Refatoração

```
Refatore o código abaixo para:
- Melhorar legibilidade
- Reduzir complexidade
- Aplicar boas práticas

Código:
<trecho>
```

---

## 4.4 Design

```
Compare abordagens para o seguinte problema:

Problema:
<descrição>

Contexto:
<stack + restrições>

Apresente trade-offs e recomendação.
```

---

# 5. Exemplos Base (Java)

## 5.1 Debug — NullPointerException

### Código

```
public String getUserName(User user) {
    return user.getProfile().getName();
}
```

### Correção esperada

```
public String getUserName(User user) {
    if (user == null || user.getProfile() == null) {
        return null;
    }
    return user.getProfile().getName();
}
```

---

## 5.2 Refatoração

### Antes

```
if (x == 1) {
    if (y == 2) {
        doSomething();
    }
}
```

### Depois

```
if (x == 1 && y == 2) {
    doSomething();
}
```

---

## 5.3 Teste Unitário

```
@Test
void shouldSumCorrectly() {
    Calculator calc = new Calculator();
    assertEquals(5, calc.sum(2, 3));
}
```

---

## 5.4 Cliente REST (Quarkus)

```
@RegisterRestClient
public interface UserClient {

    @GET
    @Path("/users/{id}")
    User getUser(@PathParam("id") String id);
}
```

---

# 6. Boas Práticas

## Obrigatórias

* Fornecer contexto completo
* Utilizar templates
* Validar todas as respostas

## Recomendadas

* Iterar com IA para refinar resposta
* Compartilhar prompts úteis com o time

---

# 7. Más Práticas

* Perguntas vagas
* Uso sem validação
* Copiar código sem entendimento
* Uso para geração de sistemas completos sem revisão

---

# 8. Governança

* Uso de IA é incentivado
* Validação humana é obrigatória
* Código deve seguir padrões internos
* Prompts relevantes devem ser compartilhados

---

# 9. Modelo de Maturidade

## Nível 1 — Inicial

Uso pontual

## Nível 2 — Produtivo

Uso estruturado com templates

## Nível 3 — Avançado

Uso para apoio em decisões técnicas

---

# 10. Evolução do Guideline

Este documento é a base inicial.

Evoluções serão adicionadas como **apêndices**, incluindo:

* Apêndice A — Prompts avançados
* Apêndice B — Casos reais do projeto
* Apêndice C — Padrões específicos da arquitetura interna
* Apêndice D — Uso de IA em troubleshooting distribuído
* Apêndice E — Uso de IA Integrada ao IDE
* Apêndice F — Diferencial do Gemini Code Assist
* Apêndice G — Quadro de Decisão Operacional (Uso de IA)
* Apêndice H — Acoplamento de Templates às Ferramentas de IDE com IA
* Apêndice I — Método Avançado de Engenharia Assistida por IA (Iterativo)
* Apêndice K — Modernização de Legados Assistida por IA (Modelo de Especialização)
* Apêndice L — Engenharia de Conhecimento do Legado Assistida por IA
* Apêndice M — Engenharia da Plataforma de Destino Assistida por IA

---

# Conclusão

O uso disciplinado de IA deve ser tratado como prática de engenharia. O ganho de produtividade depende diretamente da padronização, qualidade dos prompts e validação técnica aplicada.
