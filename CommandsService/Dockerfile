# Use the official Microsoft .NET SDK image as the base image
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build-env

# Set the working directory
WORKDIR /app

# Copy the project files into the container
COPY *csproj .

# Restore the dependencies
RUN dotnet restore

COPY . ./

# Build the project
RUN dotnet build --configuration Release

# Publish the project
RUN dotnet publish --configuration Release --output out

# Set the runtime image
FROM mcr.microsoft.com/dotnet/aspnet:6.0

# Set the working directory
WORKDIR /app

# Copy the output from the build image
COPY --from=build-env /app/out .

# Set the entry point for the container
ENTRYPOINT ["dotnet", "CommandsService.dll"]