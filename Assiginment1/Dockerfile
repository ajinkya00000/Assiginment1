#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Assiginment1/Assiginment1.csproj", "Assiginment1/"]
RUN dotnet restore "Assiginment1/Assiginment1.csproj"
COPY . .
WORKDIR "/src/Assiginment1"
RUN dotnet build "Assiginment1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Assiginment1.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Assiginment1.dll"]