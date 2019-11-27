FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["EESite/EESite.csproj", "EESite/"]
RUN dotnet restore "EESite/EESite.csproj"
COPY . .
WORKDIR "/src/EESite"
RUN dotnet build "EESite.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "EESite.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "EESite.dll"]