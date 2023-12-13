FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["Reptil/Reptil.csproj", "Reptil/"]
RUN dotnet restore "Reptil/Reptil.csproj"
COPY . .
WORKDIR "/src/Reptil"
RUN dotnet build "Reptil.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Reptil.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Reptil.dll"]
