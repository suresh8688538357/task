FROM mcr.microsoft.com/dotnet/sdk:7.0 as BUILD
WORKDIR /app
This is base img as build in that /app anaa oka directory will create 

# Copy the project file(s) and restore dependencies into present working directory
COPY ./*.csproj ./
RUN dotnet restore

# Copy the entire project directory to the container
COPY . ./

# Build the application
Run dotnet build

publish the application into release as output
RUN dotnet publish -c Release -o out

# Stage 2: Create the runtime image
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS runtime
WORKDIR /app

image should be light weight so we took another one in that /app anaa directory will be created

# Copy the published output from the build stage to the runtime stage
COPY --from=build /app/out .

# Set the entry point for the application
ENTRYPOINT ["dotnet", "HelloWorldApp.Web.dll"]




