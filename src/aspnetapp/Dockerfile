# Learn about building tets .NET container images:
# https://github.com/dotnet/dotnet-docker/blob/main/samples/README.md
FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build
WORKDIR /src

# Copy solution and project files
COPY ["aspnetapp.csproj", "src/aspnetapp/"]

# Restore dependencies
RUN dotnet restore "src/aspnetapp/aspnetapp.csproj"

# Copy remaining source code
COPY . .

# Publish the app
RUN dotnet publish "src/aspnetapp/aspnetapp.csproj" -c Release -o /app/publish

# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:10.0
EXPOSE 8080
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "aspnetapp.dll"]