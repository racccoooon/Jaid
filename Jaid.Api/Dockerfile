FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Jaid.Api/Jaid.Api.csproj", "Jaid.Api/"]
RUN dotnet restore "Jaid.Api/Jaid.Api.csproj"
COPY . .
WORKDIR "/src/Jaid.Api"
RUN dotnet build "Jaid.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Jaid.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Jaid.Api.dll"]
