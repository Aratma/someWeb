FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["someWeb/someWeb.csproj", "someWeb/"]
RUN dotnet restore "someWeb/someWeb.csproj"
COPY . .
WORKDIR "/src/someWeb"
RUN dotnet build "someWeb.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "someWeb.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "someWeb.dll"]