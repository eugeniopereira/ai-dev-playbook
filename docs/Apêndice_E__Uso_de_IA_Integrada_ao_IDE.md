📎 Apêndice E — Uso de IA Integrada ao IDE
E.1 Escopo
Este apêndice define o uso de ferramentas de IA que atuam diretamente no código, como:
GitHub Copilot
Cursor IDE
Visual Studio Code + plugins (ex: Claude, Copilot Chat)

E.2 Princípio central
Essas ferramentas não substituem o guideline anterior — elas mudam a interface.
👉 Antes: você escrevia prompt
👉 Agora: você interage direto com o código
Mas o risco aumenta:
quanto mais fácil gerar código, maior o risco de erro silencioso

E.3 Modos de uso dentro do IDE
E.3.1 Autocomplete inteligente (baixo risco)
Exemplo:
completar método
gerar boilerplate
✔ Uso recomendado
 ⚠ Pouco impacto arquitetural

E.3.2 Edição assistida de código (médio risco)
Exemplo:
refatorar classe
ajustar lógica
✔ Usar com contexto claro
 ⚠ Revisão obrigatória

E.3.3 Geração de código (alto risco)
Exemplo:
criar serviço inteiro
implementar integração
⚠ Aqui mora o perigo
Regra:
nunca aceitar código grande sem validação rigorosa

E.3.4 Chat contextual no código (alto valor)
Exemplo no Cursor ou VSCode:
“explique esse método”
“onde pode dar erro aqui?”
👉 Esse é o uso mais poderoso para devs iniciantes

E.4 Padrão de uso recomendado (dentro do IDE)
Fluxo ideal
Dev seleciona código
Faz pergunta contextual
IA responde com base no código real
Dev valida e adapta

E.5 Templates adaptados para IDE
E.5.1 Debug direto no código
Selecionar trecho e usar:
Analise esse código no contexto de Java + Quarkus.

Objetivo:
- identificar possíveis erros
- apontar edge cases
- sugerir correção

E.5.2 Refatoração segura
Refatore esse código aplicando:
- clean code
- redução de complexidade

Sem alterar comportamento funcional.

E.5.3 Explicação de código (onboarding)
Explique esse código como se eu fosse um dev novo no projeto.

Inclua:
- propósito
- fluxo
- pontos críticos

E.5.4 Geração de testes
Gere testes unitários para esse código usando JUnit 5.

Inclua:
- casos de sucesso
- casos de erro
- edge cases

E.6 Boas práticas específicas
✔ Sempre
Trabalhar com trechos pequenos de código
Dar contexto (framework, objetivo)
Revisar tudo antes de aceitar

✔ Ideal
Usar IA para:
entender código legado
acelerar tarefas repetitivas
gerar testes

E.7 Más práticas críticas
❌ Aceitar sugestão automática sem ler
Copilot principalmente incentiva isso.

❌ Gerar código sem contexto
Exemplo:
“crie um service”
→ resultado genérico e fora do padrão do projeto

❌ Refatorar múltiplos arquivos sem controle
Ferramentas como o Cursor IDE permitem isso — alto risco.

E.8 Controle de qualidade (obrigatório)
Qualquer código gerado deve passar por:
build local
testes
code review humano

E.9 Uso avançado (nível 3)
Quando o time evoluir, usar:
✔ Navegação assistida
“onde esse método é usado?”
“impacto dessa mudança?”
✔ Refatoração guiada
dividir classe grande
extrair responsabilidades
✔ Análise de impacto
mudanças em cascata

E.10 Integração com o guideline geral
Regra chave:
IDE com IA NÃO substitui prompts estruturados — complementa
Quando usar cada um:
Situação
Ferramenta
Debug complexo
Chat estruturado
Refatoração local
IDE
Design
Chat
Testes
IDE


E.11 Governança para o time
Pode-se formalizar:
uso liberado das ferramentas
obrigatoriedade de revisão
proibição de commits “cegos”

E.12 Risco principal
Esse é o ponto mais crítico de todo o guideline:
Ferramentas como GitHub Copilot aumentam velocidade, mas podem reduzir qualidade se mal usadas.

🚀 Resultado esperado
Com esse apêndice:
o time usa IA dentro do fluxo real de desenvolvimento
reduz curva de aprendizado
evita uso ingênuo dessas ferramentas
mantém controle arquitetural

