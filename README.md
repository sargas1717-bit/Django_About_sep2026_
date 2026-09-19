# Home/About con Django

Este proyecto demuestra un flujo básico de Django para manejar dos páginas estáticas: la página de inicio y la página “Acerca de”. El objetivo es mostrar cómo se estructura una aplicación pequeña, cómo se conectan las rutas con las vistas y cómo se renderizan las plantillas HTML.

## Descripción general

La aplicación utiliza:

- Django como framework principal.
- Una app llamada `pages` para manejar la lógica de las vistas.
- Dos URLs: una para la página principal y otra para la sección de información.
- Dos plantillas HTML: `home.html` y `about.html`.

## Estructura del proyecto

```text
home_about/
├── db.sqlite3
├── manage.py
├── requirements.txt
├── django_base/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
├── pages/
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── tests.py
│   ├── urls.py
│   ├── views.py
│   └── migrations/
├── templates/
│   ├── home.html
│   └── about.html
└── README.md
```

## Flujo del proceso Home/About

### 1. Configuración de rutas principales

En el archivo `django_base/urls.py` se incluye la configuración de rutas de la app `pages`:

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('pages.urls')),
]
```

Esto indica que todas las rutas del proyecto serán manejadas por la aplicación `pages`.

### 2. Definición de rutas internas

En `pages/urls.py` se registran las URL del sitio:

```python
from django.urls import path
from .views import HomeView, AboutView

urlpatterns = [
    path('', HomeView.as_view(), name='home'),
    path('about/', AboutView.as_view(), name='about'),
]
```

- La ruta raíz `/` apunta a la vista de inicio.
- La ruta `/about/` apunta a la vista “Acerca de”.
- El argumento `name='home'` y `name='about'` permite reutilizar estas rutas en los templates con `{% url 'home' %}` y `{% url 'about' %}`.

### 3. Vistas creadas con TemplateView

En `pages/views.py` se usan vistas basadas en clases, específicamente `TemplateView`:

```python
from django.views.generic import TemplateView

class HomeView(TemplateView):
    template_name = 'home.html'

class AboutView(TemplateView):
    template_name = 'about.html'
```

`TemplateView` es ideal para páginas estáticas porque solo renderiza una plantilla HTML sin lógica compleja.

### 4. Plantillas HTML

Las plantillas están en la carpeta `templates/`:

- `home.html`: muestra la pantalla principal.
- `about.html`: muestra la sección de información.

Ejemplo de `home.html`:

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

Ejemplo de `about.html`:

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

## Requisitos

- Python instalado
- Django instalado en el entorno virtual
- Git para control de versiones

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

- En Windows:

```bash
venv\Scripts\activate
```

- En macOS/Linux:

```bash
source venv/bin/activate
```

4. Instala las dependencias:

```bash
pip install -r requirements.txt
```

## Ejecución del proyecto

1. Aplica migraciones iniciales:

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

- En la ruta raíz se muestra la página de inicio.
- En la ruta `/about/` se muestra la página “Acerca de”.
- El navegador puede navegar entre ambos enlaces sin necesidad de lógica adicional.

## Conceptos aprendidos

Este proyecto enseña de forma clara la base del patrón MVC/MVT de Django:

- Modelo: no se usa en este caso porque son páginas estáticas.
- Vista: `HomeView` y `AboutView`.
- Template: `home.html` y `about.html`.
- URLConf: la conexión entre URLs y vistas.

## Siguientes pasos

Para mejorar este proyecto, puedes seguir con:

- Agregar estilos CSS para una mejor presentación.
- Crear contenido dinámico con modelos y bases de datos.
- Separar la navegación en un layout reutilizable.
- Añadir más secciones como servicios, contacto o blog.

## Conclusión

La implementación de Home/About en Django es una excelente base para comprender cómo funcionan las rutas, las vistas y las plantillas. Con este patrón, se puede expandir rápidamente hacia aplicaciones más complejas manteniendo una estructura clara y escalable.
