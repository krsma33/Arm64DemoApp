#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/runtime:6.0.16-jammy-arm64v8 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0.408-jammy-arm64v8 AS build
WORKDIR /src
COPY ["Arm64DemoApp/Arm64DemoApp.csproj", "Arm64DemoApp/"]
RUN dotnet restore "Arm64DemoApp/Arm64DemoApp.csproj"
COPY . .
WORKDIR "/src/Arm64DemoApp"
RUN dotnet build "Arm64DemoApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Arm64DemoApp.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Arm64DemoApp.dll"]