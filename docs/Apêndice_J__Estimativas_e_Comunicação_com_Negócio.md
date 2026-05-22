📎 Apêndice J — Estimativas e Comunicação com Negócio

J.1 Princípio
Dev não deve só estimar — deve explicar o porquê da estimativa
Isso muda completamente a percepção do gerente.

J.2 Qual IA usar?
Aqui muda bastante:
✔ Melhor escolha: Claude
Por quê?
melhor estruturação de texto
melhor argumentação
melhor equilíbrio técnico + explicação

✔ Complemento: Gemini Code Assist
Use para:
validar impacto técnico
cenários distribuídos

❌ Não usar para isso:
GitHub Copilot
 👉 ele não é bom em narrativa/explicação

J.3 Problema do prompt padrão
Seu prompt:
“elabore plano + custo”
👉 Resultado típico:
estimativa rasa
sem justificativa
difícil de defender

J.4 Modelo correto (separar 3 coisas)
Você precisa gerar:
Plano técnico
Estimativa estruturada
Explicação para negócio
👉 Isso não pode vir tudo misturado

J.5 Template ideal (para Claude)
Seja um desenvolvedor sênior com experiência em estimativas de software.
Contexto do projeto:


Tarefa:
<descrição do Jira>
Objetivo:
Gerar uma resposta para stakeholders não técnicos contendo:
Resumo da solução (alto nível, sem jargão)
Principais etapas técnicas (simplificadas)
Estimativa de esforço por etapa
Riscos e incertezas
Dependências externas
Possíveis cenários:
otimista
realista
pessimista
Importante:
evitar jargão técnico desnecessário
justificar cada estimativa
deixar claro o que pode impactar prazo

J.6 Exemplo de saída esperada
Isso aqui é o padrão que você quer gerar (resumo):

📌 Resumo
Implementação envolve ajuste na API + validação de dados + integração com serviço externo.

⚙️ Etapas
Etapa
Descrição
Esforço
Ajuste API
Alterar endpoint
Baixo
Validação
Regras de negócio
Médio
Integração
Serviço externo
Alto


⏱️ Estimativa
Otimista: 1 dia
Realista: 2 dias
Pessimista: 4 dias

⚠️ Riscos
dependência externa
inconsistência de dados

👉 Isso é justificável em reunião.

J.7 Template técnico (interno, antes do gerencial)
Você deve continuar usando seu fluxo técnico, mas separado:
Quebre a tarefa em passos técnicos detalhados e estime esforço técnico.
👉 Depois transforma em linguagem de negócio (com template acima)

J.8 Fluxo ideal (importante)
Você usa IA para plano técnico
Você valida
Você pede para IA traduzir para negócio
👉 Isso resolve o seu problema atual

J.9 Anti-pattern comum
❌ Pedir direto:
“me diga quanto tempo leva”
Resultado:
chute sofisticado

J.10 Passos para o processo sugerido
Faça:
1. plano técnico
2. refinamento
3. estimativa estruturada
4. tradução para negócio

J.11 Insight importante
Gerente não quer:
saber código
saber framework
Ele quer:
previsibilidade
risco
impacto

J.12 Resultado esperado
Com esse modelo:
suas estimativas ficam justificáveis
você reduz pressão
melhora percepção de senioridade
evita retrabalho de explicação

