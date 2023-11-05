#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["DevOps-cp3/DevOps-cp3.csproj", "DevOps-cp3/"]
RUN dotnet restore "DevOps-cp3/DevOps-cp3.csproj"
COPY . .
WORKDIR "/src/DevOps-cp3"
RUN dotnet build "DevOps-cp3.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DevOps-cp3.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DevOps-cp3.dll"]