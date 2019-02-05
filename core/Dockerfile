FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 56310
EXPOSE 44316

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["core/core.csproj", "core/"]
RUN dotnet restore "core/core.csproj"
COPY . .
WORKDIR "/src/core"
RUN dotnet build "core.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "core.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "core.dll"]