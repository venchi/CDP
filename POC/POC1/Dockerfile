FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 64344
EXPOSE 44303

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["POC1/POC1.csproj", "POC1/"]
RUN dotnet restore "POC1/POC1.csproj"
COPY . .
WORKDIR "/src/POC1"
RUN dotnet build "POC1.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "POC1.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "POC1.dll"]