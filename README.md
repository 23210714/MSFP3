<div align="center">

#  Práctica 3
## Modelado y control del sistema musculoesquelético

### Modelo mecánico y analogía electromecánica

**Modelado de Sistemas Fisiológicos | Ingeniería Biomédica**

**Tecnológico Nacional de México — Instituto Tecnológico de Tijuana**

![MATLAB](https://img.shields.io/badge/MATLAB-Simulink-orange)
![Python](https://img.shields.io/badge/Python-VS%20Code-blue)
![Simscape](https://img.shields.io/badge/Simscape-Electrical-green)
![Control](https://img.shields.io/badge/Control-PID-purple)

</div>

---

## Información académica

| Campo | Información |
|---|---|
| **Estudiante** | María Luisa Michelle Muñoz Meneses |
| **Número de control** | 23210714 |
| **Correo institucional** | l23210714@tectijuana.edu.mx |
| **Asignatura** | Modelado de Sistemas Fisiológicos |
| **Carrera** | Ingeniería Biomédica |
| **Docente** | Dr. Paul Antonio Valle Trujillo |
| **Correo del docente** | paul.valle@tectijuana.edu.mx |
| **Institución** | Tecnológico Nacional de México / Instituto Tecnológico de Tijuana |
| **Departamento** | Ingeniería Eléctrica y Electrónica |
| **Ubicación** | Tijuana, Baja California, México |

**Repositorio de la asignatura:**  
https://github.com/DrPaulValle/MSF-IBF1020

---

# Contenido

1. [Resumen](#1-resumen)
2. [Competencia y objetivos](#2-competencia-y-objetivos)
3. [Introducción](#3-introducción)
4. [Modelo mecánico del sistema musculoesquelético](#4-modelo-mecánico-del-sistema-musculoesquelético)
5. [Analogía electromecánica](#5-analogía-electromecánica)
6. [Variables y parámetros](#6-variables-y-parámetros)
7. [Formulación matemática](#7-formulación-matemática)
8. [Función de transferencia](#8-función-de-transferencia)
9. [Estabilidad y error en estado estacionario](#9-estabilidad-y-error-en-estado-estacionario)
10. [Implementación en MATLAB y Simulink](#10-implementación-en-matlab-y-simulink)
11. [Análisis en lazo abierto](#11-análisis-en-lazo-abierto)
12. [Diseño y sintonización PID](#12-diseño-y-sintonización-pid)
13. [Análisis en lazo cerrado](#13-análisis-en-lazo-cerrado)
14. [Implementación en Python](#14-implementación-en-python)
15. [Verificación cruzada](#15-verificación-cruzada)
16. [Diagrama biológico](#16-diagrama-biológico)
17. [Actividades y entregables](#17-actividades-y-entregables)
18. [Estructura del repositorio](#18-estructura-del-repositorio)
19. [Resultados y conclusiones](#19-resultados-y-conclusiones)
20. [Referencias](#20-referencias)

---

# 1. Resumen

En esta práctica se analiza el comportamiento dinámico del sistema musculoesquelético mediante un modelo mecánico simplificado que representa las propiedades contráctiles, elásticas y viscosas del músculo.

El sistema se describe utilizando elementos mecánicos equivalentes a resortes y amortiguadores, los cuales permiten estudiar la relación entre la fuerza muscular y el desplazamiento producido.

Posteriormente, se desarrolla una analogía electromecánica utilizando la correspondencia fuerza–voltaje, con la finalidad de representar el sistema mediante un circuito eléctrico equivalente.

Se consideran dos condiciones:

- **Control:** individuo sano.
- **Caso:** individuo con atrofia muscular simulada.

La principal diferencia entre ambas condiciones se representa mediante la modificación de la resistencia eléctrica equivalente, asociada al amortiguamiento viscoso.

Finalmente, se implementa un controlador PID para reducir la diferencia entre la respuesta del caso y la referencia correspondiente al individuo sano.

Las simulaciones se desarrollan mediante MATLAB, Simulink, Simscape Electrical y Python.

**Palabras clave:** sistema musculoesquelético, analogía electromecánica, amortiguamiento, elasticidad, controlador PID, MATLAB, Simulink, Python, atrofia muscular.

---

# 2. Competencia y objetivos

## Competencia a desarrollar

Modelar sistemas fisiológicos mediante analogías entre sistemas físicos, ecuaciones diferenciales y funciones de transferencia para analizar su comportamiento dinámico y diseñar estrategias de control mediante técnicas de control clásico.

## Objetivo general

Analizar el comportamiento dinámico de un modelo musculoesquelético simplificado, comparando las respuestas de un individuo sano y un caso simulado de atrofia muscular, para posteriormente diseñar un controlador PID que reduzca las diferencias entre ambas condiciones.

## Objetivos específicos

- Identificar los elementos mecánicos del sistema musculoesquelético.
- Comprender la relación entre fuerza, desplazamiento, elasticidad y amortiguamiento.
- Construir el circuito eléctrico equivalente mediante la analogía fuerza–voltaje.
- Formular las ecuaciones diferenciales del sistema.
- Obtener las funciones de transferencia correspondientes al control y al caso.
- Analizar la estabilidad y el error en estado estacionario.
- Simular las respuestas mediante MATLAB y Simulink.
- Comparar las respuestas en lazo abierto.
- Diseñar y sintonizar un controlador PID.
- Analizar el comportamiento del sistema en lazo cerrado.
- Reproducir las simulaciones mediante Python.
- Relacionar los componentes del modelo con estructuras anatómicas mediante BioRender.

---

# 3. Introducción

El sistema musculoesquelético está formado principalmente por músculos, tendones, huesos y articulaciones, los cuales trabajan de manera conjunta para generar movimiento y mantener la estabilidad corporal.

Los músculos poseen propiedades mecánicas que pueden describirse mediante elementos elásticos, viscosos y contráctiles.

La elasticidad permite que los tejidos recuperen su forma después de una deformación, mientras que el comportamiento viscoso representa la resistencia al movimiento y la disipación de energía.

Para analizar estas propiedades se utiliza un modelo mecánico simplificado inspirado en la representación de Hill y en los modelos viscoelásticos de tejidos biológicos.

Este modelo permite estudiar cómo la fuerza desarrollada por un músculo produce desplazamientos y cómo estos se ven afectados por sus propiedades mecánicas.

En esta práctica se analiza una condición de referencia correspondiente a un individuo sano y un caso de atrofia muscular simulado.

La diferencia entre ambos modelos se representa mediante el incremento del amortiguamiento equivalente.

El estudio se desarrolla exclusivamente mediante simulación computacional (*in silico*), por lo que los resultados tienen fines académicos y no representan tratamientos clínicos.

---

# 4. Modelo mecánico del sistema musculoesquelético

El modelo está compuesto por un elemento contráctil activo, dos elementos elásticos y un amortiguador viscoso.

Cada componente representa una propiedad mecánica del sistema muscular.

| Elemento | Símbolo | Función |
|---|---|---|
| Elemento contráctil | $F_0(t)$ | Representa la fuerza activa generada por el músculo. |
| Fuerza transmitida | $F(t)$ | Fuerza resultante transmitida por el sistema. |
| Amortiguador | $R$ | Representa el comportamiento viscoso del tejido. |
| Elemento elástico paralelo | $C_p$ | Representa propiedades elásticas pasivas del músculo. |
| Elemento elástico en serie | $C_s$ | Representa propiedades elásticas asociadas con el músculo y el tendón. |
| Desplazamiento total | $x(t)$ | Desplazamiento del sistema mecánico. |
| Desplazamiento interno | $x_1(t)$ | Desplazamiento asociado con el elemento elástico en serie. |

La fuerza activa desarrollada por el músculo se expresa como:

$$
F_0(t)=\alpha F(t)
$$

Donde:

$$
0<\alpha<1
$$

El parámetro $\alpha$ representa un factor de proporcionalidad entre la fuerza activa y la fuerza aplicada.

Para esta práctica se utiliza:

$$
\alpha=0.25
$$

## Comportamiento viscoso

La deformación correspondiente al amortiguador se expresa mediante:

$$
x_R(t)=x(t)-x_1(t)
$$

Por lo tanto, la velocidad relativa es:

$$
v_R(t)=\frac{d}{dt}[x(t)-x_1(t)]
$$

La fuerza asociada al amortiguamiento es proporcional a dicha velocidad:

$$
F_R(t)=R\frac{d}{dt}[x(t)-x_1(t)]
$$

El incremento del amortiguamiento modifica la respuesta dinámica del sistema, especialmente su velocidad de respuesta y comportamiento transitorio.

---

# 5. Analogía electromecánica

Para representar el modelo mediante un circuito eléctrico se utiliza la analogía fuerza–voltaje.

Esta analogía permite relacionar las variables mecánicas con magnitudes eléctricas.

| Sistema mecánico | Sistema eléctrico equivalente |
|---|---|
| Fuerza $F(t)$ | Voltaje $V(t)$ |
| Velocidad $\dot{x}(t)$ | Corriente $I(t)$ |
| Desplazamiento $x(t)$ | Carga eléctrica $q(t)$ |
| Amortiguador viscoso | Resistencia $R$ |
| Compliancia mecánica | Capacitancia $C$ |
| Masa | Inductancia $L$ |

Las correspondencias fundamentales son:

$$
F(t)\longleftrightarrow V(t)
$$

$$
\frac{dx(t)}{dt}\longleftrightarrow I(t)
$$

$$
x(t)\longleftrightarrow q(t)
$$

La conversión debe considerar que las conexiones mecánicas y eléctricas no necesariamente conservan la misma topología.

Los elementos mecánicos conectados en paralelo pueden representarse mediante elementos eléctricos conectados en serie, mientras que elementos mecánicos conectados en serie pueden representarse mediante elementos eléctricos conectados en paralelo.

Por esta razón, es importante identificar correctamente los nodos de referencia y los desplazamientos antes de construir el circuito equivalente.

---

# 6. Variables y parámetros

Para la simulación se consideran los siguientes valores:

| Parámetro | Control | Caso |
|---|---:|---:|
| $F(t)$ | 1 V | 1 V |
| $\alpha$ | 0.25 | 0.25 |
| $C_s$ | 10 µF | 10 µF |
| $C_p$ | 100 µF | 100 µF |
| $R$ | 100 Ω | 10 kΩ |

Los valores corresponden al circuito eléctrico equivalente utilizado durante la experimentación computacional.

## Condición de control

El modelo correspondiente al individuo sano utiliza:

$$
R_{\mathrm{control}}=100\ \Omega
$$

## Condición de atrofia muscular

El caso simulado utiliza:

$$
R_{\mathrm{caso}}=10\,000\ \Omega
$$

La relación entre ambas resistencias es:

$$
\frac{R_{\mathrm{caso}}}{R_{\mathrm{control}}}
=\frac{10\,000}{100}=100
$$

Por lo tanto, el valor de la resistencia equivalente aumenta 100 veces.

Este incremento representa una modificación importante del comportamiento viscoso del modelo.

Los demás parámetros permanecen constantes para que las diferencias observadas dependan únicamente del cambio de resistencia.

---

# 7. Formulación matemática

El modelo se analiza utilizando las relaciones constitutivas de los elementos mecánicos y las condiciones de equilibrio de fuerzas.

## Elemento viscoso

La fuerza del amortiguador está relacionada con la velocidad relativa:

$$
F_R(t)=R[\dot{x}(t)-\dot{x}_1(t)]
$$

## Elementos elásticos

Para un elemento elástico con compliancia mecánica $C$, la relación entre fuerza y desplazamiento es:

$$
F_C(t)=\frac{x(t)}{C}
$$

La fuerza correspondiente al elemento elástico paralelo puede expresarse como:

$$
F_{C_p}(t)=\frac{x(t)}{C_p}
$$

Mientras que, para el elemento elástico en serie:

$$
F_{C_s}(t)=\frac{x_1(t)}{C_s}
$$

Estas relaciones permiten construir las ecuaciones de equilibrio del sistema.

## Representación mediante ecuaciones diferenciales

La formulación del modelo se obtiene al relacionar las fuerzas de los elementos contráctiles, elásticos y viscosos.

De manera general, un sistema lineal puede representarse como:

$$
a_2\frac{d^2x(t)}{dt^2}
+a_1\frac{dx(t)}{dt}
+a_0x(t)
=
b_1\frac{dF(t)}{dt}
+b_0F(t)
$$

Los coeficientes dependen de la estructura del modelo y de sus parámetros.

**Nota:** la ecuación anterior representa una forma general. Los coeficientes específicos deben obtenerse mediante el análisis del circuito equivalente construido en la práctica.

---

# 8. Función de transferencia

La función de transferencia permite estudiar la relación entre la fuerza aplicada y el desplazamiento producido.

Considerando condiciones iniciales nulas, se aplica la transformada de Laplace.

La función de transferencia se define como:

$$
\boxed{
G(s)=\frac{X(s)}{F(s)}
}
$$

Donde:

- $X(s)$ representa el desplazamiento en el dominio de Laplace.
- $F(s)$ representa la fuerza aplicada.
- $G(s)$ representa la dinámica del sistema.

Se deben obtener dos funciones de transferencia independientes.

## Modelo de control

$$
G_{\mathrm{control}}(s)
=
\frac{X_{\mathrm{control}}(s)}{F(s)}
$$

Utilizando:

$$
R=100\ \Omega
$$

## Modelo del caso

$$
G_{\mathrm{caso}}(s)
=
\frac{X_{\mathrm{caso}}(s)}{F(s)}
$$

Utilizando:

$$
R=10\,000\ \Omega
$$

Ambas funciones deben conservar la misma estructura matemática y diferenciarse únicamente por el valor de la resistencia.

Una vez obtenidas, se implementarán en MATLAB, Simulink y Python.

---

# 9. Estabilidad y error en estado estacionario

## Análisis de estabilidad

La estabilidad del sistema se determina mediante los polos de su función de transferencia.

Para una función racional:

$$
G(s)=\frac{N(s)}{D(s)}
$$

Los polos se obtienen resolviendo:

$$
D(s)=0
$$

Un sistema lineal continuo es asintóticamente estable cuando todos sus polos tienen parte real negativa.

Se deben calcular y comparar los polos de:

$$
G_{\mathrm{control}}(s)
$$

y

$$
G_{\mathrm{caso}}(s)
$$

La comparación permitirá analizar cómo el incremento del amortiguamiento modifica la dinámica del sistema.

## Error en estado estacionario

El error entre la entrada y la salida depende de la referencia elegida y de la función de transferencia.

Para una entrada escalón unitario, cuando se cumplen las condiciones del teorema del valor final:

$$
x(\infty)=\lim_{s\to0}sX(s)
$$

Si:

$$
F(s)=\frac{1}{s}
$$

Entonces:

$$
x(\infty)=\lim_{s\to0}G(s)
$$

Este procedimiento permite comparar los valores finales de ambos modelos.

Para una entrada impulso, el valor final debe analizarse considerando las características de estabilidad del sistema.

---

# 10. Implementación en MATLAB y Simulink

La simulación se realizará mediante tres representaciones equivalentes.

| Implementación | Herramienta | Descripción |
|---|---|---|
| Modelo matemático | Simulink | Ecuaciones diferenciales del sistema. |
| Función de transferencia | Simulink | Representación entrada–salida. |
| Circuito eléctrico equivalente | Simscape Electrical | Implementación mediante resistencias y capacitancias. |

Las tres representaciones deben utilizar los mismos parámetros y condiciones iniciales.

## Configuración de simulación

| Parámetro | Valor |
|---|---|
| Tiempo inicial | 0 s |
| Tiempo final | 10 s |
| Entrada | Impulso unitario |
| Modelo de referencia | Individuo sano |
| Modelo del caso | Atrofia muscular simulada |
| Variable de salida | Desplazamiento |

El intervalo de simulación es:

$$
0\leq t\leq10\ \mathrm{s}
$$

Las respuestas deben almacenarse en el Workspace para su posterior análisis.

---

# 11. Análisis en lazo abierto

En esta etapa se comparan las respuestas del individuo sano y del caso simulado sin incorporar controladores.

Las señales principales son:

$$
x_{\mathrm{control}}(t)
$$

$$
x_{\mathrm{caso}}(t)
$$

Se aplica la misma entrada impulso unitario a ambos modelos.

La comparación debe considerar:

- Amplitud máxima de la respuesta.
- Velocidad de respuesta.
- Tiempo de establecimiento.
- Comportamiento transitorio.
- Efecto del incremento de la resistencia.
- Diferencia entre ambas condiciones.

El objetivo es identificar cómo la modificación del amortiguamiento afecta el desplazamiento del sistema.

### Evidencia de simulación

**Pendiente:** incorporar la gráfica de las respuestas en lazo abierto obtenidas mediante MATLAB/Simulink.

---

# 12. Diseño y sintonización PID

El modelo del individuo sano se utiliza como referencia para el sistema de control.

La finalidad es reducir la diferencia entre la respuesta del caso simulado y la del individuo sano.

## Señal de error

La señal de error se define como:

$$
\boxed{
e(t)=x_{\mathrm{control}}(t)-x_{\mathrm{caso}}(t)
}
$$

## Controlador PID

La acción de control está formada por tres componentes:

- Proporcional.
- Integral.
- Derivativa.

La expresión temporal del controlador es:

$$
u(t)=k_Pe(t)
+k_I\int_0^t e(\tau)\,d\tau
+k_D\frac{de(t)}{dt}
$$

En el dominio de Laplace:

$$
\boxed{
K(s)=k_P+\frac{k_I}{s}+k_Ds
}
$$

Donde:

| Parámetro | Función |
|---|---|
| $k_P$ | Acción proporcional al error. |
| $k_I$ | Acción integral para reducir el error acumulado. |
| $k_D$ | Acción derivativa que responde a la variación del error. |

## Sintonización

La sintonización se realiza mediante la herramienta **Tune** del bloque `PID Controller` en Simulink.

El controlador debe ajustarse buscando:

1. Una respuesta estable.
2. Reducción del error respecto al individuo sano.
3. Mejor seguimiento de la referencia.
4. Comportamiento transitorio adecuado.

### Ganancias del controlador

| Ganancia | Valor |
|---|---|
| $k_P$ | Pendiente |
| $k_I$ | Pendiente |
| $k_D$ | Pendiente |

Los valores se incorporarán después de realizar la sintonización.

---

# 13. Análisis en lazo cerrado

Una vez sintonizado el controlador, se repite la simulación utilizando una entrada impulso.

Se comparan tres respuestas:

$$
x_{\mathrm{control}}(t)
$$

$$
x_{\mathrm{caso}}(t)
$$

$$
x_{\mathrm{PID}}(t)
$$

Donde:

- $x_{\mathrm{control}}(t)$ representa la respuesta del individuo sano.
- $x_{\mathrm{caso}}(t)$ representa la respuesta del caso sin controlador.
- $x_{\mathrm{PID}}(t)$ representa la respuesta del caso con controlador.

El análisis debe determinar si el controlador consigue reducir la diferencia respecto a la referencia.

También se deben evaluar los cambios en amplitud, velocidad de respuesta y amortiguamiento.

### Evidencia

**Pendiente:** incorporar la gráfica comparativa de las tres respuestas y la captura de las ganancias PID obtenidas.

---

# 14. Implementación en Python

Las funciones de transferencia del modelo de control y del caso se implementarán mediante Python utilizando Visual Studio Code.

La finalidad es reproducir los resultados obtenidos en MATLAB/Simulink.

## Procedimiento

1. Definir los parámetros del modelo.
2. Construir las funciones de transferencia.
3. Establecer el vector de tiempo.
4. Generar la entrada impulso.
5. Calcular la respuesta del individuo sano.
6. Calcular la respuesta del caso simulado.
7. Incorporar las ganancias PID obtenidas mediante Tune.
8. Construir el sistema de lazo cerrado.
9. Graficar las tres respuestas.
10. Guardar las figuras para su comparación.

## Condiciones

La simulación deberá realizarse en:

$$
t\in[0,10]\ \mathrm{s}
$$

Utilizando los mismos parámetros y condiciones iniciales que MATLAB/Simulink.

Las gráficas deberán identificar adecuadamente las variables, unidades y leyendas.

---

# 15. Verificación cruzada

La verificación cruzada permite comprobar que las distintas implementaciones describen consistentemente la dinámica del sistema.

Se compararán cinco representaciones.

| Método | Herramienta | Elemento de comparación |
|---|---|---|
| Ecuaciones del sistema | Simulink | Respuesta dinámica |
| Función de transferencia | Simulink | Respuesta entrada–salida |
| Circuito equivalente | Simscape Electrical | Respuesta eléctrica equivalente |
| Cuaderno computacional | MATLAB | Gráficas y datos |
| Código independiente | Python | Respuestas simuladas |

Las diferencias observadas pueden estar relacionadas con:

- Condiciones iniciales distintas.
- Configuración del solucionador numérico.
- Diferencias en la representación del impulso.
- Discretización temporal.
- Errores en la implementación.
- Parámetros inconsistentes.

Se deberá verificar que las respuestas obtenidas sean equivalentes dentro de las tolerancias numéricas correspondientes.

---

# 16. Diagrama biológico

Se elaborará un diagrama biológico mediante BioRender para representar las estructuras musculoesqueléticas relacionadas con el modelo mecánico.

## Elementos requeridos

| Elemento anatómico | Relación con el modelo |
|---|---|
| Elemento contráctil muscular | Fuerza activa $F_0(t)$ |
| Estructuras elásticas musculares | Elemento elástico paralelo $C_p$ |
| Tendón | Elemento elástico en serie $C_s$ |
| Desplazamiento | $x(t)$ |
| Fuerza generada | $F(t)$ |
| Comportamiento viscoso | Amortiguador $R$ |

El diagrama deberá mostrar la relación entre el músculo, sus propiedades mecánicas y los elementos del circuito equivalente.

Se utilizará la misma representación anatómica para comparar el individuo sano y el caso simulado de atrofia muscular.

La diferencia principal se identificará mediante el incremento del amortiguamiento equivalente.

### Evidencia

**Pendiente:** incorporar el diagrama elaborado en BioRender.

---

# 17. Actividades y entregables

## Etapa 1. Análisis del modelo

- [ ] Identificar los elementos mecánicos.
- [ ] Analizar las fuerzas y desplazamientos.
- [ ] Establecer la analogía electromecánica.
- [ ] Construir el circuito equivalente.
- [ ] Formular las ecuaciones diferenciales.
- [ ] Obtener las funciones de transferencia.

## Etapa 2. Simulación

- [ ] Implementar el modelo matemático en Simulink.
- [ ] Implementar las funciones de transferencia.
- [ ] Construir el circuito en Simscape Electrical.
- [ ] Simular el individuo sano.
- [ ] Simular el caso de atrofia muscular.
- [ ] Comparar las respuestas en lazo abierto.

## Etapa 3. Control PID

- [ ] Construir el sistema de retroalimentación.
- [ ] Incorporar el bloque PID Controller.
- [ ] Sintonizar las ganancias mediante Tune.
- [ ] Registrar los valores de $k_P$, $k_I$ y $k_D$.
- [ ] Simular el sistema controlado.
- [ ] Comparar las tres respuestas.

## Etapa 4. Análisis computacional

- [ ] Elaborar el cuaderno MATLAB.
- [ ] Almacenar las respuestas en el Workspace.
- [ ] Crear una función para generar gráficas.
- [ ] Exportar las figuras en PDF.
- [ ] Implementar el modelo en Python.
- [ ] Comparar MATLAB y Python.

## Etapa 5. Documentación

- [ ] Elaborar el diagrama biológico.
- [ ] Guardar capturas de las simulaciones.
- [ ] Documentar los resultados.
- [ ] Redactar conclusiones.
- [ ] Organizar el repositorio de GitHub.
- [ ] Incorporar el archivo `README.md`.
- [ ] Incorporar el archivo `CITATION.cff`.

---

# 18. Estructura del repositorio

Se propone la siguiente organización:

```text
MSFP3/
│
├── README.md
├── CITATION.cff
│
├── MATLAB/
│   ├── practica_musculoesqueletico.mlx
│   └── funciones_graficas.m
│
├── Simulink/
│   ├── modelo_matematico.slx
│   ├── funcion_transferencia.slx
│   └── circuito_equivalente.slx
│
├── Python/
│   └── sistema_musculoesqueletico.py
│
├── Resultados/
│   ├── lazo_abierto.pdf
│   ├── lazo_cerrado.pdf
│   ├── control_python.pdf
│   ├── caso_python.pdf
│   └── respuesta_pid.pdf
│
├── Imagenes/
│   ├── modelo_mecanico.png
│   ├── circuito_equivalente.png
│   ├── controlador_pid.png
│   └── diagrama_biorender.png
│
└── Documentacion/
    ├── analisis_matematico.pdf
    └── conclusiones.pdf
```

Los nombres anteriores son una propuesta de organización y deberán ajustarse a los archivos utilizados durante la práctica.

---

# 19. Resultados y conclusiones

## Resultados

En esta sección se incorporarán las respuestas obtenidas mediante las diferentes herramientas computacionales.

Se deberán presentar:

- Respuesta del individuo sano.
- Respuesta del caso simulado de atrofia muscular.
- Comparación en lazo abierto.
- Ganancias del controlador PID.
- Comparación en lazo cerrado.
- Resultados obtenidos mediante Python.
- Verificación entre las diferentes implementaciones.

### Tabla de resultados

| Característica | Control | Caso | Caso con PID |
|---|---|---|---|
| Amplitud máxima | Pendiente | Pendiente | Pendiente |
| Tiempo de establecimiento | Pendiente | Pendiente | Pendiente |
| Estabilidad | Pendiente | Pendiente | Pendiente |
| Error respecto a la referencia | — | Pendiente | Pendiente |

## Discusión

El análisis se centrará en determinar cómo el incremento de la resistencia equivalente modifica la respuesta del sistema musculoesquelético.

Se comparará la respuesta del individuo sano con la del caso simulado para identificar diferencias en amplitud, velocidad de respuesta y comportamiento transitorio.

Posteriormente se evaluará si el controlador PID permite reducir dichas diferencias.

## Conclusiones

El modelado del sistema musculoesquelético mediante elementos mecánicos y circuitos eléctricos equivalentes permite estudiar la relación entre las propiedades elásticas, viscosas y contráctiles del músculo.

La analogía fuerza–voltaje facilita la implementación del sistema mediante herramientas de simulación eléctrica.

La comparación entre el individuo sano y el caso simulado permite analizar el efecto del incremento del amortiguamiento equivalente sobre la dinámica del sistema.

El diseño del controlador PID permitirá evaluar la posibilidad de reducir las diferencias entre ambas respuestas.

Finalmente, la comparación entre MATLAB, Simulink, Simscape Electrical y Python permitirá verificar la consistencia de los modelos implementados.

Las conclusiones cuantitativas se completarán después de obtener y analizar los resultados de las simulaciones.

> **Nota:** Esta práctica tiene fines exclusivamente académicos y de simulación. El controlador diseñado no constituye un tratamiento médico para la atrofia muscular.

---

# 20. Referencias

[1] M. C. Khoo, *Physiological Control Systems: Analysis, Simulation, and Estimation*, 2nd ed., IEEE Press, 2018.

[2] F. C. Hoppensteadt y C. S. Peskin, *Modeling and Simulation in Medicine and the Life Sciences*, Springer.

[3] J. E. Hall, *Guyton and Hall Textbook of Medical Physiology*, 14th ed., Elsevier, 2021.

[4] P. A. Valle, *Syllabus para Modelado de Sistemas Fisiológicos*, Tecnológico Nacional de México / Instituto Tecnológico de Tijuana, México, 2026.

---

<div align="center">

**Tecnológico Nacional de México**  
**Instituto Tecnológico de Tijuana**

**Ingeniería Biomédica**

*Modelado de Sistemas Fisiológicos — Práctica 3*

**María Luisa Michelle Muñoz Meneses**

</div>
