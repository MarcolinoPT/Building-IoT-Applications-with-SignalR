#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Building IoT Applications with SignalR/Building IoT Applications with SignalR.csproj", "Building IoT Applications with SignalR/"]
RUN dotnet restore "Building IoT Applications with SignalR/Building IoT Applications with SignalR.csproj"
COPY . .
WORKDIR "/src/Building IoT Applications with SignalR"
RUN dotnet build "Building IoT Applications with SignalR.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Building IoT Applications with SignalR.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Building IoT Applications with SignalR.dll"]