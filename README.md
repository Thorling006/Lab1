# Laboratorio 1 Segundo Cómputo – Vue.js

## Integrantes
- Yensi Elizabeth Valladares Ventura
- Omar David Ventura Cruz

---

## Situación problemática

En la universidad, muchos estudiantes necesitan reservar cubículos para estudiar, trabajar en grupo o preparar exposiciones. Sin embargo, en algunos casos este proceso se realiza de forma manual, por apuntes o mensajes, lo cual puede causar desorden, reservas repetidas, pérdida de información y confusión sobre qué cubículos están disponibles.

Esta situación afecta principalmente al sector educativo, especialmente a universidades, bibliotecas y centros de estudio, donde se requiere una mejor organización para administrar el uso de los cubículos de manera rápida y clara.

Para resolver este problema, se propone una página web desarrollada con Vue.js que permita registrar préstamos de cubículos, validar los datos ingresados, mostrar una lista de reservas activas y eliminar registros cuando ya no sean necesarios. De esta forma se mejora el control, se reduce el error humano y se facilita la gestión de espacios para los estudiantes.

---

## Funciones del sistema

- Registrar una nueva reserva de cubículo.
- Capturar nombre del estudiante.
- Capturar número de carné.
- Seleccionar el cubículo.
- Ingresar motivo de uso.
- Validar campos obligatorios.
- Mostrar mensajes de error si faltan datos.
- Mostrar mensaje de éxito cuando la reserva se guarda correctamente.
- Listar las reservas activas.
- Eliminar reservas registradas.

---

## ¿Qué es Vue.js y cuál es su función dentro de la página web desarrollada?

Vue.js es un framework de JavaScript que sirve para crear interfaces web interactivas y dinámicas. En este proyecto se utilizó para manejar los datos de la página en tiempo real, capturar lo que el usuario escribe en los campos del formulario, validar la información y actualizar automáticamente la lista de reservas sin necesidad de recargar la página. Vue usa directivas como `v-model`, `v-bind`, `v-for` y `v-if`, además de eventos para reaccionar a las acciones del usuario. :contentReference[oaicite:0]{index=0}

---

## Variables reactivas utilizadas y función de cada una

Las variables reactivas usadas en la aplicación son las siguientes:

- `nombre`: guarda el nombre del estudiante que solicita el cubículo.
- `carnet`: almacena el número de carné del estudiante.
- `cubiculo`: guarda el cubículo seleccionado.
- `motivo`: registra el motivo por el cual se solicita el cubículo.
- `reservas`: almacena todas las reservas ingresadas en forma de lista.
- `mensaje`: muestra un mensaje de éxito cuando una reserva se registra correctamente.
- `error`: muestra mensajes de validación cuando hay campos vacíos o incorrectos.
- `soloActivas`: permite mostrar únicamente las reservas activas.
- `contador`: genera un identificador único para cada reserva.

---

## Diferencia entre `v-bind` y `v-model`

La diferencia es que `v-bind` se usa para enlazar atributos o propiedades de un elemento HTML con datos de Vue. Por ejemplo, se puede usar para cambiar una clase o deshabilitar un botón según una condición. En cambio, `v-model` se usa para enlazar un campo de formulario con una variable reactiva, de manera que lo que el usuario escribe se guarda automáticamente en esa variable. En resumen, `v-bind` conecta atributos dinámicos y `v-model` conecta entradas de formulario con los datos del sistema. :contentReference[oaicite:1]{index=1}

---

## Ejemplo de evento utilizado dentro de la aplicación

Un evento utilizado fue `@submit.prevent` en el formulario. Este evento se ejecuta cuando el usuario presiona el botón para registrar la reserva y evita que la página se recargue. También se utilizó el evento `@click` para eliminar reservas de la lista. Vue permite escuchar eventos del DOM con `v-on` o su forma corta `@`. :contentReference[oaicite:2]{index=2}

---

## ¿Para qué se utilizó la directiva `v-for`?

La directiva `v-for` se utilizó para recorrer y mostrar en pantalla la lista de reservas registradas. Gracias a esta directiva, cada vez que se agrega una nueva reserva, esta aparece automáticamente en la interfaz sin necesidad de actualizar manualmente la página.

---

## ¿En qué situación se utilizó `v-if` y qué problema resuelve?

La directiva `v-if` se utilizó para mostrar mensajes de error, mensajes de éxito y también para indicar cuando no existen reservas registradas. Esto ayuda a que la interfaz sea más clara, ya que solo muestra cierta información cuando realmente se necesita. `v-if` se usa para renderizar contenido condicionalmente. :contentReference[oaicite:3]{index=3}

---

## ¿Cómo se realiza la validación de datos y por qué es importante?

La validación se realiza revisando que los campos no estén vacíos, que el carné tenga una longitud mínima válida y que el motivo tenga una cantidad suficiente de caracteres. Si algún dato está incorrecto, el sistema muestra un mensaje de error y no permite guardar la reserva.

Validar los datos es importante porque evita registros incompletos o incorrectos, mejora la confiabilidad del sistema y ayuda a que la información almacenada sea útil y ordenada.

---

## Tecnologías utilizadas

- HTML
- CSS
- JavaScript
- Vue.js

---

## Etiquetas HTML utilizadas

En el proyecto se utilizaron más de cinco etiquetas HTML, por ejemplo:

- `header`
- `main`
- `section`
- `form`
- `input`
- `select`
- `textarea`
- `button`
- `article`
- `p`
- `h1`
- `h2`

---

## Directivas Vue utilizadas

- `v-model`
- `v-bind`
- `v-for`
- `v-if`

