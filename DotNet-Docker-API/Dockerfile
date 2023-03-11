#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["DotNet-Docker-API/DotNet-Docker-API.csproj", "DotNet-Docker-API/"]
RUN dotnet restore "DotNet-Docker-API/DotNet-Docker-API.csproj"
COPY . .
WORKDIR "/src/DotNet-Docker-API"
RUN dotnet build "DotNet-Docker-API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DotNet-Docker-API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DotNet-Docker-API.dll"]