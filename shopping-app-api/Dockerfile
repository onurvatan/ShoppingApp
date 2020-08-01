FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["shopping-app-api/shopping-app-api.csproj", "shopping-app-api/"]
RUN dotnet restore "shopping-app-api/shopping-app-api.csproj"
COPY . .
WORKDIR "/src/shopping-app-api"
RUN dotnet build "shopping-app-api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "shopping-app-api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "shopping-app-api.dll"]
