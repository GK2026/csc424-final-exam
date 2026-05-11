# syntax=docker/dockerfile:1

# Build stage 
FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build

WORKDIR /src

# Copy project file and restore dependencies
COPY backend.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . .
RUN dotnet publish -c Release -o /app/publish


# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:10.0 AS runtime

WORKDIR /app

# Copy only published output (no SDK, no source code)
COPY --from=build /app/publish .

# Correct port for ASP.NET container
EXPOSE 80

# Run the application
ENTRYPOINT ["dotnet", "backend.dll"]
