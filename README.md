# Proyecto Mini Core - Aplicación de Gestión de Ventas (React - Django)

Aplicación interconectada de gestión de comisiones que combina la robustez de **Django REST Framework** para exponer una API REST, con un frontend **React + Vite** que consume esos endpoints mediante Axios y ofrece una UI en modo oscuro moderna y responsiva. El stack se despliega en **Render**: el backend corre como **Web Service** (Gunicorn + Django, con migraciones automáticas y archivos estáticos recopilados) y el frontend como **Static Site** generado por Vite, con una regla global de rewrite (/* → /index.html) para permitir el enrutado del SPA.

---

## Descripción del Proyecto

Este proyecto contempla un Sistema de Comisiones completo que permite a los usuarios desarrollar las funciones:

- Crear, listar y eliminar **Ventas**.
- Gestionar **Reglas de Comisión** configurables por monto mínimo y porcentaje.
- **Cálculo automático de comisiones** basado en las reglas establecidas.
- **Reportes detallados** de comisiones por vendedor y período.
- Filtrar comisiones por rango de fechas con análisis comparativo.

El backend se encuentra construido con **Django** y utiliza **SQLite** en desarrollo para almacenar la información. El frontend usa **React (Javascript)** con **Vite** y consume la API REST vía **Axios**.

---

## 🌐 Demo en Vivo

- **🖥️ Aplicación Frontend:** [https://frontend-comisiones.onrender.com](https://frontend-comisiones.onrender.com)
  
---

## Tabla de Contenidos

1. [Instalación](#instalación)  
2. [Uso del Proyecto](#uso-del-proyecto)  
3. [Características](#características)
4. [Estructura del Proyecto](#estructura-del-proyecto)
5. [API Endpoints](#api-endpoints)
6. [Deployment](#deployment)
7. [Contribución](#contribución)  
8. [Créditos](#créditos)  
9. [Licencia](#licencia)

---

## Instalación

### Requisitos previos

- **Node.js** y **npm** instalados para el frontend (Versión recomendada: **Node: v18+**).
- **Python 3.8 o superior** instalado para el backend (Versión utilizada: **3.11+**).
- **Django**, **Django REST Framework** y **django-cors-headers** instalados en el backend.
- **Axios**, **date-fns** y **React Router** en el frontend.

La base de datos SQLite se utiliza por defecto en desarrollo y PostgreSQL en producción (Render).

### Pasos para instalar y ejecutar el proyecto

#### Configuración del Backend

1. Clonar el repositorio:
   ```bash
   git clone https://github.com/Mattair39/Proyecto-Mini-Core-MVC.git
   ```
2. Ubicarse en la carpeta principal del proyecto:
   ```bash
   cd Proyecto-Mini-Core-MVC
   ```
3. Ir a la carpeta backend:
   ```bash
   cd backend
   ```
4. Crear un entorno virtual e instalar dependencias:
   ```bash
   python -m venv env
   source env/bin/activate  # En Windows: env\Scripts\activate
   pip install -r requirements.txt
   ```
5. Aplicar las migraciones:
   ```bash
   python manage.py migrate
   ```
6. (Opcional) Cargar datos de ejemplo:
   ```bash
   python manage.py loaddata commission_app/fixtures/initial_data.json
   ```
7. Iniciar el servidor del backend:
   ```bash
   python manage.py runserver
   ```
El servidor estará disponible en **http://127.0.0.1:8000/**

---
#### Configuración del Frontend

1. Regresar a la carpeta raíz del proyecto y ubicarse en **frontend**:
   ```bash
   cd ../frontend
   ```
2. Instalar las dependencias:
   ```bash
   npm install
   ```

---
### Ejecución
#### Iniciar el Backend (Django)

1. Desde la carpeta backend (donde se encuentra manage.py):
   ```bash
   python manage.py runserver
   ```
2. El servidor de Django estará disponible en **http://127.0.0.1:8000/**
3. API disponible en **http://127.0.0.1:8000/api/**

#### Iniciar el Frontend (React)

1. Ir a la carpeta frontend y ejecutar:
   ```bash
   npm run dev
   ```
2. La aplicación de React estará disponible en **http://localhost:3000/**

---

## Uso del Proyecto

### 📊 **Gestión de Ventas:**

1. **Registrar Ventas:** Agregar ventas asociando vendedor, fecha y monto.
2. **Visualizar Comisiones:** Ver automáticamente la comisión calculada para cada venta.

### 📈 **Cálculo de Comisiones:**

1. **Configurar Reglas:** Definir reglas de comisión por porcentaje y monto mínimo.
2. **Análisis por Período:** Seleccionar rango de fechas para calcular comisiones.
3. **Reportes Detallados:** Ver resumen por vendedor con desglose individual.
4. **Métricas Comparativas:** Analizar totales, promedios y rendimiento.

### 🔍 **Funcionalidades Avanzadas:**

- **Dropdown Expandible:** Explorar comisiones individuales por vendedor.
- **Cálculo Automático:** Las comisiones se calculan automáticamente según las reglas.
- **Validación de Datos:** Controles de entrada y mensajes de error informativos.
- **Interfaz Responsiva:** Optimizada para desktop y móvil.

---

## Características

### 🚀 **Funcionalidades Principales:**
- **Cálculo automático de comisiones basado en reglas configurables**
- **Sistema de reportes con filtros por rango de fechas**
- **Interfaz de usuario moderna con modo oscuro**
- **Dropdown expandible para análisis detallado por vendedor**

### 🔧 **Tecnologías Backend:**
- **Django REST Framework** con endpoints RESTful
- **SQLite** (Desarrollo)
- **CORS** habilitado para comunicación segura
- **Migraciones automáticas** y **fixtures** para datos iniciales

### 🎨 **Tecnologías Frontend:**
- **React 19** con **Vite** para desarrollo rápido
- **Axios** para consumo de API REST
- **date-fns** para manejo de fechas
- **CSS Custom Properties** para theming consistente

### 🌐 **Deployment:**
- **Backend:** Web Service en Render con Gunicorn
- **Frontend:** Static Site en Render con rewrite rules
- **Base de Datos:** SQLite automática en Render
- **Variables de entorno** para configuración de producción

---

## Estructura del Proyecto

```
Proyecto-Mini-Core-MVC/
├── backend/
│   ├── commission_app/
│   │   ├── models.py          # Modelos de Vendedor, Venta, Regla, ComisionCalculada
│   │   ├── serializers.py     # Serializers para API REST
│   │   ├── views.py           # ViewSets y vistas personalizadas
│   │   ├── urls.py            # URLs de la API
│   │   ├── admin.py           # Configuración del panel admin
│   │   └── fixtures/          # Datos iniciales
│   ├── commission_project/
│   │   ├── settings.py        # Configuración con soporte para producción
│   │   ├── urls.py            # URLs principales
│   │   └── wsgi.py            # WSGI para deployment
│   ├── requirements.txt       # Dependencias de Python
│   └── manage.py              # Comando principal de Django
└── frontend/
    ├── src/
    │   ├── components/        # Componentes reutilizables
    │   ├── services/          # API client con Axios
    │   ├── utils/             # Utilidades para formateo y fechas
    │   ├── App.jsx            # Componente principal
    │   └── main.jsx           # Punto de entrada
    ├── public/                # Archivos estáticos
    ├── package.json           # Dependencias de Node.js
    └── vite.config.js         # Configuración de Vite
```

---

## API Endpoints

### 📋 **Vendedores**
```
GET    /api/vendedores/           # Listar vendedores
POST   /api/vendedores/           # Crear vendedor
GET    /api/vendedores/{id}/      # Obtener vendedor
PUT    /api/vendedores/{id}/      # Actualizar vendedor
DELETE /api/vendedores/{id}/      # Eliminar vendedor
GET    /api/vendedores/{id}/ventas/     # Ventas de un vendedor
GET    /api/vendedores/{id}/comisiones/ # Comisiones de un vendedor
```

### 💰 **Ventas**
```
GET    /api/ventas/              # Listar ventas (con filtros)
POST   /api/ventas/              # Crear venta
GET    /api/ventas/{id}/         # Obtener venta
PUT    /api/ventas/{id}/         # Actualizar venta
DELETE /api/ventas/{id}/         # Eliminar venta
```

### ⚙️ **Reglas de Comisión**
```
GET    /api/reglas/              # Listar reglas activas
POST   /api/reglas/              # Crear regla
PUT    /api/reglas/{id}/         # Actualizar regla
```

### 📊 **Cálculo de Comisiones**
```
POST   /api/comisiones/calcular/ # Calcular comisiones por rango de fechas
GET    /api/comisiones/resumen/  # Resumen general de comisiones
```

### 📈 **Parámetros de consulta disponibles:**
- `?vendedor={id}` - Filtrar por vendedor
- `?fecha_inicio={YYYY-MM-DD}` - Filtrar desde fecha
- `?fecha_fin={YYYY-MM-DD}` - Filtrar hasta fecha

---

## Deployment

### 🚀 **Render Deployment**

Este proyecto está configurado para deployment automático en Render:

#### **Variables de Entorno - Backend:**
```env
SECRET_KEY=tu-secret-key-generada
DEBUG=False
DATABASE_URL=postgresql://user:pass@host:port/db
CORS_ALLOWED_ORIGINS=https://proyecto-mini-core-mvc-static.onrender.com
```

#### **Variables de Entorno - Frontend:**
```env
VITE_API_URL=https://proyecto-mini-core-mvc.onrender.com
```

#### **Comandos de Build:**
- **Backend:** `pip install -r requirements.txt && python manage.py collectstatic --noinput && python manage.py migrate`
- **Frontend:** `npm install && npm run build`

### 🔧 **Desarrollo Local**

Para desarrollo local, el proyecto usa configuración automática:
- **Backend:** SQLite + `DEBUG=True`
- **Frontend:** API URL apunta a `http://127.0.0.1:8000`

---

## Contribución

Para contribuir a este proyecto, sigue estos pasos:

1. Realizar un fork del repositorio.
2. Crea una nueva rama (`git checkout -b feature/nueva-funcionalidad`).
3. Realiza tus cambios y haz commit (`git commit -m "Agregar nueva funcionalidad"`).
4. Haz push a la rama (`git push origin feature/nueva-funcionalidad`).
5. Abrir un Pull Request.

### 📝 **Guidelines de Contribución:**
- Seguir las convenciones de código existentes
- Agregar tests para nuevas funcionalidades
- Actualizar documentación cuando sea necesario
- Usar commits descriptivos y claros

---

## Créditos

Este proyecto fue desarrollado por:

- **Matías Flores (Universidad de las Américas)**  
  - [GitHub](https://github.com/pitHongo)  

### 🙏 **Tecnologías utilizadas:**
- [Django](https://www.djangoproject.com/) - Framework web de Python
- [Django REST Framework](https://www.django-rest-framework.org/) - API REST para Django
- [React](https://react.dev/) - Biblioteca de JavaScript para UI
- [Vite](https://vitejs.dev/) - Build tool para desarrollo frontend
- [Render](https://render.com/) - Plataforma de deployment

---

## Licencia

Este proyecto está licenciado bajo la [MIT License](https://choosealicense.com/licenses/mit/). Puedes usar, modificar y distribuir este proyecto libremente.
