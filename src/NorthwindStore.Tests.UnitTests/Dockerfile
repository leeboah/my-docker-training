#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["nuget.config", "."]
COPY ["packages/", "packages/"]
COPY ["NorthwindStore.Tests.UnitTests/NorthwindStore.Tests.UnitTests.csproj", "NorthwindStore.Tests.UnitTests/"]
COPY ["NorthwindStore.BL/NorthwindStore.BL.csproj", "NorthwindStore.BL/"]
COPY ["NorthwindStore.DAL/NorthwindStore.DAL.csproj", "NorthwindStore.DAL/"]
RUN dotnet restore "NorthwindStore.Tests.UnitTests/NorthwindStore.Tests.UnitTests.csproj"
COPY . .
WORKDIR "/src/NorthwindStore.Tests.UnitTests"
RUN dotnet build "NorthwindStore.Tests.UnitTests.csproj"
ENTRYPOINT dotnet test NorthwindStore.Tests.UnitTests.csproj --no-build