#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["ServiceInvocation/Stock.Api/Stock.Api.csproj", "ServiceInvocation/Stock.Api/"]
RUN dotnet restore "ServiceInvocation/Stock.Api/Stock.Api.csproj"
COPY . .
WORKDIR "/src/ServiceInvocation/Stock.Api"
RUN dotnet build "Stock.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Stock.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Stock.Api.dll"]