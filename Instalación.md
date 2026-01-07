 

## 1. Preparación del Entorno

MySQL tiene más dependencias de compilación que Postgres. Necesitarás herramientas de C++ y la librería **Boost**.

```bash
sudo apt update
sudo apt install cmake expat libncurses5-dev libssl-dev build-essential zlib1g-dev pkg-config libtirpc-dev

```

## 2. Descarga y Configuración (El equivalente a `./configure`)

En lugar de `./configure`, usamos `cmake`. El parámetro `-DCMAKE_INSTALL_PREFIX` es el equivalente exacto a tu `--prefix` de Postgres.

```bash
# Descargar el source (Asegúrate de buscar la versión más reciente, ej. 8.4 o 9.x)
wget https://dev.mysql.com/get/Downloads/MySQL-8.4/mysql-8.4.0.tar.gz
tar -xvf mysql-8.4.0.tar.gz
cd mysql-8.4.0

# Crear un directorio para la compilación (Buena práctica en CMake)
mkdir build && cd build

# Configurar la compilación
cmake .. \
-DCMAKE_INSTALL_PREFIX=/opt/mysql \
-DMYSQL_DATADIR=/opt/mysql/data \
-DSYSCONFDIR=/opt/mysql/etc \
-DWITH_SSL=system \
-DWITH_ZLIB=system \
-DDEFAULT_CHARSET=utf8mb4 \
-DDEFAULT_COLLATION=utf8mb4_general_ci \
-DFORCE_INSOURCE_BUILD=1 \
-DDOWNLOAD_BOOST=1 \
-DWITH_BOOST=../boost 

```

## 3. Compilación e Instalación

Este paso es idéntico a lo que ya conoces.

```bash
make -j$(nproc)       # El -j usa todos tus núcleos para ir más rápido
sudo make install

```

---

## 4. Inicialización del Cluster (El equivalente a `initdb`)

En PostgreSQL usas `initdb -D /ruta/data`. En MySQL, el comando moderno es `mysqld --initialize`.

Primero, por seguridad, crea un usuario dedicado (igual que el usuario `postgres`):

```bash
sudo groupadd mysql
sudo useradd -r -g mysql -s /bin/false mysql

# Crear el directorio de datos y dar permisos
sudo mkdir /opt/mysql/data
sudo chown -R mysql:mysql /opt/mysql

```

Ahora, ejecutamos la **inicialización**:

```bash
sudo /opt/mysql/bin/mysqld --initialize --user=mysql --basedir=/opt/mysql --datadir=/opt/mysql/data

```

> **Nota importante:** A diferencia de `initdb`, MySQL generará una **contraseña temporal** para el usuario `root` que verás en la terminal o en el archivo de log. ¡Guárdala!

---

## 5. Diferencias clave que debes considerar como experto en Postgres

| Característica | PostgreSQL (Source) | MySQL (Source) |
| --- | --- | --- |
| **Herramienta de Construcción** | `make` (Autotools) | `cmake` |
| **Comando de Inicio** | `initdb` | `mysqld --initialize` |
| **Configuración** | `postgresql.conf` | `my.cnf` |
| **Instancias** | Un cluster = Un `initdb` | Un cluster = Un `mysqld` con su `datadir` |
| **Socket** | `/tmp` o `/var/run/postgresql` | Se define en `my.cnf` (ej. `/opt/mysql/mysql.sock`) |

---

## 6. Puesta en marcha

Para arrancar tu nueva instalación limpia, no dependas de los scripts de `apt`. Puedes lanzarlo directamente para probar:

```bash
sudo /opt/mysql/bin/mysqld_safe --user=mysql &

```

Y para entrar a la consola:

```bash
/opt/mysql/bin/mysql -u root -p

```

### ¿Por qué esto es mejor?

1. **Aislamiento:** Todo (binarios, logs, datos, configs) vive dentro de `/opt/mysql`. Si quieres borrar MySQL, solo haces `rm -rf /opt/mysql`.
2. **Portabilidad:** Puedes mover esa carpeta `/opt/mysql` a otro servidor con la misma arquitectura y funcionará casi de inmediato.
3. **Versiones múltiples:** Puedes tener `/opt/mysql_8.4` y `/opt/mysql_9.0` corriendo en puertos distintos sin que sus librerías choquen.
 
