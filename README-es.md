# Análisis de desempeño hospitalario: Hospital María Auxiliadora (2023)

[![English](https://img.shields.io/badge/Read%20in-English-71bcf0?style=for-the-badge)](README.md)

## 1. Introducción
Este proyecto presenta un análisis de la gestión de citas médicas en el Hospital María Auxiliadora. El objetivo principal es transformar datos en información estratégica para optimizar la gestión hospitalaria y mejorar la calidad de atención al paciente mediante el monitoreo de indicadores clave (KPIs).

## 2. 🔍 El problema
El Hospital María Auxiliadora tiene un serio problema de citas perdidas: muchos pacientes reservan una cita, pero no llegan a la consulta. En 2023, 143,646 de 450,629 citas (31.9%) no fueron atendidas. Hay consultorios que operan vacíos porque nadie asiste, lo que genera una gran pérdida de tiempo médico, mientras que otros pacientes siguen esperando semanas para ser atendidos.

**Preguntas clave de negocio:**
- ¿Qué especialidades presentan los mayores cuellos de botella en tiempos de espera?
- ¿Qué áreas requieren una intervención inmediata para reducir el abandono de citas?
- ¿A más espera, más inasistencia?
- ¿Cómo se comporta la inasistencia por mes y por día de la semana en cada especialidad?
- ¿Cuáles son las especialidades que recaudan más?

## 3. 🛠️ Stack Tecnológico
- **Herramienta de BI:** Power BI Desktop.
- **Origen de Datos:** Archivo CSV con las citas de 2023 y un diccionario de datos en Excel.
- **DAX:** Para el cálculo de medidas.

## 4. 🔄 Procesamiento de Datos (ETL)
- **Limpieza:** Eliminación de registros duplicados y depuración de columnas irrelevantes para optimizar el peso del modelo.
- **Inteligencia de Tiempo:** Creación de una tabla calendario, diseñada para analizar las tendencias específicas del periodo 2023.

## 5. ⚙️ Modelado de datos
Implementación de un Esquema de Estrella (Star Schema), facilitando la escalabilidad y velocidad de las consultas.
- **Tabla de Hechos (Fact_Citas):** Contiene los eventos de citas, costos y el estado de atención.
- **Dimensiones:**
  - Dim_Calendario: Para análisis de tendencias temporales (mes, día de la semana).
  - Dim_Especialidad: Atributos de las unidades médicas.
  - Dim_Paciente: Datos demográficos.

## 6. 📊 Indicadores Clave (KPIs)
- **Valor de citas no atendidas:** Recaudación que no se cobró por citas no atendidas (S/ 1.62 millones en 2023).
- **Tasa de inasistencia:** Porcentaje de citas reservadas que no fueron atendidas (31.9%). Cada especialidad se compara con este promedio del hospital.
- **Citas atendidas y pacientes únicos:** 306,983 citas atendidas de 73,625 pacientes únicos, un promedio de 4.2 citas por paciente.
- **Oportunidad de Atención:** Tiempo promedio de espera desde la solicitud hasta la cita (19.8 días), junto con la mediana (17 días), porque algunas esperas muy largas elevan el promedio.
- **Impacto Financiero:** Top N de especialidades por recaudación de citas atendidas.

**Reglas de los rankings:** Los rankings de inasistencia y de espera solo incluyen especialidades con al menos 100 citas y al menos una cita atendida, para que unidades pequeñas o sin actividad no distorsionen la comparación. Las 17 especialidades sin ninguna cita atendida en 2023 (20,212 citas) se muestran en una vista aparte.

## 7. 🚀 Insights de negocio
- 📌 **Mayores tiempos de espera:** Entre las especialidades con actividad real, Medicina Física y Rehabilitación (43 días), Endocrinología (33 días) y Reumatología (30 días) tienen los mayores tiempos de espera promedio.
- 📌 **Alerta en Medicina Física y Rehabilitación:** Esta especialidad presenta una situación crítica, con una tasa de inasistencia del 98.1% (17,332 citas no atendidas) y la mayor espera promedio (43 días), lo que sugiere que la larga espera desincentiva la asistencia.
- 📌 **Espera e inasistencia tienen una relación débil:** Entre especialidades, la correlación entre tiempo de espera promedio y tasa de inasistencia es r = 0.23. La espera por sí sola no explica la inasistencia, por lo que conviene revisar otras causas por especialidad.
- 📌 **Especialidades sin asistencia registrada:** 17 especialidades, entre ellas Nutrición y Endocrinología, Salud Mental, Ginecología de Alto Riesgo, Neurología Pediátrica y Dermatología Pediátrica, no registraron ninguna cita atendida en 2023 (20,212 citas). Dermatología Pediátrica tiene además la mayor espera promedio del hospital (59 días).
- 📌 **Anomalía en dermatología pediátrica:** Se detectó un patrón de inasistencia el día 31 de enero de 2023, donde el 100% de los pacientes (14 citas) programados específicamente los martes no asistieron. Este hallazgo sugiere una desconexión operativa, como un error en la comunicación de la disponibilidad del especialista o un cierre administrativo no registrado en el sistema de citas, resultando en una pérdida total de eficiencia para ese turno.
- 📌 **Obstetricia por encima del promedio todos los meses:** Su tasa de inasistencia es del 55.5% frente al 31.9% del hospital, y se mantiene por encima del promedio en los 12 meses de 2023.
- 📌 **Rendimiento Financiero:** A pesar de los problemas de asistencia, Oftalmología, Psiquiatría y Cardiología lideran la recaudación, consolidándose como los pilares económicos del hospital durante el periodo analizado.

## 8. 📊 Previsualización del dashboard
- **Página 1, Desempeño:** Resumen ejecutivo con los cuatro KPIs y el ranking de especialidades con mayor inasistencia. Un botón cambia a las especialidades sin asistencia registrada.
  <img width="1600" height="900" alt="Dashboard Hospital Maria Auxiliadora" src="https://github.com/user-attachments/assets/27bcd110-5bc5-4e47-b66f-2c3298d7da28" />
- **Página 2, Valor por especialidad:** Especialidades con mayor espera, relación entre espera e inasistencia y especialidades con mayor recaudación.
  <img width="1920" height="1080" alt="Dashboard Hospital Maria Auxiliadora (1)" src="https://github.com/user-attachments/assets/4bd2ce63-7504-4d4c-b1db-21a97f1780a3" />
- **Página 3, Detalle de especialidad (obtener detalles):** Clic derecho sobre una especialidad y "Obtener detalles" para ver sus KPIs, su inasistencia mensual y su inasistencia por día de la semana, comparadas con el promedio del hospital. Se mantiene el filtro de mes elegido en la página 1.
  <!-- Agregar aquí la imagen de la Página 3 -->

## 9. Conclusiones y Recomendaciones
- **Intervención en casos críticos:** Los tiempos de espera largos se concentran en pocas especialidades, encabezadas por Medicina Física y Rehabilitación (43 días) y Dermatología Pediátrica (59 días). Se recomienda una auditoría en estas áreas para determinar si el retraso se debe a falta de personal médico, a una sobreoferta de citas u otro motivo.
- **Sistema de Recordatorios:** Implementar alertas (SMS/WhatsApp) específicamente en las 17 especialidades que presentan abandono total y en Medicina Física y Rehabilitación.
- **Sincronización de agendas médicas:** Es necesario auditar las especialidades sin asistencia en periodos específicos para asegurar que los horarios del sistema de citas coincidan con la disponibilidad real de los médicos, evitando así que los pacientes ocupen cupos en días que el servicio no está operativo.
- **Optimización de Recursos:** Reasignar el personal de especialidades con 100% de inasistencia hacia áreas de mayor demanda y recaudación, maximizando así el uso de la infraestructura hospitalaria.

## 10. Limitaciones
- **Significado del campo Atendido:** El dataset define el campo con valores Sí o No; sin embargo, en el diccionario de datos se describe el campo como Vino o No Vino (Asistencia).
  - **Impacto en el Análisis:** Existe una brecha de interpretación entre la responsabilidad del paciente (no asistir a la cita) y la gestión hospitalaria (el paciente asistió, pero no fue atendido por falta de médico, tiempo o insumos).
  - **Decisión Técnica:** Para efectos de este dashboard, se ha asumido el campo como Asistencia. Sin embargo, se recomienda estandarizar este campo en el origen para diferenciar la inasistencia.
- **Calidad de datos en el origen:** El origen incluye registros de prueba (especialidad ZPRUEBA, 2 citas) y algunos nombres de especialidad con espacios de más. Se mantuvieron tal como vienen del origen y su limpieza en Power Query está pendiente. Los conteos de especialidades de este README excluyen ZPRUEBA.
- **Umbral de los rankings:** El mínimo de 100 citas para entrar en los rankings es una decisión analítica para evitar tasas poco confiables, no una regla del hospital.
