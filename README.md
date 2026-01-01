# Análisis de desempeño hospitalario: Hospital María Auxiliadora (2023)

## 1. Introducción
Este proyecto presenta un análisis de la gestión de citas médicas en el Hospital María Auxiliadora. El objetivo principal es transformar datos en información estratégica para optimizar la gestión hospitalaria y mejorar la calidad de atención al paciente mediante el monitoreo de indicadores clave (KPIs).
## 2. El problema
El Hospital María Auxiliadora tiene un serio problema de citas perdidas: muchos pacientes reservan una cita, pero no llegan a la consulta. Actualmente, hay consultorios que están operando vacíos porque nadie asiste, lo que genera una gran pérdida de tiempo médico, mientras que otros pacientes siguen esperando semanas para ser atendidos.

**Preguntas clave de negocio:**
- ¿Qué especialidades presentan los mayores cuellos de botella en tiempos de espera?
- ¿Qué áreas requieren una intervención inmediata para reducir el abandono de citas?
- ¿Existe un perfil asociado a las mayores tasas de inasistencia?
- ¿Cuáles son las especialidades que recaudan más?
## 3. 🛠️ Stack Tecnológico
- Herramienta de BI: Power BI Desktop.
- Origen de Datos: Excel.
- DAX: ara el cálculo de medidas.
## 4. Procesamiento de Datos (ETL) y modelado
- Limpieza: Eliminación de registros duplicados y depuración de columnas irrelevantes para optimizar el peso del modelo.
- Modelado: Implementación de un Esquema de Estrella (Star Schema), facilitando la escalabilidad y velocidad de las consultas.
- Inteligencia de Tiempo: Creación de una tabla Calendario personalizada, diseñada para analizar las tendencias específicas del periodo 2023.
## 5. Modelado de datos
- Tabla de Hechos (Fact_Citas): Contiene los eventos de citas, costos y el estado de atención.
- Dimensiones:
  - Dim_Calendario: Para análisis de tendencias temporales (mes, día de la
semana).
  - Dim_Especialidad: Atributos de las unidades médicas.
  - Dim_Paciente: Datos demográficos (Sexo, Edad).
## 6. 📊 Indicadores Clave (KPIs)
- Eficiencia de Asistencia: Tasa de asistencia vs. inasistencia.
- Volumen de Pacientes: Total de atenciones segmentadas por género.
- Oportunidad de Atención: Tiempo promedio de espera (días) desde la solicitud hasta la cita.
- Tasa de inasistencia por especialidad: Análisis de especialidades con Tasa de Inasistencia del 100%, permitiendo detectar áreas donde la
oferta de citas no se traduce en atención real.
- Impacto Financiero: Top 5 de recaudación total por especialidad.
## 7. 🚀 Insights de negocio
- 📌 Se identificó un comportamiento en el Top 3 de especialidades con mayor tiempo de espera:
  + La primera (dermatología pediátrica) y tercera especialidad (neurología pediátrica) con mayor espera registran un 100% de inasistencia.
  + La segunda especialidad en espera (Medicina Física) registra un 98.1% de inasistencia.
- 📌 Alerta en Medicina Física y Rehabilitación: Esta especialidad presenta una situación crítica con una tasa de inasistencia del 98.10%
(17,332 pacientes perdidos). Además, se encuentra en el Top 3 de espera con un promedio de 43 días, sugiriendo que la larga espera
desincentiva la asistencia final.
- 📌 Anomalías en Especialidades Pediátricas: Dermatología Pediátrica y otras 17 áreas (incluyendo Nutrición y Salud Mental) registraron una
inasistencia del 100%. En el caso de dermatología pediátrica, el tiempo de espera promedio alcanza los 59 días.
- 📌 Anomalía en dermatología pediátrica: Se detectó un patrón de inasistencia el día 31 de enero de 2023, donde el 100% de los pacientes
(14 citas) programados específicamente los martes no asistieron. Este hallazgo sugiere una desconexión operativa, como un error en la comunicación de la disponibilidad del especialista o un cierre administrativo no registrado en el sistema de citas, resultando en una
pérdida total de eficiencia para ese turno.
- 📌 Rendimiento Financiero: A pesar de los problemas de asistencia, las especialidades de Oftalmología, Psiquiatría y Cardiología lideran
la recaudación, consolidándose como los pilares económicos del hospital durante el periodo analizado.
## 8. Previsualización del dashboard
- Página 1: Resumen ejecutivo del desempeño hospitalario.
- Página 2: Más análisis.
## 9. Conclusiones y Recomendaciones
- Intervención en casos críticos: Se identificó que el problema de tiempos de espera extremos (superiores a 36 días) está concentrado en
tres especialidades: Dermatología pediátrica, Medicina Física y Rehabilitación y neurología pediátrica. Se recomienda una auditoría en
estas áreas para determinar si el retraso se debe a falta de personal médico, a una sobreoferta de citas u otro motivo.
- Sistema de Recordatorios: Implementar alertas (SMS/WhatsApp) específicamente en las 18 especialidades que presentan abandono total
y en la especialidad de Medicina Física y Rehabilitación.
- Sincronización de agendas médicas: Es necesario auditar las especialidades con inasistencia perfecta en periodos específicos para
asegurar que los horarios del sistema de citas coincidan con la disponibilidad real de los médicos, evitando así que los pacientes
ocupen cupos en días que el servicio no está operativo.
- Optimización de Recursos: Reasignar el personal de especialidades con 100% de inasistencia hacia áreas de mayor demanda y recaudación, maximizando así el uso de la infraestructura hospitalaria.
## 10. Limitaciones
Durante el desarrollo del proyecto, se identificó una discrepancia en la columna
Atendido:
- Dataset: Define el campo con valores Sí o No.
- Diccionario de Datos: Describe el campo como Vino o No Vino (Asistencia).
Impacto en el Análisis: Existe una brecha de interpretación entre la responsabilidad del paciente (no asistir a la cita) y la gestión hospitalaria (el paciente asistió, pero no fue atendido por falta de médico, tiempo o insumos).
Decisión Técnica: Para efectos de este dashboard, se ha asumido el campo como Asistencia. Sin embargo, se recomienda estandarizar este campo en el origen para diferenciar la inasistencia
