Apêndice M — Engenharia da Plataforma de Destino Assistida por IA 
M.1 Objetivo
Definir e estruturar a arquitetura alvo antes da migração incremental do legado.

M.2 Novo princípio
O backlog deve migrar para uma plataforma padronizada, não para projetos improvisados.

M.3 Modelo organizacional
Cada perfil contribui em uma camada da plataforma.
Perfil
Ferramenta
Responsabilidade
Arquitetura
Claude
definição de padrões
Plataforma
Gemini
integração sistêmica
Execução
Cursor
implementação base


M.4 O que deve existir antes da migração
Área
Exemplo
Linguagem
Java 21
Framework
Quarkus
Observabilidade
OpenTelemetry
Segurança
OAuth2
Persistência
JPA
CI/CD
GitLab CI
Containers
Docker/OpenShift


M.5 Fluxo recomendado
1. Definir princípios
2. Modelar arquitetura alvo
3. Criar baseline técnico
4. Gerar projeto base
5. Definir padrões obrigatórios
6. Publicar arquitetura de referência

M.6 Etapa 1 — Definir princípios arquiteturais
Ferramenta recomendada
Preferencial:
Claude
Alternativa:
Gemini

Template
Estamos modernizando um sistema legado.

Contexto:
- ambiente OpenShift
- microsserviços
- foco em observabilidade
- segurança corporativa
- manutenção simplificada

Proponha princípios arquiteturais para a plataforma alvo.

M.7 Etapa 2 — Modelagem da arquitetura alvo
Objetivo
Definir:
camadas
padrões
observabilidade
integração
contratos
organização de projetos

Template
Com base nesses princípios:

<princípios>

Proponha:
- arquitetura de referência
- divisão de camadas
- padrões de integração
- padrões de segurança
- observabilidade
- organização de projetos

M.8 Etapa 3 — Baseline técnico
Objetivo
Criar um projeto base reutilizável.

Deve conter
Item
Obrigatório
Logging
✔
Tracing
✔
Metrics
✔
Health checks
✔
Segurança
✔
Tratamento de erro
✔
Dockerfile
✔
Pipeline
✔


M.9 Etapa 4 — Bootstrap assistido
Ferramenta recomendada
Preferencial:
Cursor
Alternativa:
Claude

Template
Gere um projeto base Quarkus Java 21 contendo:

- REST API
- OpenTelemetry
- Health checks
- Dockerfile
- Configuração OpenShift
- Tratamento global de erros
- Estrutura padrão corporativa

M.10 Etapa 5 — Padrões obrigatórios
Obrigatório
DTO separado
exception mapper global
logs estruturados
tracing distribuído
configuração externalizada

Proibido
lógica em controller
SQL hardcoded
configuração fixa
acoplamento entre serviços

M.11 Etapa 6 — Validação arquitetural
Ferramenta recomendada
Preferencial:
Claude
Alternativa:
Gemini

Template
Analise este projeto e valide aderência à arquitetura padrão:

<colar padrões>

Aponte violações e melhorias.

M.12 Estratégia de migração
Fluxo correto
baseline pronta
↓
backlog funcional
↓
histórias
↓
migração incremental

M.13 Anti-patterns
❌ Criar serviços sem baseline
❌ Não padronizar observabilidade
❌ Misturar arquitetura nova e antiga
❌ Não validar aderência arquitetural

M.14 Resultado esperado
Você ganha:
consistência
onboarding mais rápido
menos erro arquitetural
modernização previsível
plataforma sustentável

M.15 Insight final
O objetivo não é apenas reescrever sistemas.
É construir uma plataforma sustentável para evolução futura.
A IA passa a atuar como acelerador organizacional de modernização arquitetural.



