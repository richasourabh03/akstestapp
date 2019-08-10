FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["akstestapp/akstestapp.csproj", "akstestapp/"]
RUN dotnet restore "akstestapp/akstestapp.csproj"
COPY . .
WORKDIR "/src/akstestapp"
RUN dotnet build "akstestapp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "akstestapp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "akstestapp.dll"]