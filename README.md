# Convertidor Buck 30V a 15V con Sistema de Protección para Paneles Solares

> Proyecto de electrónica de potencia desarrollado y simulado en PLECS para aplicaciones fotovoltaicas con protección automática por sobrevoltaje y bajo voltaje.

## Descripción General

Este proyecto consiste en el diseño y simulación de un convertidor DC-DC tipo Buck realizado completamente en **PLECS**, cuyo propósito es reducir un voltaje de entrada de **30V a 15V**.

El sistema está enfocado en aplicaciones fotovoltaicas, donde la energía proveniente de un panel solar puede presentar variaciones importantes de voltaje dependiendo de las condiciones ambientales.

El objetivo principal del proyecto es alimentar una carga DC con un voltaje estable y seguro, además de implementar un sistema de protección inteligente que permita apagar automáticamente el convertidor cuando el voltaje de entrada salga de los límites establecidos.

---

# 📖 Introducción

Los convertidores DC-DC son ampliamente utilizados en sistemas de electrónica de potencia para adaptar niveles de voltaje de acuerdo con los requerimientos de diferentes dispositivos electrónicos.

En este proyecto se implementó un convertidor Buck capaz de reducir el voltaje proveniente de un panel solar de **30V a 15V**, permitiendo alimentar correctamente una carga de corriente directa.

Debido a que los paneles solares pueden presentar variaciones de voltaje ocasionadas por cambios de irradiancia, temperatura o condiciones de carga, se agregó un sistema de protección que supervisa constantemente el voltaje de entrada.

Cuando el voltaje supera el límite superior de **50V** o disminuye por debajo de **24V**, el convertidor se apaga automáticamente colocando el ciclo de trabajo (Duty Cycle) en cero, evitando daños en los componentes electrónicos y garantizando una operación segura.

---

# 🎯 Objetivos

## Objetivo General

Diseñar y simular un convertidor Buck de 30V a 15V con protecciones de seguridad para sistemas fotovoltaicos utilizando PLECS.

## Objetivos Específicos

* Reducir el voltaje de entrada de 30V a 15V.
* Implementar el control PWM del convertidor.
* Diseñar un sistema de protección por sobretensión y bajo voltaje.
* Desactivar automáticamente el convertidor en condiciones inseguras.
* Analizar el comportamiento del sistema mediante simulación.

---

# ⚙️ Funcionamiento del Convertidor

El convertidor Buck opera reduciendo el voltaje de entrada mediante el control del ciclo de trabajo del PWM aplicado al MOSFET de conmutación.

Para este proyecto:

* Voltaje de entrada nominal: **30V**
* Voltaje de salida deseado: **15V**

El sistema monitorea constantemente el voltaje proveniente del panel solar y evalúa si se encuentra dentro del rango seguro de operación.

---

# 🛡️ Sistema de Protección

El convertidor cuenta con dos protecciones principales:

## 1. Protección por Sobretensión

Cuando el voltaje de entrada:

```text
Vin > 50V
```

El sistema realiza las siguientes acciones:

* El ciclo de trabajo se vuelve cero.
* El PWM se deshabilita.
* El convertidor se apaga automáticamente.
* Se protege la carga y los componentes electrónicos.

---

## 2. Protección por Bajo Voltaje

Cuando el voltaje de entrada:

```text
Vin < 24V
```

El sistema:

* Desactiva el PWM.
* Lleva el Duty Cycle a cero.
* Apaga completamente el convertidor.
* Evita funcionamiento inestable.

<h2>Grafica de Simulación</h2>

<p align="center">
  <img src="https://github.com/Salazar0423/STM32_PANEL_SOLAR_LOCEIN/blob/7183db9c91f53e97b2cf27032a8a98d85ff01e95/Simula.png" width="350"/>
</p>

<p align="center">
  Gráfica de validación del sistema de protección del convertidor Buck.
</p>

---

# 🔍 Lógica de Operación

| Condición del Voltaje | Estado del Convertidor |
| --------------------- | ---------------------- |
| 24V ≤ Vin ≤ 50V       | Operación normal       |
| Vin > 50V             | Protección activada    |
| Vin < 24V             | Protección activada    |

---

# 📡 Variables Utilizadas

## Voltaje de Entrada (Vin)

Variable principal obtenida desde el panel solar.

Se utiliza para:

* Supervisar el rango seguro de operación.
* Activar las protecciones.
* Habilitar o deshabilitar el convertidor.

## Duty Cycle

Controla el tiempo de conducción del MOSFET.

* En condiciones normales permite obtener 15V de salida.
* En condición de falla se establece en cero.

---

# 🖥️ Simulación en PLECS

Todo el sistema fue desarrollado y simulado en **PLECS**, incluyendo:

* Etapa de potencia.
* Control PWM.
* Comparadores de protección.
* Lógica AND de habilitación.
* Monitoreo de voltaje.
* Señales de control.

La simulación permitió verificar:

* La correcta reducción de voltaje.
* El funcionamiento de las protecciones.
* El apagado automático del convertidor.
* La estabilidad del sistema.

---

##  Lógica de Protección

La siguiente implementación muestra la lógica utilizada en PLECS para habilitar o deshabilitar el PWM dependiendo del voltaje de entrada del convertidor.

<p align="center">
  <img src="https://github.com/Salazar0423/STM32_PANEL_SOLAR_LOCEIN/blob/bb5dead720c56d651e5754f11edced24e1dcd779/protec.png" width="500"/>
</p>

<p align="center">
  Implementación de protección por sobrevoltaje y bajo voltaje.
</p>

# 🔌 Diseño Electrónico

El repositorio ahora incluye:

## 📐 Esquemático de la PCB

Diseño esquemático del convertidor Buck incluyendo:

* Etapa de potencia.
* Control PWM.
* Protecciones.
* Componentes pasivos.
* Interconexiones principales.

## 🖥️ Implementación PCB

Como parte del desarrollo del proyecto, se contempla el diseño de una PCB dedicada para integrar la etapa de potencia, control y protección en una sola tarjeta electrónica compacta y eficiente.

El diseño de la PCB estará orientado a:

* Reducir ruido eléctrico.
* Mejorar la disipación térmica.
* Optimizar trayectorias de corriente.
* Facilitar el ensamblaje SMD.
* Incrementar la confiabilidad del sistema.

### Consideraciones del PCB

#### Etapa de Potencia

Los MOSFETs de potencia en encapsulado D2PAK requerirán:

* Planos de cobre amplios.
* Vías térmicas.
* Separación adecuada entre potencia y control.

#### Señales de Control

Las señales PWM y retroalimentación serán ruteadas lejos de las líneas de alta corriente para minimizar interferencias electromagnéticas.

#### Resistencia Shunt

La resistencia shunt contará con conexiones Kelvin para mejorar la precisión de medición de corriente.

#### Fuentes Auxiliares

Las etapas basadas en LM5169 incluirán:

* Capacitores de desacoplo cercanos.
* Bucles de corriente reducidos.
* Distribución compacta.

## 📊 Validación del Sistema

El proyecto incluye:

* Simulación completa en PLECS.
* Validación de protecciones.
* Verificación de PWM.
* Formas de onda de validación.
* Verificación de señales de control.
* Análisis de estabilidad.

## 🎯 Objetivo del PCB

El objetivo final del diseño PCB es obtener un sistema:

* Compacto.
* Seguro.
* Eficiente.
* Fácil de fabricar.
* Preparado para futuras pruebas físicas.

---

# ☀️ Aplicaciones

El convertidor está enfocado principalmente en aplicaciones fotovoltaicas, donde el voltaje proveniente del panel solar puede variar dependiendo de:

* Irradiancia solar.
* Temperatura.
* Condiciones climáticas.
* Variaciones de carga.

Debido a estas variaciones, se implementó una ventana segura de operación para proteger la etapa de potencia.

## Aplicaciones del convertidor Buck

* Sistemas fotovoltaicos.
* Regulación de energía DC.
* Electrónica de potencia.
* Alimentación de cargas DC.
* Conversión de energía renovable.

---

# 📦 Lista de Materiales (BOM)

| Componente / Función   | Designador     | Descripción Técnica                  | Encapsulado      | Cantidad | Precio Unitario (USD) | Total (USD) |
| ---------------------- | -------------- | ------------------------------------ | ---------------- | -------- | --------------------- | ----------- |
| Regulador Auxiliar     | U1, U2         | LM5169FDDAR 100V Sincrónico          | SO PowerPAD-8    | 2        | $2.45                 | $4.90       |
| Control (MCU)          | U3             | STM32F103C8T6, 64KB Flash, 72MHz     | LQFP-48          | 1        | $3.50                 | $3.50       |
| Driver de Compuerta    | U4, U5         | IR2110S High/Low Side Driver         | SOIC-16W         | 2        | $1.85                 | $3.70       |
| MOSFETs de Potencia    | Q1, Q2         | IRFS460 N-Channel 500V 20A           | D2PAK            | 2        | $4.20                 | $8.40       |
| Resistencia Shunt      | R2             | 10 mΩ, Seteo de Corriente, 1-2W      | 2512             | 1        | $0.45                 | $0.45       |
| Inductor Principal     | L1             | 100 µH Blindado, Alta Corriente      | SMD (12x12mm)    | 1        | $2.10                 | $2.10       |
| Inductores Auxiliares  | L2, L3         | 22 µH para LM5169                    | SMD 6045         | 2        | $0.65                 | $1.30       |
| Capacitores de Entrada | C2, C3, C4, C5 | 22 µF, 50V Banco de Filtrado         | 1210             | 4        | $0.35                 | $1.40       |
| Capacitores de Salida  | C8 al C13      | 150 µF, 35V Electrolítico / Polímero | SMD Can / Caso D | 6        | $0.60                 | $3.60       |
| Pasivos Varios         | R, C genéricos | Resistores y capacitores 0805/1206   | 0805 / 1206      | 24       | $0.04                 | $0.94       |
| Conectores de Prueba   | J1 al J6       | Headers PWM, DRV y señales           | SMD / TH 2.54mm  | 6        | $0.10                 | $0.60       |

## Costo Total Estimado

```text
$30.89 USD
```

---

# 🔩 Componentes Principales

# 📋 Parámetros del Sistema

| Parámetro                  | Valor |
| -------------------------- | ----- |
| Voltaje de entrada nominal | 30V   |
| Voltaje de salida          | 15V   |
| Voltaje máximo permitido   | 50V   |
| Voltaje mínimo permitido   | 24V   |
| Tipo de convertidor        | Buck  |
| Plataforma de simulación   | PLECS |

---

# 🧩 Diagrama General

```text
Panel Solar
     │
     ▼
Sensor de Voltaje
     │
     ▼
Sistema de Protección
     │
     ▼
PWM + Control
     │
     ▼
Convertidor Buck
     │
     ▼
Carga DC
```

---

# 📈 Resultados Esperados

* Conversión estable de 30V a 15V.
* Funcionamiento seguro ante variaciones del panel solar.
* Apagado automático en condiciones críticas.
* Protección de los componentes electrónicos.
* Estabilidad del sistema bajo diferentes condiciones.

---

# Aplicaciones

* Sistemas fotovoltaicos.
* Regulación de energía DC.
* Electrónica de potencia.
* Alimentación de cargas DC.
* Conversión de energía renovable.

---

# 🚀 Trabajo Futuro

Actualmente el proyecto fue desarrollado completamente mediante simulación en PLECS para validar el comportamiento del convertidor Buck y el funcionamiento del sistema de protección.

Como trabajo futuro, se buscará implementar el sistema en hardware físico mediante el diseño y fabricación de una PCB funcional, permitiendo realizar pruebas reales de operación con paneles solares y cargas DC.

Las futuras etapas del proyecto contemplan:

* Fabricación de la PCB.
* Implementación física del convertidor.
* Pruebas experimentales.
* Validación térmica de los MOSFETs.
* Optimización del sistema de control.
* Integración completa con paneles solares reales.
* Análisis de eficiencia energética.

El objetivo final es convertir la simulación desarrollada en un prototipo funcional de electrónica de potencia aplicable a sistemas fotovoltaicos.

---

# 👨‍💻 Integrantes
    
* Cesar Rodolfo Tovar Salazar
* Ian Miguel Muñoz Chairez
* Oscar Lopez Zaragoza

---

Proyecto académico desarrollado para el análisis y simulación de un convertidor Buck con protecciones de seguridad aplicado a sistemas fotovoltaicos utilizando PLECS.
