FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["Kubernetes5/Kubernetes5.csproj", "Kubernetes5/"]

RUN dotnet restore "Kubernetes5/Kubernetes5.csproj"
COPY . .
WORKDIR "/src/Kubernetes5"
RUN dotnet build "Kubernetes5.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Kubernetes5.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Kubernetes5.dll"]