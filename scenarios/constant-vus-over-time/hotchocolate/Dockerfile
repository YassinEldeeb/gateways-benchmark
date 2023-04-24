FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY Program.cs Startup.cs Gateway.csproj appsettings.json appsettings.Development.json ./
RUN dotnet build "Gateway.csproj" -c Release -o /app/build
RUN dotnet publish "Gateway.csproj" -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
EXPOSE 5000

FROM build
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "Gateway.dll"]