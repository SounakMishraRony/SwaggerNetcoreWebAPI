FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["SwaggerWeather/SwaggerWeather.csproj", "SwaggerWeather/"]
RUN dotnet restore "ContailerApp/SwaggerWeather.csproj"
COPY . .
WORKDIR "/src/SwaggerWeather"
RUN dotnet build "SwaggerWeather.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SwaggerWeather.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SwaggerWeather.dll"]