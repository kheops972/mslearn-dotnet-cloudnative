FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
RUN apt-get update && apt-get install -y ca-certificates

WORKDIR /DataEntities
COPY ["./eShopLite/DataEntities/DataEntities.csproj", "./"]
RUN dotnet restore
COPY "./eShopLite/DataEntities" .
RUN dotnet publish -c release -o /app

WORKDIR /src
COPY ["./eShopLite/Products/Products.csproj", "./"]
RUN dotnet restore
COPY "./eShopLite/Products" .
RUN dotnet publish -c release -o /app

FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
EXPOSE 8080
EXPOSE 443
COPY --from=build /app .
ENTRYPOINT ["dotnet", "Products.dll"]