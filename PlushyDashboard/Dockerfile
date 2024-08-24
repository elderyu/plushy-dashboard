FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["PlushyDashboard/PlushyDashboard.csproj", "PlushyDashboard/"]
RUN dotnet restore "PlushyDashboard/PlushyDashboard.csproj"
COPY . .
WORKDIR "/src/PlushyDashboard"
RUN dotnet build "PlushyDashboard.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PlushyDashboard.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PlushyDashboard.dll"]
