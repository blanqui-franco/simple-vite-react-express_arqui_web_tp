# Simple Vite React Express — Trabajo Práctico Arquitectura Web

**Trazabilidad End-to-End de una Solicitud Web**  
FP-UNA — Arquitectura Web 2026  
Prof. Rodrigo Benítez  
Integrantes: Blanca Franco, Matías Gaona, Diego Duarte

---

## Descripción

Aplicación full-stack utilizada como sistema de prueba para el análisis y documentación del ciclo completo de una petición web real. El stack incluye React 19 + Vite 7 en el frontend, Express 5 + Node.js 22 en el backend, y PostgreSQL 15 con Prisma ORM como capa de persistencia.

**URL de producción:** https://simple-vite-react-expressarquiwebtp-production.up.railway.app

---

## Stack tecnológico

| Capa | Tecnología | Versión |
|---|---|---|
| Frontend | React + Vite | 19 / 7 |
| Backend | Node.js + Express | 22 / 5 |
| Base de datos | PostgreSQL | 15.4 |
| ORM | Prisma | 7.4 |
| Deploy | Railway | — |

---

## Requisitos previos

- Node.js >= 22.0.0
- npm >= 11.0.0
- PostgreSQL >= 15
- Git

Verificar versiones instaladas:

```bash
node --version
npm --version
psql --version
git --version
```

---

## Instalación local

### 1. Clonar el repositorio

```bash
git clone https://github.com/blanqui-franco/simple-vite-react-express_arqui_web_tp.git
cd simple-vite-react-express_arqui_web_tp
```

### 2. Instalar dependencias

```bash
npm install
```

### 3. Configurar variables de entorno

Copiar el archivo de ejemplo y editarlo:

```bash
cp example.env .env
```

Editar `.env` con los valores correspondientes:

```env
PORT=8080
NODE_ENV=development
DATABASE_URL=postgresql://postgres:TU_CONTRASEÑA@localhost:5432/myapp?schema=public
```

### 4. Crear la base de datos

En PostgreSQL, crear la base de datos:

```sql
CREATE DATABASE myapp;
```

### 5. Ejecutar migraciones con Prisma

```bash
npx prisma db push --force-reset
```

Esto crea las tablas `Contact`, `Project`, `ProjectMember` y `Task` en la base de datos.

### 6. Iniciar el proyecto en modo desarrollo

```bash
npm run dev
```

Esto levanta simultáneamente:
- Frontend Vite en `http://localhost:3000`
- Backend Express en `http://localhost:8080`

---

## Scripts disponibles

| Script | Descripción |
|---|---|
| `npm run dev` | Inicia frontend y backend en modo desarrollo |
| `npm run build` | Genera el build de producción del frontend |
| `npm start` | Inicia el servidor en modo producción |
| `npm run db:studio` | Abre Prisma Studio para gestionar la base de datos |
| `npm run db:reset` | Resetea la base de datos |
| `npm run lint` | Ejecuta el linter ESLint |

---

## Estructura del proyecto
├── src/
│   ├── client/          # Frontend React
│   │   ├── components/  # Componentes React
│   │   └── index.jsx    # Punto de entrada del frontend
│   └── server/          # Backend Express
│       ├── config/      # Configuración del servidor
│       ├── middleware/  # Middleware (seguridad, validación)
│       ├── routes/      # Rutas de la API
│       │   └── v1/      # Versión 1 de la API
│       └── services/    # Lógica de negocio y base de datos
├── prisma/
│   └── schema.prisma    # Esquema de la base de datos
├── public/              # Assets estáticos
├── .env                 # Variables de entorno (no commitear)
├── example.env          # Ejemplo de variables de entorno
├── package.json         # Dependencias y scripts
└── vite.config.js       # Configuración de Vite
---

## Endpoints de la API

Base URL local: `http://localhost:8080/api/v1`  
Base URL producción: `https://simple-vite-react-expressarquiwebtp-production.up.railway.app/api/v1`

| Método | Endpoint | Descripción |
|---|---|---|
| GET | `/health` | Health check del servidor |
| GET | `/contact/list` | Listar contactos |
| POST | `/contact` | Crear contacto |
| GET | `/task/list` | Listar tareas |
| POST | `/task` | Crear tarea |
| GET | `/project/list` | Listar proyectos |
| POST | `/project` | Crear proyecto |

---

## Despliegue en Railway

### 1. Crear cuenta en Railway

Registrarse en [railway.app](https://railway.app) con cuenta de GitHub.

### 2. Crear nuevo proyecto

- Seleccionar **GitHub Repository**
- Elegir el repositorio del proyecto

### 3. Agregar PostgreSQL

- Hacer clic en **+ Add** → **Database** → **PostgreSQL**
- Railway provisiona automáticamente la base de datos

### 4. Configurar variables de entorno

En el servicio de la aplicación → **Variables**:

NODE_ENV=production
DATABASE_URL=${{Postgres.DATABASE_URL}}

### 5. Configurar scripts de build

En `package.json`:

```json
"build": "npx prisma generate && vite build",
"start": "node src/server/index.js"
```

### 6. Ejecutar migraciones en producción

Usando la `DATABASE_PUBLIC_URL` del servicio Postgres:

```bash
npx prisma db push --url "postgresql://..."
```

### 7. Generar dominio público

En Railway → Settings → **Generate Domain**

---

## Evidencias técnicas del TP

El proyecto fue utilizado para documentar y evidenciar el flujo completo de una solicitud web, incluyendo:

- Análisis DNS con `nslookup` y `ipconfig /displaydns`
- Trazabilidad de red con `tracert` hacia `pol.una.py` y `google.com`
- Análisis TCP con `netstat` y Wireshark
- Inspección de headers HTTP con `curl` y DevTools
- Análisis de performance con DevTools Performance
- Despliegue en Railway con CI/CD automático

---

## Licencia

MIT
