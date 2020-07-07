#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["TinyApi/TinyApi.csproj", "TinyApi/"]
RUN dotnet restore "TinyApi/TinyApi.csproj"
COPY . .
WORKDIR "/src/TinyApi"
RUN dotnet build "TinyApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TinyApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TinyApi.dll"]