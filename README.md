# Sistema_Facturacion
Python, Django, jwt,sql

# Installar Django
pip install Django==2.2

## Instalar Django rest framework para construir el proyecto
pip install djangorestframework

# Crear usuario para poder usar el ORM de Django
python manage.py createsuperuser

# Crear proyecto en Django
django-admin start project sistemaFacturaion .

## Installar 'rest_framework' en settings del proyecto
En INSTALLED_APPS agregar 'rest_frameework'

## Migrar todos los archivos que vienen con django
python manage.py migrate

## Crear las aplicaciones que va a contener el proyecto con sus respectivas llaves foraneas y pk.
python manage.py starapp clients
python manage.py starapp bills
python manage.py starapp products
python manage.py starapp billsProducts

## Installar las aplicaciones en settings del proyecto
INSTALLED_APPS = [
    'clients.apps.ClientsConfig',

## Crear modelos
Crear la estructura de cada una de las aplicaciones en el archivo models de la
carpeta de cada aplicación

## Resgistar aplicacion para poderla visualizar en el ORM
Agregar modelo al admin.py de la carpeta de cada aplicación
admin.site.register(Client)

## Agregar la ruta en el archivo urls en la carpeta del proyecto
path('clients/', include('clients.urls'))

## Realizar migraciones
python manage.y makemigrations
python manage.py migrate

### Verificar Migraciones
Usar para verificar como quedaron las migraciones

## Crear la visualizacion de las aplicaciones
Crear archivo serializers.py dentro de la carpeta de cada app y crear codigo para la visualización de las apps
Ir al archivos views.py y con ayuda de generics crear la logica para crear el CRUD de cada una de las aplicaciones

### ListCreateAPIView
Provee metodo get y post

### RetriveUpdateDestroyAPIView
Provee los metodos de get, put, delete y patch

## Crear archivos urls en cada aplicacion para proyectar vistas
Crear archivo urls.py en la carpeta de cada app e importar las vistas creadas anteriormente

## Probar cada una de las peticiones en el ORM o en POSTMAN
http://127.0.0.1:8000/clients/

# ENDPOINT REGISTRAR UN USUARIO

## Installar jwt
pip install djangorestframework-simplejwt

## Configurar jwt en el proyecto
Con ayuda de la documentacion de jwt para django escribir codigo en settings del proyecto

## Crear endpoints de registro
En archivo urls.py del proyecto agrego las rutas para el registro de los usuarios
 path('api/token/', TokenObtainPairView.as_view(), name='token_obtain_pair'),
 path('api/token/refresh/', TokenRefreshView.as_view(), name='token_refresh'),

## Comprobar registro
Verificar codigo usando la ruta http://127.0.0.1:8000/api/token/ y los parametros asignados para el registro,
este endpoint se hizo para ingresar con el usuario y contraseña del ORM de Django

# ENDPOINT PARA   USO DE ENCABEZADOS

## Editar configuraciones del proyecto
Con la documentación de Django agregar la configuracion para poder utilizar los encabezados
EST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': (
        'rest_framework_simplejwt.authentication.JWTAuthentication',
    ),
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.IsAuthenticated',
    ]
}

## Uso del encabezado
Al crear un usuario copiar el token de la parte refresh, dirijirse a headers de Postman
en key escribir authorization y en value Bearer y justo al lado de Bearer pasar el token
http://127.0.0.1:8000/api/token/

### Registro del encabezado
El registro del encabezado se hace con el usuario del ORM de Django y con la contraseña

# ENDPOITN PARA REGISTRAR UN USUARIO E INICIAR SESIÓN

## Crear app users
python manage.py starapp users

## Installar la aplicaciones en settings del proyecto
'users.apps.UsersConfig'

## Crear serializers.py
Crear codigo con los parametros que usare para el registro del usuario

## Crear vistas
Para este registro e inició de sesion me apoye usando Viewset y DefaultRouter para crear la ruta

## Crear ruta 
En archivo urls.py crear logica, aqui utilizar DefaultRouter

## Agregar ruta a proyecto
Agregar ruta en urls.py en la carpeta del proyecto

## Probar registro de usuario 
Se ingresan parameteros para registro 
http://127.0.0.1:8000/users/

## Probar inicio de sesión
Usando parametro de usuario y contraseña
http://127.0.0.1:8000/api/token/
