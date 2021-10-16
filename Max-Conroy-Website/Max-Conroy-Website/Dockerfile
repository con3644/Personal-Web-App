FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 62144
EXPOSE 44380

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["Max-Conroy-Website/Max-Conroy-Website.csproj", "Max-Conroy-Website/"]
RUN dotnet restore "Max-Conroy-Website/Max-Conroy-Website.csproj"
COPY . .
WORKDIR "/src/Max-Conroy-Website"
RUN dotnet build "Max-Conroy-Website.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Max-Conroy-Website.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Max-Conroy-Website.dll"]