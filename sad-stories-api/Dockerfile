FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["sad-stories-api/sad-stories-api.csproj", "sad-stories-api/"]
RUN dotnet restore "sad-stories-api/sad-stories-api.csproj"
COPY . .
WORKDIR "/src/sad-stories-api"
RUN dotnet build "sad-stories-api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "sad-stories-api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "sad-stories-api.dll"]
