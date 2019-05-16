FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["MillerLightUI/MillerLightUI.csproj", "MillerLightUI/"]
RUN dotnet restore "MillerLightUI/MillerLightUI.csproj"
COPY . .
WORKDIR "/src/MillerLightUI"
RUN dotnet build "MillerLightUI.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MillerLightUI.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MillerLightUI.dll"]