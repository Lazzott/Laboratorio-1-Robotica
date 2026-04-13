# Laboratorio 1 - Robótica y Sistemas Autónomos

## Integrantes
- Nicolás Soto  
- Julián Toro  
- Agustín Tapia  

---

## Descripción del laboratorio

En este laboratorio se estudia el comportamiento de un robot diferencial, analizando cómo su movimiento depende de la velocidad de cada uno de sus motores.

Se evalúan:
- Las trayectorias generadas por el robot
- Cómo cambia el movimiento según la velocidad independiente de cada motor
- El efecto del control diferencial en la navegación

---

## Plataforma utilizada

Se utilizó el robot diferencial **E-puck**, el cual fue modificado para permitir control manual mediante teclado.

- Lenguaje de programación: **C**
- Entorno de simulación: **Webots**
- Tipo de control: **Manual (teclado)**

---

## Modificaciones realizadas

El código original del robot fue adaptado para:
- Permitir la interacción con el usuario
- Controlar el movimiento mediante entradas del teclado
- Ajustar las velocidades de los motores en tiempo real

---

## Instrucciones de uso

### 1. Descomprimir archivos
Descomprimir el archivo `.zip` entregado, que contiene:
- El robot
- El mundo de simulación
- Configuraciones necesarias

---

### 2. Abrir el mundo en Webots

Dentro de la carpeta descomprimida, abrir la siguiente ruta:

<img width="649" height="211" alt="image" src="https://github.com/user-attachments/assets/ed0d155a-7cac-4636-9ee5-cc8ad02adda1" />

---

### 3. Configurar el controlador

Una vez abierto el mundo en Webots:

1. En el panel izquierdo (árbol de escenas), seleccionar el robot **E-puck**
2. En el panel de propiedades, buscar el campo **controller**
3. Hacer clic y seleccionar el controlador:

<img width="246" height="580" alt="image" src="https://github.com/user-attachments/assets/c8355d7a-0901-43a8-8c66-b5e87874fd65" />
<img width="278" height="314" alt="image" src="https://github.com/user-attachments/assets/36c5acaf-d4d0-49c5-ae46-10113626035f" />



---

### 4. Ejecutar la simulación

- Iniciar la simulación en Webots
- Utilizar el teclado para controlar el robot
<img width="272" height="153" alt="image" src="https://github.com/user-attachments/assets/58ef15d4-39c7-45f4-a5e1-cc636d1400ae" />

- El robot por defecto se mueve en linea recta, el boton avanzar solo hara que vaya mas rapido mientras se mantenga presionado
  


---

## Objetivo del experimento

Comprender cómo un robot diferencial:
- Genera movimiento a partir de dos motores independientes
- Cambia su trayectoria según las velocidades relativas
- Puede ser controlado manualmente en un entorno simulado

---
## Resultados obtenidos

A partir de la implementación y ejecución del controlador del robot, se logró cumplir con los objetivos planteados para el laboratorio.

El robot diferencial fue capaz de responder correctamente a las entradas del teclado, permitiendo un control adecuado de la velocidad de cada motor. Esto se vio reflejado en los siguientes comportamientos observados:

- **Movimiento en línea recta:** al asignar la misma velocidad a ambos motores, el robot avanzó de forma recta y estable.  
- **Rotación en su propio eje:** al aplicar velocidades opuestas en los motores, el robot logró girar sobre sí mismo sin desplazarse.  
- **Movimiento curvo:** al establecer diferentes velocidades entre ambos motores, el robot generó trayectorias curvas de manera controlada.  

Estos resultados demuestran que el robot cumple con el modelo de movimiento diferencial esperado, validando que la implementación del control es correcta.

En conclusión, se consiguió lo buscado en el laboratorio, ya que el robot es capaz de moverse adecuadamente y ejecutar los distintos tipos de desplazamiento requeridos, cumpliendo con los requisitos establecidos.
