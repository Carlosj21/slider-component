# Image Slider Canvas

Demo de un slider de imágenes con arrastre (drag) usando Vue 3, Vite y TypeScript.  
El carrusel se renderiza en un único `<canvas>` y permite cambiar de imagen arrastrando lateralmente con el mouse.

## Características del slider

Un único elemento canvas de tamaño fijo (640×400 px) por imagen visible.

Al menos 4 imágenes con dimensiones diferentes (img1.png, img2.png, img3.png, img4.png).

Lógica de escalado para que cada imagen se ajuste manteniendo su proporción y centrada dentro del canvas.

Manejo de drag con eventos mouse (mousedown / mousemove / mouseup) para desplazar el carrusel.

Código totalmente en TypeScript y Vue 3 Composition API para mejor mantenimiento.

## Requisitos del navegador

El slider ha sido probado en:

- Chrome/Edge Chromium (latest)

Solo se requiere un navegador moderno con soporte para `<canvas>` y ES6+.

## Requisitos del sistema

- Node.js (v16 o superior)
- npm
- `nws` (simple static file server) o cualquier servidor estático (opcional)

## Instalar y ejecutar

1. Clonar el repositorio:

    ```bash
    git clone https://github.com/Carlosj21/slider-component.git
    ```

    ```bash
    cd slider-component
    ```

2. Instalar las dependencias:

    ```bash
    npm install
    ```

3. Construir versión estática:

    ```bash
    npm run build
    ```

4. Iniciar la aplicación (modo preview):

    ```bash
    npm run preview
    ```

## Iniciar en modo desarrollo

1. Iniciar el modo de desarrollo:

    ```bash
    npm run dev
    ```

    (Esto abrirá el slider en el navegador con la ruta: <http://localhost:5173>)

## Tecnologías utilizadas

- Vue 3 + Composition API

- TypeScript

- Vite

- Canvas 2D API
