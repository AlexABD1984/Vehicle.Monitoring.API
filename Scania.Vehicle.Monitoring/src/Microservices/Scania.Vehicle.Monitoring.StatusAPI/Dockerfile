FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY src/Microservices/Scania.Vehicle.Monitoring.StatusAPI/Scania.Vehicle.Monitoring.StatusAPI.csproj src/Microservices/Scania.Vehicle.Monitoring.StatusAPI/
RUN dotnet restore src/Microservices/Scania.Vehicle.Monitoring.StatusAPI/Scania.Vehicle.Monitoring.StatusAPI.csproj
COPY . .
WORKDIR /src/src/Microservices/Scania.Vehicle.Monitoring.StatusAPI
RUN dotnet build Scania.Vehicle.Monitoring.StatusAPI.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Scania.Vehicle.Monitoring.StatusAPI.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Scania.Vehicle.Monitoring.StatusAPI.dll"]
