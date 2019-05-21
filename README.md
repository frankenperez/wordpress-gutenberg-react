# Desarrollo de bloques de WordPress Gutenberg con React

## Introducción

Gutenberg, el nuevo editor de WordPress basado en bloques, está cambiando el modo de trabajar y desarrollar con este gestor de contenidos. Una de sus novedades es el cambio en el stack de tecnologías, que han convertido a JavaScript en la principal herramienta de desarrollo para este editor.

Las posibilidades que nos ofrece Gutenberg se hacen casi infinitas cuando podemos crear nuestros propios bloques de contenido personalizados. Partiendo de un ejemplo sencillo, desarrollaremos nuevos bloques de contenido mediante JavaScript, sirviéndonos de la propia capa de abstracción que Gutenberg ha implementado sobre React.

## WordPress Gutenberg

WordPress, empleando su API REST, JavaScript y React, ha diseñado una nueva experiencia de edición para páginas y publicaciones basada en bloques, conocida como Gutenberg y disponible a partir de su versión 5.0.

Puedes echar un vistazo a la [demo de las principales funcionalidades presentadas en la WordCamp US de 2017](https://videopress.com/v/DK5mLrbr) y probar cómo funciona [en su web oficial](https://wordpress.org/gutenberg/).

### Los Bloques

Un **bloque** de Gutenberg es la unidad fundamental en la que se inserta y organiza el contenido y que, junto a otros, compone una publicación en la web, de modo similar a los tradicionales shortcodes.

Encontramos una serie de **bloques predeterminados** en el nuevo editor de WordPress y que se dividen en categorías según su contenido o función en:

- Comunes
- Formato
- Diseño
- Widgets
- Incrustados

Cada bloque está delimitado por un comentario **HTML**, ya sea una etiqueta de cierre automático o con una etiqueta de inicio y una etiqueta de fin. En la etiqueta principal, según el tipo de bloque y las personalizaciones del usuario, podemos encontrar un objeto JSON.

Ejemplo de estructura de un **bloque serializado**.

```html
<!-- wp:paragraph {"key": "value"} -->
<p>Welcome to the world of blocks.</p>
<!-- /wp:paragraph -->
```

Cada bloque contiene **atributos** o ajustes de configuración, que se pueden obtener a partir de HTML sin procesar en el contenido, a través de meta u otros orígenes personalizables.

Los bloques son elementos **jerárquicos**, de modo que un bloque puede contener múltiples bloques en su interior y, a su vez, estar contenido en un bloque de orden superior.

Los bloques pueden ser estáticos o dinámicos en función de su contenido. Esta separación conceptual de bloques es útil para diseñar nuestro proyecto:

- Los bloques **estáticos** contienen contenido representado y un objeto de atributos que se utiliza para mostrarse.
- Los bloques **dinámicos** requieren datos y representación del lado del servidor mientras se genera el contenido de la publicación.

Muchos de los bloques predeterminados de WordPress pueden que no cubran la funcionalidad que requiera tu proyecto, por lo que será un buen momento para crear tu propio bloque de Gutenberg.

## Paso a paso: Creando un bloque de WordPress Gutenberg

### Antes de empezar

En este taller trabajaremos con diferentes tecnologías sobre las que sería recomendable que tuvieras  **conocimientos previos** antes de continuar:

- JavaScript (ES6+)
- React y sintaxis JSX
- Node y NPM
- PHP
- Desarrollo de temas y/o plugins para WordPress

El proyecto Gutenberg ha incorporado las librerías de **React y ReactDOM** en el núcleo de WordPress, proporcionando mayor libertad y flexibilidad para crear nuevas interfaces de usuario en WordPress.

> Si a lo largo del taller necesitas ayuda o información extra, puedes consultar [el manual oficial de Gutenberg](https://developer.wordpress.org/block-editor/) y su [repositorio en GitHub](https://github.com/WordPress/gutenberg)

### Primeros pasos

1. Configura un **entorno de desarrollo local** con la última versión de WordPress. Puedes encontrar más información en la [Guía de desarrollo de WordPress](https://make.wordpress.org/core/handbook/tutorials/installing-a-local-server/)

2. Instala **Node.js** para tu sistema operativo. Node es un intérprete de Javascript del lado del servidor, de código abierto y gratuito que se ejecuta en varias plataformas (Windows, Linux, Unix, Mac OS X, etc.) utilizando el motor de JavaScript V8 de Chrome.

    [Descárgalo aquí](https://nodejs.org/es/download/) e instálalo.

    Durante la instalación de Node, se instalará también **npm**, el sistema de gestión de paquetes por defecto para Node.js

Para la creación de un nuevo bloque personalizados de Gutenberg, trabajaremos en el **contexto de plugins** o "territorio plugin" de WordPress.

Entre otras, existen dos opciones principales para crear nuestros propios bloques de contenido para mostrar en páginas y artículos: utilizando el paquete de herramientas `create-guten-block` y trabajando con la API de Bloque o Block API.

### Create Guten Block

[Create Guten Block](https://github.com/ahmadawais/create-guten-block) es un kit de herramientas para desarrolladores, similar al paquete `create-react-app`, con frecuentes actualizaciones, que no requiere configuración y que contiene todo el código necesario para la creación de bloques, por lo que es un buen *punto de partida* para conocer la estructura y los archivos necesarios para tener un nuevo bloque en Gutenberg.

Para comenzar, accede al directorio de plugins `/wp-content/plugins/` de tu entorno WordPress local y ejecuta en el terminal el siguiente comando, reemplazando `my-block` por el nombre único que desees para tu nuevo plugin:

```bash
npx create-guten-block my-block
```

> Se requiere Node v8 o superior y npm v5.3 o superior en tu entorno de desarrollo local. Puedes emplear nvm en  sistemas macOS/Linux o `nvm-windows` para cambiar fácilmente entre distintas versiones de Node.

Una vez finalizado, se habrá generado un **nuevo plugin** con el nombre que hayas introducido para tu proyecto. En este nuevo directorio encontrarás todos los archivos y herramientas necesarias para crear un nuevo componente:

```txt
/wp-content/plugins/my-block

├── .gitignore
├── plugin.php
├── package.json
├── README.md
|
├── dist
|  ├── blocks.build.js
|  ├── blocks.editor.build.css
|  └── blocks.style.build.css
|
└── src
   ├── block
   |  ├── block.js
   |  ├── editor.scss
   |  └── style.scss
   |
   ├── blocks.js
   ├── common.scss
   └── init.php
```

Abre este directorio a través del terminal, en nuestro caso con: `cd my-block`, y ejecuta `npm start` para lanzar nuestro plugin en modo de desarrollo (podrás ver mensajes de error, alertas y otras notificaciones en la consola del navegador web).

> Puedes encontrar más información sobre los scripts disponibles y lo que incluye este kit de herramientas en su [repositorio en GitHub](https://github.com/ahmadawais/create-guten-block).

Accede al panel de administración de WordPress y activa el nuevo plugin que encontrarás con el nombre `my-block - CGB Gutenberg Block Plugin`. El plugin creará un nuevo bloque disponible en el editor Gutenberg que podrás emplear en cualquier página o entrada de tu sitio.

...

### Block API

Para ello, crearemos un nuevo plugin en el que incluiremos los archivos necesarios para un nuevo bloque de Gutenberg.

...

## Recursos

[Tutorial de WordPress para la creación de bloques](https://developer.wordpress.org/block-editor/tutorials/block-tutorial/)