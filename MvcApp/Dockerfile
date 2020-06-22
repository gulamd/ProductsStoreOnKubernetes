FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY "MvcApp.csproj" .
RUN dotnet restore "MvcApp.csproj"  #restore the depenencies and project related tools
COPY . .
RUN dotnet build . -c Release -o /app/build   # it will generate .dll pkg

FROM build AS publish
RUN dotnet publish "MvcApp.csproj" -c Release -o /app/publish      #it will complile the app and reads dependencies and project files

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MvcApp.dll"]
