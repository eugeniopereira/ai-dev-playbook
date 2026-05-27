---
name: ai-context-create
description: Analisa aplicação do projeto e gera documentação ai-context.md com arquitetura, padrões e convenções
---

# AI Context Create - Gerador de Contexto para IA

Analisa a estrutura da aplicação e gera documentação contextual para desenvolvimento assistido por IA.

## Uso

```bash
/ai-context-create <app>
```

**Apps disponíveis:**
- `api` - FastAPI backend (GCP)
- `web` - Next.js frontend (GCP)
- `worker` - Worker assíncrono (GCP)
- `agent` - Vertex AI agent

## Exemplos

```bash
/ai-context-create api
/ai-context-create web
/ai-context-create worker
/ai-context-create agent
```

---

## Validação de Argumentos

Antes de iniciar, valide:

- **App válido**: Deve ser exatamente um dos valores: `api`, `web`, `worker`, `agent`
  - Se inválido, retorne erro listando os apps disponíveis
  - Se ausente, solicite ao usuário que informe qual aplicação analisar

---

## Instruções de Execução

Ao ser invocado com argumento válido, você deve:

1. **Identificar a pasta da aplicação** conforme mapeamento:
   - `api` → `/opt/iplanrio/apps/danfe-ai/api`
   - `web` → `/opt/iplanrio/apps/danfe-ai/web`
   - `worker` → `/opt/iplanrio/apps/danfe-ai/app-danfe-worker`
   - `agent` → `/opt/iplanrio/apps/danfe-ai/app-danfe-agent`

2. **Explorar a estrutura da aplicação**:
   - Listar estrutura de diretórios principais
   - Identificar arquivos de configuração (package.json, requirements.txt, pyproject.toml, etc.)
   - Ler arquivos principais (main.py, app.py, index.ts, etc.)
   - Analisar estrutura de pastas (models/, routes/, services/, components/, etc.)

3. **Executar a análise** seguindo o template abaixo:

---

**Você é um arquiteto de software especializado em documentação técnica.**

**Aplicação a analisar:** {app}

**Pasta da aplicação:** {caminho_completo}

**Tarefa:**

Analise esta aplicação e identifique:

1. **Arquitetura predominante**
   - Padrão arquitetural (MVC, Clean Architecture, Layered, etc.)
   - Organização de responsabilidades
   - Fluxo de dados

2. **Frameworks e bibliotecas principais**
   - Framework principal e versão
   - Bibliotecas essenciais para funcionamento
   - Dependências de infraestrutura (banco, cache, filas, etc.)

3. **Padrões de código**:
   - **Tratamento de erro**: Como erros são capturados, logados e tratados
   - **Persistência**: ORM, queries, transações, migrações
   - **Integração externa**: HTTP clients, APIs externas, autenticação
   - **Logging e observabilidade**: Como logs são estruturados, tracing, métricas

4. **Convenções relevantes**
   - Nomenclatura de arquivos e pastas
   - Estrutura de imports
   - Padrões de teste
   - Boas práticas adotadas

**Formato de saída esperado:**

Gere um arquivo markdown estruturado e objetivo com as seguintes seções:

```markdown
# AI Context - {App Name}

> Documentação gerada automaticamente em {data}

## Arquitetura

[Descrição do padrão arquitetural, organização de camadas, fluxo de dados]

## Stack Tecnológica

### Framework Principal
- **{Framework}** ({versão})
- [Descrição breve do propósito]

### Dependências Principais
| Biblioteca | Versão | Propósito |
|------------|--------|-----------|
| {nome}     | {ver}  | {uso}     |

### Infraestrutura
- **Banco de dados**: {tipo e ORM}
- **Cache**: {se aplicável}
- **Mensageria**: {se aplicável}
- **Storage**: {se aplicável}

## Padrões de Código

### Tratamento de Erros
- **Estratégia**: {como erros são tratados}
- **Logging**: {como erros são logados}
- **Exemplos**:
  ```{linguagem}
  # Exemplo de tratamento de erro padrão
  ```

### Persistência de Dados
- **ORM/Query Builder**: {ferramenta usada}
- **Migrações**: {como são gerenciadas}
- **Transações**: {padrão adotado}
- **Exemplos**:
  ```{linguagem}
  # Exemplo de acesso ao banco
  ```

### Integrações Externas
- **HTTP Client**: {biblioteca usada}
- **Autenticação**: {método - JWT, OAuth, etc.}
- **APIs consumidas**: {lista principal}
- **Exemplos**:
  ```{linguagem}
  # Exemplo de chamada externa
  ```

### Observabilidade
- **Logging**: {estratégia - structured logging, níveis}
- **Tracing**: {ferramenta - OpenTelemetry, Jaeger, etc.}
- **Métricas**: {se aplicável}
- **Exemplos**:
  ```{linguagem}
  # Exemplo de log estruturado
  ```

## Convenções de Código

### Estrutura de Arquivos
- **Organização**: {descrição da estrutura de pastas}
- **Nomenclatura**: {padrões de nome de arquivo}

### Imports
- **Ordem**: {convenção de ordenação}
- **Estilo**: {absoluto vs relativo}

### Testes
- **Framework**: {pytest, jest, etc.}
- **Localização**: {onde ficam os testes}
- **Convenções**: {nomenclatura, estrutura}

## Pontos de Atenção para Desenvolvimento

1. **{Ponto importante 1}**: {explicação}
2. **{Ponto importante 2}**: {explicação}
3. **{Ponto importante 3}**: {explicação}

## Arquivos de Referência

- **Configuração principal**: `{caminho/arquivo}`
- **Entry point**: `{caminho/arquivo}`
- **Modelos de dados**: `{caminho/pasta}`
- **Rotas/Controllers**: `{caminho/pasta}`
- **Utils/Helpers**: `{caminho/pasta}`

---

*Documento gerado por IA. Revise e ajuste conforme necessário.*
```

---

## Pós-Execução

Após gerar o conteúdo:

1. **Criar pasta `docs/` se não existir** na raiz da aplicação
2. **Salvar o arquivo** em `{app_path}/docs/ai-context.md`
3. **Confirmar com o usuário**:
   - Caminho completo do arquivo criado
   - Resumo em 2-3 linhas do que foi documentado
   - Sugerir revisão manual para ajustes específicos

---

## Observações

- A análise deve ser **objetiva e prática** - foco em informações úteis para desenvolvimento
- **Evite redundância** com CLAUDE.md - este arquivo deve complementar, não duplicar
- **Inclua exemplos de código reais** encontrados na aplicação
- Se a aplicação não existir, informe o usuário e não crie o arquivo