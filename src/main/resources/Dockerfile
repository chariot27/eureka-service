# ⚙️ Etapa 1: Build com cache
FROM gradle:8.5-jdk17 AS builder

WORKDIR /app

# Copia apenas os arquivos de configuração para cache de dependências
COPY build.gradle settings.gradle gradle.properties ./
COPY gradle ./gradle

# Baixa as dependências em cache
RUN gradle build --no-daemon || true

# Agora copia o restante (código-fonte)
COPY . .

# Gera o .jar
RUN gradle bootJar -x test --no-daemon

