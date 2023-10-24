# Umbraco 12 Docker Image &middot; [![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](../LICENSE.md) [![Docker Image CI](https://github.com/alexsee/umbraco-container/actions/workflows/docker-image.yml/badge.svg)](https://github.com/alexsee/umbraco-container/actions/workflows/docker-image.yml)

This repository provides a simple Umbraco project template with build scripts for docker images.
You can run your Umbraco instance as a docker container with easy upgrade capabilities (i.e., just exchange the image).

## Additional installed packages
* uSync Complete Edition

## Example docker-compose.yml
```
version: '3.7'
name: "umbraco"
services:
  umbraco-container:
    container_name: umbraco-12
    image: ghcr.io/alexsee/umbraco-container:latest
    restart: always
    entrypoint: ["dotnet", "UmbracoContainer.dll", "--urls", "http://0.0.0.0"]
    ports:
      - "82:80"
    volumes:
      - umbraco_data:/Logs:/output/umbraco/Logs
      - umbraco_data:/uSync:/output/uSync
      - umbraco_data:/Views:/output/Views
      - umbraco_data:/wwwroot/css:/output/wwwroot/css
      - umbraco_data:/wwwroot/fonts:/output/wwwroot/fonts
      - umbraco_data:/wwwroot/media:/output/wwwroot/media
      - umbraco_data:/appsettings.json:/output/appsettings.json
      - umbraco_data:/Data:/output/umbraco/Data

volumes: 
  umbraco_data:
```

**Note**: The docker-compose example maps the relevant subfolders of `wwwroot` to a local folder / docker volume individually. If you include the entire `wwwroot` directory, this can lead to upgrade issues since the container image itself contains the `wwwroot/umbraco` directory. Therefore, only include additional folders and files here such as the `css`, `media`, or `scripts` folders separately.
