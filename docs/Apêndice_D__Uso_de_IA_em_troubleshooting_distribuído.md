📎 Apêndice D — Uso de IA em Troubleshooting Distribuído
Esse é o ponto onde seu time começa a operar próximo de um modelo de engenharia de produção (SRE-like) com apoio de IA.

D.1 Princípio central
IA não resolve incidente — ela acelera diagnóstico estruturado.
Objetivo:
reduzir MTTR (Mean Time to Resolution)
padronizar investigação
evitar tentativa/erro desorganizada

D.2 Fluxo padrão de troubleshooting com IA
Etapa 1 — Classificação do problema
Sempre identificar:
Tipo:
❗ erro funcional
⚠️ degradação (lento)
💥 indisponibilidade
Escopo:
serviço único
integração
sistema inteiro

Etapa 2 — Coleta mínima obrigatória
Antes de acionar IA:
logs relevantes
endpoint afetado
timestamp
ambiente (pod, namespace, etc.)
mudanças recentes (deploy)

Etapa 3 — Uso da IA (modo diagnóstico)

D.3 Prompt padrão de incidente
Você é um engenheiro de produção especialista em sistemas distribuídos.

Contexto:
- Java 17 + Quarkus
- OpenShift/Kubernetes
- Microsserviços

Problema:
<descrição objetiva>

Sintomas:
<erros, lentidão, etc.>

Logs:
<logs relevantes>

Objetivo:
1. Levantar hipóteses priorizadas
2. Sugerir como validar cada hipótese
3. Indicar ações imediatas (mitigação)

D.4 Diagnóstico por categoria
D.4.1 Timeout / Latência
Prompt:
Problema: Timeout entre serviços

Objetivo:
- Identificar causa (rede, serviço downstream, pool, DNS)
- Sugerir validação prática
Checklist que a IA deve sugerir:
latência de rede
health do serviço downstream
uso de CPU/memória
timeout configurado

D.4.2 Pod instável (CrashLoopBackOff)
Problema: Pod reiniciando

Logs:
<logs>

Objetivo:
Diagnosticar causa raiz e sugerir correção
Possíveis causas:
erro de startup
config inválida
falta de memória

D.4.3 Erro intermitente
Erro ocorre de forma não determinística.

Objetivo:
- Listar hipóteses priorizadas
- Estratégia de investigação
IA deve apontar:
race condition
concorrência
dependência externa instável

D.4.4 Degradação de performance
API ficou lenta em produção.

Objetivo:
- Identificar gargalos
- Sugerir métricas e investigação

D.5 Uso da IA para investigação guiada
Aqui está o salto de maturidade:
👉 não usar IA uma vez — usar em loop
Exemplo:
IA sugere hipóteses
Dev coleta novos dados
Reenvia para IA
Refina diagnóstico
Isso simula um processo de investigação assistida

D.6 Integração com comandos reais (OpenShift)
Você pode evoluir para isso:
Prompt:
Com base no problema abaixo, sugira comandos `oc` para diagnóstico.

Problema:
<descrição>

Objetivo:
Investigar no OpenShift
Saída esperada:
oc logs
oc describe pod
oc get events
oc top pod

D.7 Mitigação vs Correção
A IA deve sempre separar:
Mitigação (curto prazo)
restart de pod
aumentar timeout
rollback
Correção (longo prazo)
corrigir código
ajustar arquitetura
otimizar recurso

D.8 Padrão de registro de incidente (para Apêndice B)
Cada incidente deve gerar:
- Problema
- Impacto
- Prompt usado
- Hipóteses levantadas
- Solução aplicada
- Lições aprendidas
👉 Isso alimenta continuamente sua base de conhecimento

D.9 Anti-patterns críticos
❌ Usar IA sem logs
 ❌ Pedir solução sem contexto
 ❌ Confiar na primeira resposta
 ❌ Não validar hipótese sugerida

D.10 Resultado esperado
Com esse modelo:
troubleshooting vira processo estruturado
IA vira “analista de suporte nível 3”
redução forte de tempo de diagnóstico
aumento da maturidade do time

Quando a ferramenta voltar, eu gero o PDF do Apêndice C imedi

