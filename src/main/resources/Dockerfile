# ⚙️ Etapa 1: Build com cache
FROM gradle:8.5-jdk17 AS builder

WORKDIR /app

# Copia apenas arquivos para cache de dependências
COPY build.gradle settings.gradle ./
COPY gradle ./gradle
RUN gradle dependencies --no-daemon || true

# Copia o restante do projeto
COPY . .

# Gera o JAR
RUN gradle bootJar -x test --no-daemon

# 🐳 Etapa 2: Imagem final leve
FROM eclipse-temurin:17-jdk-alpine

WORKDIR /app
COPY --from=builder /app/build/libs/*.jar app.jar

ENV SERVER_PORT=8761
EXPOSE ${SERVER_PORT}

ENTRYPOINT ["java", "-jar", "app.jar"]
