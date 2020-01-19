FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["TestDockerFile.csproj", "TestDockerFile/"]
RUN dotnet restore "TestDockerFile/TestDockerFile.csproj"
COPY . .
WORKDIR "/src/TestDockerFile"
RUN dotnet build "TestDockerFile.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "TestDockerFile.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TestDockerFile.dll"]