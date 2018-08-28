FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 40051
EXPOSE 44382

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["DotnetCoreWithVue/DotnetCoreWithVue.csproj", "DotnetCoreWithVue/"]
RUN dotnet restore "DotnetCoreWithVue/DotnetCoreWithVue.csproj"
COPY . .
WORKDIR "/src/DotnetCoreWithVue"
RUN dotnet build "DotnetCoreWithVue.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "DotnetCoreWithVue.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DotnetCoreWithVue.dll"]