# After completing the following steps, this code will set up the DataEntities library in the Products docker image:
    # Pull the mcr.microsoft.com/dotnet/sdk:8.0 image and name the image build.
    # Set the working directory within the image to /DataEntities.
    # Copy the file named DataEntities.csproj found locally to the /DataEntities directory that you created.
    # Call dotnet restore on the project.
    # Copy everything in the local DataEntities directory to the image.
    # Call dotnet publish on the project.

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /DataEntities
COPY "DataEntities/DataEntities.csproj" .
RUN dotnet restore
COPY "DataEntities" .
RUN dotnet publish -c release -o /app


# This code does the following steps sequentially when invoked:
   # Set the working directory within the image to /src.
   # Copy the file named Products.csproj found locally to the /src directory that you created.
   # Call dotnet restore on the project.
   # Copy everything in the local Products directory to the image.
   # Call dotnet publish on the project.

WORKDIR /src
COPY Products/Products.csproj .
RUN dotnet restore
COPY Products .
RUN dotnet publish -c release -o /app

# This code does the following steps sequentially when invoked:

   # Pull the mcr.microsoft.com/dotnet/aspnet:8.0 image.
   # Set the working directory within the image to /app.
   # Expose port 80 and 443.
   # Copy everything from the app directory of the build image you created into the app directory of this image.
   # Set the entry point of this image to dotnet and pass Products.dll as an argument.

FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
EXPOSE 80
EXPOSE 443
COPY --from=build /app .
ENTRYPOINT ["dotnet", "Products.dll"]

# Having completed the Dockerfile, the next step is to use it to create a Docker image:

    # To create the image for the Products back-end service, go to the TERMINAL tab and run this command:

        # cd ./dotnet-docker 
        # docker build -t productsbackend:latest -f Products/Dockerfile .        

        # This runs the commands in Dockerfile in the current directory and applies the tag productsbackend:latest to the resulting image.

# Entering on the terminal "docker images" to shows you a list of all images in your codespace


# To create and run a container from the new products image and expose the service on port 32001, run this command:
     # docker run -it --rm -p 32001:8080  products

# Or if you'd like to run the image you created using the Dockerfile, run:
    # docker run -it --rm -p 32001:8080 productsbackend


# To query some products, append the address with /api/product and then press Enter. You should see some product information listed in JSON format.
    # http://localhost:32001/api/product