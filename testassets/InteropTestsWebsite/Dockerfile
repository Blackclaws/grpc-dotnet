FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build-env
WORKDIR /app

# Copy everything
COPY . ./
RUN dotnet --info
RUN dotnet restore testassets/InteropTestsWebsite
RUN dotnet publish testassets/InteropTestsWebsite --framework net7.0 -c Release -o out -p:LatestFramework=true

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:7.0
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "InteropTestsWebsite.dll", "--port_http1", "80"]