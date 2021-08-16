#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["DanceCool.Web/DanceCool.Web.csproj", "DanceCool.Web/"]
RUN dotnet restore "DanceCool.Web/DanceCool.Web.csproj"
COPY . .
WORKDIR "/src/DanceCool.Web"
RUN dotnet build "DanceCool.Web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DanceCool.Web.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DanceCool.Web.dll"]