# Padrão Arquitetural Quarkus

**Objetivo**

Este documento define o padrão arquitetural oficial para modernização incremental de sistemas legados utilizando:

- Java 17
- Quarkus JVM
- Containers
- OpenShift/Kubernetes
- Observabilidade nativa
- APIs orientadas a contratos
- Frontend BFF com Next.js
- Keycloak
- GitLab CI/CD
- SonarQube
- IA generativa assistiva

Este documento deve ser utilizado como:

- Template arquitetural oficial
- Contexto base para IA (Claude, ChatGPT e Gemini)
- Padrão de novos serviços Java
- Base para bootstrap de aplicações
- Modelo de governança técnica

---

## 1. Princípios Arquiteturais

### 1.1 Modernização Incremental

Padrões obrigatórios:

- Strangler Fig Pattern
- Anti-Corruption Layer
- Encapsulamento do legado
- Extração gradual de domínio
- APIs intermediárias

Nunca realizar:

- Big Bang Rewrite
- Reescrita completa do sistema
- Acoplamento direto ao legado

---

### 1.2 Arquitetura Orientada a Contratos

Toda integração deve possuir:

- OpenAPI 3
- DTOs explícitos
- Versionamento
- Contratos documentados
- APIs desacopladas

---

### 1.3 Observabilidade Nativa

Todo serviço deve nascer com:

- OpenTelemetry
- Logs estruturados JSON
- Tracing distribuído
- Métricas Prometheus
- Correlation ID
- Health checks
- Readiness/Liveness

Observabilidade não é opcional.

---

### 1.4 IA Assistiva

A IA deve:

- acelerar desenvolvimento
- gerar boilerplates
- gerar adapters
- auxiliar troubleshooting
- auxiliar documentação
- gerar testes
- acelerar migração incremental

A IA NÃO deve:

- alterar arquitetura
- remover observabilidade
- ignorar contratos
- modificar padrões corporativos

---

## 2. Arquitetura Alvo

```
Frontend Next.js (BFF)
        ↓
API Gateway / BFF
        ↓
Serviços Quarkus
        ↓
Mensageria / APIs
        ↓
Legado / Banco / Sistemas externos
```

---

## 3. Stack Oficial Backend

**Linguagem**
- Java 17

---

**Framework**
- Quarkus

---

**Configuração JVM Obrigatória**

```
<compiler-plugin.version>3.11.0</compiler-plugin.version>
<maven.compiler.release>17</maven.compiler.release>
```

---

**REST**
- RESTEasy Reactive

---

**Segurança**

- JWT
- OAuth2
- OpenID Connect
- Keycloak

---

**Banco**
MariaDB
Hibernate ORM Panache
Flyway

---

**Observabilidade**
- OpenTelemetry
- Micrometer
- Prometheus

---

**Mensageria**

- RabbitMQ

---

## 4. Estrutura Oficial Backend Quarkus

```
/backend-quarkus-service
│
├── src
│   ├── main
│   │   ├── java
│   │   │   └── com/company/platform
│   │   │       ├── api
│   │   │       ├── domain
│   │   │       ├── application
│   │   │       ├── infra
│   │   │       ├── security
│   │   │       ├── observability
│   │   │       ├── contracts
│   │   │       └── config
│   │   │
│   │   └── resources
│   │       ├── application.properties
│   │       └── openapi
│   │
│   └── test
│
├── openshift
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── route.yaml
│   ├── configmap.yaml
│   ├── secret.yaml
│   └── hpa.yaml
│
├── Dockerfile.jvm
├── pom.xml
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

## 6. Dependências Oficiais Quarkus

**REST**

```
<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-resteasy-reactive</artifactId>
</dependency>

<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-resteasy-reactive-jackson</artifactId>
</dependency>
```

---

**Segurança**

```
<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-oidc</artifactId>
</dependency>

<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-smallrye-jwt</artifactId>
</dependency>
```

---

**OpenAPI**

```
<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-smallrye-openapi</artifactId>
</dependency>
```

---

**Observabilidade**

```
<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-opentelemetry</artifactId>
</dependency>

<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-micrometer-registry-prometheus</artifactId>
</dependency>
```

---

**Banco**

```
<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-jdbc-mariadb</artifactId>
</dependency

<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-hibernate-orm-panache</artifactId>
</dependency>
```

---

**Health Checks**

```
<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-smallrye-health</artifactId>
</dependency>
```

---

## 7. Bibliotecas Oficiais Frontend

```
next
react
react-dom
next-auth
keycloak-js
axios
zod
react-hook-form
```

---

## 8. Requisitos Obrigatórios Backend

Todo serviço deve possuir:

- Swagger/OpenAPI
- JWT Authentication
- Integração Keycloak
- Health checks
- Readiness probe
- Liveness probe
- Structured logging
- OpenTelemetry
- Metrics endpoint
- Correlation ID
- Dockerfile JVM
- Configuração via variáveis de ambiente
- Graceful shutdown
- Compatibilidade OpenShift

---

## 9. Exemplo application.properties

```
quarkus.http.port=8080

quarkus.smallrye-openapi.path=/openapi
quarkus.swagger-ui.always-include=true

quarkus.oidc.auth-server-url=https://keycloak.company.com/realms/platform
quarkus.oidc.client-id=backend-api
quarkus.oidc.credentials.secret=secret

quarkus.datasource.db-kind=postgresql
quarkus.datasource.jdbc.url=jdbc:postgresql://db:5432/app
quarkus.datasource.username=user
quarkus.datasource.password=pass

quarkus.hibernate-orm.database.generation=none

quarkus.opentelemetry.enabled=true
quarkus.micrometer.export.prometheus.enabled=true

quarkus.smallrye-health.root-path=/health
```

---

## 10. Exemplo Health Resource

```
package com.company.platform.api;

import jakarta.ws.rs.GET;
import jakarta.ws.rs.Path;
import jakarta.ws.rs.Produces;
import jakarta.ws.rs.core.MediaType;

@Path("/health/live")
public class HealthResource {

    @GET
    @Produces(MediaType.APPLICATION_JSON)
    public String live() {
        return "{\"status\":\"UP\"}";
    }
}
```

---

## 11. Exemplo Dockerfile JVM

```
FROM registry.access.redhat.com/ubi8/openjdk-17

WORKDIR /deployments

COPY target/quarkus-app/lib/ /deployments/lib/
COPY target/quarkus-app/*.jar /deployments/
COPY target/quarkus-app/app/ /deployments/app/
COPY target/quarkus-app/quarkus/ /deployments/quarkus/

EXPOSE 8080

CMD ["java", "-jar", "/deployments/quarkus-run.jar"]
```

---

## 12. Exemplo deployment.yaml OpenShift

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: backend-quarkus-service
spec:
  replicas: 1
  selector:
    matchLabels:
      app: backend-quarkus-service
  template:
    metadata:
      labels:
        app: backend-quarkus-service
    spec:
      containers:
        - name: backend-quarkus-service
          image: backend-quarkus-service:latest

          ports:
            - containerPort: 8080

          livenessProbe:
            httpGet:
              path: /q/health/live
              port: 8080
            initialDelaySeconds: 10
            periodSeconds: 10

          readinessProbe:
            httpGet:
              path: /q/health/ready
              port: 8080
            initialDelaySeconds: 5
            periodSeconds: 5
```

---

## 13. Segurança e Qualidade de Código

Toda esteira CI/CD deve possuir:

- SonarQube
- análise SAST
- análise de vulnerabilidades
- análise de cobertura
- análise de code smells
- dependency scanning
- container scanning
- quality gates obrigatórios

---

### Ferramentas obrigatórias GitLab CI/CD

**Qualidade**

- SonarQube
- Checkstyle
- SpotBugs
- PMD

---

**Segurança**

- Trivy
- OWASP Dependency Check
- GitLab Security Scanning

---

**Regras obrigatórias**

Pipeline deve falhar quando:

- vulnerabilidades críticas forem encontradas
- quality gate do SonarQube falhar
- cobertura mínima não for atingida
- CVEs críticos forem encontrados

---

## 14. Padrão de Logs

Formato obrigatório:

```
{
  "timestamp": "2026-01-01T10:00:00Z",
  "level": "INFO",
  "service": "backend-quarkus-service",
  "trace_id": "abc123",
  "span_id": "def456",
  "correlation_id": "ghi789",
  "message": "Request processed"
}
```

---

## 15. Contratos de API

**Erros**

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
APP_NAME=backend-quarkus-service
APP_ENV=dev
QUARKUS_HTTP_PORT=8080
KEYCLOAK_SERVER_URL=https://keycloak.company.com
KEYCLOAK_REALM=platform
KEYCLOAK_CLIENT_ID=backend-api
DATABASE_URL=jdbc:postgresql://db:5432/app
OTEL_EXPORTER_OTLP_ENDPOINT=http://otel-collector:4317
```

---

## 17. Regras Arquiteturais Obrigatórias

**Nunca:**

- colocar regra de negócio nos resources REST
- acessar banco diretamente pelos endpoints
- acoplar domínio ao framework
- ignorar contratos OpenAPI
- integrar diretamente ao legado
- criar serviços sem observabilidade

---

**Sempre:**

- utilizar DTOs
- utilizar adapters
- utilizar interfaces
- versionar APIs
- externalizar configurações
- implementar tracing
- implementar métricas
= implementar correlation-id

---

##18. Prompt Base Oficial para IA

```
Você está implementando um serviço aderente à Plataforma Corporativa de Modernização Assistida por IA.

Stack obrigatória:
- Java 17
- Quarkus
- RESTEasy Reactive
- OpenTelemetry
- JWT
- Keycloak
- PostgreSQL
- OpenShift
- Docker
- Prometheus
- SonarQube

Estrutura obrigatória:
- api
- domain
- application
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
- Sem regra de negócio nos endpoints REST

Nunca:
- misture domínio com infraestrutura
- acople diretamente ao legado
- ignore observabilidade
- gere logs sem trace_id
```

---

## 19. Estratégia Oficial de Modernização

**Fase 1**
Encapsular legado.

---

**Fase 2**
Criar APIs intermediárias.

---

**Fase 3**
Introduzir observabilidade.

---

**Fase 4**
Extrair domínio gradualmente.

---

**Fase 5**
Migrar integrações.

---

**Fase 6**
Desativar módulos legados.

---

## 20. Resultado Esperado

A plataforma deve permitir:

- modernização incremental
- menor acoplamento
- observabilidade nativa
- padronização arquitetural
- aderência OpenShift
- governança técnica uniforme
- aceleração assistida por IA
- onboarding técnico simplificado
- redução de conhecimento tribal

