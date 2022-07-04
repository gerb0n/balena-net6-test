#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

#FROM balenalib/amd64-dotnet:6.0-aspnet AS base
FROM balenalib/raspberrypi4-64-dotnet:6.0-aspnet AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

#FROM balenalib/amd64-dotnet:6.0-sdk AS build
FROM balenalib/raspberrypi4-64-dotnet:6.0-sdk AS build
WORKDIR /src
COPY ["Balena-Net6-Test.Api/Balena-Net6-Test.Api.csproj", "Balena-Net6-Test.Api/"]
RUN dotnet restore "Balena-Net6-Test.Api/Balena-Net6-Test.Api.csproj"
COPY . .
WORKDIR "/src/Balena-Net6-Test.Api"
RUN dotnet build "Balena-Net6-Test.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Balena-Net6-Test.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Balena-Net6-Test.Api.dll"]

