# use alpine linux distro with dotnet core build tool
FROM microsoft/dotnet:2.1-sdk-alpine

# set the process to start at src
WORKDIR /src

# copy multi stage project file to src
COPY MultiStage.csproj .

# at src restore the package
# We copy only the project's manifest file first, then restore dependencies so we can benefit from Docker's layer caching
# To maximize layer re-use between builds, 
# it's important to structure the Dockerfile so that frequently changing steps (eg. ADDing code) are towards the end, 
# and less frequently changing steps (eg. RUNing apt-get install) are on top. 
#This will ensure that the steps concerned with doing the same action are not unnecessarily rebuilt. 
RUN dotnet restore MultiStage.csproj

# copy the rest from current dir to /src
COPY . .

# build the application !
RUN dotnet build MultiStage.csproj -c Release

# publish to app dir (if app dir is not present, it will auto create)
RUN dotnet publish MultiStage.csproj -c Release -o /app

# check process to work on /app this is identical to "mkdir -p /app && cd /app"
WORKDIR /app

# set web server port as environment variable
ENV ASPNETCORE_URLS http://+:5000

# expose the port
EXPOSE 5000

# at /app when the container started execute dotnet MultiStage.dll
CMD ["dotnet", "MultiStage.dll"]
