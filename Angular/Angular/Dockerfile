FROM microsoft/aspnetcore-build:latest AS build-env
WORKDIR /


# copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

# build runtime image
FROM microsoft/aspnetcore:latest
COPY --from=build-env /app/out /app
WORKDIR /app
#RUN npm restore
EXPOSE 5000
ENTRYPOINT ["dotnet", "Angular.dll"]