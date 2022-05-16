# Build image based on aspnet:5.0
# Multi stage build -
# Stage Called base
# https://hub.docker.com/_/microsoft-dotnet-aspnet
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

ENV ASPNETCORE_URLS=http://+:80
ENV ASPNETCORE_ENVIRONMENT=Development

# Stage build
# https://hub.docker.com/_/microsoft-dotnet-sdk
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
# Copy ServiceA.Api.csproj from project and place it under /src folder
COPY ["ServiceA.Api.csproj", "./"]
# Run command to restore project dependencies (nuget packages)
RUN dotnet restore "ServiceA.Api.csproj"
# Copy all files from project root to /src
COPY . .
WORKDIR "/src/."
# Build App as release and set output to /app/build
RUN dotnet build "ServiceA.Api.csproj" -c Release -o /app/build

# Stage publish from build
FROM build AS publish
# Run command to publish app to create excect files
RUN dotnet publish "ServiceA.Api.csproj" -c Release -o /app/publish

# Stage final from base
FROM base AS final
WORKDIR /app
# Copy files /app/publish to /app
COPY --from=publish /app/publish .
# Define Entry point dotnet ServiceA.Api.dll command
ENTRYPOINT ["dotnet", "ServiceA.Api.dll"]
