---
name: step
description: Executa um passo específico do plano de implementação
---

# Step - Executor de Passo do Plano

Implementa um passo individual do plano de implementação de forma focada e controlada.

## Uso

```bash
/step <número_ou_letra> "<descrição_do_passo>" [<app>]
```

**Parâmetros:**
- `<número_ou_letra>`: Identificador do passo (1, 2, 3... ou A, B, C...)
- `<descrição_do_passo>`: Descrição completa do que deve ser feito neste passo
- `<app>` (opcional): api, web, worker ou agent (para carregar contextos específicos)

## Exemplos

```bash
# Com número
/step 1 "Criar migration para adicionar campo analise_llm na tabela danfe_processamento" api

# Com letra
/step A "Implementar função de validação de CNPJ no utils" api

# Sem especificar app (infere do contexto)
/step 3 "Adicionar testes unitários para o endpoint de callback"

# Passo com sub-tarefas
/step 2 "Atualizar DanfeProcessor: adicionar validação de duplicidade por chave NFe antes do processamento"
```

---

## Prompt de Execução

Ao receber os parâmetros, execute:

1. **Identifique o passo** do primeiro argumento (número ou letra)

2. **Identifique a aplicação** (do terceiro argumento ou infira do contexto/descrição)

3. **Carregue os contextos relevantes:**
   - `CLAUDE.md` (raiz)
   - `{app}/CLAUDE.md` (se existir)
   - `{app}/docs/ai-context.md` (se existir)

4. **Execute o prompt:**

---

Seja um desenvolvedor sênior focado e disciplinado.

**Contextos do projeto carregados:**
- CLAUDE.md (raiz)
- {app-specific CLAUDE.md se existir}
- {ai-context.md se existir}

**Passo a implementar:** {número_ou_letra}

**Descrição do passo:**
{descrição_do_passo}

---

**IMPORTANTE - Regras de Execução:**

1. **Implemente APENAS o passo solicitado**
   - Não faça refatorações extras
   - Não adicione features não mencionadas
   - Não "melhore" código não relacionado
   - Foque exclusivamente no escopo deste passo

2. **Respeitando padrões do projeto:**
   - Siga convenções de código estabelecidas (CLAUDE.md)
   - Use as ferramentas e bibliotecas do stack atual
   - Mantenha consistência com código existente
   - Respeite estrutura de pastas e nomenclatura

3. **Aplicando boas práticas:**
   - Type hints em Python, TypeScript strict
   - Tratamento de erros apropriado
   - Logging estruturado
   - Validação de entrada
   - Código limpo e legível
   - Comentários apenas quando necessário (WHY, não WHAT)

4. **Validação e testes:**
   - Se o passo mencionar testes, implemente-os
   - Se for código de produção, garanta que está testável
   - Execute testes existentes se aplicável

5. **Não assuma contexto externo:**
   - Use apenas informações da descrição do passo
   - Se precisar de informações de outros passos, pergunte
   - Não "adivinhe" decisões de design não especificadas

---

**Formato de execução esperado:**

1. **Confirme o entendimento**
   ```
   Vou implementar o passo {X}: {resumo_curto}
   Arquivos a serem modificados: [lista]
   ```

2. **Implemente o passo**
   - Use as ferramentas apropriadas (Edit, Write, Bash)
   - Faça uma mudança atômica e completa
   - Execute testes se aplicável

3. **Reporte conclusão**
   ```
   ✅ Passo {X} concluído
   
   Mudanças:
   - [arquivo]: [o que foi feito]
   
   Próximo passo sugerido: [passo X+1 se houver no plano]
   ```

---

**Anti-patterns a evitar:**
- ❌ Implementar múltiplos passos de uma vez
- ❌ Refatorar código não relacionado ao passo
- ❌ Adicionar abstrações não solicitadas
- ❌ Criar arquivos de documentação não pedidos
- ❌ "Melhorar" sem ser solicitado

---
