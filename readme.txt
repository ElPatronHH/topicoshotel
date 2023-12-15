>> Sugerencias:
Instalar DBeaver y MySQL Workbench, ahí se puede ver e insertar muy fácil en la base de datos respectivamente.
NO USAR python manage.py makemigrations y python manage.py migrate sin avisar, esto modifica la base de datos, y está bien, pero implica que todos debemos tener el mismo archivo de models, así que nos lo debemos de estar pasando y si perdemos el rastro del estado actual, ya valió, primero me avisan a mí (Alex), yo reviso su cambio rápido, lo subo y lo vuelven a descargar para que todos vayamos a la par.
El superusuario se comparte.

>>Entorno Virtual:
virtualenv venv
venv\Scripts\activate  

>> Dependencias:
pip install django
pip install mysqlclient 

>> Rutas:
/admin
/hotel_app/crear_reserva/

>> Admin:
user=Hotel 
password=Topicos2023

>> Credenciales Conexión Base de Datos:
hostname=topicoshotel.mysql.database.azure.com
username=topicoshotel
name=topicoshotel
password=1234database!
ssl-mode=require

>> Correr el Proyecto:
python manage.py runserver  

>> Superusuarios:
python manage.py createsuperuser
python manage.py changepassword Hotel<nombre_de_usuario>
python manage.py shell (abre la consola de Django y luego se debe pegar el code para listar usuarios)
from django.contrib.auth.models import User 
superusers = User.objects.filter(is_superuser=True)
for superuser in superusers:
    print(superuser.username)

>> Correr el Proyecto en Server Local (debes estar en la misma red):
En settings busca y coloca ALLOWED_HOSTS = ['*']
python manage.py runserver 0.0.0.0:8000

>> Migraciones:
python manage.py makemigrations
	Si sale -> It is impossible to add a non-nullable field 'nombre_de_un_campo_nuevo' to reserva without specifying a default. This is because the database needs something to populate existing rows.
	Please select a fix:
 	1) Provide a one-off default now (will be set on all existing rows with a null value for this column)
 	2) Quit and manually define a default value in models.py.
    Elegimos opción 2 y revisamos manualmente los modelos, deben de tener un campo por default porque
	el error dice que ya hay registros sin ese campo y van a tener nulo, entonces debes colocar un 	default.
python manage.py migrate