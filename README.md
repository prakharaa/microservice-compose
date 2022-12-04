
## Motivation:

To deploy existing .Net Core microservices to `docker` and then using `docker-compose`, spinning all microservices up.

## Prerequisites

- Docker Desktop 4.14.1 (91661)
- Visual Studio 2019


## Issues encountered:

- Issue 1: `Failed to compute cache key: ".csproj" not found` while running docker-compose build, 
    - https://stackoverflow.com/questions/66933949/failed-to-compute-cache-key-csproj-not-found
    - Solution - use `build` object instead of `build dockerfileParentFolder`
        > build:
        >    context: .
        >    dockerfile: GloboTicket.Services.Discount/Dockerfile

- Issue 2: `then an error occurred during the pre-login handshake.`
    - https://github.com/dotnet/SqlClient/issues/1479#issuecomment-1015587779
    
- Issue 3: `Discount MS` URL showing can't reach this page `http://localhost:5007/api/discount/code/Awesome`
    - Updated "applicationUrl": "http://localhost:5007" in launchSettings.json (https -> http)
    - Now URL shows proper response: http://localhost:5007/api/discount/code/Awesome

- Issue 4: Can't reach sql.discount DB from SSMS (outside of api.discount docker container)

## Done:
- Use mssql server container for database and mount volumn
- Start other services with DB dependencies and start using Az Message Bus
- Provide config details from compose env file

## TODO:
- Fix errors in Payment & Marketing microservices