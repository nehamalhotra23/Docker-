FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
WORKDIR /src
COPY ["HairSalon/HairSalon.csproj", "HairSalon/"]
RUN dotnet restore "HairSalon/HairSalon.csproj"
COPY . .
WORKDIR "/src/HairSalon"
RUN dotnet build "HairSalon.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "HairSalon.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "HairSalon.dll"]
