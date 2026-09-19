# Home/About con Django

## Descripción del proyecto

Este proyecto es una implementación básica pero funcional de una aplicación web con Django para manejar dos páginas estáticas: una página de inicio y una sección “Acerca de”. La finalidad principal es mostrar de forma clara el flujo estándar de Django para enlazar URLs, vistas y plantillas.

La versión actual del proyecto se encuentra en un estado estable y funcional, con una estructura simple, navegación básica y dos templates HTML renderizados desde vistas basadas en clases.

## Estado actual

- Proyecto creado con Django.
- App principal: `pages`.
- Rutas configuradas para la home y la vista About.
- Plantillas HTML creadas en la carpeta `templates`.
- Navegación funcional entre Inicio y Acerca de.
- Base de datos SQLite por defecto de Django.

## Tecnologías utilizadas

- Python
- Django
- SQLite
- HTML

## Estructura del proyecto

```text
home_about/
├── db.sqlite3
├── manage.py
├── requirements.txt
├── README.md
├── django_base/
│   ├── __init__.py
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── pages/
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── migrations/
│   ├── models.py
│   ├── tests.py
│   ├── urls.py
│   └── views.py
└── templates/
    ├── about.html
    └── home.html
```

## Flujo actual de funcionamiento

### 1. Configuración principal de URLs

El proyecto principal incluye la app `pages` desde `django_base/urls.py`:

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('pages.urls')),
]
```

Esto permite que todas las rutas del sitio sean gestionadas por la aplicación `pages`.

### 2. Rutas internas de la app

En `pages/urls.py` se definen las rutas del sitio:

```python
from django.urls import path
from .views import HomeView, AboutView

urlpatterns = [
    path('', HomeView.as_view(), name='home'),
    path('about/', AboutView.as_view(), name='about'),
]
```

- `/` → vista principal del home.
- `/about/` → vista de la sección “Acerca de”.
- Los nombres `home` y `about` se utilizan para generar enlaces con `{% url %}` en los templates.

### 3. Vistas con TemplateView

En `pages/views.py` se usan vistas basadas en clases:

```python
from django.views.generic import TemplateView

class HomeView(TemplateView):
    template_name = 'home.html'

class AboutView(TemplateView):
    template_name = 'about.html'
```

Este patrón es ideal para páginas estáticas porque solo renderiza una plantilla sin lógica compleja de negocio.

### 4. Plantillas HTML

Las páginas se renderizan desde la carpeta `templates/`.

#### home.html

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Inicio</title>
</head>
<body>
    <nav>
        <a href="{% url 'home' %}">Inicio</a> | 
        <a href="{% url 'about' %}">Acerca de</a>
    </nav>
    <h1>Página de Inicio</h1>
    <p>Bienvenido al proyecto Django Home-About.</p>
</body>
</html>
```

#### about.html

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Acerca de</title>
</head>
<body>
    <nav>
        <a href="{% url 'home' %}">Inicio</a> | 
        <a href="{% url 'about' %}">Acerca de</a>
    </nav>
    <h1>Acerca de Nosotros</h1>
    <p>Esta es la sección descriptiva del proyecto.</p>
</body>
</html>
```

## Requisitos previos

- Python 3.x instalado.
- Django disponible en el entorno virtual.
- Git para clonar y versionar el proyecto.

## Instalación

1. Clona el repositorio:

```bash
git clone <url-del-repositorio>
cd home_about
```

2. Crea un entorno virtual:

```bash
python -m venv venv
```

3. Activa el entorno virtual:

- Windows:

```bash
venv\Scripts\activate
```

- macOS/Linux:

```bash
source venv/bin/activate
```

4. Instala las dependencias:

```bash
pip install -r requirements.txt
```

## Ejecución del proyecto

1. Ejecuta las migraciones iniciales:

```bash
python manage.py migrate
```

2. Inicia el servidor:

```bash
python manage.py runserver
```

3. Abre en el navegador:

- http://127.0.0.1:8000/
- http://127.0.0.1:8000/about/

## Resultado esperado

- La ruta raíz muestra la vista de inicio.
- La ruta `/about/` muestra la vista de Acerca de.
- La navegación entre ambas páginas funciona correctamente.

## Conceptos aplicados

Este proyecto demuestra la base del patrón MVT de Django:

- Modelo: no se usa por ser una app de contenido estático.
- Vista: `HomeView` y `AboutView`.
- Template: `home.html` y `about.html`.
- URLConf: conexión entre rutas y vistas.

## Próximos pasos recomendados

Para continuar con el proyecto, se pueden implementar:

- estilos CSS personalizados
- archivos base y layout reutilizable
- ampliación del contenido con más secciones
- uso de modelos y datos dinámicos
- formularios y autenticación

## Conclusión

La versión actual del proyecto presenta una base sólida para entender el funcionamiento de Django en una aplicación sencilla. El flujo de home/about ilustra de manera práctica cómo se conectan las rutas, vistas y templates en el patrón MVT, siendo una base ideal para proyectos más complejos.
