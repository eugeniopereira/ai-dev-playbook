# Padrão Arquitetural Python

** Objetivo **

Este documento define o padrão arquitetural oficial para modernização incremental de sistemas legados utilizando:

- IA generativa assistiva
- Microsserviços
- Containers
- OpenShift/Kubernetes
- Observabilidade nativa
- APIs orientadas a contratos
- Frontend BFF com Next.js
- Backend Python/FastAPI

Este documento deve ser utilizado como:

- Template arquitetural
- Contexto base para IA (Claude, ChatGPT, Gemini)
- Padrão oficial de novos serviços
- Modelo de bootstrap de aplicações
- Base de governança técnica

## 1. Princípios Arquiteturais

### 1.1 Modernização Incremental

Padrão obrigatório:

- Strangler Fig Pattern
- Anti-Corruption Layer
- Extração gradual de domínio
- Convivência controlada com legado

Nunca realizar:

- Big Bang Rewrite
- Reescrita total do sistema
- Acoplamento direto ao legado

---

### 1.2 Arquitetura Orientada a Contratos

Toda integração deve possuir:

- OpenAPI 3
- DTOs explícitos
- Versionamento
- Contratos documentados

---

### 1.3 Observabilidade Nativa

Todo serviço deve nascer com:

- Logs estruturados JSON
- OpenTelemetry
- Tracing distribuído
- Métricas Prometheus
- Correlation ID
- Health checks

Observabilidade não é opcional.

---

### 1.4 IA Assistiva

A IA deve:

- acelerar desenvolvimento
- gerar código boilerplate
- criar adapters
- gerar testes
- auxiliar documentação
- auxiliar troubleshooting

A IA NÃO deve:

- decidir arquitetura
- alterar padrões estruturais
- modificar observabilidade
- remover contratos

---

## 2. Arquitetura Alvo

```
Frontend Next.js (BFF)
        ↓
API Gateway / BFF
        ↓
Serviços FastAPI
        ↓
Mensageria / APIs
        ↓
Legado / Banco / IA / Sistemas externos
```

---

## 3. Stack Oficial

### 3.1 Backend

** Linguagem **

- Python 3.12+

** Framework **

- FastAPI

** Servidor ASGI **

- Granian
ou
- Uvicorn

** Validação **

- Pydantic v2

** Autenticação **

- JWT
- Keycloak
- OAuth2/OpenID Connect

** Observabilidade **

- OpenTelemetry
- Prometheus
- Structlog

** Banco **

- MySQL
- SQLAlchemy
- Alembic

** Mensageria **
RabbitMQ

---

### 3.2 Frontend

** Framework oficial **

- Next.js

** Objetivo **

- BFF
- SSR
- Controle de autenticação
- Proxy de APIs
- Sessão segura

** Autenticação **

- NextAuth.js
ou
- integração direta Keycloak OIDC

** UI **

- React
- Tailwind

---

## 4. Estrutura Oficial Backend FastAPI

```
/backend-service
│
├── app
│   ├── api
│   │   ├── routes
│   │   ├── dependencies
│   │   └── middlewares
│   │
│   ├── domain
│   │   ├── entities
│   │   ├── usecases
│   │   └── interfaces
│   │
│   ├── infra
│   │   ├── database
│   │   ├── repositories
│   │   ├── clients
│   │   └── messaging
│   │
│   ├── security
│   │   ├── jwt
│   │   ├── keycloak
│   │   └── permissions
│   │
│   ├── observability
│   │   ├── logging
│   │   ├── tracing
│   │   └── metrics
│   │
│   ├── contracts
│   │   ├── request
│   │   └── response
│   │
│   ├── config
│   │   └── settings.py
│   │
│   └── main.py
│
├── tests
│
├── openshift
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── route.yaml
│   ├── configmap.yaml
│   ├── secret.yaml
│   └── hpa.yaml
│
├── Dockerfile
├── Makefile
├── pyproject.toml
└── README.md
```

---

## 5. Estrutura Oficial Frontend Next.js BFF

```
/web
│
├── src
│   ├── app
│   ├── components
│   ├── services
│   ├── auth
│   ├── middleware
│   ├── lib
│   ├── hooks
│   ├── types
│   └── config
│
├── public
├── tests
├── Dockerfile
├── next.config.js
├── package.json
└── README.md
```

---

## 6. Bibliotecas Oficiais Backend

### APIs

- fastapi
- uvicorn
- granian
- pydantic

### Segurança

- python-jose
- passlib
- python-multipart
- Authlib
- python-keycloak

### Observabilidade

- opentelemetry-api
- opentelemetry-sdk
- opentelemetry-exporter-otlp
- opentelemetry-instrumentation-fastapi
- prometheus-client
- structlog

### Banco

- sqlalchemy
- alembic

### Qualidade

- pytest
- pytest-asyncio
- ruff
- black
- mypy

---

## 7. Bibliotecas Oficiais Frontend

```
- next
- react
- react-dom
- next-auth
- keycloak-js
- axios
- zod
- react-hook-form
```

---

## 8. Requisitos Obrigatórios Backend

Todo serviço deve possuir:

- Swagger/OpenAPI
- JWT Authentication
- Keycloak integration
- Health checks
- Readiness probe
- Liveness probe
- Structured logging
- OpenTelemetry
- Metrics endpoint
- Correlation ID
- Dockerfile multi-stage
- Configuração por variáveis de ambiente
- Graceful shutdown

---

## 9. Exemplo de main.py

```
from fastapi import FastAPI
from fastapi.responses import JSONResponse

app = FastAPI(
    title="Modernization Platform API",
    version="1.0.0",
    docs_url="/docs",
    redoc_url="/redoc",
    openapi_url="/openapi.json"
)


@app.get("/health/live")
async def liveness():
    return JSONResponse(
        content={
            "status": "UP"
        }
    )


@app.get("/health/ready")
async def readiness():
    return JSONResponse(
        content={
            "status": "READY"
        }
    )


@app.get("/")
async def root():
    return {
        "service": "modernization-platform",
        "version": "1.0.0"
    }

```

---

## 10. Exemplo de JWT Authentication

```
from fastapi.security import HTTPBearer

security = HTTPBearer()
```

---

## 11. Exemplo de Integração Keycloak

Variáveis obrigatórias:

```
KEYCLOAK_SERVER_URL=https://keycloak.company.com
KEYCLOAK_REALM=platform
KEYCLOAK_CLIENT_ID=backend-api
KEYCLOAK_CLIENT_SECRET=secret
```

---

## 12. Exemplo Dockerfile Backend

```
FROM python:3.12-slim AS builder

WORKDIR /app

COPY pyproject.toml .

RUN pip install --upgrade pip

COPY . .

RUN pip install .

FROM python:3.12-slim

WORKDIR /app

COPY --from=builder /usr/local/lib/python3.12 /usr/local/lib/python3.12
COPY . .

EXPOSE 8080

CMD ["granian", "app.main:app", "--host", "0.0.0.0", "--port", "8080"]
```
---

## 13. Exemplo deployment.yaml OpenShift

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: modernization-platform
spec:
  replicas: 1
  selector:
    matchLabels:
      app: modernization-platform
  template:
    metadata:
      labels:
        app: modernization-platform
    spec:
      containers:
        - name: modernization-platform
          image: modernization-platform:latest
          ports:
            - containerPort: 8080

          livenessProbe:
            httpGet:
              path: /health/live
              port: 8080
            initialDelaySeconds: 10
            periodSeconds: 10

          readinessProbe:
            httpGet:
              path: /health/ready
              port: 8080
            initialDelaySeconds: 5
            periodSeconds: 5
```

---

## 14. Padrão de Logs

Formato obrigatório:

```
{
  "timestamp": "2026-01-01T10:00:00Z",
  "level": "INFO",
  "service": "modernization-platform",
  "trace_id": "abc123",
  "span_id": "def456",
  "correlation_id": "ghi789",
  "message": "Request processed"
}
```

---

## 15. Contratos de API

Padrão obrigatório:

** Erros **
```
{
  "code": "DOCUMENT_NOT_FOUND",
  "message": "Document not found",
  "trace_id": "abc123"
}
```

---

## 16. Padrão de Variáveis de Ambiente

```
APP_NAME=modernization-platform
APP_ENV=dev
APP_PORT=8080
LOG_LEVEL=INFO
JWT_SECRET=secret
DATABASE_URL=postgresql://user:pass@db/app
OTEL_EXPORTER_OTLP_ENDPOINT=http://otel-collector:4317
```

## 17. Regras Arquiteturais Obrigatórias

** Nunca: **

- colocar regra de negócio em controllers
- acessar banco diretamente pela rota
- acoplar domínio ao framework
- usar prints
- criar logs sem trace_id
- integrar diretamente ao legado
- ignorar contratos OpenAPI

** Sempre: **

- utilizar DTOs
- utilizar adapters
- utilizar interfaces
- versionar APIs
- implementar testes
- utilizar correlation-id
- implementar observabilidade
- externalizar configuração

---

## 18. Prompt Base Oficial para IA

```
Você está implementando um serviço aderente à Plataforma Corporativa de Modernização Assistida por IA.

Stack obrigatória:
- Python 3.12
- FastAPI
- OpenTelemetry
- Structured Logging
- JWT Authentication
- Keycloak
- OpenShift
- Docker
- PostgreSQL
- Prometheus

Estrutura obrigatória:
- api
- domain
- infra
- security
- observability
- contracts

Requisitos:
- Swagger/OpenAPI habilitado
- Health checks
- Readiness/Liveness probes
- Configuração via variáveis de ambiente
- Logs estruturados JSON
- Tracing distribuído
- Código desacoplado de infraestrutura
- Sem regra de negócio nos controllers

Nunca:
- use prints
- misture domínio com infraestrutura
- acople serviços diretamente ao legado
- gere logs sem trace_id
```

---

## 19. Estratégia Oficial de Modernização

** Fase 1 **
Encapsular legado.

---

** Fase 2 **
Introduzir APIs intermediárias.

---

** Fase 3 **
Adicionar observabilidade.

---

** Fase 4 **
Extrair domínio gradualmente.

---

** Fase 5 **
Migrar integrações.

---

** Fase 6 **
Desativar módulos legados.

---

## 20. Resultado Esperado

A plataforma deve permitir:

- modernização incremental
- redução de acoplamento
- observabilidade nativa
- padronização arquitetural
- aceleração via IA
- deploy consistente no OpenShift
- menor dependência de conhecimento tribal
- onboarding acelerado
- governança técnica uniforme

