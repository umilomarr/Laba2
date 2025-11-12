# --- Стадия сборки (build) ---
FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src

# Копируем и восстанавливаем зависимости
COPY *.csproj .
RUN dotnet restore

# Копируем и публикуем приложение
COPY . .
RUN dotnet publish -c Release -o /app/publish

# --- Стадия выполнения (runtime) ---
FROM mcr.microsoft.com/dotnet/aspnet:9.0-alpine
WORKDIR /app

# Копируем только опубликованные файлы
COPY --from=build /app/publish .

EXPOSE 8080
ENTRYPOINT ["dotnet", "WebApplication.dll"]
