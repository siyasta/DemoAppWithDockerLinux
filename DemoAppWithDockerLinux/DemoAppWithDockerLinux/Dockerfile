FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 62316
EXPOSE 44396

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["DemoAppWithDockerLinux/DemoAppWithDockerLinux.csproj", "DemoAppWithDockerLinux/"]
RUN dotnet restore "DemoAppWithDockerLinux/DemoAppWithDockerLinux.csproj"
COPY . .
WORKDIR "/src/DemoAppWithDockerLinux"
RUN dotnet build "DemoAppWithDockerLinux.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "DemoAppWithDockerLinux.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DemoAppWithDockerLinux.dll"]