FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY WebApplication1/WebApplication1.csproj WebApplication1/
COPY ClassLibrary1/ClassLibrary1.csproj ClassLibrary1/
RUN dotnet restore WebApplication1/WebApplication1.csproj
COPY . .
WORKDIR /src/WebApplication1
RUN dotnet build WebApplication1.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish WebApplication1.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebApplication1.dll"]
