FROM mcr.microsoft.com/dotnet/framework/sdk:4.8 AS build
WORKDIR /app

# copy csproj and restore as distinct layers
COPY *.csproj ./tanzu-dotnet-framework-web-mvc/
COPY *.config ./tanzu-dotnet-framework-web-mvc/
RUN nuget restore

# copy everything else and build app
COPY tanzu-dotnet-framework-web-mvc/. ./tanzu-dotnet-framework-web-mvc/
WORKDIR /app/tanzu-dotnet-framework-web-mvc
RUN msbuild /p:Configuration=Release


FROM mcr.microsoft.com/dotnet/framework/aspnet:4.8 AS runtime
WORKDIR /inetpub/wwwroot
COPY --from=build /app/tanzu-dotnet-framework-web-mvc/. ./