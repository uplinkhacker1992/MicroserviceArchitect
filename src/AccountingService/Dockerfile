FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY AccountingService/AccountingService.csproj AccountingService/
RUN dotnet restore AccountingService/AccountingService.csproj
COPY . .
WORKDIR /src/AccountingService
RUN dotnet build AccountingService.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish AccountingService.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AccountingService.dll"]
