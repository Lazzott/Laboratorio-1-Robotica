# Laboratorio 2 - Navegación Reactiva con Filtrado y Fusión Sensorial

## Integrantes
- Nicolás Soto  
- Julián Toro  
- Agustín Tapia  

---

# Descripción del laboratorio

En este laboratorio se implementó un sistema de navegación reactiva utilizando el robot diferencial **e-puck** en Webots.

El objetivo principal fue desarrollar un controlador autónomo capaz de:

- detectar obstáculos
- evitar colisiones
- estimar distancias
- aplicar filtros de señales
- y utilizar fusión sensorial mediante un filtro de Kalman

El sistema utiliza sensores de distancia y encoders de rueda para mejorar la percepción del entorno y la estabilidad de la navegación.

---

# Plataforma utilizada

Se utilizó el robot diferencial **e-puck** disponible en Webots.

- Lenguaje de programación: **C**
- Entorno de simulación: **Webots**
- Tipo de control: **Autónomo**
- Estrategia: **Navegación reactiva**

---

# Objetivos del laboratorio

Implementar un sistema robótico capaz de:

- detectar obstáculos mediante sensores infrarrojos
- estimar movimiento utilizando encoders
- registrar señales del robot
- aplicar filtros de suavizado
- implementar un filtro de Kalman
- y navegar autónomamente evitando colisiones

---

# Robot utilizado

El robot e-puck corresponde a un robot diferencial de dos ruedas motrices independientes.

El robot incorpora:

- sensores infrarrojos de proximidad
- encoders de rueda
- motores diferenciales
- controlador programable en C

---

# Sensores utilizados

## Sensores de distancia

Se utilizaron los siguientes sensores del e-puck:

| Sensor | Función |
|---|---|
| ps0 | frontal derecho |
| ps7 | frontal izquierdo |
| ps6 | lateral izquierdo |
| ps1 | lateral derecho |

Los sensores frontales fueron utilizados para detectar obstáculos cercanos, mientras que los sensores laterales permitieron decidir la dirección de giro durante la evasión de obstáculos.

---

## Encoders de rueda

El robot utiliza encoders integrados en ambas ruedas:

- encoder izquierdo
- encoder derecho

Estos sensores permitieron estimar el desplazamiento lineal del robot mediante el cálculo del desplazamiento angular de las ruedas.

La relación utilizada fue:

```math
s = r\theta
```

donde:

- \(s\) corresponde al desplazamiento lineal
- \(r\) corresponde al radio de la rueda
- \(\theta\) corresponde al desplazamiento angular

---

# Frecuencia de muestreo

El controlador fue ejecutado utilizando un:

| Parámetro | Valor |
|---|---|
| TIME_STEP | 64 ms |
| Frecuencia aproximada | 15.625 Hz |

La frecuencia de muestreo utilizada corresponde a:

```math
f_s = \frac{1}{T_s}
```

---

# Registro de señales

Durante la ejecución del robot se registraron:

- señales RAW de sensores
- señales filtradas mediante EMA
- estimación Kalman
- valores de encoders

La información fue almacenada en:

```text
sensor_log.csv
```

---

# Análisis de señales

## Señal RAW

La señal RAW corresponde a la lectura directa de los sensores de distancia.

Esta señal presentó:

- ruido,
- variaciones bruscas
- fluctuaciones rápidas
- sensibilidad a obstáculos cercanos

---

## Filtro EMA

Se implementó un filtro EMA (Exponential Moving Average) para suavizar las señales provenientes de los sensores frontales.

La ecuación utilizada fue:

```math
EMA_k = \alpha EMA_{k-1} + (1-\alpha)x_k
```

Este filtro permitió reducir variaciones rápidas y estabilizar la señal utilizada por el controlador.

---

# Estimación del avance mediante encoders

El desplazamiento del robot fue estimado utilizando los encoders de las ruedas.

Primero se calculó el cambio angular:

```c
delta_left = left_enc - prev_left_enc;
delta_right = right_enc - prev_right_enc;
```

Posteriormente se transformó el desplazamiento angular en desplazamiento lineal:

```math
s = r\theta
```

Finalmente se calculó el avance promedio del robot:

```math
d = \frac{d_{left}+d_{right}}{2}
```

---

# Implementación del filtro de Kalman

Se implementó un filtro de Kalman escalar para estimar la distancia frontal al obstáculo más cercano.

El filtro combina:

- predicción basada en encoders
- corrección utilizando sensores de distancia

Esto permitió mejorar significativamente la estabilidad de la estimación.

---

# Etapa de predicción

La predicción utiliza el avance estimado mediante encoders para calcular la nueva distancia esperada.

La ecuación utilizada fue:

```math
\hat{d}_k^{-} = \hat{d}_{k-1} + \Delta d_k
```

Además, se actualizó la incertidumbre del modelo:

```math
P_k^{-} = P_{k-1} + Q
```

---

# Etapa de corrección

La corrección ajusta la predicción utilizando la medición real obtenida desde los sensores frontales.

La ganancia de Kalman utilizada fue:

```math
K_k = \frac{P_k^{-}}{P_k^{-}+R}
```

La actualización de la estimación fue:

```math
\hat{d}_k = \hat{d}_k^{-} + K_k(z_k-\hat{d}_k^{-})
```

Esta etapa permitió fusionar las mediciones reales con la predicción obtenida desde los encoders.

---

# Navegación reactiva implementada

El robot utiliza una estrategia reactiva basada en la distancia frontal estimada.

## Estrategia utilizada

- Si no existen obstáculos cercanos → avanzar
- Si existe un obstáculo → girar para evitar colisión

La dirección del giro se determina utilizando sensores laterales:

- obstáculo más cercano a la izquierda → girar derecha
- obstáculo más cercano a la derecha → girar izquierda

---

# Escenarios de prueba

## Escenario 1 - Entorno limpio

Se creó un entorno sin obstaculos y amplios espacios de movimiento.
<img width="613" height="464" alt="Captura de pantalla 2026-05-24 a la(s) 11 24 09 p m" src="https://github.com/user-attachments/assets/21d31d9e-3697-4dfb-83fc-8e24bdbcfe67" />


### Resultados observados

- navegación estable
- trayectorias suaves
- pocas colisiones

---

## Escenario 2 - Entorno complejo

Se utilizó un escenario con múltiples paredes y espacios reducidos.
<img width="609" height="409" alt="Captura de pantalla 2026-05-24 a la(s) 11 25 27 p m" src="https://github.com/user-attachments/assets/c614de2e-8877-428f-805b-02072373120f" />


### Resultados observados

- aumento en maniobras evasivas
- mayor dificultad de navegación
- mejor desempeño utilizando Kalman respecto a señales RAW
- reducción de movimientos bruscos gracias al EMA

---

# Comparación de señales

| Tipo de señal | Características |
|---|---|
| RAW | señal ruidosa y variable |
| EMA | señal suavizada |
| Kalman | estimación estable y robusta |

---

# Instrucciones de ejecución

## 1. Abrir el mundo en Webots

Abrir el archivo `.wbt` incluido en el repositorio, ubicado en la carpeta worlds.
<img width="733" height="180" alt="Captura de pantalla 2026-05-24 a la(s) 11 06 40 p m" src="https://github.com/user-attachments/assets/cd171c65-d6e3-4fc4-81e1-598a9de63cd5" />
<img width="735" height="86" alt="Captura de pantalla 2026-05-24 a la(s) 11 08 24 p m" src="https://github.com/user-attachments/assets/918459de-0236-490c-9837-c6b2f51b458c" />

Se encuentran los dos escenarios disponibles, el que contiene obstaculos y el que tiene el area libre de ellos.



---

## 2. Configurar controlador

Seleccionar el robot e-puck y verificar que el controlador asignado corresponda al controlador desarrollado.
<img width="343" height="550" alt="Captura de pantalla 2026-05-24 a la(s) 11 11 55 p m" src="https://github.com/user-attachments/assets/d5404867-ff27-446e-9ba2-55adbe7a0aa7" />

<img width="343" height="415" alt="Captura de pantalla 2026-05-24 a la(s) 11 12 44 p m" src="https://github.com/user-attachments/assets/543013a8-ccad-4083-8e49-5a62445e4e70" />



---

## 3. Compilar controlador

Dentro de Webots:

```text
Build → Build Controller
```

## 4. Ejecutar simulación

Presionar:

```text
Play
```

El robot comenzará automáticamente la navegación reactiva.

---

# Resultados obtenidos

A partir de la implementación desarrollada, el robot fue capaz de:

- detectar obstáculos automáticamente
- evitar colisiones
- navegar autónomamente
- registrar señales del entorno
- suavizar señales ruidosas
- estimar distancias mediante fusión sensorial

El filtro de Kalman entregó una estimación considerablemente más estable que las señales crudas provenientes de los sensores.

---

# Conclusiones

El laboratorio permitió comprender la importancia de:

- la percepción robótica
- el procesamiento de señales
- el filtrado de ruido
- la estimación de estados
- y la fusión sensorial

La combinación entre sensores de distancia y encoders mediante Kalman permitió mejorar significativamente la estabilidad del sistema de navegación.

Además, se observó que las señales RAW presentan bastante ruido, por lo que la aplicación de filtros resulta fundamental en sistemas robóticos autónomos.
