#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["DVDStore.Api/DVDStore.Api.csproj", "DVDStore.Api/"]
RUN dotnet restore "DVDStore.Api/DVDStore.Api.csproj"
COPY . .
WORKDIR "/src/DVDStore.Api"
RUN dotnet build "DVDStore.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DVDStore.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DVDStore.Api.dll"]
