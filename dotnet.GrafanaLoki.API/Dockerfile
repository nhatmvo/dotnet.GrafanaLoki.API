#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["dotnet.GrafanaLoki.API/dotnet.GrafanaLoki.API.csproj", "dotnet.GrafanaLoki.API/"]
RUN dotnet restore "dotnet.GrafanaLoki.API/dotnet.GrafanaLoki.API.csproj"
COPY . .
WORKDIR "/src/dotnet.GrafanaLoki.API"
RUN dotnet build "dotnet.GrafanaLoki.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "dotnet.GrafanaLoki.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "dotnet.GrafanaLoki.API.dll"]