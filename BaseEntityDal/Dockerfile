FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["BaseEntityDal/BaseEntityDal.csproj", "BaseEntityDal/"]
RUN dotnet restore "BaseEntityDal/BaseEntityDal.csproj"
COPY . .
WORKDIR "/src/BaseEntityDal"
RUN dotnet build "BaseEntityDal.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BaseEntityDal.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BaseEntityDal.dll"]
