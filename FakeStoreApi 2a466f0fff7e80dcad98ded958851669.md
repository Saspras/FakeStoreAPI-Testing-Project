# FakeStoreApi

FakeStoreAPI es una API pública diseñada para simular un entorno de comercio electrónico y permitir la práctica de pruebas sobre endpoints reales.

Esta API reproduce funcionalidades comunes en aplicaciones de venta online, como **autenticación (Auth/Login), gestión de productos, carritos de compra e información de usuarios.**

El objetivo de este proyecto es **validar la correcta funcionalidad, estabilidad y rendimiento** de los principales endpoints expuestos por el sistema, asegurando que las respuestas cumplan con los estándares esperados en un entorno de calidad.

# TEST PLAN

| Campo | Descripción |
| --- | --- |
| **Proyecto** | Fake Store API Testing |
| **Objetivo** | Validar el funcionamiento de los endpoints principales (Auth, Products, Cart y Users) asegurando respuestas correctas, tiempos aceptables y estructuras válidas. |
| **Alcance** | Pruebas funcionales, smoke test y performance test sobre endpoints públicos. |
| **Fuera de alcance** | Pruebas de UI, seguridad avanzada o base de datos. |
| **Herramientas utilizadas** | Postman, Notion, variables de entorno, colección estructurada. |
| **Tipos de prueba** | Smoke, Funcionales, Performance. |
| **Criterios de pase/falla** | Código 200/201, tiempo <2000ms, estructura JSON válida. |
| **Entorno** | API pública [https://fakestoreapi.com](https://fakestoreapi.com/) |
| **Resultado general** | 100% de los casos ejecutados con resultado PASS. Sin defectos detectados. |
| **Observaciones** | API estable, documentación confusa en PUT (respuesta no coincide con lo esperado). |
| **Conclusión** | Todos los endpoints respondieron dentro de los parámetros esperados. No se detectaron bugs ni caídas del servidor. El sistema cumple con las condiciones de calidad esperadas. |

# Test Case

| ID | Título | Módulo | Método | Endpoint | Precondiciones | Pasos | Datos de entrada | Resultado esperado | Estado | Evidencia |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| TC001 | Login exitoso | Auth | POST | `/auth/login` | Tener conexión a internet y Postman abierto | 1. Abrir Postman.2. Seleccionar método `POST`.3. Escribir la URL del login.4. En la pestaña “Body”, ingresar usuario y contraseña válidos.5. Enviar la solicitud. | `{ "username": "mor_2314", "password": "83r5^_" }` | La respuesta debe contener código **200 OK** y un campo `"token"`. | PASS/~~FAIL~~ | [{FA4DC784-925B-4E07-AB41-EDA2E0E7B203}.png](FakeStoreApi%202a466f0fff7e80dcad98ded958851669.md)  |
| TC002 | Login con credenciales inválidas | Auth | POST | `/auth/login` | Tener conexión a internet y Postman abierto | 1. Repetir los pasos del TC001, pero ingresar usuario o contraseña incorrectos. | `{ "username": "mor_fake", "password": "wrong" }` | El sistema debe responder con **400 Bad Request**. | PASS/~~FAIL~~ | [{68C871F1-170F-497A-AD6A-864061C6F229}.png](FakeStoreApi%202a466f0fff7e80dcad98ded958851669.md)  |
| TC003 | Obtener todos los productos | Products | GET | `/products` | Tener conexión a internet y Postman abierto | 1. Crear una nueva request.2. Seleccionar `GET`.3 Ingresar enpoint. correspondiente con la seccion de products. 4. Enviar la solicitud. | - | La respuesta debe devolver código **200 OK** y un array con productos. | PASS/~~FAIL~~ | [{24D5A770-7D0A-4AA5-B884-828B88CA0431}.png](FakeStoreApi%202a466f0fff7e80dcad98ded958851669.md)  |
| TC004 | Crear producto nuevo | Products | POST | `/products` | Tener conexión a internet y Postman abierto | 1. Crear nueva request.2. Seleccionar `POST`.3. Ingresar el endpoint.4. Ingresar body con datos del producto.5. Enviar la solicitud. | `{"id": 12, "title": "heladera","price": 100000.12,"description": "Heladera No-frost Drean", "category": "Linea Blanca","image": "[https://images.fravega.com/f1000/3bf43a9808b4fc9e2ba14318e6cfe068.jpg](https://images.fravega.com/f1000/3bf43a9808b4fc9e2ba14318e6cfe068.jpg)"}` | La API debe responder con status **201 OK** y retornar los datos creados con un nuevo `"id"`. | PASS/~~FAIL~~ | [{BF3FD327-2AAF-4E35-8C61-0E37B4043A4E}.png](FakeStoreApi%202a466f0fff7e80dcad98ded958851669.md)  |
| TC005 | Actualizar producto | Products | PUT | `/products/{id}` | Tener conexión a internet , Postman abierto y Haber creado un producto previamente. | 1. Crear request `PUT` con el ID del producto.2. Enviar nuevos valores en el body. 3. Enviar la solicitud. | `{ "title": "Monitor actualizado", "price": 360 }` | La API debe devolver código **200 OK** y mostrar el producto actualizado. | PASS/~~FAIL~~ | [{7F4E038F-6F3B-467B-AEF2-2E905D23A3A6}.png](FakeStoreApi%202a466f0fff7e80dcad98ded958851669.md)  |
| TC006 | Eliminar producto | Products | DELETE | `/products/{id}` | Tener conexión a internet , Postman abierto y Tener un producto existente creado por el usuario. | 1. Crear request `DELETE` con el ID que se desea eliminar.2.  Enviar la solicitud. | - | La API debe devolver código **200 OK** y el producto eliminado. | PASS/~~FAIL~~ | [{AF085B93-C448-421A-846A-227A95C13002}.png](FakeStoreApi%202a466f0fff7e80dcad98ded958851669.md)  |
| TC007 | Nuevo carrio | Cart | POST | `/carts` | Tener conexión a internet , Postman abierto  | 1. Crear una request `POST` con un body correspondiente. 2 Enviar la solicitud. | `{"id":1,"userId":1,"products": {"id":1,"title":"HELADERA","price": 50.1,"description": "Heladear Blanca","category": "Linea Blanca","image":"[https://arcencohogar.vtexassets.com/arquivos/ids/369372-800-800?v=638392835895130000&width=800&height=800&aspect=true](https://arcencohogar.vtexassets.com/arquivos/ids/369372-800-800?v=638392835895130000&width=800&height=800&aspect=true)"}}` | La API debe de devolver codigo 201 Creado. y debe de dmostrar los datos de carrito creado | PASS/~~FAIL~~ | [{B9FD0402-BA08-4E3B-9204-C6156CD9C63D}.png](https://www.notion.so/2a866f0fff7e80d397dadcccf87e6181?pvs=21)  |
| TC008 | Obtener carritos | Cart | GET | `/carts` | Tener conexión a internet , Postman abierto y Tener un carrito creado | 1. Crear una request `GET`con el endpoint correspondiente.  2 Enviar la solicitud. | - | La API debe de devolver un status 200 OK  y un aray con todos los carritos existentes y sus productos | PASS/~~FAIL~~ | [{0D6E8F7D-B470-44DF-AF13-8079ADBEE29F}.png](FakeStoreApi%202a466f0fff7e80dcad98ded958851669.md)  |
| TC009 | Actualizar carrito | Cart | PUT  | `/carts/{id}` | Tener conexión a internet , Postman abierto y Tener un carrito creado | 1. Crear una Request `PUT` con el body correspondiente. 2 Enviar la solicitud . | `{"id": 0,"userId": 1,"products": [{}]}` | La API debe de devolver un status 200 Ok y la actualizacion del carrito con sus productos corresondientes | PASS/~~FAIL~~ | [{39F463AF-B1F5-4D57-B9CD-09AE218AB12A}.png](FakeStoreApi%202a466f0fff7e80dcad98ded958851669.md)  |
| TC010 | Borrar carrito | Cart | DELETE | `/carts/{id}` | Tener conexión a internet , Postman abierto y Tener un carrito creado | 1. Crear una request `DELETE` con el id del carrito que se va a eliminar. 2 Enviar la solicitud. | - | La API debe de devolver un status 200 Ok y un array del carrito que se elimino | PASS/~~FAIL~~ | [{FA390546-B70A-4608-BA7E-D907B9679C8A}.png](FakeStoreApi%202a466f0fff7e80dcad98ded958851669.md)  |
| TC011 | Obtener todos los usuarios | User | GET | `/user` | Tener conexión a internet , Postman abierto  | 1. Crear una request `GET` con el endpoint correspondiente. 2 Enviar la solicitud. | - | La API debe de devolver un status 200 OK, y un array de los usuarios existentes | PASS/~~FAIL~~ | [{55626AA2-A8AB-4E66-810A-E6F7AE22EAB8}.png](FakeStoreApi%202a466f0fff7e80dcad98ded958851669.md)  |
| TC012 | Agregar usuarios | Users | POST | `/users` | Tener conexión a internet , Postman abierto  | 1. Crear una request `POST` con el body correspondiente a los datos de usuario. 2 Enviar la solicitud. | `{"id": 11,"username": "testuser123","email":"[test@example.com](mailto:test@example.com)","password": "testpass123"}` | La API debe de devolver un status 201 Creado, y el id del usuario crado | PASS/~~FAIL~~ | [{4CA2DEA8-7EC3-4872-BA1E-9A0EDD300D32}.png](FakeStoreApi%202a466f0fff7e80dcad98ded958851669.md)  |
| TC013 | Obtener usuario particular | Users | GET | `/users/{id}` | Tener conexión a internet , Postman abierto y  tener usuarios ya creados en la pagina | 1. Crear una request `GET`  con el id del usuario que desea buscar. 2. Enviar la solicitud | - | La API debe de devolver un status 200 OK y un array de los datos del usuario elegido | PASS~~/FAIL~~ | [{30B6455B-5D3E-44AE-937A-0DCEB4BBED2B}.png](FakeStoreApi%202a466f0fff7e80dcad98ded958851669.md)  |
| TC014 | Actualizar usuario | Users | PUT | `/users/{id}` | Tener conexión a internet , Postman abierto y  tener usuarios ya creados en la pagina | 1. Crear una request `PUT` con el id del usuario que desea actualizar. 2 Ingrese los datos que se van a actualizar en el body. 3. Enviar la solicitud  | `{"id": 3,"username": "juan","email":"[juan@gmail.com](mailto:juan@gmail.com)","password": "juancontraseña"}`  | La API debe de devolver un satus 200 OK, y un array de los datos actualizados | PASS~~/FAIL~~ | [{6FEECFF9-D373-432A-AC41-0E421959FF8F}.png](FakeStoreApi%202a466f0fff7e80dcad98ded958851669.md)  |
| TC015 | Eliminar usuario | Users | DELETE | `/users/{id}` | Tener conexión a internet , Postman abierto y  tener usuarios ya creados en la pagina | 1.Crear una request `DELETE` con el id del usuario que desea eleiminar. 2. Enviar la solicitud | - | La API debe de devolver un status 200 OK, y un array de los datos eliminados. | PASS~~/FAIL~~ | [{38473070-5207-4728-8536-8E0707C70A22}.png](FakeStoreApi%202a466f0fff7e80dcad98ded958851669.md)  |

# EVIDENCIA

## Auth

### TC001

![{FA4DC784-925B-4E07-AB41-EDA2E0E7B203}.png](FakeStoreApi/FA4DC784-925B-4E07-AB41-EDA2E0E7B203.png)

### TC002

![{68C871F1-170F-497A-AD6A-864061C6F229}.png](FakeStoreApi/68C871F1-170F-497A-AD6A-864061C6F229.png)

## Products

### TC003

![{24D5A770-7D0A-4AA5-B884-828B88CA0431}.png](FakeStoreApi/24D5A770-7D0A-4AA5-B884-828B88CA0431.png)

### TC004

![{BF3FD327-2AAF-4E35-8C61-0E37B4043A4E}.png](FakeStoreApi/BF3FD327-2AAF-4E35-8C61-0E37B4043A4E.png)

### TC005

![{7F4E038F-6F3B-467B-AEF2-2E905D23A3A6}.png](FakeStoreApi/7F4E038F-6F3B-467B-AEF2-2E905D23A3A6.png)

### TC006

![{AF085B93-C448-421A-846A-227A95C13002}.png](FakeStoreApi/AF085B93-C448-421A-846A-227A95C13002.png)

## Cart

### TC007

![{980A5559-1D2F-4D32-A68E-CDC262C5E7D3}.png](FakeStoreApi/980A5559-1D2F-4D32-A68E-CDC262C5E7D3.png)

### TC008

![{0D6E8F7D-B470-44DF-AF13-8079ADBEE29F}.png](FakeStoreApi/0D6E8F7D-B470-44DF-AF13-8079ADBEE29F.png)

### TC009

![{39F463AF-B1F5-4D57-B9CD-09AE218AB12A}.png](FakeStoreApi/39F463AF-B1F5-4D57-B9CD-09AE218AB12A.png)

### TC010

![{FA390546-B70A-4608-BA7E-D907B9679C8A}.png](FakeStoreApi/FA390546-B70A-4608-BA7E-D907B9679C8A.png)

## Users

### TC011

![{55626AA2-A8AB-4E66-810A-E6F7AE22EAB8}.png](FakeStoreApi/55626AA2-A8AB-4E66-810A-E6F7AE22EAB8.png)

### TC012

![{4CA2DEA8-7EC3-4872-BA1E-9A0EDD300D32}.png](FakeStoreApi/4CA2DEA8-7EC3-4872-BA1E-9A0EDD300D32.png)

### TC013

![{30B6455B-5D3E-44AE-937A-0DCEB4BBED2B}.png](FakeStoreApi/30B6455B-5D3E-44AE-937A-0DCEB4BBED2B.png)

### TC014

![{6FEECFF9-D373-432A-AC41-0E421959FF8F}.png](FakeStoreApi/6FEECFF9-D373-432A-AC41-0E421959FF8F.png)

### TC015

![{38473070-5207-4728-8536-8E0707C70A22}.png](FakeStoreApi/38473070-5207-4728-8536-8E0707C70A22.png)

# PERFORMANCE TEST

Se realizo un performance test, para revisar los tiempos de carga de cada seccion. La evaluacion se realizo con 10 usuarios virtuales durante 3 minutos. Dando una tasa de error 0% con un time request max de 967ms, y un min de 247ms, promediando en 302ms. Con un total de 4.870 request sended en total y 25.37 request per second.

![{EE8741F6-3445-49C1-BF80-3A15623FC2F7}.png](FakeStoreApi/EE8741F6-3445-49C1-BF80-3A15623FC2F7.png)

[fakestoreapi-performance-report-4.html](FakeStoreApi/fakestoreapi-performance-report-4.html)

# SMOKE TEST

Se realizó una prueba de humo (smoke test) al endpoint de productos para validar su funcionalidad básica y rendimiento. La prueba fue **exitosa en todos los aspectos**, verificando tanto la respuesta HTTP como la estructura de datos. El endpoint respondió correctamente con un código **200 OK** en **311 ms**, muy por debajo del límite aceptable de 2000ms. Se validó que el cuerpo de respuesta es un array JSON que contiene productos con todas las propiedades requeridas (id, title, price, description, category, image), con sus tipos de datos correctos y valores válidos, confirmando que la API está operativa y cumpliendo con los estándares esperados.

![{5C754643-7B1F-4EE7-9E6E-2B27C1DDCC79}.png](FakeStoreApi/5C754643-7B1F-4EE7-9E6E-2B27C1DDCC79.png)

# REPORTE NEWMAN

Reporte generado automáticamente con Newman y reporter htmlextra.
Incluye resultados de todas las solicitudes, tiempos promedio, tests ejecutados y resultados.

[Reporte de ejecucion - Newman](FakeStoreApi/FakeStoreReport.html)

# Conclusion del proyecto

Durante la ejecución de las pruebas sobre *FakeStoreAPI*, se validaron los endpoints principales de **autenticación, productos, carritos y usuarios**, abarcando pruebas **funcionales, de smoke y de performance**.

Todas las solicitudes respondieron correctamente, con tiempos promedio de entre **500 y 800 ms**, y sin detección de errores en las respuestas del servidor.

Se concluye que la API cumple con los **criterios de calidad, estabilidad y rendimiento** esperados para un entorno público de prueba.

Este proyecto demuestra el proceso completo de **QA API Testing**, desde la planificación hasta la documentación y generación automática de reportes mediante *Postman* y *Newman*.