FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Jaid.Web/Jaid.Web.csproj", "Jaid.Web/"]
RUN dotnet restore "Jaid.Web/Jaid.Web.csproj"
COPY . .
WORKDIR "/src/Jaid.Web"
RUN dotnet build "Jaid.Web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Jaid.Web.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Jaid.Web.dll"]
