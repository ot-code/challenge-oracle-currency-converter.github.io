<h1 align="center">Conversor de divisas</h1>💱

Este proyecto es una aplicación web interactiva desarrollada con **HTML**, **CSS** y **JavaScript**. Su propósito es facilitar la conversión de montos entre diversas divisas en tiempo real, ofreciendo una experiencia de usuario fluida y atractiva.

---

## Características 🌟

- **Conversión en tiempo real:** Utiliza una API para obtener tasas de cambio actualizadas.
- **Interfaz responsiva:** Se adapta a dispositivos móviles y de escritorio.
- **Diseño moderno:** Implementa Flexbox, transiciones y tipografía elegante (Google Fonts - *Poppins*).

---

## Estructura 📁

### HTML

- **Entrada de cantidad:** 
  - Campo numérico para ingresar el monto a convertir.
- **Menús desplegables:**
  - Selección de divisa de origen y destino.
- **Botón de conversión:**
  - Activa la función de cambio de moneda.
- **Visualización del resultado:**
  - Muestra el monto convertido en un párrafo.

### CSS

- **Reset global:** 
  - Elimina márgenes y paddings por defecto, establece `box-sizing: border-box` y define la fuente *Poppins*.
- **Diseño responsivo:** 
  - Uso de Flexbox para una correcta distribución y alineación de elementos.
- **Estilos personalizados:**
  - Transiciones de color, imágenes (ícono de la app, flechas en los selectores) y un esquema de colores atractivo.

### JavaScript

- **Lógica de la aplicación:**
  - Captura eventos y realiza la conversión utilizando datos obtenidos de una API.
- **Población dinámica de selectores:**
  - Itera sobre un array de códigos de divisas (definido en `currency-codes.js`) para generar las opciones.
- **Validación y manejo de eventos:**
  - Verifica la entrada de datos y actualiza la interfaz al clic en el botón "Convertir".
- **Integración con API:**
  - Usa la clave API de `api-key.js` para obtener tasas de cambio en tiempo real.

---

## Detalles técnicos 🔍

### Código HTML

- **Estructura y metadatos:**
  - Inicio con `<!DOCTYPE html>` y `<html lang="es">`.
  - `<head>` incluye meta viewport, título, Google Fonts y enlace al CSS.
- **Cuerpo (`<body>`):**
  - Contenedor principal (`.wrapper`) que centraliza y limita el ancho del contenido.
  - Sección `.app-details` con el ícono y título de la aplicación.
  - Formulario interactivo: campo de entrada, menús desplegables, botón de conversión y área para mostrar resultados.
- **Inclusión de scripts:**
  - Se cargan `currency-codes.js`, `api-key.js` y `script.js` para habilitar la funcionalidad.

### Código JavaScript

- **Selección y manipulación del DOM:**
  - Uso de `document.getElementById` para acceder a elementos HTML.
- **Población dinámica de selectores:**
  - Utiliza `forEach` para crear elementos `<option>` a partir de un array de códigos de divisas.
- **Función de conversión:**
  - Valida la entrada, realiza una solicitud `fetch` a la API y actualiza el resultado.
- **Eventos:**
  - Listener para el clic en el botón "Convertir" y ejecución automática al cargar la página.

### Código CSS

- **Estilos globales:**
  - Reset de márgenes, paddings, y definición de la fuente.
- **Diseño del contenedor:**
  - Uso de `position: absolute` y `transform: translate(-50%, -50%)` para centrar el contenido.
- **Estilos de componentes:**
  - Personalización de inputs, selectores y botones con transiciones y colores contrastantes.
- **Visualización del resultado:**
  - Párrafo estilizado para resaltar el monto convertido con colores y tipografía centrada.

---

## ¿Cómo ejecutar la aplicación? 🚀

1. **Clona el repositorio:**  
   ```bash
   git clone https://github.com/ot-code/challenge-oracle-currency-converter.github.io.git

2. **Abre el archivo index.html en tu navegador.
3. **Ingresa la cantidad a convertir y selecciona las divisas deseadas.
4. **Haz clic en "Convertir" para ver el resultado actualizado en tiempo real.

---

## Imágenes de la aplicación
<div align="center">
  <img src="https://github.com/user-attachments/assets/0ae25fff-8a70-4462-b203-c7dedc857d00" alt="Conversor de divisas por defecto" width="700" height="600" />
  <img src="https://github.com/user-attachments/assets/06096e18-6ec0-4328-823d-5d0d08168627" alt="Conversor de divisas en acción" width="700" height="600" />
</div>

---

<p align="center">
  <big><strong>¡Gracias por visitar este repositorio!✨💱</strong></big>
</p> 
