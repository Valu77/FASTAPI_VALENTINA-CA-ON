# mi readme del proyecto fastapi

Bueno aca explico como monte todo el proyecto y las cosas que me salieron mal en la terminal y como las arregle para que el servidor por fin funcionara

Primero que todo cree un entorno virtual para que no se mezclaran las librerías con las del computador y lo active en la consola con .\python-3407187\Scripts\activate despues instale fastapi uvicorn y sqlmodel usando pip install para poder manejar las rutas la base de datos sqlite y arrancar el servidor

Cuando fui a encender el proyecto me salio un error en la consola que decia que no encontraba la ruta del uvicorn asi que me toco meter el comando python -m uvicorn main:app --reload para que llamara directamente al python del entorno y ahi si me dio el link

Despues me empeso a sacar errores de ModuleNotFoundError porque las carpetas se llamaban DataBase Enrutadores y Modelos con mayuscula inicial y en las importaciones del codigo estaban en minuscula como Python reconoce las mayusculas me toco cambiarle el nombre a las carpetas fisicas de la pc a minusculas para que leyera bien las rutas

Tambien me salio un SyntaxError en el archivo de transacciones porque decia rom en vez de from en la primera linea y lo corregi de una y el ultimo error fue un AttributeError que decia que no existia el router en facturas y era porque habia hecho los cambios pero no habia guardado los archivos en el visual studio code entonces Python seguia leyendo el codigo viejo sin guardar apenas hize el guardado masivo de todo el servidor reconocio la variable router y anduvo de una

El proyecto quedo organizado con la carpeta database para la conexion de sqlite enrutadores para los controladores de clientes facturas y transacciones modelos para las tablas de la base de datos y el main.py que une todo

En conexion.py configure el create_engine y el get_session con un yield para que la base de datos se abra y se cierre sola en cada peticion y en facturas.py cree los metodos de GET POST PUT y DELETE donde el GET de listar trae todas las facturas de la base de datos y hace un for para buscar el cliente que le pertenece a esa factura usando su id asi la respuesta sale completa con los datos del cliente adentro de la factura tambien maneja el HTTPException con estado 404 por si buscan un id que no existe

Al final cuando el comando de uvicorn arranca ejecuta el SQLModel.metadata.create_all para crear el archivo database.db en la carpeta si es que no existe y te da el enlace local para abrir la api si entras al link normal sale el mensaje de API funcionando pero si le pones /docs al final de la url te abre la pagina de swagger con todos los botones de colores para probar el crud de clientes facturas y transacciones interactuando directamente con la base de datos