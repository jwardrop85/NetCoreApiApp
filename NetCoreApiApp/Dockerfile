FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["NetCoreApiApp/NetCoreApiApp.csproj", "NetCoreApiApp/"]
RUN dotnet restore "NetCoreApiApp/NetCoreApiApp.csproj"
COPY . .
WORKDIR "/src/NetCoreApiApp"
RUN dotnet build "NetCoreApiApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "NetCoreApiApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "NetCoreApiApp.dll"]