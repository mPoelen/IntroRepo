#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["DeployAPI.csproj", "."]
RUN dotnet restore "./DeployAPI.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "DeployAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DeployAPI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DeployAPI.dll"]

#FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build-env
#WORKDIR /app
#
#COPY *.csproj ./
#RUN dotnet restore
#
#COPY . ./
#RUN dotnet publish -c Release -o out
#
#FROM mcr.microsoft.com/dotnet/core/sdk:2.2 
#WORKDIR /app
#EXPOSE 80
#COPY --from=build-env /app/out .
#ENTRYPOINT ["dotnet", "DockerAPI.dll"]
