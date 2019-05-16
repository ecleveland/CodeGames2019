FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["JournalEntriesAPI/JournalEntriesAPI.csproj", "JournalEntriesAPI/"]
RUN dotnet restore "JournalEntriesAPI/JournalEntriesAPI.csproj"
COPY . .
WORKDIR "/src/JournalEntriesAPI"
RUN dotnet build "JournalEntriesAPI.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "JournalEntriesAPI.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "JournalEntriesAPI.dll"]