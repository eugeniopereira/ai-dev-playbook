Apêndice K — Modernização de Legados Assistida por IA (Modelo de Especialização)
K.1 Objetivo
Padronizar upgrades de aplicações legadas utilizando IA para:
reduzir risco
acelerar análise
mapear impacto
automatizar parte da migração
distribuir responsabilidades conforme o perfil da ferramenta utilizada

K.2 Modelo de especialização
Perfil
Ferramenta Principal
Responsabilidade
Engenharia / arquitetura
Claude
entendimento profundo e planejamento
Execução e refatoração
Cursor
implementação e modernização incremental
Plataforma / cloud / distribuído
Gemini Code Assist
análise sistêmica e integração


K.3 Problema clássico do legado
Erro comum:
Atualizar biblioteca → corrigir compilação → subir em produção
Isso ignora:
comportamento
integração
impacto indireto
breaking changes
riscos arquiteturais

K.4 Princípio técnico
IA deve ajudar primeiro a ENTENDER o legado, depois MODERNIZAR.

K.5 Fluxo recomendado
1. Inventário
2. Análise de risco
3. Planejamento incremental
4. Modernização controlada
5. Validação

K.6 Etapa 1 — Inventário assistido
Ferramenta recomendada
Preferencial:
Claude
Alternativa:
Gemini Code Assist

Objetivo
Mapear:
frameworks
dependências
padrões antigos
riscos
integrações
acoplamentos

Template
Analise este projeto Java legado e identifique:

1. Frameworks utilizados
2. Dependências antigas
3. Possíveis riscos de upgrade
4. Acoplamentos fortes
5. Padrões obsoletos
6. Áreas críticas do sistema

Gere um resumo técnico estruturado.

K.7 Etapa 2 — Análise de vulnerabilidade e impacto
Ferramenta recomendada
Preferencial:
Gemini Code Assist
Alternativa:
Claude

Ferramentas complementares
OWASP Dependency Check
Snyk
Dependabot

Objetivo
Transformar CVEs em impacto técnico real.

Template
Estamos atualizando:

<lib atual> → <lib nova>

Contexto:
<frameworks>

Analise:
- breaking changes
- impactos indiretos
- pontos de atenção
- estratégia segura

K.8 Etapa 3 — Estratégia incremental
Regra obrigatória
❌ Nunca modernizar tudo junto.

Estratégia correta
Tipo
Prioridade
Segurança crítica
Alta
Dependência transitiva
Média
Refatoração estrutural
Baixa


K.9 Etapa 4 — Refatoração assistida
Ferramenta recomendada
Preferencial:
Cursor
Alternativa:
Claude

Cursor deve ser usado para
alteração multi-arquivo
reorganização estrutural
renomeações
ajustes incrementais

Claude deve ser usado para
entendimento funcional
explicação de regras obscuras
planejamento técnico

K.10 Etapa 5 — Validação assistida
Ferramenta recomendada
Claude
Gemini Code Assist

Objetivo
Gerar:
cenários de regressão
testes prioritários
hipóteses de falha
áreas críticas

Template
Com base nessa modernização:

<descrição>

Identifique:
- possíveis regressões
- cenários críticos
- testes prioritários

K.11 Estratégia organizacional
Não tratar upgrade como tarefa simples
Criar categorias:
Tipo
Exemplo
Upgrade seguro
patch
Upgrade moderado
minor
Upgrade crítico
major/framework


K.12 Anti-patterns
❌ Atualizar tudo junto
❌ Não mapear dependências transitivas
❌ Não validar regressão
❌ Misturar arquitetura nova e antiga
❌ Usar IA sem contexto do sistema

K.13 Resultado esperado
modernização incremental
menos regressão
menor risco arquitetural
maior previsibilidade
redução de dívida técnica

K.14 Insight final
O maior problema do legado não é código antigo.
É conhecimento implícito perdido.
A IA ajuda a recuperar esse conhecimento antes da modernização.

