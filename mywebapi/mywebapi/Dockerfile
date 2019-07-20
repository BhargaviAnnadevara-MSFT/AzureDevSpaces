FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
WORKDIR /src
COPY ["mywebapi/mywebapi.csproj", "mywebapi/"]

RUN dotnet restore "mywebapi/mywebapi.csproj"
COPY . .
WORKDIR "/src/mywebapi"
RUN dotnet build "mywebapi.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "mywebapi.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "mywebapi.dll"]