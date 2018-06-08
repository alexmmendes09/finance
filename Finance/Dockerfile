FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY Finance/Finance.csproj Finance/
RUN dotnet restore Finance/Finance.csproj
COPY . .
WORKDIR /src/Finance
RUN dotnet build Finance.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Finance.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Finance.dll"]
