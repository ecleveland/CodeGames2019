FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-stretch AS build
WORKDIR /src
COPY ["CodeGames2019_UI/CodeGames2019_UI.csproj", "CodeGames2019_UI/"]
RUN dotnet restore "CodeGames2019_UI/CodeGames2019_UI.csproj"
COPY . .
WORKDIR "/src/CodeGames2019_UI"
RUN dotnet build "CodeGames2019_UI.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "CodeGames2019_UI.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CodeGames2019_UI.dll"]