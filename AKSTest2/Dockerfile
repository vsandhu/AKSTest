FROM mcr.microsoft.com/dotnet/core/runtime:2.2-stretch-slim AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["AKSTest2/AKSTest2.csproj", "AKSTest2/"]
RUN dotnet restore "AKSTest2/AKSTest2.csproj"
COPY . .
WORKDIR "/src/AKSTest2"
RUN dotnet build "AKSTest2.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "AKSTest2.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AKSTest2.dll"]