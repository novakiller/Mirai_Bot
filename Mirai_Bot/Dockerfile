#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

#FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
FROM mcr.microsoft.com/dotnet/aspnet:6.0.0-rc.1-focal-arm64v8 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

#FROM mcr.microsoft.com/dotnet/sdk:6.0-focal-arm32v7 AS build
FROM mcr.microsoft.com/dotnet/sdk:6.0.100-rc.1-focal-arm64v8 AS build
WORKDIR /src
COPY ["/Mirai_Bot.csproj", "Mirai_Bot/"]
RUN dotnet restore "Mirai_Bot/Mirai_Bot.csproj"
COPY . .
WORKDIR "/src/Mirai_Bot"
RUN dotnet build "Mirai_Bot.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Mirai_Bot.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Mirai_Bot.dll"]