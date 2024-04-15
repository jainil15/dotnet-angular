FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build-env
WORKDIR /App
# Copy everything
COPY . ./
# Restore as distinct layers
RUN dotnet restore
# Build and publish a release
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /App
COPY --from=build-env /App/out .
COPY ./openiddict.pfx ./openiddict.pfx
ENV ConnectionStrings__Default "Host=aws-0-ap-south-1.pooler.supabase.com;Port=5432;Database=postgres;Username=postgres.gxktohfiumetxtmcsetv;Password=jainil115asdf;"
ENV App__CorsOrigins "https://localhost:4200,http://localhost:8080,https://3.109.208.80,https://localhost,"

EXPOSE 8080
ENTRYPOINT ["dotnet", "Promact.CustomerSuccess.Platform.dll"]
