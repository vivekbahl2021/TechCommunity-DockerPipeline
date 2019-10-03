FROM mcr.microsoft.com/dotnet/core/runtime:2.2-stretch-slim AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["HelloWorld.csproj", ""]
RUN dotnet restore "./HelloWorld.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "HelloWorld.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "HelloWorld.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "HelloWorld.dll"]