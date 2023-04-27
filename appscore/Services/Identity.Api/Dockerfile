
FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY "appscore/Services/Identity.Api" "Services/Identity.Api/"
COPY "appscore/Foundation/Events" "Foundation/Events/"

RUN dotnet restore "Services/Identity.Api/Identity.Api.csproj"
COPY . .
WORKDIR "/src/Services/Identity.Api"
RUN dotnet build "Identity.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Identity.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "identity.api.dll"]