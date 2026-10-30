<div align="justify">
[![Open in MATLAB Online](https://www.mathworks.com/images/responsive/global/open-in-matlab-online.svg)](https://matlab.mathworks.com/open/github/v1?repo=23210714/MSFP3)

    
<div align="justify">

# Práctica 3
## Modelado y control del sistema musculoesquelético

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
| **Institución** | Tecnológico Nacional de México / Instituto Tecnológico de Tijuana |
| **Departamento** | Ingeniería Eléctrica y Electrónica |

---

## Contenido

1. [Resumen](#1-resumen)
2. [Palabras clave](#2-palabras-clave)
3. [Competencia y objetivos](#3-competencia-y-objetivos)
4. [Introducción](#4-introducción)
5. [Modelo mecánico](#5-modelo-mecánico)
6. [Analogía electromecánica](#6-analogía-electromecánica)
7. [Variables y parámetros](#7-variables-y-parámetros)
8. [Formulación matemática](#8-formulación-matemática)
9. [Función de transferencia](#9-función-de-transferencia)
10. [Estabilidad y error](#10-estabilidad-y-error)
11. [Simulación en MATLAB y Simulink](#11-simulación-en-matlab-y-simulink)
12. [Análisis en lazo abierto](#12-análisis-en-lazo-abierto)
13. [Controlador PID](#13-controlador-pid)
14. [Análisis en lazo cerrado](#14-análisis-en-lazo-cerrado)
15. [Implementación en Python](#15-implementación-en-python)
16. [Verificación cruzada](#16-verificación-cruzada)
17. [Diagrama biológico](#17-diagrama-biológico)
18. [Entregables](#18-entregables)
19. [Resultados y conclusiones](#19-resultados-y-conclusiones)
20. [Referencias](#20-referencias)

---

## 1. Resumen

En esta práctica se analiza el sistema musculoesquelético mediante un modelo mecánico simplificado que representa las propiedades contráctiles, elásticas y viscosas del músculo.

Se desarrolla una analogía electromecánica fuerza–voltaje para construir un circuito eléctrico equivalente y obtener su función de transferencia.

Se comparan dos condiciones: un individuo sano (**control**) y un caso simulado de atrofia muscular (**caso**), modificando la resistencia equivalente del sistema.

Posteriormente, se diseña un controlador PID para reducir las diferencias entre ambas respuestas. Las simulaciones se realizan mediante MATLAB, Simulink, Simscape Electrical y Python.

## 2. Palabras clave

**Sistema musculoesquelético; modelo mecánico; analogía electromecánica; atrofia muscular; elasticidad; amortiguamiento viscoso; función de transferencia; controlador PID; MATLAB/Simulink; Python; simulación *in silico*.**

---

## 3. Competencia y objetivos

### Competencia a desarrollar

Modelar sistemas fisiológicos mediante analogías entre sistemas físicos, ecuaciones diferenciales y funciones de transferencia para analizar su comportamiento dinámico y diseñar estrategias de control clásico.

### Objetivo general

Analizar el comportamiento dinámico del sistema musculoesquelético mediante un modelo mecánico y su equivalente eléctrico, comparando un individuo sano con un caso simulado de atrofia muscular e implementando un controlador PID.

### Objetivos específicos

- Identificar los elementos mecánicos del sistema.
- Construir la analogía electromecánica.
- Obtener las ecuaciones y funciones de transferencia.
- Analizar estabilidad y error en estado estacionario.
- Comparar las respuestas en lazo abierto.
- Diseñar y sintonizar un controlador PID.
- Simular las respuestas mediante MATLAB y Python.
- Relacionar el modelo con estructuras musculoesqueléticas.

---

## 4. Introducción

El sistema musculoesquelético está formado por músculos, tendones, huesos y articulaciones que permiten generar movimiento.

Sus propiedades mecánicas pueden representarse mediante elementos contráctiles, resortes y amortiguadores.

El modelo utilizado permite analizar la relación entre fuerza, desplazamiento, elasticidad y amortiguamiento.

Para representar la atrofia muscular simulada se modifica la resistencia equivalente, manteniendo constantes los demás parámetros.

---

## 5. Modelo mecánico

El modelo está compuesto por elementos contráctiles, elásticos y viscosos.

| Elemento | Símbolo | Descripción |
|---|---|---|
| Fuerza activa | $F_0(t)$ | Fuerza generada por el músculo |
| Fuerza aplicada | $F(t)$ | Fuerza transmitida |
| Amortiguador | $R$ | Comportamiento viscoso |
| Elemento elástico paralelo | $C_p$ | Elasticidad muscular pasiva |
| Elemento elástico en serie | $C_s$ | Elasticidad asociada al músculo y tendón |
| Desplazamiento | $x(t)$ | Desplazamiento total |
| Desplazamiento interno | $x_1(t)$ | Desplazamiento del elemento en serie |

La fuerza activa se expresa mediante:

$$
F_0(t)=\alpha F(t)
$$

Donde:

$$
0<\alpha<1
$$

Para esta práctica:

$$
\alpha=0.25
$$

La deformación del amortiguador es:

$$
x_R(t)=x(t)-x_1(t)
$$

---

## 6. Analogía electromecánica

Se utiliza la analogía fuerza–voltaje para transformar el modelo mecánico en un circuito eléctrico equivalente.

| Sistema mecánico | Equivalente eléctrico |
|---|---|
| Fuerza $F(t)$ | Voltaje $V(t)$ |
| Velocidad $\dot{x}(t)$ | Corriente $I(t)$ |
| Desplazamiento $x(t)$ | Carga $q(t)$ |
| Amortiguador | Resistencia $R$ |
| Compliancia mecánica | Capacitancia $C$ |
| Masa | Inductancia $L$ |

Las relaciones principales son:

$$
F(t)\longleftrightarrow V(t)
$$

$$
\dot{x}(t)\longleftrightarrow I(t)
$$

$$
x(t)\longleftrightarrow q(t)
$$

La conversión debe respetar las conexiones y referencias del modelo mecánico, considerando que la topología eléctrica puede ser diferente.

---

## 7. Variables y parámetros

Los valores utilizados para las simulaciones son:

| Parámetro | Control | Caso |
|---|---:|---:|
| $F(t)$ | 1 V | 1 V |
| $\alpha$ | 0.25 | 0.25 |
| $C_s$ | 10 µF | 10 µF |
| $C_p$ | 100 µF | 100 µF |
| $R$ | 100 Ω | 10 kΩ |

### Individuo sano

$$
R_{\mathrm{control}}=100\ \Omega
$$

### Caso de atrofia muscular

$$
R_{\mathrm{caso}}=10\,000\ \Omega
$$

La resistencia del caso es 100 veces mayor que la del control.

Esta modificación permite analizar el efecto del incremento del amortiguamiento equivalente.

---

## 8. Formulación matemática

La fuerza correspondiente al amortiguador se expresa como:

$$
F_R(t)=R\frac{d}{dt}[x(t)-x_1(t)]
$$

Para los elementos elásticos:

$$
F_{C_p}(t)=\frac{x(t)}{C_p}
$$

$$
F_{C_s}(t)=\frac{x_1(t)}{C_s}
$$

Las ecuaciones del sistema se obtienen aplicando las relaciones constitutivas y las condiciones de equilibrio mecánico.

Su representación eléctrica equivalente debe conservar el comportamiento dinámico del modelo original.

---

## 9. Función de transferencia

La función de transferencia relaciona la fuerza aplicada con el desplazamiento:

$$
\boxed{G(s)=\frac{X(s)}{F(s)}}
$$

Se consideran dos modelos.

**Individuo sano:**

$$
G_{\mathrm{control}}(s)=
\frac{X_{\mathrm{control}}(s)}{F(s)}
$$

**Caso de atrofia muscular:**

$$
G_{\mathrm{caso}}(s)=
\frac{X_{\mathrm{caso}}(s)}{F(s)}
$$

Las expresiones específicas se obtendrán mediante el análisis del circuito equivalente, sustituyendo los valores correspondientes de resistencia.

---

## 10. Estabilidad y error

### Estabilidad

La estabilidad se analiza mediante los polos de la función de transferencia:

$$
G(s)=\frac{N(s)}{D(s)}
$$

Los polos se obtienen resolviendo:

$$
D(s)=0
$$

Para un sistema continuo asintóticamente estable, todos los polos deben tener parte real negativa.

### Error en estado estacionario

Aplicando el teorema del valor final, cuando corresponde:

$$
x(\infty)=\lim_{s\to0}sX(s)
$$

Se compararán las respuestas finales del control y del caso, considerando el tipo de entrada aplicado.

---

## 11. Simulación en MATLAB y Simulink

Se implementarán tres representaciones:

| Método | Herramienta |
|---|---|
| Ecuaciones del sistema | Simulink |
| Función de transferencia | Simulink |
| Circuito eléctrico equivalente | Simscape Electrical |

### Condiciones de simulación

| Parámetro | Valor |
|---|---|
| Tiempo inicial | 0 s |
| Tiempo final | 10 s |
| Entrada | Impulso unitario |
| Referencia | Individuo sano |
| Salida | Desplazamiento |

El intervalo es:

$$
t\in[0,10]\ \mathrm{s}
$$

---

## 12. Análisis en lazo abierto

Se comparan las respuestas:

$$
x_{\mathrm{control}}(t)
$$

$$
x_{\mathrm{caso}}(t)
$$

El análisis considera amplitud, velocidad de respuesta, amortiguamiento y comportamiento transitorio.

La finalidad es identificar el efecto del incremento de la resistencia equivalente.

**Evidencia:** pendiente de incorporar la gráfica de MATLAB/Simulink.

---

## 13. Controlador PID

El individuo sano se utiliza como referencia para el caso simulado.

La señal de error es:

$$
\boxed{
e(t)=x_{\mathrm{control}}(t)-x_{\mathrm{caso}}(t)
}
$$

La ley de control PID se expresa como:

$$
u(t)=k_Pe(t)+k_I\int_0^t e(\tau)\,d\tau+k_D\frac{de(t)}{dt}
$$

En Laplace:

$$
K(s)=k_P+\frac{k_I}{s}+k_Ds
$$

### Sintonización

Se utiliza la herramienta **Tune** del bloque `PID Controller` de Simulink.

| Ganancia | Valor |
|---|---|
| $k_P$ | Pendiente |
| $k_I$ | Pendiente |
| $k_D$ | Pendiente |

El objetivo es obtener una respuesta estable y reducir el error respecto al individuo sano.

---

## 14. Análisis en lazo cerrado

Se compararán tres respuestas:

$$
x_{\mathrm{control}}(t),\qquad
x_{\mathrm{caso}}(t),\qquad
x_{\mathrm{PID}}(t)
$$

Se analizará el efecto del controlador sobre la amplitud, velocidad de respuesta, amortiguamiento y seguimiento de referencia.

**Evidencia:** pendiente de incorporar las gráficas y ganancias PID.

---

## 15. Implementación en Python

Mediante Visual Studio Code se implementarán las funciones de transferencia del control y del caso.

El procedimiento consiste en:

1. Definir los parámetros.
2. Construir las funciones de transferencia.
3. Simular la respuesta al impulso.
4. Incorporar las ganancias PID.
5. Obtener la respuesta en lazo cerrado.
6. Graficar y guardar los resultados.

Las simulaciones deberán utilizar las mismas condiciones de MATLAB/Simulink.

---

## 16. Verificación cruzada

Se compararán las respuestas obtenidas mediante cinco implementaciones.

| Método | Herramienta |
|---|---|
| Ecuaciones del sistema | Simulink |
| Función de transferencia | Simulink |
| Circuito equivalente | Simscape Electrical |
| Cuaderno computacional | MATLAB |
| Código independiente | Python |

Las diferencias pueden relacionarse con las condiciones iniciales, el solucionador numérico, la discretización del impulso o los parámetros utilizados.

---

## 17. Diagrama biológico

Mediante BioRender se elaborará un diagrama que relacione las estructuras musculoesqueléticas con los elementos del modelo.

| Estructura | Elemento del modelo |
|---|---|
| Elemento contráctil muscular | $F_0(t)$ |
| Elasticidad muscular pasiva | $C_p$ |
| Tendón | $C_s$ |
| Comportamiento viscoso | $R$ |
| Desplazamiento | $x(t)$ |
| Fuerza generada | $F(t)$ |

El diagrama permitirá identificar las diferencias entre el individuo sano y el caso simulado.

---

## 18. Entregables

El repositorio deberá contener:

- [ ] Análisis del modelo mecánico.
- [ ] Analogía electromecánica.
- [ ] Circuito eléctrico equivalente.
- [ ] Desarrollo matemático.
- [ ] Funciones de transferencia.
- [ ] Archivos MATLAB y Simulink.
- [ ] Modelo Simscape Electrical.
- [ ] Código Python.
- [ ] Gráficas de lazo abierto y cerrado.
- [ ] Ganancias PID.
- [ ] Diagrama BioRender.
- [ ] Capturas de simulaciones.
- [ ] Resultados y conclusiones.
- [ ] Archivo `README.md`.
- [ ] Archivo `CITATION.cff`.

---

## 19. Resultados y conclusiones

### Resultados

Los resultados se incorporarán después de ejecutar las simulaciones.

| Característica | Control | Caso | Caso con PID |
|---|---|---|---|
| Amplitud máxima | Pendiente | Pendiente | Pendiente |
| Tiempo de establecimiento | Pendiente | Pendiente | Pendiente |
| Estabilidad | Pendiente | Pendiente | Pendiente |
| Error respecto a referencia | — | Pendiente | Pendiente |

### Conclusiones

El modelo musculoesquelético permite analizar las propiedades elásticas, viscosas y contráctiles del músculo mediante una representación mecánica y eléctrica equivalente.

La comparación entre el individuo sano y el caso simulado permite estudiar cómo el incremento del amortiguamiento modifica la respuesta dinámica.

El controlador PID se utilizará para reducir las diferencias entre ambas condiciones, mientras que MATLAB, Simulink y Python permitirán verificar la consistencia de los resultados.

**Nota:** La práctica se desarrolla exclusivamente con fines académicos mediante simulación *in silico*.

---

## 20. Referencias

[1] M. C. Khoo, *Physiological Control Systems: Analysis, Simulation, and Estimation*, 2nd ed., IEEE Press, 2018.

[2] F. C. Hoppensteadt y C. S. Peskin, *Modeling and Simulation in Medicine and the Life Sciences*, Springer.

[3] J. E. Hall, *Guyton and Hall Textbook of Medical Physiology*, 14th ed., Elsevier, 2021.

[4] P. A. Valle, *Syllabus para Modelado de Sistemas Fisiológicos*, Tecnológico Nacional de México / Instituto Tecnológico de Tijuana, 2026.

---

<div align="justify">

**Tecnológico Nacional de México**  
**Instituto Tecnológico de Tijuana**

**Ingeniería Biomédica**

**María Luisa Michelle Muñoz Meneses**

*Modelado de Sistemas Fisiológicos — Práctica 3*

</div>
