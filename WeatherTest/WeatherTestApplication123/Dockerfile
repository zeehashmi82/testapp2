FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 81
EXPOSE 80

EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["WeatherTestApplication123/WeatherTestApplication123.csproj", "WeatherTestApplication123/"]
RUN dotnet restore "WeatherTestApplication123/WeatherTestApplication123.csproj"
COPY . .
WORKDIR "/src/WeatherTestApplication123"
RUN dotnet build "WeatherTestApplication123.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WeatherTestApplication123.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WeatherTestApplication123.dll"]
