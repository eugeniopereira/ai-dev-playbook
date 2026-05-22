📎 Apêndice B — Casos Reais (Base de Conhecimento)
Aqui é onde seu time realmente evolui. Cada caso segue um padrão replicável:
Problema → Prompt → Resposta esperada → Solução validada

B.1 Timeout entre microsserviços
Problema
Serviço A chama Serviço B
Timeout intermitente (HTTP 504)
Prompt usado
Você é especialista em microsserviços Java.

Contexto:
- Quarkus
- OpenShift
- Comunicação REST

Problema:
Timeout ao chamar serviço downstream

Logs:
<timeout stacktrace>

Objetivo:
Diagnosticar causa e sugerir solução
Resposta esperada da IA
Possíveis causas:
timeout baixo
latência de rede
pool de conexões esgotado
DNS lento
Sugestões:
aumentar timeout
verificar readiness/liveness
analisar métricas
Solução validada
Ajuste de timeout no client
Aumento do pool de conexões
Identificação de gargalo no serviço B

B.2 NullPointerException em produção
Problema
Erro em método simples, mas não reproduz localmente
Prompt
Analise o stacktrace abaixo e identifique causa raiz.

Stacktrace:
<java.lang.NullPointerException...>

Código:
<trecho>
Resposta esperada
Identificar objeto potencialmente nulo
Sugerir validação defensiva
Solução
Adição de null check
Ajuste no fluxo de dados upstream

B.3 API lenta em produção
Problema
Endpoint com tempo > 5s
Prompt
Você é especialista em performance Java.

Endpoint lento:
<descrição>

Código:
<trecho>

Objetivo:
Identificar gargalos
Resposta esperada
Possíveis gargalos:
query no banco
chamadas externas
processamento síncrono
Solução
Otimização de query
Introdução de cache
Paralelização

B.4 Falha de pod no OpenShift
Problema
Pod reiniciando constantemente (CrashLoopBackOff)
Prompt
Você é especialista em OpenShift.

Problema:
Pod em CrashLoopBackOff

Logs:
<logs>

Objetivo:
Diagnosticar causa
Resposta esperada
Possíveis causas:
erro na inicialização
falta de memória
configuração errada
Solução
Ajuste de memory/CPU
Correção de variável de ambiente
Fix em startup da aplicação

B.5 Erro de integração REST (404/500)
Problema
Chamada REST retornando erro inesperado
Prompt
Analise erro de integração REST.

Request:
<request>

Response:
<response>

Objetivo:
Identificar problema e sugerir correção
Resposta esperada
Problemas possíveis:
endpoint incorreto
contrato divergente
payload inválido
Solução
Correção de path
Ajuste de DTO
Validação de contrato

B.6 Código legado difícil de manter
Problema
Classe com alta complexidade
Prompt
Refatore o código abaixo aplicando clean code.

Código:
<classe grande>
Resposta esperada
Separação de responsabilidades
Redução de complexidade
Solução
Quebra em métodos menores
Introdução de serviços auxiliares

B.7 Falha intermitente em produção
Problema
Erro não determinístico
Prompt
Sistema distribuído com erro intermitente.

Sintoma:
<descrição>

Logs:
<logs>

Objetivo:
Listar hipóteses e validação
Resposta esperada
Lista priorizada de hipóteses
Estratégia de investigação
Solução
Identificação de race condition
Ajuste de sincronização

