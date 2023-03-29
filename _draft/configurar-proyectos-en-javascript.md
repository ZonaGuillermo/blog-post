---

---


# Configurar proyectos en Javascript: jsconfig.json

Aunque, en pricipio, al crear un proyecto en Javascript no necesitamos una configuración previa, __es altamente recomendable__. 

Al realizar esta configuración podremos definir como debe comportarse nuestro proyecto. Esto es especialmente util en las siguientes situaciones:

- Cuando __trabajamos con algún framework__ como React, Vue, etc.
- Tenemos pensado __realizar testing__, ya que necesitaremos hacer configuraciones previas.
- Para un __uso de IntelliSense adecuado__ y optimizado a nuestro proyecto.

<br>


## Creando `jsconfig.json`

Para configurar nuestro proyecto debemos __crear en la raíz de nuestro proyecto el archivo `jsconfig.json`__. Si tenemos varios proyectos en nuestro espacio de trabajo, deberemos crear este archivo en la raíz de cada uno de los proyectos que lo integran. De esta forma evitamos que el IntelliSense de un proyecto se mezcle con el de otro.

![Workspace con varios proyectos en su interior](https://code.visualstudio.com/assets/docs/nodejs/working-with-javascript/complex_jsconfig_setup.png "Workspace con varios proyectos en su interior")

<br>


## Configurando `jsconfig.json`

`jsconfig.json` es un archivo de configuración que proviene de `tsconfig.json` por lo que podemos usar la [__referencia de TSConfig__](https://www.typescriptlang.org/tsconfig) como guía para crear nuestra configuración.

No obstante, al usar javascript en lugar de Typescript, nuestras opciones  de configuración son menores ya que no necesitamos compilar el proyecto. La referencia de TSConfig está dividida en cuatro categorías de opciones, de las cuales podemos usar las siguientes:

- [Root fields o Top level](#root-fields-o-top-level)
    - [file](#file)
    - [include](#include)
    - [exclude](#exclude)
    - [extends](#extends)
- [CompilerOptions](#compileroptions):
    - [moduleResolution](#moduleresolution)
    - [module](#module)
    - [target](#target)
    - [checkJs](#checkjs)
    - [noLib](#nolib)
    - [baseUrl](#baseurl)
    - [paths](#paths)
    - [allowSyntheticDefaultImports](#allowsyntheticdefaultimports)
    - [experimentalDecorators](#experimentaldecorators)
- [typeAquisition](#typeacquisition):
    - [enable](#enable)
    - [disableFilenameBasedTypeAcquisition](#disablefilenamebasedtypeacquisition)
    - [include](#include-1)
    - [exclude](#exclude-1)

<br>


[//]: # (Falta explicar las opciones de cada categoría)

### Root fields o Top level

### `file`

Sirve para incluir en el proyecto archivos concretos en forma de array. Si el archivo no se encuentra aparece un error.
```json
{
  "files": [
    "main.js",
    "tests.js",
    "modules.js"
  ]
}
```

### `include`

Especifica, en forma de array, rutas a nombres de archivos a incluir en el proyecto. Las rutas son relativas al directorio del `jsconfig.json`. Si no se incluye la extensión en el nombre de archivo solo que incluirán extensiones soportadas (`.js` y `.jsx`)
```json
{
  "include": ["src/**/*", "tests/**/*"]
}
```

### `exclude`

Indica un array con rutas a nombres de archivos a excluir del proyecto. Si el archivo excluido con `exclude` es importado por algún otro archivo, este se incluirá en el proyecto.

```json
{
  "exclude": ["node_modules", "**/node_modules/*"]
}
```

> __IMPORTANTE__ tanto `include`como `exclude` soportan los siguientes comodines:
- `*` sustituye a cero o más caracteres (excluyendo los separadores de directorio `/`)
- `?` sustituye a un único caracter
- `**/` Cualquier directorio anidado en cualquier nivel


### `extends`

Contiene una ruta a otro fichero de configuración del cual hereda sus propiedades.
```json
{
  "extends": "./configs/base",
}
```

The value of extends is a string which contains a path to another configuration file to inherit from. The path may use Node.js style resolution.

<br>


### CompilerOptions

### `moduleResolution`

Delimita el algoritmo que se utilizará para encontrar los módulos de nuestro código ([más info aquí](https://www.typescriptlang.org/docs/handbook/module-resolution.html)). Puede tomar 3 valores:
- `classic` actualmente en desuso (para versiones anteriores a Typescript 1.6)
- `node` Busca los módulos a la manera de __NodeJS__ (`var express = require('express');`).
- `node16` Para dar soporte a __ESModules__ desde la versión de Typescript 4.7.  (`import express from 'express';`)
```json
{
    "compilerOptions": {
        "moduleResolution": "node16",
    }
}
```

> __RECORDAD__ Si vamos a trabajar con __ESModules__ en nuestro proyecto tenemos que actualizar `package.json` con la regla `type`. Esta regla puede tomar los valores `commonjs` y `module` para módulos ESM. Si no se indica esta regla se tomará `commonjs` por defecto.
>```json
>{
>    "name": "my-project",
>    "type": "module",
>
>    "//": "...",
>    "dependencies": {
>    }
>}
>```
>
> Con esta regla debemos usar extensiones de archivo en nuestros `import` (más información [aquí](https://devblogs.microsoft.com/typescript/announcing-typescript-4-7/#type-in-package-json-and-new-extensions)).
>
> Además podremos usar otras funcionalidades como Top Level `await`.


### `module`

Especifica el sistema de módulos para la aplicación. El valor de `module` puede afectar a `moduleResolution`. Puede tener los siguientes valores:
- `none`
- `commonjs` (por defecto)
- `es6` / `es2015` (para ESModules)
- `es2020` (ESModules con importaciones dinámicas e `import.meta`)
- `esnext` (usa la última actualización de ESModules que exista)
- `node16` Permite usar módulos CommonJS o ESModules en el proyecto. La propiedad `"type": "module"` debe aparecer en `package.json`. Actualmente esta opción no funciona correctamente.
- `amd`
- `umd`
- `system`
```json
{
  "compilerOptions": {
    "module": "es6"
  }
}
```


### `target`

Configura a qué versión de Javascript se pasará el código en caso de ser transpilado. Por ejemplo, una función flecha `() => {}` se convertirá en `function () {}` si el valor de `target` es `es5` o menor.

> __RECUERDA__ para transpilar el código necesitamos instalar y configurar en el proyecto un transpilador como __Babel__ o similar, o bien usar el transpilador nativo de Typescript si nuestro proyecto en javascript está dentro de una aplicación de Typescript.

Los valores que puede usar `target` son: `es3`, `es5`, `es6` (o `es2015`), `es2016`, `es2017`, `es2018`, `es2019`,  `es2020`, `es2021`, `es2022` (hay que tener en cuenta que cada año sale una versión nueva de javascript, de ahí los diferentes valores). 
```json
{
  "compilerOptions": {
    "target": "es6"
  }
}
```


### `checkJs`

Verifica los tipos en nuestro código Javascript. El IntelliSense de nuestro IDE nos mostrará ayudas para escribir el código y nos mostrará los errores en caso de cometerlos. Conviene, por tanto, tenerla activada.
```json
{
  "compilerOptions": {
    "checkJs": true
  }
}
```


### `noLib`

Deshabilita la inclusión automática de cualquier biblioteca de definición de tipos `lib.d.ts`. Es una opción practicamente sin uso.
```json
{
  "compilerOptions": {
    "noLib": true
  }
}
```


### `baseUrl`

Se refiere a la ruta raíz de tu aplicación. Por ejemplo, en un proyecto de React sería la carpeta `src`.
```json
{
  "compilerOptions": {
    "baseUrl": "./src/"
  }
}

// -- index.js --
// import * from 'components/home.js'

// La ruta completa sería ./src/components/home.js

```

### `paths`






```json

```

### `allowSyntheticDefaultImports`
```json

```

### `experimentalDecorators`
```json

```

<br>


### typeAcquisition

 ### `enable`

 Evita que se descargen los tipos de forma automática. Esto provocará que no funcione el IntelliSense en nuestro proyecto. Si necesitas descargarlos puedes usar el [TypeSearch](https://www.typescriptlang.org/dt/search?search=) para encontrar los paquetes que necesites.
```json
{
  "typeAcquisition": { "enable": false }
}
```


### `disableFilenameBasedTypeAcquisition`

La descarga de paquetes de tipos inferida por el nombre de nuestros archivos nos permite, por ejemplo, que si tenemos un archivo llamado `jquery.js` automáticamente se descargue el paquete de tipos para JQuery en nuestro proyecto. Esto nos aporta, entre otras cosas, ayudas para escribir nuestro código mediante IntelliSense.

Con esta opción podemos desactivar ese comportamiento.
```json
{
  "typeAcquisition": { "disableFilenameBasedTypeAcquisition": true }
}
```


### `include`

Nos permite activar el uso de tipos de los paquetes instalados en nuestro proyecto, por ejemplo, para mostrar las ayudas de Intellisense. __Recuerda__ que previamente habrás tenido que descargar e instalar el paquete de tipos en el proyecto.
```json
{
  "typeAcquisition": {
    "include": ["jquery"]
  }
}
```


### `exclude`

Exluye el uso de los tipos indicados en el proyecto. Aún cuando estén instalados. Es útil cuando tenemos varios proyectos en nuestra aplicación y, por ejemplo, usamos una tecnología de testing en la aplicación principal y otra diferente en algún proyecto dentro de esta.
```json
{
  "typeAcquisition": {
    "exclude": ["jest"]
  }
}
```

<br>


## Caso de uso de `jsconfig.json`

Supongamos que vamos a crear un proyecto de React con testing por Jest, además:

- Utilizaremos el sistema de módulos nativo de Javascript.
- El Intellisense de nuestro IDE debe comprobar los tipos de datos para nuestro código Javascript moderno y para Jest.
- Al compilar, queremos que React ignore los archivos de la carpeta "node_modules" esté donde esté.

El resultado al crear y configurar nuestro `jsconfig.json` sería el siguiente:
```json
{
	"compilerOptions": {
        "module": "ES6",
        "target": "ES6",
		"checkJs": true
	},
	"typeAcquisition": {
		"include": [
			"jest"
		]
	},
	"exclude": [
		"node_modules",
		"**/node_modules/*"
	]
}
```

<br>
<br>
<hr>

## Fuentes relacionadas
- [Working with JavaScript (VSCode Docs)](https://code.visualstudio.com/docs/nodejs/working-with-javascript)
- [Jsconfig options (VSCode)](https://code.visualstudio.com/docs/languages/jsconfig#_jsconfig-options)
- [Intro to the TSConfig Reference (TS Docs)](https://www.typescriptlang.org/tsconfig)
- [Module resolution - Typescript](https://www.typescriptlang.org/docs/handbook/module-resolution.html)
- [ECMAScript Module Support in Node.js](https://devblogs.microsoft.com/typescript/announcing-typescript-4-7/#esm-nodejs)
- [Paths and baseUrl in tsconfig.json](https://medhatdawoud.net/blog/paths-and-baseUrl-in-tsconfig.json)
- [Migrating from Javascript: Writing a configuration file](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html#writing-a-configuration-file)
- [JavaScript in Visual Studio Code](https://code.visualstudio.com/docs/languages/javascript)