# Conversor de divisas

Este proyecto es una aplicación web diseñada para convertir montos entre diferentes divisas de manera sencilla e interactiva. Fue desarrollada utilizando **HTML**, **CSS** y **JavaScript**, aprovechando las ventajas de cada tecnología para lograr una experiencia de usuario fluida.

**Componentes y estructura:**

- **HTML:**
    
    La estructura principal se define en un archivo HTML que organiza los elementos visuales de la aplicación. Incluye:
    
    - Un encabezado con el título e ícono representativo.
    - Un campo de entrada para que el usuario ingrese la cantidad a convertir.
    - Dos menús desplegables (select) que permiten seleccionar las divisas de origen y destino.
    - Un botón de conversión que, al hacer clic, activa la funcionalidad de cambio de moneda.
    - Un párrafo para mostrar el resultado de la conversión.
- **CSS:**
    
    El archivo CSS se encarga de estilizar la aplicación, garantizando un diseño responsivo y moderno. Se usaron técnicas como:
    
    - **Flexbox** para la organización de los elementos.
    - **Google Fonts (Poppins)** para una tipografía elegante.
    - Estilos personalizados para inputs, botones y selectores, con transiciones de color para mejorar la interacción del usuario.
    - Uso de imágenes (ícono de la app y flechas en los select) para un toque visual atractivo.
- **JavaScript:**
    
    La lógica de la aplicación se implementa en JavaScript, permitiendo la interactividad necesaria para:
    
    - Obtener y gestionar un array de códigos de divisas (proporcionado en el archivo `currency-codes.js`).
    - Integrar una clave API (en `api-key.js`) para conectarse a servicios externos y obtener tasas de cambio en tiempo real.
    - Capturar eventos (como el clic en el botón de "Convertir") para realizar la conversión y actualizar dinámicamente el resultado en la interfaz.
    - Manejar la validación de los datos ingresados y la selección de divisas para asegurar un correcto funcionamiento.

**Ejecución esperada:**

- Permite al usuario ingresar una cantidad y seleccionar las divisas deseadas para obtener una conversión inmediata y precisa.
- La conversión se realiza al instante tras la acción del usuario, proporcionando una respuesta clara.
- La aplicación se adapta a diferentes tamaños de pantalla, garantizando una experiencia óptima tanto en dispositivos móviles como en escritorio.
- Al utilizar una clave API, el conversor se actualiza con las tasas de cambio actuales, lo que asegura resultados confiables y en tiempo real.

## Código HTML

### Estructura y metadatos

- **Declaración de DOCTYPE y etiqueta `<html>`:**
    
    Se inicia con `<!DOCTYPE html>` para definir el documento como HTML5. La etiqueta `<html lang="es">` especifica que el contenido está en español, lo cual es importante para la accesibilidad y optimización SEO.
    
- **Elemento `<head>`:**
    
    Contiene metadatos y recursos externos esenciales:
    
    - **Meta viewport:**
        
        ```html
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        ```
        
        Este elemento asegura que la aplicación se visualice correctamente en dispositivos móviles al controlar el tamaño y la escala.
        
    - **Título de la página:**
        
        ```html
        <title>Conversor de divisas</title>
        ```
        
        Define el nombre que se mostrará en la pestaña del navegador.
        
    - **Google Fonts:**
        
        Se utiliza para incluir la fuente "Poppins", lo cual mejora la estética y la legibilidad.
        
    - **Enlace al CSS:**
        
        ```html
        <link rel="stylesheet" href="style.css" />
        ```
        
        Se carga la hoja de estilos externa para dar forma visual a la aplicación.
        

---

### Cuerpo del documento (`<body>`)

- **Contenedor (`.wrapper`):**
    
    Este `<div>` agrupa todos los elementos de la aplicación, centralizando y limitando el ancho para lograr un diseño limpio y responsivo.
    
- **Detalles de la Aplicación (`.app-details`):**
    
    Dentro de este contenedor se agrupan:
    
    - **Ícono de la Aplicación:**
        
        ```html
        <img src="app-icon.svg" class="app-icon" />
        ```
        
        Proporciona una representación visual que refuerza la identidad del proyecto.
        
    - **Título de la aplicación:**
        
        ```html
        <h1 class="app-title">Conversor de divisas</h1>
        ```
        
        Se utiliza un encabezado para identificar de forma clara el propósito de la aplicación.
        
- **Interacción del usuario:**
    - **Campo de entrada:**
        
        ```html
        <label for="amount">Cantidad:</label>
        <input type="number" id="amount" value="100" />
        ```
        
        Permite al usuario introducir la cantidad a convertir, validado como número. El atributo `value="100"` sirve como valor inicial.
        
    - **Menús desplegables:**
        
        ```html
        <div class="dropdowns">
          <select id="from-currency-select"></select>
          <select id="to-currency-select"></select>
        </div>
        ```
        
        Se usan dos `<select>` para seleccionar la divisa de origen y destino. Su contenido se poblará dinámicamente (probablemente mediante JavaScript) con los códigos de divisas.
        
    - **Botón de conversión:**
        
        ```html
        <button id="convert-button">Convertir</button>
        ```
        
        Este botón desencadena el proceso de conversión mediante un evento en JavaScript.
        
    - **Visualización del resultado:**
        
        ```html
        <p id="result"></p>
        ```
        
        Un párrafo vacío que se actualizará con el resultado de la conversión, mostrando el monto convertido.
        

---

### Inclusión de scripts

- **Scripts externos:**
    
    Al final del `<body>` se incluyen varios archivos JavaScript que proporcionan la funcionalidad de la aplicación:
    
    - `currency-codes.js`: Contiene una estructura con los códigos de divisas soportados.
    - `api-key.js`: Gestiona la clave API para acceder a servicios de tasas de cambio.
    - `script.js`: Contiene la lógica principal, incluyendo la interacción con el DOM, manejo de eventos y la realización de la conversión.

## Código JavaScript

### 1. Lógica principal (script.js)

**Definición de Variables y referencias:**

- **URL de la API:**
    
    Se define la variable `api` que construye la URL para obtener las tasas de cambio desde un servicio externo. La URL incorpora una variable `apiKey` para la autenticación:
    
    ```jsx
    let api = `...`;
    ```
    
- **Selección de elementos del DOM:**
    
    Se capturan los elementos HTML de los desplegables (select) para divisas mediante `document.getElementById`, permitiendo manipularlos dinámicamente.
    
    ```jsx
    const fromDropDown = document.getElementById("from-currency-select");
    const toDropDown = document.getElementById("to-currency-select");
    ```
    

**Población de los desplegables:**

- **Uso de la función `forEach`:**
    
    Se itera sobre el array `currencies` (definido en otro archivo) para crear elementos `<option>` para cada divisa. Se realiza dos veces, uno para el desplegable de origen y otro para el de destino:
    
    ```jsx
    currencies.forEach((currency) => {
      const option = document.createElement("option");
      option.value = currency;
      option.text = currency;
      fromDropDown.add(option);
    });
    ```
    
    La misma lógica se repite para `toDropDown`.
    
- **Valores por defecto:**
    
    Se establecen valores predeterminados para ambos desplegables:
    
    ```jsx
    fromDropDown.value = "MXN";
    toDropDown.value = "USD";
    ```
    

**Función de conversión:**

- **Extracción de datos y validación:**
    
    La función `convertCurrency` recupera:
    
    - La cantidad ingresada por el usuario.
    - Los valores seleccionados de ambas divisas.
    
    Se verifica que el campo de cantidad no esté vacío:
    
    ```jsx
    if (amount.length != 0) { ... } else { alert("Please fill in the amount"); }
    ```
    
- **Uso de `fetch` para obtener datos:**
    
    Se realiza una solicitud a la API para obtener las tasas de conversión en formato JSON. Una vez obtenida la respuesta, se extraen las tasas de cambio correspondientes a la divisa de origen y destino:
    
    ```jsx
    fetch(api)
      .then((resp) => resp.json())
      .then((data) => {
        let fromExchangeRate = data.conversion_rates[fromCurrency];
        let toExchangeRate = data.conversion_rates[toCurrency];
        // Cálculo del monto convertido
      });
    ```
    
- **Cálculo y actualización de la interfaz:**

Se calcula el monto convertido utilizando la fórmula:

monto convertido = (cantidad / tasa de origen) × tasa de destino

El resultado se muestra en el elemento `<p id="result">`, formateado a dos decimales:

```jsx
result.innerHTML = `${amount} ${fromCurrency} = ${convertedAmount.toFixed(2)} ${toCurrency}`;
```

**Manejo de eventos:**

- **Evento click en el botón:**
    
    Se añade un listener al botón de conversión para ejecutar `convertCurrency` cuando se haga clic.
    
    ```jsx
    document.querySelector("#convert-button").addEventListener("click", convertCurrency);
    ```
    
- **Ejecución automática al cargar la página:**
    
    Se añade un evento `load` para que la conversión se realice automáticamente cuando la página termine de cargar:
    
    ```jsx
    window.addEventListener("load", convertCurrency);
    ```
    

---

### 2. Definición de la matriz de divisas (currency-codes.js)

**Array de códigos de divisas:**

- **Listado:**
    
    El archivo define una variable `currencies` que es un array con códigos ISO de divisas, lo que permite que la aplicación sea compatible con una amplia gama de monedas. Esto facilita la generación dinámica de los elementos `<option>` en los desplegables.
    
    ```
    js
    Copy
    currencies = [
      "AED", "AFN", "ALL", "AMD", "ANG", "AOA", "ARS", "AUD",
      "AWG", "AZN", "BAM", "BBD", "BDT", "BGN", "BHD", "BIF",
      // ... (continúa la lista completa)
    ];
    
    ```
    

**Importancia del array:**

- **Dinamismo y escalabilidad:**
    
    La utilización de este array permite que cualquier cambio en la lista de monedas (agregar o eliminar) se refleje automáticamente en la interfaz de usuario sin necesidad de modificar el HTML.
    
- **Soporte internacional:**
    
    Al incluir una gran cantidad de códigos, se garantiza que la aplicación pueda ser útil para usuarios de diferentes regiones y necesidades de conversión de divisas.
    

---

## Código CSS

### 1. Reglas globales y reset

- **Reset de márgenes y paddings:**
    
    ```css
    * {
      padding: 0;
      margin: 0;
      box-sizing: border-box;
      font-family: "Poppins", sans-serif;
      border: none;
      outline: none;
    }
    ```
    
    - Se aplica un *reset* a todos los elementos (), eliminando márgenes y paddings para evitar estilos por defecto inconsistentes entre navegadores.
    - La propiedad `box-sizing: border-box` asegura que el padding y el borde se incluyan en el ancho total del elemento, facilitando la maquetación.
    - Se establece la fuente "Poppins" a nivel global, lo que garantiza consistencia tipográfica en toda la aplicación.
    - Se eliminan bordes y outlines, lo que puede ser útil para personalizar completamente la apariencia, aunque se debe considerar la accesibilidad.

---

### 2. Estilos para el “Body”

- **Fondo del body:**
    
    ```css
    body {
      background-color: #313638;
    }
    ```
    
    Se define un color de fondo oscuro para el body, proporcionando un contraste adecuado con el contenido principal de la aplicación.
    

---

### 3. Contenedor (.wrapper)

- **Centralización y diseño del contenedor:**
    
    ```css
    .wrapper {
      width: 90%;
      max-width: 25em;
      background-color: #ffffff;
      position: absolute;
      transform: translate(-50%, -50%);
      left: 50%;
      top: 50%;
      padding: 2em;
      border-radius: 0.8em;
    }
    ```
    
    - Se establece un ancho flexible (90%) y un límite máximo (`max-width`) para asegurar que el contenedor se vea bien en distintos dispositivos.
    - Se utiliza `position: absolute` junto con `transform: translate(-50%, -50%)` para centrar el contenedor en la pantalla.
    - Se asigna un fondo blanco, lo que resalta el contenido frente al fondo oscuro del body.
    - El `padding` y `border-radius` aportan un diseño espacioso y moderno.

---

### 4. Estilos para detalles de la aplicación (.app-details)

- **Organización con Flexbox:**
    
    ```css
    .app-details {
      display: flex;
      align-items: center;
      flex-direction: column;
    }
    ```
    
    Se utiliza Flexbox para centrar los elementos de forma vertical y alinear de manera amigable la imagen y el título, facilitando un diseño limpio y ordenado.
    
- **Imagen del ícono:**
    
    ```css
    .app-icon {
      width: 9.37em;
    }
    ```
    
    Se controla el ancho de la imagen para mantener la coherencia visual.
    
- **Título de la aplicación:**
    
    ```css
    .app-title {
      font-size: 1.6em;
      text-transform: uppercase;
      margin-bottom: 1em;
    }
    ```
    
    - Se aumenta el tamaño de la fuente para dar énfasis al título.
    - `text-transform: uppercase` ayuda a resaltar el título.
    - El `margin-bottom` aporta separación respecto a otros elementos.

---

### 5. Estilos para formularios y controles

- **Etiquetas (`label`):**
    
    ```css
    label {
      display: block;
      font-weight: 600;
    }
    ```
    
    Se garantiza que las etiquetas se muestren en bloque, facilitando la legibilidad y jerarquía visual, con un peso de fuente medio que resalta su importancia.
    
- **Campo de entrada (`input#amount`):**
    
    ```css
    input#amount {
      font-weight: 400;
      font-size: 1.2em;
      display: block;
      width: 100%;
      border-bottom: 2px solid #02002c;
      color: #7a789d;
      margin-bottom: 2em;
      padding: 0.5em;
    }
    input#amount:focus {
      color: #DB5375;
      border-color: #DB5375;
    }
    ```
    
    - El campo de entrada se estiliza para ocupar el 100% del ancho disponible, con una tipografía clara y un diseño minimalista.
    - La transición visual en el estado `:focus` (cambio de color y borde) mejora la experiencia del usuario, destacando el campo activo.
- **Menús desplegables (`select`):**
    
    ```css
    .dropdowns {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 1em;
    }
    select {
      width: 100%;
      padding: 0.6em;
      font-size: 1em;
      border-radius: 0.2em;
      appearance: none;
      -webkit-appearance: none;
      -moz-appearance: none;
      background-image: url("arrow-down.svg");
      background-repeat: no-repeat;
      background-position: right 15px top 50%, center;
      background-size: 20px 20px;
      background-color: #729EA1;
      color: #ffffff;
    }
    select option {
      background-color: #ffffff;
      color: #02002c;
    }
    ```
    
    - Se utiliza Flexbox en el contenedor `.dropdowns` para alinear correctamente ambos select y añadir espacio entre ellos.
    - La eliminación de la apariencia nativa (`appearance: none`) permite un estilo personalizado, y la adición de una imagen de flecha mejora la interfaz visual.
    - Se definen estilos distintos para las opciones, asegurando legibilidad y contraste.
- **Botón de conversión:**
    
    ```css
    button {
      font-size: 1em;
      width: 100%;
      background-color: #DB5375;
      padding: 1em 0;
      margin-top: 2em;
      border-radius: 0.3em;
      color: #ffffff;
      font-weight: 600;
    }
    ```
    
    - El botón ocupa el ancho total disponible, con un color de fondo vibrante y tipografía en negrita para hacerlo resaltar como elemento de acción.
    - Los márgenes y el padding proporcionan un espacio adecuado, aumentando la facilidad de uso en dispositivos táctiles.
- **Visualización del resultado (`#result`):**
    
    ```css
    #result {
      font-size: 1.2em;
      text-align: center;
      margin-top: 1em;
      color: #313638;
      background-color: #F9DB6D;
      padding: 0.8em 0;
    }
    ```
    
    - Se estiliza para que el resultado de la conversión se destaque mediante un color de fondo y tipografía centrada, facilitando la lectura.

---

### Buenas prácticas

- La elección de colores, tipografía y espaciado está cuidadosamente pensada para ofrecer una interfaz moderna y limpia, con buen contraste y legibilidad.
- Permite una disposición flexible y responsiva de los elementos, asegurando que la aplicación se adapte bien a diferentes tamaños de pantalla.
- La eliminación de estilos por defecto (márgenes, bordes, apariencia) y la personalización (como en el caso de los select) demuestran un enfoque en la coherencia estética y la experiencia del usuario.
- Las reglas establecidas, como el `max-width` en el contenedor principal y el uso de porcentajes, aseguran que la aplicación se vea bien tanto en dispositivos móviles como en escritorio.

---