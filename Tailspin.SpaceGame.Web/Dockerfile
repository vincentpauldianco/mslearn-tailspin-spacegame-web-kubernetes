#FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
#WORKDIR /app
#EXPOSE 80

#FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
#WORKDIR /src
#COPY ["Tailspin.SpaceGame.Web/Tailspin.SpaceGame.Web.csproj", "Tailspin.SpaceGame.Web/"]

#RUN dotnet restore "Tailspin.SpaceGame.Web/Tailspin.SpaceGame.Web.csproj"
#COPY . .
#WORKDIR "/src/Tailspin.SpaceGame.Web"
#RUN dotnet build "Tailspin.SpaceGame.Web.csproj" -c Release -o /app/build

#FROM build AS publish
#RUN dotnet publish "Tailspin.SpaceGame.Web.csproj" -c Release -o /app/publish

#FROM base AS final
#WORKDIR /app
#COPY --from=publish /app/publish .
#ENTRYPOINT ["dotnet", "Tailspin.SpaceGame.Web.dll"]


FROM mcr.microsoft.com/dotnet/sdk:5.0
ARG BUILD_CONFIGURATION=Debug
ENV ASPNETCORE_ENVIRONMENT=Development
ENV ASPNETCORE_URLS=http://+:80
ENV DOTNET_USE_POLLING_FILE_WATCHER=true
EXPOSE 80

WORKDIR /src
COPY ["Tailspin.SpaceGame.Web/Tailspin.SpaceGame.Web.csproj", "Tailspin.SpaceGame.Web/"]

RUN dotnet restore "Tailspin.SpaceGame.Web/Tailspin.SpaceGame.Web.csproj"
COPY . .
WORKDIR "/src/Tailspin.SpaceGame.Web"
RUN dotnet build --no-restore "Tailspin.SpaceGame.Web.csproj" -c $BUILD_CONFIGURATION

RUN echo "exec dotnet run --no-build --no-launch-profile -c $BUILD_CONFIGURATION --" > /entrypoint.sh

ENTRYPOINT ["/bin/bash", "/entrypoint.sh"]
