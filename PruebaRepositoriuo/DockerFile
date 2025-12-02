# Etapa base (runtime)
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 8080

# Etapa build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["PruebaRepositorioiu.csproj", "./"]
RUN dotnet restore "PruebaRepositorioiu.csproj"
COPY . .
RUN dotnet build "PruebaRepositorioiu.csproj" -c Release -o /app/build

# Etapa publish
FROM build AS publish
RUN dotnet publish "PruebaRepositorioiu.csproj" -c Release -o /app/publish

# Etapa final
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PruebaRepositorioiu.dll"]
