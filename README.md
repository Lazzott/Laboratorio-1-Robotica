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

<img width="626" height="340" alt="image" src="https://github.com/user-attachments/assets/c87ff8a0-9204-43cb-869e-a92b60059a38" />

- Se adjunta en el github un video moviendo la simulacion y el como cambia la trayectoria del robot

---
## Resultados obtenidos

A partir de la implementación y ejecución del controlador del robot, se logró cumplir con los objetivos planteados para el laboratorio.

El robot diferencial fue capaz de responder correctamente a las entradas del teclado, permitiendo un control adecuado de la velocidad de cada motor. Esto se vio reflejado en los siguientes comportamientos observados:

- **Movimiento en línea recta:** al asignar la misma velocidad a ambos motores, el robot avanzó de forma recta y estable.  
- **Rotación en su propio eje:** al aplicar velocidades opuestas en los motores, el robot logró girar sobre sí mismo sin desplazarse.  
- **Movimiento curvo:** al establecer diferentes velocidades entre ambos motores, el robot generó trayectorias curvas de manera controlada.  

Estos resultados demuestran que el robot cumple con el modelo de movimiento diferencial esperado, validando que la implementación del control es correcta.

En conclusión, se consiguió lo buscado en el laboratorio, ya que el robot es capaz de moverse adecuadamente y ejecutar los distintos tipos de desplazamiento requeridos, cumpliendo con los requisitos establecidos.

## Preguntas de análisis

1. **¿Qué ocurre cuando ambas ruedas tienen la misma velocidad?**  
Cuando ambas ruedas del robot tienen la misma velocidad y giran en el mismo sentido, el robot avanza en línea recta. Esto se debe a que no existe diferencia de velocidades que genere un cambio en la orientación, por lo tanto, el movimiento es uniforme y sin desviaciones. Este comportamiento es característico de los robots diferenciales cuando no hay diferencia angular entre las ruedas.

---

2. **¿Cómo cambia la trayectoria cuando las velocidades son diferentes?**  
Cuando las velocidades de las ruedas son distintas, el robot comienza a curvarse y desviarse de la trayectoria recta. La rueda que gira más rápido recorre una mayor distancia en el mismo tiempo, lo que provoca que el robot gire hacia el lado de la rueda más lenta. Dependiendo de la diferencia de velocidades, la curva puede ser más abierta o más cerrada, generando trayectorias circulares o arcos.

---

3. **¿Qué ocurre cuando una rueda gira en sentido opuesto a la otra?**  
Cuando una rueda gira en sentido contrario a la otra, el robot rota sobre su propio eje sin desplazarse hacia adelante ni hacia atrás. Este movimiento se conoce como rotación pura, ya que el centro del robot permanece prácticamente en el mismo punto mientras cambia su orientación. Es útil para realizar giros precisos o cambiar de dirección rápidamente.

---

4. **¿Qué tipo de movimiento permite dibujar un círculo?**  
Para que el robot describa un círculo, debe realizar un movimiento curvo constante, donde ambas ruedas giran en el mismo sentido pero con diferentes velocidades. Generalmente, una rueda mantiene una velocidad mayor mientras la otra tiene una velocidad reducida, ambas constantes. Esto genera una trayectoria circular estable, donde el radio del círculo depende de la diferencia entre las velocidades de las ruedas: a mayor diferencia, menor es el radio del círculo.

