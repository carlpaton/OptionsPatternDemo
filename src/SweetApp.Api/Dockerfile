FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["src/SweetApp.Api/SweetApp.Api.csproj", "src/SweetApp.Api/"]
RUN dotnet restore "src/SweetApp.Api/SweetApp.Api.csproj"
COPY . .
WORKDIR "/src/src/SweetApp.Api"
RUN dotnet build "SweetApp.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SweetApp.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SweetApp.Api.dll"]