#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["Avanade.SubTCSE.Projeto.API/Avanade.SubTCSE.Projeto.API.csproj", "Avanade.SubTCSE.Projeto.API/"]
RUN dotnet restore "Avanade.SubTCSE.Projeto.API/Avanade.SubTCSE.Projeto.API.csproj"
COPY . .
WORKDIR "/src/Avanade.SubTCSE.Projeto.API"
RUN dotnet build "Avanade.SubTCSE.Projeto.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Avanade.SubTCSE.Projeto.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Avanade.SubTCSE.Projeto.API.dll"]