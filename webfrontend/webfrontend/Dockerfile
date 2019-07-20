FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
WORKDIR /src
COPY ["webfrontend/webfrontend.csproj", "webfrontend/"]

RUN dotnet restore "webfrontend/webfrontend.csproj"
COPY . .
WORKDIR "/src/webfrontend"
RUN dotnet build "webfrontend.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "webfrontend.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "webfrontend.dll"]