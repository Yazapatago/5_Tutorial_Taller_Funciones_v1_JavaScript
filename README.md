# 5_Tutorial_Taller_Funciones_v1_JavaScript
Taller 5 de JavaScript para compañeros del SENA de la carrera de ADSO

# Sección 15: Funciones - Creando Nuestros Propios Bloques de Código 🧱⚙️

Hasta ahora, hemos utilizado funciones que JavaScript ya nos provee, como `console.log()`, `.length`, o `prompt()`. Pero, ¿y si pudiéramos crear nuestras propias "mini-herramientas" para realizar tareas específicas que necesitamos repetir? ¡Eso es exactamente lo que son las **funciones**!

Las funciones son uno de los conceptos más importantes en programación. Nos permiten empaquetar un bloque de código, darle un nombre y luego llamarlo (ejecutarlo) cuantas veces queramos desde cualquier parte de nuestro programa.

---

### 15.1 Introducción a las Funciones

* **Concepto de Función:** Una función es un **bloque de código reutilizable** que realiza una acción específica. Piensa en ellas como recetas: tienes una receta para "hacer una suma" o para "saludar a alguien". En lugar de escribir todos los pasos cada vez, simplemente dices "quiero usar la receta de la suma".
    * **Organización:** Ayudan a que nuestro código sea más ordenado y fácil de leer.
    * **Reutilización:** Evitan que repitamos el mismo código una y otra vez (principio DRY: Don't Repeat Yourself - No te repitas).
    * **Abstracción:** Nos permiten usar un bloque de código sin necesidad de saber todos los detalles de su implementación interna.

* **Definición de Funciones:**
    Para crear una función en JavaScript, usamos la palabra clave `function` o arrow functions para versiones más modernas y concisas.

    **Sintaxis básica (con `function`):**
    ```javascript
    function nombreDeLaFuncion(parametro1, parametro2) {
        /**
         * Este es el JSDoc. Aquí se explica qué hace la función.
         * @param {tipo} parametro1 - Descripción del parámetro 1
         * @param {tipo} parametro2 - Descripción del parámetro 2
         * @returns {tipo} - Descripción del retorno
         */
        // Cuerpo de la función
        // ...realiza alguna acción...
        return valorDeRetorno;
    }
    ```

    **Sintaxis con arrow function (más moderna):**
    ```javascript
    const nombreDeLaFuncion = (parametro1, parametro2) => {
        // Cuerpo...
        return valorDeRetorno;
    };
    ```

    * **`function` o arrow `=>`**: Define la función.
    * **`nombreDeLaFuncion`**: Nombre en camelCase.
    * **`()`**: Paréntesis para parámetros.
    * **`parametro1, parametro2`**: (Opcionales) Entradas de la función.
    * **JSDoc (comentario de documentación)**: (Opcional pero recomendado) Comentario multi-línea para describir la función, params y returns.
    * **`{}`**: Bloque de código de la función.
    * **`return`**: (Opcional) Devuelve un valor. Si no hay return, devuelve `undefined`.

**Ejemplos prácticos de definición:**

```javascript
// Ejemplo 1: Función simple que no recibe ni devuelve nada
function saludar() {
    /** Imprime un saludo genérico en la consola. */
    console.log("¡Hola, aprendiz del SENA!");
}

// Ejemplo 2: Función que recibe un parámetro
function saludarPersonalizado(nombre) {
    /** Imprime un saludo personalizado usando el nombre proporcionado. */
    console.log(`¡Hola, ${nombre}! Qué bueno verte.`);
}

// Ejemplo 3: Función que recibe parámetros y devuelve un valor
function sumar(a, b) {
    /** Recibe dos números (a y b) y devuelve su suma. */
    const resultado = a + b;
    return resultado;
}

saludar();
saludarPersonalizado("Juan");
const resultadoSuma = sumar(5, 3);
console.log(`El resultado de la suma es: ${resultadoSuma}`);
```

---

## 15.2 Llamada a Funciones y Ámbito de Variables

Definir una función no la ejecuta. Es como escribir la receta, pero no cocinarla. Para usar la función, necesitas llamarla.

- **Llamada a Funciones:**  
  Se hace escribiendo el nombre de la función seguido de paréntesis `()`. Si la función espera argumentos, debes pasárselos dentro de los paréntesis.

- **Paso de Argumentos:**  
  Cuando llamas a una función, los valores que le pasas se llaman **argumentos**.  
    - **Argumentos Posicionales:** Se asignan a los parámetros en el orden en que se escriben.  
    - **Argumentos Nombrados:** En JS, se simulan pasando un objeto con claves nombradas (e.g., `{ nombre: "Juan", edad: 25 }`).

**Ejemplos Prácticos (Llamada y Argumentos):**

```javascript
// Llamando a la primera función
console.log("Llamando a la función saludar():");
saludar();

// Llamando a la segunda función con un argumento posicional
console.log("\nLlamando a saludarPersonalizado():");
saludarPersonalizado("Maria");

// Llamando a la tercera función y guardando el valor de retorno
console.log("\nLlamando a sumar() y guardando el resultado:");
const valorSuma = sumar(10, 5);
console.log(`El resultado de sumar 10 y 5 es: ${valorSuma}`);

// También se puede usar el resultado directamente
console.log(`El resultado de sumar 7 y 3 es: ${sumar(7, 3)}`);

// Simulando argumentos nombrados con un objeto
function describirPersona({ nombre, edad, ciudad }) {
    /** Muestra una descripción de una persona usando un objeto de parámetros. */
    console.log(`${nombre} tiene ${edad} años y vive en ${ciudad}.`);
}

console.log("\nLlamando con argumentos nombrados (objeto):");
describirPersona({ edad: 25, ciudad: "Bogotá", nombre: "Juan" }); // El orden no importa
```

- **Ámbito de las Variables (Scope) - Local o Global:**  
  El *ámbito* o *scope* de una variable se refiere a la parte del programa donde esa variable es accesible.  

  - **Variables Locales:** Se crean dentro de una función (con `let` o `const`). Solo existen y pueden ser usadas dentro de esa función. Una vez que la función termina, la variable local "desaparece". Los parámetros de una función también son variables locales.  
  - **Variables Globales:** Se declaran fuera de todas las funciones (o en `window` en browser). Pueden ser accedidas (leídas) desde cualquier parte del código, incluyendo dentro de las funciones.  

  **Advertencia:** Modificar variables globales desde funciones generalmente se considera una mala práctica porque puede hacer que el código sea difícil de seguir y depurar. Es preferible que las funciones reciban datos a través de sus parámetros y devuelvan resultados con `return`. En browser, usa `window.variableGlobal = valor;`.

**Ejemplos Prácticos (Ámbito):**

```javascript
// Variable Global
let saldoGlobal = 1000;

function consultarSaldo() {
    // Podemos LEER la variable global sin problemas
    console.log(`(Dentro de la función) Saldo global: ${saldoGlobal}`);
}

function realizarCompra(monto) {
    // NO modificamos la global directamente, mejor devolvemos un nuevo valor
    const nuevoSaldo = saldoGlobal - monto;
    if (nuevoSaldo >= 0) {
        console.log(`Compra realizada. Nuevo saldo: ${nuevoSaldo}`);
        return nuevoSaldo;
    } else {
        console.log("Saldo insuficiente.");
        return saldoGlobal; // Devolvemos el saldo original
    }
}

console.log("--- Ámbito de Variables ---");
consultarSaldo();
saldoGlobal = realizarCompra(200); // Reasignamos la variable global con el valor devuelto
console.log(`(Fuera de la función) Saldo global actualizado: ${saldoGlobal}`);

// Ejemplo modificando global (usar con precaución, mejor evitar)
let contadorGlobal = 0;

function incrementarContador() {
    contadorGlobal += 1; // En JS, si es global, se puede modificar directamente
    console.log(`(Dentro de incrementar) Contador ahora es: ${contadorGlobal}`);
}

console.log("\n--- Modificando variable global ---");
incrementarContador();
incrementarContador();
console.log(`(Fuera) El valor final del contador es: ${contadorGlobal}`);
```

---

## ¡A Tu Teclado! ⌨️

**Ejercicio 15.1: Función de Área de Rectángulo**

1. Define una función llamada `calcularAreaRectangulo` que reciba dos parámetros: `base` y `altura`.
2. Dentro de la función, calcula el área (`base * altura`).
3. La función debe `return` (devolver) el área calculada.
4. Fuera de la función, llama a tu función con los valores que quieras (ej: base=10, altura=5) y guarda el resultado en una variable.
5. Imprime el resultado.

```javascript
function calcularAreaRectangulo(base, altura) {
    return base * altura;
}

const base = parseFloat(prompt("Ingrese la base del rectángulo"));
const altura = parseFloat(prompt("Ingrese la altura del rectángulo"));

const rectangulo = calcularAreaRectangulo(base, altura);

console.log(`El área del rectángulo es: ${rectangulo} cm²`);
```

---

**Ejercicio 15.2: Función de Bienvenida**

1. Define una función **bienvenidaCurso** que reciba dos parámetros: **nombreAprendiz** y **nombreCurso**.
2. La función debe imprimir un mensaje de bienvenida usando template literals, por ejemplo: `¡Bienvenido/a ${nombreAprendiz} al curso de ${nombreCurso}!`.
3. Esta función no necesita devolver nada (no usará `return`).
4. Llama a la función usando argumentos posicionales.
5. Llama a la misma función simulando argumentos nombrados (con un objeto).

```javascript
function bienvenidaCurso(nombreAprendiz, nombreCurso) {
    console.log(`¡Bienvenido/a ${nombreAprendiz} al curso de ${nombreCurso}!`);
}

const nombreAprendiz = prompt("Ingrese el nombre del aprendiz: ");
const nombreCurso = prompt("Ingrese el nombre del curso: ");

bienvenidaCurso(nombreAprendiz, nombreCurso);

// Simulando nombrados con objeto
function bienvenidaCursoObj({ nombreAprendiz, nombreCurso }) {
    console.log(`¡Bienvenido/a ${nombreAprendiz} al curso de ${nombreCurso}!`);
}

bienvenidaCursoObj({ nombreAprendiz, nombreCurso });
```

---

## ¡Desafíate! 🤯

**Reto 15.1: Mini Calculadora con Funciones**  
Retoma el **Reto 8.2 (Mini Calculadora)**, pero esta vez, reestructúralo usando funciones.

1. Crea una función para cada operación matemática (`sumar`, `restar`, `multiplicar`, `dividir`). Cada una debe recibir dos números y devolver el resultado. La función de dividir debe manejar el caso de la división por cero (puede devolver `null` o un mensaje de error si el divisor es 0).
2. Crea una función principal llamada `iniciarCalculadora` que no reciba parámetros.
3. Dentro de `iniciarCalculadora`, pon el bucle while que muestra el menú, pide la opción al usuario y los dos números.
4. Dentro del bucle, según la opción del usuario, llama a la función correspondiente (`sumar`, `restar`, etc.) y muestra el resultado que esta devuelve.
5. Al final de tu script, solo necesitas hacer una llamada: `iniciarCalculadora()`.

Esta estructura hace que el código sea mucho más limpio y organizado.

```javascript
function sumar(a, b) {
    return a + b;
}

function restar(a, b) {
    return a - b;
}

function multiplicar(a, b) {
    return a * b;
}

function dividir(a, b) {
    if (b === 0) {
        return "Error: No se puede dividir por cero";
    }
    return a / b;
}

function iniciarCalculadora() {
    while (true) {
        console.log("-----------Bienvenido-----------\nMini-Calculadora");
        console.log("1. suma\n2. resta\n3. multiplicacion\n4. division\n5. salir");
        const opcion = parseFloat(prompt("Ingrese una de las opciones: "));
        
        if (opcion === 5) {
            console.log("Proceso Finalizado!! \n");
            break;
        }
        
        const num1 = parseFloat(prompt("Ingrese el 1er numero: "));
        const num2 = parseFloat(prompt("Ingrese el 2do numero: \n"));
        
        let resultado;
        if (opcion === 1) {
            resultado = sumar(num1, num2);
        } else if (opcion === 2) {
            resultado = restar(num1, num2);
        } else if (opcion === 3) {
            resultado = multiplicar(num1, num2);
        } else if (opcion === 4) {
            resultado = dividir(num1, num2);
        } else {
            console.log("Opción no válida....\n");
            continue;
        }
        
        console.log(`El resultado es: ${resultado}`);
    }
}

iniciarCalculadora();
```

---

**¡Muy bien!** Has cubierto una parte fundamental de la programación: cómo hacer que tus programas sean modulares y reutilizables con funciones. Las funciones son herramientas que usarás constantemente.
