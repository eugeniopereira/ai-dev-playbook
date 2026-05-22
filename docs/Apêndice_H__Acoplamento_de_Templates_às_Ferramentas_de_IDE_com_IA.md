📎 Apêndice H — Acoplamento de Templates às Ferramentas de IDE com IA
H.1 Princípio
Template bom não pode depender de copiar/colar manual.
Ele deve estar:
acessível em 1–2 ações
contextual ao código
reutilizável pelo time

H.2 Estratégias (da mais simples à mais madura)

🟢 Nível 1 — Snippets de prompt (baixo esforço, alto impacto)
Funciona muito bem com:
Visual Studio Code
Cursor IDE

Como funciona
Você cria snippets tipo:
debug-java
Que expandem para:
Você é um especialista em Java.

Contexto:
- Framework: Quarkus
- Ambiente: OpenShift

Erro:
$SELECTION

Objetivo:
Identificar causa raiz e propor correção.

Vantagem
rápido
padroniza uso
fácil de versionar

Implementação (VSCode)
Criar:
"IA Debug Java": {
 "prefix": "ia-debug",
 "body": [
   "Você é um especialista em Java.",
   "",
   "Contexto:",
   "- Framework: Quarkus",
   "- Ambiente: OpenShift",
   "",
   "Erro:",
   "$TM_SELECTED_TEXT",
   "",
   "Objetivo:",
   "Identificar causa raiz e propor correção."
 ]
}

🟡 Nível 2 — Prompt Library (time inteiro)
Você cria um repositório interno:
/ai-prompts/
 debug.md
 refactor.md
 troubleshooting.md
E o dev:
abre o arquivo
copia rapidamente
usa no chat da IA

Evolução
No Cursor IDE isso funciona muito bem, porque:
ele lê contexto do projeto
aplica o prompt direto no código

🟠 Nível 3 — Comandos customizados (IDE + extensão)
Aqui começa a ficar interessante.

Exemplo de fluxo
Dev seleciona código
Executa comando:
Ctrl + Shift + P → "IA: Debug Java"
Prompt já vai estruturado para:
Claude
Gemini

Implementação
extensão interna do VSCode (simples)
ou uso de tasks/scripts

🔵 Nível 4 — Integração direta com IA (Cursor / Plugins)
Ferramentas como:
Cursor IDE
plugins de chat no VSCode
Permitem:
👉 criar prompts “fixos” reutilizáveis

Exemplo
No Cursor:
criar prompt salvo:
“Debug padrão Java”
“Refatoração clean code”

🔴 Nível 5 — Automação inteligente (nível avançado)
Aqui você acopla:
template + contexto automático + ferramenta

Exemplo real
Selecionou código + abriu log →
Sistema monta automaticamente:
- stacktrace
- código
- contexto (framework)
E envia para:
Claude ou Gemini

Como fazer
extensão customizada
ou scripts internos
👉 Isso já é nível “plataforma interna de IA”

H.3 Estratégia recomendada para o seu time
Não comece complexo.
Fase 1 (imediata)
snippets no VSCode
biblioteca de prompts

Fase 2 (2–4 semanas)
padronizar prompts
usar Cursor com prompts salvos

Fase 3 (maduro)
criar comandos customizados
integrar com fluxo real

H.4 Integração com ferramentas específicas

✔ GitHub Copilot
não usa bem templates longos
melhor para:
autocomplete
pequenos prompts

✔ Claude
excelente com templates estruturados
ideal para:
debug
análise
design

✔ Gemini Code Assist
bom com contexto + prompts claros
ideal para:
troubleshooting
sistema distribuído

✔ Cursor IDE
melhor integração geral
permite:
prompts reutilizáveis
contexto automático

H.5 Padrão ideal de uso (operacional)
Dev não deve:
❌ abrir chat e pensar “o que escrever”
Deve:
✔ selecionar código
 ✔ usar comando/snippet
 ✔ ajustar contexto
 ✔ executar

H.6 Ganho real
Com templates acoplados:
↓ tempo de escrita de prompt
↓ variabilidade entre devs
↑ qualidade das respostas
↑ velocidade de debug

H.7 Risco
Se fizer mal:
templates viram “engessados”
dev usa sem pensar
👉 solução:
manter templates curtos
permitir adaptação
