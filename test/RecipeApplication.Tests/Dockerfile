#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

#FROM mcr.microsoft.com/dotnet/runtime:5.0 AS base
#WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["test/RecipeApplication.Tests/RecipeApplication.Tests.csproj", "test/RecipeApplication.Tests/"]
COPY ["src/RecipeApplication/RecipeApplication.csproj", "src/RecipeApplication/"]
RUN dotnet restore "test/RecipeApplication.Tests/RecipeApplication.Tests.csproj"
COPY . .
WORKDIR "/src/test/RecipeApplication.Tests"
#RUN dotnet build "RecipeApplication.Tests.csproj" -c Release -o /app/build

# FROM build AS publish
RUN dotnet publish "RecipeApplication.Tests.csproj" -c Release -o /app/publish

# FROM base AS final # Can't do this, dotnet test is only available in the sdk
WORKDIR /app
#COPY --from=publish /app/publish .
COPY /app/publish .
ENTRYPOINT ["dotnet", "test"]