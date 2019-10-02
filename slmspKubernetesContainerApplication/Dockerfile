FROM mcr.microsoft.com/dotnet/core/aspnet:2.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.1 AS build
WORKDIR /src
COPY ["slmspKubernetesContainerApplication/slmspKubernetesContainerApplication.csproj", "slmspKubernetesContainerApplication/"]

RUN dotnet restore "slmspKubernetesContainerApplication/slmspKubernetesContainerApplication.csproj"
COPY . .
WORKDIR "/src/slmspKubernetesContainerApplication"
RUN dotnet build "slmspKubernetesContainerApplication.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "slmspKubernetesContainerApplication.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "slmspKubernetesContainerApplication.dll"]