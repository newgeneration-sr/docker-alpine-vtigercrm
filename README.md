![docker build automated](https://img.shields.io/docker/cloud/automated/dotriver/vtigercrm)
![docker build status](https://img.shields.io/docker/cloud/build/dotriver/vtigercrm)
![docker build status](https://img.shields.io/docker/pulls/dotriver/vtigercrm)

# Vtiger 7.1.10

# Auto configuration parameters :

- DATABASE_HOST=localhost       ( Name of the mariadb service )
- DATABASE_PORT=3306            ( Port of the mariadb service )
- VTIGER_DB_NAME=vtiger         ( Name of the vtiger database )
- VTIGER_DB_USERNAME=vtiger     ( Username to connect to the vtiger database )
- VTIGER_DB_PASSWORD=password   ( Password to connect to the vtiger database )
- ADMIN_USERNAME=admin          ( Vtiger admin username )
- ADMIN_PASSWORD=password       ( Vtiger admin password )
- ADMIN_EMAIL=admin@exemple.org ( Vtiger admin email )

# Compose file exemple

```
version: '3'

services:

  vtigercrm:
    image: dotriver/vtigercrm
    environment:
      - DATABASE_HOST=mariadb
      - DATABASE_PORT=3306
      - VTIGER_DB_NAME=vtigercrm
      - VTIGER_DB_USERNAME=vtigercrm
      - VTIGER_DB_PASSWORD=password
      - ADMIN_USERNAME=admin
      - ADMIN_PASSWORD=password
      - ADMIN_EMAIL=admin@exemple.org
    ports:
      - 8080:80
    networks:
      default:
    volumes:
      - vtigercrm-data:/var/www/vtigercrm/
    

  mariadb:
    image: dotriver/mariadb
    environment:
      - ROOT_PASSWORD=password
      - DB_0_NAME=vtigercrm
      - DB_0_PASS=password
    ports:
      - 3306:3306
      - 8081:80
    volumes:
      - mariadb-data:/var/lib/mysql/
      - mariadb-config:/etc/mysql/
    networks:
      default:
    
volumes:
    mariadb-data:
    mariadb-config:
    vtigercrm-data:

```