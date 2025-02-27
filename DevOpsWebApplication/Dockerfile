# Brug en officiel .NET runtime som baseimage
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

# Brug en officiel .NET SDK som build image
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["DevOpsWebApplication/DevOpsWebApplication.csproj", "DevOpsWebApplication/"]
RUN dotnet restore "DevOpsWebApplication/DevOpsWebApplication.csproj"

# Kopier resten af koden og byg applikationen
COPY . .
WORKDIR "/src/DevOpsWebApplication"
RUN dotnet publish -c Release -o /app/publish

# Brug base imaget og kopier build-outputtet
FROM base AS final
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "DevOpsWebApplication.dll"]
