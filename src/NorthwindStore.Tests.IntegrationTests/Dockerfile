#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["nuget.config", "."]
COPY ["packages/", "packages/"]
COPY ["NorthwindStore.Tests.IntegrationTests/NorthwindStore.Tests.IntegrationTests.csproj", "NorthwindStore.Tests.IntegrationTests/"]
COPY ["NorthwindStore.App/NorthwindStore.App.csproj", "NorthwindStore.App/"]
COPY ["NorthwindStore.DAL/NorthwindStore.DAL.csproj", "NorthwindStore.DAL/"]
COPY ["NorthwindStore.BL/NorthwindStore.BL.csproj", "NorthwindStore.BL/"]
RUN dotnet restore "NorthwindStore.Tests.IntegrationTests/NorthwindStore.Tests.IntegrationTests.csproj"
COPY . .
WORKDIR "/src/NorthwindStore.Tests.IntegrationTests"
RUN dotnet build "NorthwindStore.Tests.IntegrationTests.csproj"
ENTRYPOINT dotnet test "NorthwindStore.Tests.IntegrationTests.csproj" --no-build