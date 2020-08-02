#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["Blazor-Accelerometer-Example/Blazor-Accelerometer-Example.csproj", "Blazor-Accelerometer-Example/"]
RUN dotnet restore "Blazor-Accelerometer-Example/Blazor-Accelerometer-Example.csproj"
COPY . .
WORKDIR "/src/Blazor-Accelerometer-Example"
RUN dotnet build "Blazor-Accelerometer-Example.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Blazor-Accelerometer-Example.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Blazor-Accelerometer-Example.dll"]