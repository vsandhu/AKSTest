FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["AKSTest/AKSTest.csproj", "AKSTest/"]
RUN dotnet restore "AKSTest/AKSTest.csproj"
COPY . .
WORKDIR "/src/AKSTest"
RUN dotnet build "AKSTest.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "AKSTest.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AKSTest.dll"]