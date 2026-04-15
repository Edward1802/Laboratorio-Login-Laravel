# Guía de Pasos - Instalación y Configuración de Laravel

Esta guía documenta todos los pasos necesarios para instalar Composer, Laravel y ejecutar este proyecto.

---

## 1. Requisitos Previos

Antes de comenzar, asegúrate de tener instalados:

- **PHP 8.3** o superior
- **Composer** (gestor de dependencias de PHP)
- **Node.js y npm** (para compilar assets del frontend)
- **Git** (opcional, pero recomendado)
- Un servidor web como **Apache** (WAMP, LAMP) o usar el servidor integrado de Laravel

---

## 2. Instalación de Composer

### En Windows:

1. Descarga el instalador desde [getcomposer.org](https://getcomposer.org/download/)
2. Ejecuta el instalador `.exe` y sigue las instrucciones
3. Verifica la instalación:
   ```bash
   composer --version
   ```

### En macOS/Linux:

```bash
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer
composer --version
```

---

## 3. Instalación de Laravel

### Opción A: Crear un nuevo proyecto desde cero (si no existe)

```bash
composer create-project laravel/laravel nombre-proyecto
cd nombre-proyecto
```

### Opción B: Usar un proyecto existente (como este)

Si el proyecto ya existe, solo necesitas instalar las dependencias:

```bash
cd c:\wamp64\www\labLaravelLogin7
composer install
```

---

## 4. Configuración del Proyecto

### 4.1 Copiar archivo `.env`

```bash
cp .env.example .env
```

Si no existe `.env.example`, crea uno manualmente basado en `config/app.php`, `config/database.php`, etc.

### 4.2 Generar clave de aplicación

```bash
php artisan key:generate
```

### 4.3 Configurar la base de datos

Edita el archivo `.env` y configura:

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=nombre_bd
DB_USERNAME=root
DB_PASSWORD=
```

### 4.4 Ejecutar migraciones

```bash
php artisan migrate
```

Si necesitas revertir migraciones:

```bash
php artisan migrate:rollback
```

---

## 5. Instalación de Dependencias de Frontend

```bash
npm install
```

---

## 6. Compilar Assets (CSS y JavaScript)

### Modo desarrollo (con hot reload):

```bash
npm run dev
```

### Modo producción (optimizado):

```bash
npm run build
```

También puedes ejecutar ambos con Composer:

```bash
composer run dev
```

---

## 7. Ejecutar la Aplicación

### Opción A: Servidor integrado de Laravel

```bash
php artisan serve
```

La aplicación estará disponible en: `http://localhost:8000`

### Opción B: Servidor WAMP/LAMP

1. Asegúrate de que tu servidor (Apache, Nginx) está corriendo
2. Accede a través de tu dominio configurado
3. Verifica que el `public/` sea el document root

### Opción C: Con docker (si está configurado)

```bash
docker-compose up
```

---

## 8. Comandos Útiles

### Base de datos
```bash
php artisan migrate              # Ejecutar migraciones
php artisan migrate:fresh        # Rollback + migrate
php artisan db:seed              # Ejecutar seeders
php artisan tinker               # Interactuar con la app
```

### Rutas
```bash
php artisan route:list           # Ver todas las rutas
php artisan route:list --method=GET  # Filtrar por método
```

### Caché
```bash
php artisan cache:clear          # Limpiar caché
php artisan config:cache         # Cachear configuración
php artisan view:clear           # Limpiar vistas compiladas
```

### Testing
```bash
php artisan test                 # Ejecutar tests
php artisan test --filter=NombreTest  # Test específico
```

### Code Styling
```bash
vendor/bin/pint                  # Formatear código (Laravel Pint)
vendor/bin/pint --dirty          # Solo archivos modificados
```

---

## 9. Estructura del Proyecto

```
labLaravelLogin7/
├── app/                    # Código de la aplicación
│   ├── Http/              # Controllers, Middleware, Requests
│   ├── Models/            # Modelos Eloquent
│   └── Providers/         # Service Providers
├── bootstrap/             # Inicialización de la app
├── config/                # Archivos de configuración
├── database/              # Migraciones, factories, seeders
├── public/                # Punto de entrada (index.php)
├── resources/             # Vistas, CSS, JavaScript
│   ├── views/            # Archivos Blade (.blade.php)
│   └── css/js/           # Assets
├── routes/                # Definición de rutas
├── storage/               # Logs, cache, archivos temporales
├── tests/                 # Tests automáticos
├── vendor/                # Dependencias de Composer
├── .env                   # Variables de entorno (no versionado)
├── .gitignore            # Archivos a ignorar en git
├── composer.json         # Dependencias de PHP
├── package.json          # Dependencias de Node.js
└── artisan               # CLI de Laravel
```

---

## 10. Variables de Entorno Importantes

El archivo `.env` contiene configuraciones sensibles:

```env
APP_NAME=labLaravelLogin7
APP_ENV=local
APP_KEY=base64:...           # Generada con php artisan key:generate
APP_DEBUG=true               # true en desarrollo, false en producción
APP_URL=http://localhost:8000

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=tu_base_datos
DB_USERNAME=root
DB_PASSWORD=

MAIL_MAILER=log
# ... más configuraciones
```

---

## 11. Solución de Problemas

### Error: "Unable to locate file in Vite manifest"
```bash
npm run build
# O
npm run dev
```

### Error: "No such file or directory" (.env)
```bash
php artisan key:generate
```

### Base de datos no conecta
- Verifica que MySQL está corriendo
- Confirma credenciales en `.env`
- Crea la base de datos si no existe

### Permisos de directorios
```bash
chmod -R 775 storage bootstrap/cache
```

---

## 12. Flujo Completo de Inicio Rápido

Si quieres ejecutar todo de una vez:

```bash
# 1. Ir al directorio del proyecto
cd c:\wamp64\www\labLaravelLogin7

# 2. Instalar dependencias PHP
composer install

# 3. Generar clave
php artisan key:generate

# 4. Configurar .env y base de datos
# (editar manualmente .env con tus credenciales)

# 5. Ejecutar migraciones
php artisan migrate

# 6. Instalar dependencias frontend
npm install

# 7. Compilar assets
npm run build

# 8. Ejecutar servidor
php artisan serve
```

Luego abre `http://localhost:8000` en tu navegador.

---

## 13. Recursos Útiles

- [Documentación oficial de Laravel](https://laravel.com/docs)
- [Laracasts - Video tutorials](https://laracasts.com)
- [Laravel Learning - Guías interactivas](https://laravel.com/learn)
- [Laravel Boost - AI Development](https://laravel.com/docs/ai)

---

**Última actualización:** Abril 2026  
**Versión de Laravel:** 13  
**Versión de PHP:** 8.3
