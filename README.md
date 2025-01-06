

# Proyecto: Recursividad en Java

Este proyecto demuestra el uso de **recursividad** en Java mediante la construcción y recorrido de una jerarquía de componentes, simulando una estructura de árbol. Se implementan dos enfoques: uno tradicional y otro funcional utilizando la API de Streams.

## Estructura del Proyecto

El proyecto está organizado de la siguiente manera:

```
recursividad/
├── src/
│   ├── co.jmurillo.recursividad.ejemplo/
│   │   ├── EjemploRecursividad.java
│   │   ├── models/
│   │   │   ├── Componente.java
├── .gitignore
├── recursividad.iml
└── README.md
```

### Archivos principales:

- **`Componente.java`**: Clase que modela un componente jerárquico con hijos (estructura de árbol).
- **`EjemploRecursividad.java`**: Clase principal que contiene el método `main` y las implementaciones recursivas.

---

## Descripción del Proyecto

El objetivo principal es construir una estructura jerárquica de componentes y recorrerla de forma recursiva. Esto permite entender cómo navegar estructuras complejas utilizando recursividad en Java.

### Características principales:

1. Construcción de una estructura jerárquica con componentes que pueden contener subcomponentes.
2. Implementación de métodos recursivos para recorrer esta jerarquía:
   - **Recursión tradicional** con bucles.
   - **Recursión funcional** usando la API de Streams de Java 8.

---

## Clases y Métodos

### Clase `Componente`

La clase `Componente` modela un nodo en una estructura de árbol. Contiene las siguientes propiedades y métodos:

- **Propiedades:**
  - `String nombre`: El nombre del componente.
  - `List<Componente> hijos`: Lista de subcomponentes o hijos.
  - `int nivel`: Nivel de profundidad en la jerarquía (usado para la salida visual).

- **Métodos principales:**
  - `addComponente(Componente c)`: Añade un subcomponente.
  - `tieneHijos()`: Verifica si el componente tiene hijos.
  - Métodos `get` y `set` para acceder y modificar las propiedades.

### Clase `EjemploRecursividad`

Contiene el método `main` y dos implementaciones recursivas.

#### Método `metodoRecursivo`

Este método implementa recursividad tradicional:

```java
public static void metodoRecursivo(Componente c, int nivel) {
    System.out.println("\t".repeat(nivel) + c.getNombre());
    if (c.tieneHijos()) {
        for (Componente hijo : c.getHijos()) {
            metodoRecursivo(hijo, nivel + 1);
        }
    }
}
```

- Imprime el nombre del componente, con una tabulación dependiendo del nivel.
- Llama recursivamente al mismo método para los subcomponentes.

#### Método `metodoRecursivoJava8`

Este método utiliza la API de Streams para implementar la recursividad de forma funcional:

```java
public static Stream<Componente> metodoRecursivoJava8(Componente c, int nivel) {
    c.setNivel(nivel);
    return Stream.concat(
            Stream.of(c),
            c.getHijos().stream().flatMap(hijo -> metodoRecursivoJava8(hijo, nivel + 1))
    );
}
```

- Concatena el componente actual con los streams generados recursivamente por sus hijos.
- Permite procesar los resultados como un flujo de datos.

---

## Ejecución

En el método `main`, se construye una jerarquía de componentes y se recorren usando ambos métodos.

### Construcción de la jerarquía:

```java
Componente pc = new Componente("Gabinete PC ATX");
Componente poder = new Componente("Fuente Poder 700w");
// ... (otros componentes)
cpu.addComponente(ventilador).addComponente(disipador);
placaMadre.addComponente(cpu).addComponente(ram);
pc.addComponente(poder).addComponente(placaMadre);
```

### Llamada al método recursivo funcional:

```java
metodoRecursivoJava8(pc, 0)
    .forEach(c -> System.out.println("\t".repeat(c.getNivel()) + c.getNombre()));
```

### Ejemplo de salida:

```
Gabinete PC ATX
	Fuente Poder 700w
	MainBoard Asus Sockets AMD
		Cpu AMD Ryzen 5 2800
			Ventilador GPU
			Disipador
		Nvidia RTX 3080 8GB
			Nvidia GPU RTX
			4GB Ram
			$GB Ram
			Ventiladores
		Memoria Ram 32GB
		Disco SSD 2T
	Teclado
	Mause
```

---

## Requisitos

- **Java 8 o superior** (por el uso de Streams).
- Un IDE como IntelliJ IDEA o Eclipse.

---

## Cómo ejecutar el proyecto

1. Clona este repositorio en tu máquina local.
2. Abre el proyecto en tu IDE favorito.
3. Ejecuta la clase `EjemploRecursividad`.

---

## Conceptos clave

1. **Recursividad**: Técnica donde una función se llama a sí misma para resolver problemas jerárquicos.
2. **Estructura de árbol**: Modelo jerárquico donde cada nodo puede tener varios hijos.
3. **Streams en Java**: Una API para procesar flujos de datos de forma funcional y eficiente.

---

## Autor

- **Nombre del Autor**: [Jefferson Murillo]
- **Contacto**: [Jeferson Antonio (JeffMurilloDev) Murillo Palacio Linkedin]

---

### Notas adicionales

Si tienes preguntas sobre el código o cómo mejorarlo, no dudes en contactarme o abrir una discusión en este repositorio.

--- 
