FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
COPY ["CrashApi/CrashApi.csproj", "CrashApi/"]
RUN dotnet restore "CrashApi/CrashApi.csproj"
COPY . .
WORKDIR "/CrashApi"
RUN dotnet build "CrashApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CrashApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CrashApi.dll"]