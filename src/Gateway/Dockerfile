# Stage 1
FROM mcr.microsoft.com/dotnet/nightly/sdk:8.0 as build
WORKDIR /app
COPY src/Gateway src/Gateway
RUN dotnet build src/Gateway

# Stage 2
FROM build as publish
WORKDIR /app
RUN dotnet publish src/Gateway -c Release -o /app -r linux-x64

# Stage 3
FROM mcr.microsoft.com/dotnet/nightly/runtime:8.0 AS runtime
WORKDIR /app
COPY --from=publish /app .
CMD dotnet Gateway.dll