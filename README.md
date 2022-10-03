# Estudio sass desafío latam

En esta clase vimos la materia referente a Sass. El profesor enseño dos formas de instalar sass. Una primera instalación que ayuda a trabajar proyectos pequeños o para estudiar y una segunda forma que es la forma profesional de como hoy día se trabaja en el mercado.

### Ventajas de usar css

- Código fácil de entender, organizar, gestionar y mantener.
- Gran comunidad.
- Compatible con CSS.
- Aprobado por la industria.

# Documentación creada con tutorial

---

Aquí comienza documentación creada en tutorial de sass.
Se documenta la primera forma de instalar sass (lo que enseña el profesor) más una seria de formas de usar sass y css.

---

## Descargar compilador de css: "Live sass compiler"

Se crean archivos en respectivas carpetas (mirar archivos) y se abre compilador live sass compiler (iconos abajo a la derecha).

## Escribir css en el archivo main.scss.

Se debe ir escribiendo todo el css en el archivo main.scss. No se debe escribir nada en el main.css ya que el compilador irá agregando el código por si solo.

## Variables

Sass tiene variables desde hace mucho mas tiempo atr\ás que css. Css tiene una compatibilidad del 90% con los navegadores respecto a variables. El tema es que sass no compila las variables en variables de css si no que en el valor mismo, lo que le da un 100% de efectividad en navegadores.

Sintaxis de variables en sass:

```
$primary-color: #272727;
$accent-color: #ff652f;
$text-color: #fff;

body {
  background-color: $primary-color;
}
```

## Maps

Los maps son parecidos a los objetos en Js. Se usan para almacenar datos con una key y un valor. Los maps se inician con `()`.

```
$font-weight: (
  "regular": 400,
  "medium": 500,
  "bold": 700,
);
```

Para llamar a los datos del map se usa la siguiente sintaxis: map-get($map: , $key: );

```
body {
  font-weight: map-get($font-weight, regular);
}
```

## Nesting

El ejercicio de hacer nesting es el de poder encapsular elementos html, clases o ids para poder escribir código mas ordenado o jerárquico, osea hay un padre con hijos.

```
.main {
  width: 80%;
  margin: 0 auto;

  .main__paragraph {
    font-weight: map-get($font-weight, bold);
  }
}
```

Para no repetir muchas veces el `.main` podemos abreviar al padre utilizando un `&`.

```
.main {
  width: 80%;
  margin: 0 auto;

  &__paragraph {
    font-weight: map-get($font-weight, bold);
  }
}

Compila:
.main {
  width: 80%;
  margin: 0 auto;
}
.main__paragraph {
  font-weight: 700;
}
```

En este caso en particular al colocar el ampersand, el css compila sólo la clase y no la define dentro del padre .main, para esto debemos uitilizar algo llamado interpolación, `#{&}`.

```
.main {
  width: 80%;
  margin: 0 auto;

  #{&}__paragraph {
    font-weight: map-get($font-weight, bold);
  }
}

Compila:
.main {
  width: 80%;
  margin: 0 auto;
}
.main .main__paragraph {
  font-weight: 700;
}
```

## @import o partials

Podemos separar nuestro código en distintos archivos e importarlos desde otro archivo css.
Los archivos css que usaremos como partials se deben escribir con un guión bajo: `_resets.scss`. Así le decimos a sass que este archivo es un partial y así no generará un nuevo archivo css.
Para traer cualquier archivo que se haya hecho en archivos a parte debemos anteponer @import.

```
@import "./resets";
@import "./variables";
```

## Funciones

Las funciones de sass son parecidas a las de Js. Se definen con `@function`, se les agrega un nombre y un argumento. Se deben retornar con un `@return`.

```
@function weight($weight-name) {
  @return map-get($font-weight, $weight-name);
}

.main {
  width: 80%;
  margin: 0 auto;

  #{&}__paragraph {
    font-weight: weight(bold);

    &:hover {
      color: pink;
    }
  }
}
```

En este caso se define la función con nombre weight y en font-weight se llama la función con su nombre y sólo se le pasa el nombre del peso de la letra que queremos (antes definida en el map)

## Mixin

El mixin es una habilidad de sass para reutilizar código. Son muy parecidos a las funciones, sólo hay que entender que las funciones se debiesen usar para calcular y retornar valores. En cambio los mixin debiese usarse para definir estilos.

```
@mixin flexCenter($direction) {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: $direction;
}

.main {
  @include flexCenter(column);
  width: 80%;
  margin: 0 auto;

  #{&}__paragraph {
    font-weight: weight(bold);

    &:hover {
      color: pink;
    }
  }
}
```

En este ejemplo se agrega el mixin con nombre `flexCenter`, se agrega un argumento que define la dirección del flex (row o column) y dentro del main se llama al mixin con `@include` y se agrega el argumento.

En sass podemos utilizar metodos como en Js, por ejemplo, podemos utilizar la declaración if:

```
@mixin theme($light-theme: true) {
  @if $light-theme {
    background: lighten($primary-color, 100%);
    color: darken($text-color, 100%);
  }
}

.light {
  @include theme(true);
}
```

Se crea el mixin y se agrega un argumento por defecto (Como en Js) y en la clase se llama el mixin y se agrega el booleano como argumento para definir si el tema será oscuro o claro.

## @extends o extensiones

Es una forma de reutilizar código. Podemos utilizar `@extend` para heredar el código de alguna clase en específico y no tener que repetirlo.

```
.main {
  #{&}__paragraph1 {
    font-weight: weight(bold);

    &:hover {
      color: pink;
    }
  }

  #{&}__paragraph2 {
    @extend .main__paragraph1;

    &:hover {
      color: $accent-color;
    }
  }
}
```

## Operaciones

Css puede realizar operaciones matemáticas. Ejemplo:

```
.main {
  @include flexCenter(row);
  width: calc(80% - 400px);
  margin: 0 auto;
}
```

Con Sass podemos realizar el mismo calculo matemático pero sin la necesidad de agregar la función calc y colocando las unidades de medida con la misma unidad cada uno.

```
.main {
  @include flexCenter(row);
  width: 80% - 400px;
  margin: 0 auto;
}
```

---

Aquí termina la documentación creada por tutorial y comienza documentación respecto a clase de desafío Latam

---

# Sass desafío Latam

## Creación de documento de seguimiento de paquetes

Con npm nosotros podemos instalar una inmensidad de paquetes pre configurados que podemos usar en nuestros proyectos.

Es necesario entender de que en nuestros proyectos nosotros vamos a ir instalando distintos paquetes y es ideal que podamos ir registrando todos estos paquetes en nuestro proyecto. Por esto es necesario abrir la terminal y correr un comando npm para que se cree un archivo de reqgistro de paquetes.

Comando:

```
npm init -y
```

El comando "init" crea el archivo .json que llva el seguimiento de los paquetes y la bandera -y indica que debe cree el archivo con la configuración por defecto.

Si nosotros descargamos un proyecto de un tercero debemos correr un comando npm para que este lea todas las dependencias que aparecen en el archivo .json y las descargue y así poder trabar con todas las tecnologias usadas en el proyecto descargado.

Comando:

```
npm i
```

## Instalación de Bootstrap con npm

Con el comando npm vamos a instalar bootstrap desde la terminal y se crearan los archivos respectivos en la carpeta `node_modules`

Comando:

```
npm i bootstrap
```

La `i` representa install.

## Archivo gitignore

La carpeta `node_modules` es una carpeta con la que se trabaja de manera local y esta no pasa a producción ni se sube a github. Por esto que al momento en que se crea la carpeta y se comienzas a instlar dependencias es necesario crear el archivo `.gitignore` y dentro se declara que la carpeta `node_modules` no sea leida por git.

Crear archivo:

```
.gitignore
```

## Instalación de Sass con npm

Instalamos sass con el comando y la banderita final `-D` (D en mayúscula) indica que esta dependencia es sólo para desarollo.

```
npm i sass -D
```

### Crear script para que "vea" los cambios en sass y los convierta a .css

Para que sass valla viendo lo que vamos haciendo y creando los cambios en el archivo `.css` es necesario crear un script en el archivo `.json` indicando dónde esta nuestro archivo .scss y dónde queremos que se cree nuestra carpeta y archivos .css.

Script en archivo .json:

```
  "scripts": {
    "dev": "sass sass/custom.scss css/custom.css"
  },
```

Para ejecutar el script y que corra lo que le indicamos debemos usar el comando en la terminal.

Comando:

```
npm run dev
```

Para que la terminal quede a la "escucha" de los cambios de sass a css debiesemos estar corriendo `npm run dev` cada vez que queremos que se actualicen los datos. Para evitar esto podemos utilizar la bandera `--watch`.

Como debiese quedar el script en el .json:

```
  "scripts": {
    "dev": "sass --watch sass/custom.scss css/custom.css"
  },
```
prueba