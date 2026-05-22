📎 Apêndice I — Método Avançado de Engenharia Assistida por IA (Iterativo)
I.1 Objetivo
Padronizar o uso avançado de IA no desenvolvimento, transformando interações ad-hoc em um processo iterativo, controlado e reproduzível.
Este método é especialmente eficaz com ferramentas como:
Claude
Visual Studio Code (terminal/chat)
Cursor IDE

I.2 Princípio central
IA não deve gerar soluções completas — deve participar de um ciclo iterativo de engenharia.

I.3 Visão geral do método
O fluxo é dividido em 4 etapas:
1. Contexto estruturado
2. Planejamento detalhado
3. Refinamento técnico
4. Execução incremental

I.4 Etapa 1 — Contexto estruturado (evolução do /init)
Problema do /init padrão
visão superficial
não captura decisões arquiteturais
não reutilizável

Abordagem correta
Criar um contexto persistente:
Template
Analise este projeto e identifique:

1. Arquitetura predominante
2. Frameworks e bibliotecas principais
3. Padrões de:
  - tratamento de erro
  - persistência
  - integração externa
4. Convenções relevantes

Gere um resumo prático para desenvolvimento.

Uso prático
executar 1x por projeto
salvar como:
/docs/ai-context.md
👉 Esse arquivo vira base para todas as interações futuras

I.5 Etapa 2 — Planejamento estruturado
Problema do modelo comum
Plano genérico e pouco acionável

Template avançado
Seja um dev fullstack senior.

Contexto do projeto:
<colar ai-context.md>

Tarefa:
<descrição do Jira>

Logs:
<se houver>

Objetivo:
1. Quebrar a solução em passos técnicos pequenos
2. Identar dependências entre passos
3. Identificar riscos
4. Estimar esforço (baixo/médio/alto)

Resultado esperado
plano granular
pronto para execução
com riscos explícitos

I.6 Etapa 3 — Refinamento técnico (crítico)
Por que isso existe?
Evitar:
overengineering
soluções erradas bem escritas
desalinhamento com o projeto

Template
Revise o plano proposto considerando:

- padrões do projeto
- simplicidade da solução
- possíveis falhas

Ajuste para ser mais direto e seguro.

Insight
Esse passo transforma IA de “criadora de plano” em “revisora técnica”

I.7 Etapa 4 — Execução incremental
Problema comum
Dev pede implementação completa → perde controle

Abordagem correta
Executar passo a passo

Template
Implemente apenas o passo X do plano:

<descrição do passo>

Respeitando:
- padrões do projeto
- boas práticas

Benefício
controle total
fácil validação
menor risco

I.8 Fluxo completo (resumo)
/init avançado → contexto persistente
↓
planejamento estruturado
↓
refinamento técnico
↓
execução por etapas

I.9 Templates prontos para IDE
I.9.1 Snippet — Planejamento
{
 "IA Plan Task": {
   "prefix": "ia-plan",
   "body": [
     "Seja um dev fullstack senior.",
     "",
     "Contexto do projeto:",
     "${1:colar contexto}",
     "",
     "Tarefa:",
     "${2:descrição}",
     "",
     "Logs:",
     "$TM_SELECTED_TEXT",
     "",
     "Objetivo:",
     "1. Quebrar em passos técnicos",
     "2. Identar dependências",
     "3. Identificar riscos",
     "4. Estimar esforço"
   ]
 }
}

I.9.2 Snippet — Refinamento
{
 "IA Refine Plan": {
   "prefix": "ia-refine",
   "body": [
     "Revise o plano abaixo considerando:",
     "- padrões do projeto",
     "- simplicidade",
     "- possíveis falhas",
     "",
     "Plano:",
     "$TM_SELECTED_TEXT"
   ]
 }
}

I.9.3 Snippet — Execução
{
 "IA Execute Step": {
   "prefix": "ia-exec",
   "body": [
     "Implemente o passo abaixo:",
     "",
     "$TM_SELECTED_TEXT",
     "",
     "Respeitando padrões do projeto."
   ]
 }
}

I.10 Uso no dia a dia (exemplo real)
Cenário
Bug com stacktrace

Fluxo
Seleciona log → ia-plan
Gera plano
Seleciona plano → ia-refine
Seleciona passo → ia-exec
👉 Tudo dentro do IDE

I.11 Anti-patterns
❌ Pular o refinamento
❌ Executar tudo de uma vez
❌ Não usar contexto do projeto
❌ Confiar no primeiro plano

I.12 Evolução futura
Esse método pode evoluir para:
comandos automatizados (VSCode extension)
integração com Jira
geração automática de contexto

I.13 Conclusão
Esse método transforma o uso de IA:
De:
interação pontual
Para:
processo estruturado de engenharia

