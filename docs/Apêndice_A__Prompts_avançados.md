📎 Apêndice A — Prompts Avançados
A.1 Debug de microsserviços (timeout / integração)
Use quando houver falha entre serviços.
Você é um especialista em troubleshooting de microsserviços Java.

Contexto:
- Stack: Java 17 + Quarkus
- Ambiente: OpenShift / Kubernetes
- Comunicação: REST

Problema:
<descreva erro ou timeout>

Logs:
<cole logs relevantes>

Objetivo:
1. Identificar possíveis causas (rede, DNS, timeout, pool, etc.)
2. Sugerir passos de diagnóstico
3. Propor correções práticas

A.2 Análise de erro intermitente (produção)
Atue como engenheiro de produção experiente.

Contexto:
- Sistema distribuído
- Erro ocorre de forma intermitente

Sintoma:
<descrição>

Logs:
<trechos>

Objetivo:
- Listar hipóteses priorizadas
- Indicar como validar cada hipótese
- Sugerir mitigação imediata

A.3 Análise de performance (API lenta)
Você é especialista em performance Java.

Contexto:
- API REST
- Ambiente containerizado

Problema:
<endpoint lento>

Código:
<trecho>

Objetivo:
- Identificar gargalos
- Sugerir otimizações (CPU, I/O, banco, threads)
- Indicar métricas para validação

A.4 Refatoração orientada a padrão (Clean Code)
Refatore o código abaixo aplicando:
- Clean Code
- Baixo acoplamento
- Alta coesão

Código:
<trecho>

Explique as decisões tomadas.

A.5 Geração de testes com cobertura real
Gere testes unitários para o código abaixo considerando:
- Casos de sucesso
- Casos de erro
- Casos de borda

Framework: JUnit 5

Código:
<classe>

A.6 Cliente REST resiliente (Quarkus)
Você é especialista em Quarkus.

Objetivo:
Criar um cliente REST resiliente com:
- Timeout
- Retry
- Tratamento de erro

Endpoint:
<descrição>

Gerar código completo e explicar configurações.

A.7 Troubleshooting OpenShift / Kubernetes
Você é especialista em Kubernetes/OpenShift.

Problema:
<ex: pod reiniciando, erro 503, etc.>

Informações:
- Logs
- Status do pod
- Configurações relevantes

Objetivo:
- Diagnosticar causa
- Sugerir comandos (kubectl/oc)
- Propor solução

A.8 Análise de stacktrace profundo
Analise o stacktrace abaixo em profundidade.

Stacktrace:
<stacktrace>

Objetivo:
- Explicar causa raiz (não só o erro superficial)
- Identificar ponto exato do código
- Sugerir correção

A.9 Comparação arquitetural
Compare duas abordagens para o problema abaixo:

Problema:
<descrição>

Opção A:
<descrição>

Opção B:
<descrição>

Avaliar:
- Complexidade
- Escalabilidade
- Manutenção
- Riscos

Indicar recomendação final.

A.10 Revisão de código focada em produção
Faça uma revisão de código com foco em produção:

Critérios:
- Robustez
- Tratamento de erro
- Observabilidade
- Performance

Código:
<trecho>

