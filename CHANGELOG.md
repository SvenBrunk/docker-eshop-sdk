# Change Log for OXID eShop SDK

All notable changes to this project will be documented in this file.
The format is based on [Keep a Changelog](http://keepachangelog.com/)
and this project adheres to [Semantic Versioning](http://semver.org/).

## [v4.1.0] - Unreleased

### Added
- Expose mysql port 3306 to access mysql from outside the docker network
- Added deprecated xdebug 2 configuration for php 7.4
- Add NGINX_SERVER_CONFIG_DIR environment variable to nginx configuration directory
- Add NODE_VERSION environment variable for configuring the node container version
- Changed the deprecated image selenium/standalone-chrome-debug:3.141.59 to selenium/standalone-chrome:latest
- Confirmation question on `cleanup` command to avoid accidental data loss

### Changed
- Default Nginx configuration directory changed to fit development practices
- Replace Mailhog with Mailpit service
- Extended MySQL healthcheck time to give chance for slower systems
- Extracted the variables with exposed PORTS to the env file, so it can be easier adjusted [PR-34](https://github.com/OXID-eSales/docker-eshop-sdk/pull/34)

### Fixed
- Ensure having the host user and group as file owner in node container
- Replace echo with printf to make it work on Fedora
- Improved the `make cleanup` command to cleanup better on partial file existance
- Remove obsolete "version" option from docker-compose.yml.dist file
- Remove redundant spaces in .env file [PR-33](https://github.com/OXID-eSales/docker-eshop-sdk/pull/33)

## [v4.0.0] - 2022-01-11

### Added
- Github is trusted by default
- Added environment variable for MySQL version
- Add NGINX container building Dockerfile
- Add NGINX as reverse-proxy service
- Add preconfigured Elasticsearch + Kibana services
- Add self-signed certificate with supported localhost.local and oxideshop.local domains
- `make cleanup` command with all main artifacts removal to clean default state (composer cache is not cleared for now)

### Changed
- PHP container is now based on oxidesales/oxideshop-docker-php
- Renamed directory from "php-fpm" to "php"
- Extended description
- Do not cache local .user.ini values

### Removed
- SPX is not installed by default anymore
- .env file php version default value fixed

### Fixed
- xDebug host calculation configuration improved to work on Mac and Windows WSL too

## [v3.0.0] - 2022-02-04

### Added
- PHP_VERSION as environment variable
- Example recipe to install example scripts :) The idea is to create multiple different recipes in the future
- Possibility to build specific docker-compose.yml file with console command!
  - The file can be build by merging separate smaller chunks (services) together
  - The ``make addservice`` command introduced. Example of usage: ``make file=services/apache.yml addservice``

### Changed
- Example files moved to `recipes/default/examples` directory
  - Files will be copied during the example recipe - ``make example``.
- Default docker-compose.yml.dist have been split to multiple service files and moved to services directory
  - Now, no services are installed by default anymore, but rather, use the ``make addservice`` to add specific services
  - To add all basic services (php, mysql and apache), the ``make addbasicservices`` command can be used

### Fixed
- Readme adjusted by latest changes, please, read from the start, again.

## [v2.0.0] - 2021-12-12

### Added
- PHP 8.0 and PHP 8.1 containers!
- Register a link to apache container for the php container (so its possible to ping one by url)

### Changed
- Base container repositories renamed to siegfuse/php-fpm-X.X-base where (X.X is php version)
- ``latest`` tag of base container is used by default
- Move SPX package installation to base php container. 
  - 7.4 base container rebuilt with latest dependencies and spx.
  - It will allow faster start of the environment.
- ``containers/php/user.ini`` is renamed to custom.ini.dist. Setup copies it to custom.ini 

### Fixed
- Fix wrong rights for ~/.composer directory. Now composer commands will work properly.

## [v1.4.0] - 2021-11-20

### Added
- Copy ``containers/httpd/project.conf.dist`` to ``containers/httpd/project.conf`` during ``make setup``
- Copy ``docker-compose.yml.dist`` to ``docker-compose.yml`` during ``make setup``

### Changed
- Rename project.conf to project.conf.dist
- Updated the php-fpm image, so it have:
  - composer version 2
  - xDebug 3
- Use node latest

### Fixed
- Configure remote debugging on xDebug 3
- Fix wrong rights on volume synced directory in home of php container
- Update default server for adminer
- Remove node container after use

## [v1.3.0] - 2021-06-04

### Added
- Preconfigure SPX - simple php profiler

### Changed
- Mysql data is now saved between session. Mysql databases are synced to the host system in `data/mysql` directory

## [v1.2.0] - 2021-03-18

### Added
- Mailhog container preconfigured in docker-compose
- Example with php sending email added
- Makefile command ``make php`` to access bash on php container

### Changed
- Reconfigured php log and profiler paths to be always available and no additional configuration required. Available in `data/php` directory.

## [v1.1.0] - 2021-03-16

### Added
- Makefile with main commands:
    - preconfigure with ``make setup``
    - start containers with ``make up``
    - stop containers with ``make down``

## [v1.0.0] - 2019-10-23

[v4.1.0]: https://github.com/OXID-eSales/docker-eshop-sdk/compare/v4.0.0...master
[v4.0.0]: https://github.com/OXID-eSales/docker-eshop-sdk/compare/v3.0.0...v4.0.0
[v3.0.0]: https://github.com/OXID-eSales/docker-eshop-sdk/compare/v2.0.0...v3.0.0
[v2.0.0]: https://github.com/OXID-eSales/docker-eshop-sdk/compare/v1.4.0...v2.0.0
[v1.4.0]: https://github.com/OXID-eSales/docker-eshop-sdk/compare/v1.3.0...v1.4.0
[v1.3.0]: https://github.com/OXID-eSales/docker-eshop-sdk/compare/v1.2.0...v1.3.0
[v1.2.0]: https://github.com/OXID-eSales/docker-eshop-sdk/compare/v1.1.0...v1.2.0
[v1.1.0]: https://github.com/OXID-eSales/docker-eshop-sdk/compare/v1.0.0...v1.1.0
[v1.0.0]: https://github.com/OXID-eSales/docker-eshop-sdk/020f452b2a...v1.0.0
