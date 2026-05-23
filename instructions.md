Acondicionamiento de Señales y Sensores
Departamento de Tecnoloxía Electrónica

# Proyecto 1: Diseño de un sistema de instrumentación para

# pesaje estático de precisión

# Guía para la Elaboración de la Memoria

Esta guía define la estructura preceptiva que debe regir la redacción del informe técnico final. La memoria
debe redactarse con rigor académico, empleando un lenguaje técnico e impersonal, y adoptando como hilo
conductor el contraste analítico entre el diseño teórico ideal y la implementación física real, justificando
matemáticamente cualquier desviación observada durante las fases de medida y validación.

## 1. Introducción y Objetivos

- Contexto y descripción del sistema:Presentación de la arquitectura general a nivel de bloques
    (excitación, sensor, acondicionamiento analógico, digitalización y procesamiento software).
- Objetivos del proyecto:Definición clara del propósito del sistema, identificando tanto el objetivo
    principal (diseño y verificación de la báscula de precisión) como los objetivos específicos (precisión,
    robustez y validación metrológica).
- Requisitos técnicos:Síntesis de las especificaciones de diseño exigidas en el documento de Especi-
    ficaciones del Proyecto (rango de pesaje, márgenes de seguridad frente a saturación, protección del
    CMRR y superación del límite de ruido analógico).

## 2. Acondicionamiento Estático (Análisis DC y Amplificación)

- Diseño de la Ganancia (RG):Detalle del cálculo de la ganancia teórica ideal necesaria para mapear
    la salida a fondo de escala (FSO) del sensor al rango de seguridad de la tarjeta de adquisición de
    datos (DAQ). Contraste de este valor con la ganancia real obtenida según la serie comercial E96 y
    determinación de la sensibilidad teórica del sistema (mV/g).
- Análisis de Tolerancias (Worst-Case DC):Presentación de los resultados del estudio analítico
    de errores exigido en el documento de Especificaciones (desequilibrio sin carga del 5% del FSO e
    imperfecciones del amplificador). Demostración matemática de la tensión de error máxima prevista
    en el peor escenario de polaridad.
- Contraste Empírico sin Carga: Es preceptivo contrastar el límite teórico de seguridad con la
    tensión sin carga empíricamedida físicamente a la salida del amplificador. Esta medición debe
    efectuarse con la etapa analógica completamente implementada (puente sin carga, filtro de interfe-
    rencia de radiofrecuencia (RFI) y pedestal superpuesto), deduciendo el error real del sistema a partir
    de la desviación observada respecto al nivel de referencia.
- Diseño del Pedestal de Referencia:Justificación analítica de la necesidad de implementar un des-
    plazamiento de 1.0 V. Documentación del diseño del divisor resistivo e implementación de la etapa
    buffer(MCP6021 en configuración de seguidor de tensión para el aislamiento de impedancias).
    Comparativa teórico-experimental de su valor real medido en la placa de pruebas.

## 3. Acondicionamiento Dinámico (Filtrado AC y Adquisición)

- Filtros Pasivos RFI (Entrada):Exposición de las frecuencias de corte diferencial y de modo común
    teóricas. Justificación de la elección de dieléctricos (poliéster) y evaluación del impacto crítico de
    la simetría de tolerancias sobre el CMRR de la etapa de amplificación.

Proyecto 1: Diseño de un sistema de instrumentación para pesaje estático de precisión
Página 1


Acondicionamiento de Señales y Sensores
Departamento de Tecnoloxía Electrónica

- Red de Adaptación Pseudo-Diferencial:Justificación de la adopción de una topología de entrada
    diferencial en la tarjeta DAQ frente a una referenciada a masa (RSE) y demostración de la necesidad
    de implementar el equilibrio estricto de impedancias en la línea de referencia.

## 4. Análisis de Ruido y Cuantización

- Balance de error dinámico (Límite Analógico):Documentación del cálculo del suelo de ruido
    intrínseco (sumatorio en cuadratura del ruido de Johnson-Nyquist y ruido del amplificador). Con-
    versión del ruido eficaz (VRMS) a ruido pico a pico (Vp−p) y determinación del límite físico de
    detección en gramos.
- Análisis de Cuantización:Comparativa entre la amplitud del ruido analógico calculado y el escalón
    de cuantización (LSB) para justificar la idoneidad de aplicar algoritmos de promediado estadístico
    porsoftware.

## 5. Diseño del Instrumento Virtual (LabVIEW)

- Arquitectura del VI:Documentación de la estructura lógica mediante capturas delDiagrama de
    Bloques, identificando y explicando detalladamente cada etapa. Se incluirán diagramas de flujo para
    explicar la secuencia de ejecución o algoritmos específicos si se considera necesario.
- Configuración DAQ:Justificación detallada de la parametrización del móduloDAQ Assistant. Se
    deben razonar las decisiones tomadas sobre la configuración del terminal de entrada (modo diferen-
    cial frente a RSE), el rango de tensión y, muy especialmente, la estrategia de muestreo (frecuencia
    y número de muestras) para equilibrar la estabilidad de la lectura con el tiempo de respuesta del
    sistema.
- Procesado e Interfaz:Explicación detallada de la lógica matemática implementada en el bloque
    funcional de “Tara” (para la supresión de la tensión residual sin carga), el algoritmo de “Calibración
    Lineal de Dos Puntos” (fijación del cero y ajuste delspan) y el algoritmo de filtrado por “Promediado
    por bloques”. Se requiere la inclusión de capturas delPanel Frontalen funcionamiento (tanto sin
    carga como bajo carga), justificando la utilidad operativa y metrológica de todos los controles e
    indicadores desarrollados.

## 6. Validación y Resultados Experimentales

- Metodología de Calibración:Descripción detallada del procedimiento de ajuste empírico efec-
    tuado en el laboratorio mediante la captura del estado sin carga (fijación del cero) y la aplicación de
    la masa de referencia de 1.000 kg (empleada como patrón de calibración para la determinación de
    la pendiente o ajuste delspan).
- Análisis de Desempeño: Presentación de los datos experimentales obtenidos (estabilidad de la
    lectura, resolución efectiva lograda y linealidad). Inclusión de fotografías del montaje físico real en
    la placa de pruebas y de la disposición mecánica de la célula de carga.

## 7. Conclusiones

Evaluación crítica del grado de cumplimiento de los parámetros técnicos estipulados en el documento de
Especificaciones del Proyecto. Análisis técnico de los retos encontrados durante la traslación del modelo
matemático al prototipo físico y formulación de propuestas de mejora viables para futuras iteraciones del
diseño.

Proyecto 1: Diseño de un sistema de instrumentación para pesaje estático de precisión
Página 2


Acondicionamiento de Señales y Sensores
Departamento de Tecnoloxía Electrónica

## 8. Referencias Bibliográficas

Relación exhaustiva de todas las fuentes consultadas, incluyendo obligatoriamente las hojas de característi-
cas (datasheets) de los componentes electrónicos seleccionados, los manuales de usuario de la instrumenta-
ción y la bibliografía teórica de apoyo. Es preceptivo aplicar con rigor un estándar de citación reconocido
en ingeniería (p. ej., formato IEEE).

```
Nota Gráfica:La memoria debe poseer un carácter visual que certifique y facilite la comprensión técnica del
diseño. Se exige la inclusión de figuras, capturas de pantalla, esquemas eléctricos y fotografías del prototipo en
todos los apartados pertinentes. Todo elemento gráfico deberá estar debidamente numerado, titulado y explíci-
tamente referenciado en el cuerpo del texto.
```
Proyecto 1: Diseño de un sistema de instrumentación para pesaje estático de precisión
Página 3


# Proyecto 1: Diseño de un sistema de instrumentación para pesaje estático de precisión

## Rúbrica de Evaluación

```
Categoría Peso 0 - 4.9 5 - 6.9 7 - 8.9 9 - 10
```
1. Análisis Teórico 20%

```
Cálculos incompletos. No
se evalúa elWorst-Case DC
ni se determina el escalón
de cuantización (LSB).
```
```
Cálculos básicos de ganan-
cia y error DC. Balance de
ruido (Vp−p) con deficien-
cias.
```
```
Cálculos precisos.
Contraste numérico
correcto entre el ruido
analógico y el LSB.
```
```
Se justifica la idoneidad del
promediado porsoftware
basándose en el FSR y el
número de bits del ADC.
```
2. MontajeHardware 25%

```
Montaje inestable. No se
respeta el pedestal de 1.0 V
ni se implementa el filtro
pasivo RFI.
```
```
Circuito funcional pero asi-
métrico. Adaptación pseu-
do-diferencial con impedan-
cias desequilibradas.
```
```
Montaje limpio. Se imple-
menta el pedestal (1.0 V) y
se preserva el CMRR en la
etapa de entrada.
```
```
Diseño metrológicamente
robusto. Equilibrio estricto
de impedancias. Señal
acondicionada coherente
con el modelo en el rango
de carga (0-1.5 kg).
```
```
3.SoftwareLabVIEW 20%
```
```
Tarjeta DAQ configurada en
modo RSE. Función de Tara
mal definida o calibración
errónea.
```
```
Tarjeta DAQ configurada en
modo diferencial. Se imple-
menta promediado y
calibración básica sin
justificar sus parámetros.
```
```
Softwareestable. Acondi-
cionamiento matemático
exacto (fijación del cero y
ajuste delspan).
```
```
Interfaz ergonómica. Se
justifica la ventana de 32
muestras equilibrando
estabilidad y tiempo de
respuesta.
```
4. Validación y Datos 15%

```
Sin calibración con la masa
de referencia de 1.000 kg.
Conversión dinámica a
gramos defectuosa.
```
```
Calibración realizada empí-
ricamente. Conversión
funcional pero sin análisis
crítico de desviaciones.
```
```
Resultados sólidos. Se vali-
da el contraste de la tensión
sin carga frente a las previ-
siones del modelo.
```
```
Caracterización completa:
sensibilidad, linealidad y
rango dinámico. Mejora de
resolución efectiva demos-
trada empíricamente.
```
5. Calidad de Memoria 20%

```
Redacción coloquial. Sin
formato. Erratas metroló-
gicas graves (ej. “5 Voltios”
en vez de “5 voltios”).
```
```
Se sigue la estructura de la
Guía. Gráficos y capturas
incluidos pero mal referen-
ciados.
```
```
Lenguaje impersonal.
Ortotipografía impecable
(cursivas en extranjerismos,
unidades SI en minúscula).
```
```
Nivel de publicación
técnica. Trazabilidad
absoluta. Uso riguroso de
citas bibliográficas en el
cuerpo del texto para
justificar datos técnicos.
```
### 1


Notas adicionales para la calificación:

- Penalización por configuración errónea de la tarjeta DAQ:La configuración de las entradas analógicas en modo RSE supondrá el suspenso automático de la categoría
    3, al comprometer directamente el rechazo al modo común (CMRR) y vulnerar las especificaciones de inmunidad al ruido.
- Criterio de Resolución Efectiva:Se valorará la explicación matemática de cómo el promediado supera la barrera del ruido analógico respecto al límite teórico calculado
    (aplica a categoría 4).
- Penalización de estilo:El uso de la primera persona o la ruptura de las normas ortotipográficas (mayúsculas en unidades, omitir cursivas enhardware) penalizará con
    hasta 1.5 puntos la nota del apartado 5.

### 2


Acondicionamiento de Señales y Sensores
Departamento de Tecnoloxía Electrónica

# Proyecto 1: Diseño de un sistema de instrumentación para

# pesaje estático de precisión

# Especificaciones del Proyecto

## Objetivos

El objetivo principal del proyecto es diseñar, desarrollar y verificar un sistema de instrumentación electrónica
de medida, desde su concepción teórica hasta su implementación física. Este objetivo se particulariza en el
diseño de una báscula de precisión orientada al pesaje estático de recipientes de hasta 1.5 kg. Se requiere
garantizar la robustez metrológica del sistema, contrastando de forma continua el modelo matemático de
tolerancias y ruido (Error Budget) con el comportamiento real delhardwareimplementado.

## 1. Material Disponible

```
a) Célula de carga resistiva de aluminio de 5 kg de capacidad máxima y sensibilidad nominal de
1 mV/V [1].
```
```
b) Circuitos Integrados: Referencia de tensión de precisión MCP1541 [2], Amplificador Operacional
MCP6021 [3] y Amplificador de Instrumentación AD623 [4].
```
```
c) Componentes pasivos: Selección de resistencias de precisión (1%) de la serie E96 para la fijación
de ganancia y etapas críticas de acondicionamiento, resistencias estándar para funciones auxiliares,
así como condensadores cerámicos multicapa (MLCC) y de película de poliéster para el filtrado y la
estabilización de las redes de simetría del puente.
```
```
d) Tarjeta de adquisición de datos (DAQ) National Instruments NI USB-6001 [5].
```
```
e) Entorno de programación gráfica LabVIEW [6].
```
```
f) Masa de referencia: Recipiente de 1 litro de capacidad (asumido metrológicamente como patrón de
calibración de 1.000 kg).
```
## 2. Plan de Desarrollo

Para alcanzar el objetivo final del proyecto, se establecen las siguientes fases de ejecución:

```
a) Estudio previo analítico:Análisis teórico de las señales generadas por el puente de Wheatstone,
cálculo de las tolerancias de error en el peor de los escenarios (Worst-Case DC Analysis), y evalua-
ción de la resolución física del sistema, limitada por el ruido térmico y el escalón de cuantización,
estrictamente definido por el bit menos significativo (LSB), empleando como referencia las especifi-
caciones de los fabricantes [2][4][5]. Para la correcta justificación de este apartado, se deben realizar
los siguientes cálculos:
```
- Análisis de tolerancias DC (Worst-Case):Se cuantificará la tensión de error máxima prevista
    en la salida del sistema. Para este estudio analítico, se establecerá como premisa un dese-
    quilibrio sin carga del 5% de la salida a fondo de escala (FSO) para la célula de carga. Este
    error de partida deberá sumarse a las imperfecciones del amplificador extraídas de su hoja de
    características: tensión deoffsetde entrada, corrientes de polarización (evaluando su caída de
    tensión en la etapa de filtrado) y tensión deoffsetde salida. Se asumirá la superposición li-
    neal de todos los errores en el escenario de polaridad más desfavorable, aplicando la ganancia
    del sistema exclusivamente a aquellos errores generados en la etapa de entrada para demostrar
    matemáticamente el peor escenario de desviación antes de la saturación.

Proyecto 1: Diseño de un sistema de instrumentación para pesaje estático de precisión
Página 1


Acondicionamiento de Señales y Sensores
Departamento de Tecnoloxía Electrónica

- Evaluación del ruido y resolución analógica:Se determinará el suelo de ruido intrínseco del
    hardware. Para ello, se calculará el ruido térmico de Johnson-Nyquist aportado por las resis-
    tencias del filtro diferencial (aplicando el factor de corrección para el ancho de banda equiva-
    lente de ruido, NEB) y se sumará en cuadratura con el ruido de tensión de entrada del propio
    amplificador. El ruido eficaz (RMS) resultante deberá convertirse a ruido pico a pico (Vp−p)
    empleando el factor de cresta estadístico industrial (≈ 6 .6). La división de este ruido pico a
    pico entre la sensibilidad global delhardwaredefinirá el límite físico de detección en gramos.
- Análisis de cuantización:Se determinará la magnitud del LSB del convertidor analógico-digital
    de la tarjeta DAQ, basándose en su rango de tensión de entrada y en su número de bits. Este
    escalón de cuantización deberá contrastarse numéricamente con el ruido analógico pico a pico
    (Vp−p) calculado previamente, con el fin de justificar la idoneidad de aplicar algoritmos de
    promediado estadístico porsoftware.

```
b) Montaje y verificación dehardware:Diseño y montaje de las etapas de excitación, adaptación
de niveles DC y filtrado AC. Es preceptiva la verificación instrumental de los niveles de tensión en
reposo para validar los márgenes de seguridad antes de proceder a la conexión con la tarjeta DAQ.
```
```
c) Diseñosoftware:Desarrollo y verificación del instrumento virtual (VI) para la adquisición, proce-
sado digital, calibración empírica y representación de las señales empleando LabVIEW.
```
```
d) Elaboración de la memoria técnica:Redacción del informe final de proyecto conforme a la “Guía
para la Elaboración de la Memoria”, documentando la validación metrológica del sistema y justifi-
cando las desviaciones entre las previsiones analíticas y el rendimiento empírico medido.
```
## 3. Especificaciones de DiseñoHardware(Acondicionamiento de Señal)

El sistema constará de los siguientes bloques funcionales, los cuales deberán ser dimensionados y justifica-
dos analíticamente:

- Excitación del sensor: Circuito basado en la referencia de tensión de precisión MCP1541 para
    dotar al puente de Wheatstone de una polarización unipolar estable de 4.096 V.
- Generación de Referencia (Pedestal Virtual):Implementación de un divisor resistivo mediante
    componentes comerciales estándar, aislado a través de un seguidor de tensión (MCP6021), con el
    fin de superponer un potencial de referencia de 1.0 V en la etapa de amplificación. Este nivel es
    un requisito de diseño imprescindible para proteger el sistema frente a la saturación derivada de
    desequilibrios mecánicos y errores deoffsetde polaridad negativa.
- Filtrado Híbrido de Interferencia de Radiofrecuencia (RFI) (Entrada):Diseño de un filtro dife-
    rencial pasivo que priorice la simetría de impedancias (requiriendo el uso de dieléctricos de poliéster)
    para fijar una frecuencia de corte diferencial cercana a 5 Hz y maximizar la atenuación del ruido de
    modo común, preservando el CMRR del amplificador.
- Etapa de Amplificación: Implementación del AD623 para adecuar la señal diferencial de baja
    amplitud a niveles de tensión que optimicen el rango dinámico de la tarjeta DAQ sin incurrir en
    saturación. Se exigirá la justificación del valor comercial seleccionado dentro de la serie E96 para
    la resistencia de ganancia (RG, 1%).
- Red Antialiasing y Adaptación Pseudo-Diferencial (Salida):Para compensar las derivas térmicas
    inherentes al circuito generador de referencia (1.0 V), la salida del sistema no deberá referenciarse
    a la masa analógica. Es obligatoria la implementación de una red de adaptación pasiva simétrica
    (doble filtro RC) entre los terminales de salida y referencia del amplificador y los terminales de
    entrada de la tarjeta DAQ, asegurando el equilibrio estricto de impedancias.

Proyecto 1: Diseño de un sistema de instrumentación para pesaje estático de precisión
Página 2


Acondicionamiento de Señales y Sensores
Departamento de Tecnoloxía Electrónica

## 4. Especificaciones de Adquisición y Procesado (LabVIEW)

El instrumento virtual interactuará con elhardwareejecutando las siguientes etapas de procesamiento en
tiempo real:

- Configuración de la tarjeta DAQ:La adquisición de datos debe configurarse obligatoriamente
    seleccionando el terminal de entrada en modo diferencial (frente a un modo referenciado a masa,
    RSE) para maximizar el rechazo al ruido de modo común, en estricta concordancia con la red de
    adaptación implementada en elhardware. El rango de tensión y la estrategia de muestreo (frecuencia
    y número de muestras) se ajustarán para equilibrar la estabilidad de la lectura con el tiempo de
    respuesta del sistema.
- Filtrado Digital:Aplicación de un algoritmo de promediado por bloques (ventana estática de 32
    muestras) destinado a atenuar la varianza del ruido analógico residual, optimizando la resolución
    efectiva del pesaje y estabilizando la tasa de actualización en pantalla.
- Acondicionamiento Matemático:Implementación de un bloque funcional de “Tara” para la supre-
    sión de la tensión residual sin carga, y un algoritmo de “Calibración Lineal de Dos Puntos” (fijación
    del cero y ajuste delspan). Este procedimiento empleará la captura del estado sin carga y la aplica-
    ción de la masa de referencia de 1.000 kg (patrón de calibración) para la determinación empírica de
    la pendiente, permitiendo así la conversión dinámica de la variable eléctrica (voltios) a la variable
    física (gramos).
- Interfaz de Usuario (Panel Frontal):Representación ergonómica del valor instantáneo de masa y
    su evolución gráfica temporal, incorporando los controles necesarios para la operatividad integral de
    la báscula.

## 5. Referencias Bibliográficas

```
[1] Hoja de características genérica para célula de carga Single-Point de aluminio (5 kg).
```
```
[2] Microchip Technology Inc.MCP1525/41: 2.5V and 4.096V Voltage References Datasheet.
```
```
[3] Microchip Technology Inc.MCP6021/1R/2/3/4: Rail-to-Rail Input/Output, High Precision Opera-
tional Amplifier Datasheet.
```
```
[4] Analog Devices.AD623: Single-Supply, Rail-to-Rail, Low Cost Instrumentation Amplifier
Datasheet.
```
```
[5] National Instruments.NI USB-6001/6002/6003 Device SpecificationsyUser Guide.
```
```
[6] National Instruments.LabVIEW User Manual.
```
Proyecto 1: Diseño de un sistema de instrumentación para pesaje estático de precisión
Página 3





