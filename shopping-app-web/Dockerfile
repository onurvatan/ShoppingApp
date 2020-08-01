FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["shopping-app-web/shopping-app-web.csproj", "shopping-app-web/"]
RUN dotnet restore "shopping-app-web/shopping-app-web.csproj"
COPY . .
WORKDIR "/src/shopping-app-web"
RUN dotnet build "shopping-app-web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "shopping-app-web.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "shopping-app-web.dll"]
