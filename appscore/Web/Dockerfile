# --------------- Base ---------------
FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base

# Création du répertoire /app
WORKDIR /app

# Exposition du port 80 et 443
EXPOSE 80
EXPOSE 443

# --------------- Build ---------------
FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build

# Copie des fichiers 
WORKDIR /src
COPY ./appscore/Web Web
COPY ./appscore/Foundation/Http Foundation/Http

# Restaurer les dépendances et les outils d’un projet.
RUN dotnet restore /src/Web/Web.csproj

# Copie intégrale
COPY . .
WORKDIR /src/Web

# Build le projet et ses dépendances dans le dossier /app/build
RUN dotnet build Web.csproj -c Release -o /app/build

# --------------- Publish ---------------
FROM build AS publish

# Publier l’application et ses dépendances dans le dossier /app/publish.
RUN dotnet publish Web.csproj -c Release -o /app/publish

FROM base AS final

WORKDIR /app

COPY --from=publish /app/publish .

CMD [ "dotnet","Web.dll" ]