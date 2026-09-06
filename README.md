# 🥗 Análisis de Mercado y Viabilidad Gastronómica Plant-Based | Denver, CO

Este proyecto combina la extracción de datos en tiempo real mediante la **API de Yelp** y el análisis exploratorio de datos (**EDA**) de una base demográfica de consumo gastronómico en EE. UU. (30,000 registros). El objetivo principal es evaluar la viabilidad comercial y la demanda para nuevos establecimientos de comida basada en plantas (vegetariana y vegana) en la ciudad de Denver, Colorado.

---

## 📋 Tabla de Contenidos
- [Objetivos del Proyecto](#-objetivos-del-proyecto)
- [Arquitectura de Datos y Tecnologías](#-arquitectura-de-datos-y-tecnologías)
- [Procesamiento y Normalización de Datos](#-procesamiento-y-normalización-de-datos)
- [Hallazgos E Insights Clave](#-hallazgos-e-insights-clave)
- [Estructura del Repositorio](#-estructura-del-repositorio)
- [Instrucciones de Ejecución](#-instrucciones-de-ejecución)

---

## 🎯 Objetivos del Proyecto
1. **Evaluar el ecosistema actual**: Consultar la API de Yelp para catalogar la oferta competidora (restaurantes vegetarianos/veganos en Denver) en términos de rating, volumen de reseñas, rango de precios y categoría.
2. **Identificar el perfil del consumidor local**: Analizar la base demográfica de residentes de Denver ($N=2,523$) para determinar nivel socioeconómico, hábitos de gasto, consumo de alcohol y preferencias alimenticias.
3. **Validar viabilidad técnica y comercial**: Cruzar la disposición al gasto con la oferta competidora existente para detectar oportunidades de mercado no cubiertas.

---

## 🛠️ Arquitectura de Datos y Tecnologías
- **Lenguaje:** Python 3.14+
- **Extracción de Datos:** REST API (Yelp API v3) vía `requests`
- **Procesamiento de Datos:** `pandas`, `numpy`
- **Visualización:** `matplotlib`, `seaborn`
- **Archivos de Salida:** CSV (`utf-8-sig`)

---

## 🧹 Procesamiento y Normalización de Datos (Data Hygiene)
Durante la fase de auditoría de datos en la muestra de consumidores ($N=30,000$), se aplicaron las siguientes reglas de negocio y correcciones de ingeniería de datos:

- **Deduplicación:** Se verificó la inexistencia de registros duplicados (`id_persona` + `ciudad_residencia`).
- **Corrección de Outliers en Edad:** Se detectó e imputó una anomalía de tipex de $300\text{ años} \to 30\text{ años}$ ($547$ casos). Para valores nulos restantes ($0.33\%$), se utilizó la mediana.
- **Tratamiento de Nulos por Imputación Implicada:**
  - `promedio_gasto_comida`: Rellenado condicional utilizando la mediana agrupada por `ciudad_residencia`.
  - `preferencias_alimenticias`: Normalización de cadenas (trimming/capitalización), conversión de nulos implícitos (`'Nan'`, `'None'`, `''`) a `NaN` reales e imputación mediante la moda general (`'Carnes'`).
- **Segmentación Geográfica:** Filtrado final centrado exclusivamente en residentes de la ciudad de **Denver** ($N=2,523$).

---

## 📈 Hallazgos e Insights Clave
1. **Atractivo Demográfico Plant-Based:** En Denver, la preferencia por dietas basadas en plantas alcanza un **32.82%** combinado (Vegetariano: 21.93%, Vegano: 10.89%), situándose como el segundo grupo de preferencia más grande después de la carne.
2. **Consumo Complementario de Licor:** El **61.61%** de los encuestados consume licor de manera habitual. Los modelos gastronómicos en Denver incrementan su ticket promedio al integrar ofertas de coctelería o maridaje especializado.
3. **Madurez y Competitividad del Mercado en Yelp:** La oferta competidora en Denver cuenta con valoraciones altas ($4.0+$ estrellas), pero exhibe alta variabilidad en el volumen de reseñas, señalando una oportunidad para capturar mercado si se incentiva el feedback del cliente.

---

## 📂 Estructura del Repositorio
```text
.
├── notebooks/
│   └── analisis_mercado_denver.ipynb    # Código fuente principal (EDA + API Yelp)
├── data/
│   ├── base_datos_restaurantes_USA_v2.csv # Dataset demográfico crudo/procesado
│   └── restaurantes_vegetarianos_denver.csv # Datos extraídos de la API de Yelp
├── README.md                            # Documentación del proyecto
└── requirements.txt                     # Librerías necesarias

🚀 Instrucciones de Ejecución
Clonar el repositorio:

Bash
git clone [https://github.com/usuario/analisis-gastronomico-denver.git](https://github.com/usuario/analisis-gastronomico-denver.git)
cd analisis-gastronomico-denver
Instalar dependencias:

Bash
pip install -r requirements.txt
Ejecutar las celdas del cuaderno en Jupyter Notebook o Google Colab.


---

### Informe de Negocio Profesional

**A:** Comité Ejecutivo de Inversión / Dirección Estratégica  
**DE:** Equipo de Analytics & Inteligencia de Mercado  
**FECHA:** 6 de Septiembre, 2026  
**ASUNTO:** Informe de Viabilidad de Mercado Gastronómico Plant-Based en Denver, Colorado  

---

#### Executive Summary
El presente informe evalúa la factibilidad comercial para la apertura de un nuevo concepto gastronómico vegetariano/vegano en la ciudad de Denver, CO. Mediante el cruce de datos demográficos de la población objetivo ($N=2,523$) y la radiografía de competidores actuales obtenida a través de la API de Yelp, se concluye que **Denver representa un mercado maduro, de alto poder adquisitivo y con una clara demanda no saturada en la oferta de rango medio-alto**.

---

#### 1. Diagnóstico Demográfico y Hábitos del Consumidor en Denver

**Distribución Socioeconómica y Estilo de Vida**
* **Nivel Socioeconómico:** El mercado objetivo de Denver concentra un **61.21%** de consumidores pertenecientes a los estratos Medio (31.08%) y Alto (30.13%) [source: 3].
* **Preferencia Alimenticia:** Aunque la categoría "Carnes" lidera el consumo con un 31.06% [source: 3], el segmento basado en plantas representa una cuota conjunta del **32.82%** (Vegetariano: 21.93%, Vegano: 10.89%) [source: 3]. Este volumen confirma que 1 de cada 3 consumidores potenciales demanda activamente menús libres de carne.
* **Hábitos de Consumo de Licor:** Un **61.61%** de la muestra declara consumir licor [source: 3]. Este factor indica que los restaurantes que integran oferta de coctelería o bebidas artesanales logran incrementar de manera directa la rentabilidad sobre la mesa.

| Variable Analizada | Categoría Dominante | Porcentaje | Implicación Directa de Negocio |
| :--- | :--- | :--- | :--- |
| **Género** | Paridad (F: 50.15% / M: 49.85%) [source: 3] | 100.0% | El concepto debe apelar a una comunicación unisex y neutral. |
| **Preferencia Alimenticia** | Plant-Based (Veg + Vegano) [source: 3] | **32.82%** [source: 3] | Muestra base amplia para sostener un concepto especializado. |
| **Consumo de Licor** | Sí [source: 3] | **61.61%** [source: 3] | Imprescindible contar con licencia de alcohol y carta de coctelería. |
| **Estrato Socioeconómico** | Medio - Alto - Muy Alto [source: 3] | **79.46%** [source: 3] | Alta disposición al pago por experiencia y calidad de ingredientes. |

---

#### 2. Análisis del Entorno Competitivo (API de Yelp)

La extracción de datos crudos sobre la oferta vegetariana/vegana activa en Denver revela los siguientes puntos cardinales [source: 2]:

* **Alta Reputación Operativa:** Los líderes del mercado como *Root Down* (4.4 estrellas, 4,164 reseñas) [source: 2], *Coriander* (4.5 estrellas, 689 reseñas) [source: 2] y *Next Level Veggie Grill* (4.5 estrellas, 171 reseñas) [source: 2] mantienen promedios superiores a 4.0 estrellas. Esto refleja consumidores locales exigentes con la calidad.
* **Fórmula Ganadora:** Los conceptos mejor posicionados combinan la oferta basada en plantas con cocinas de nicho o estilo de vida, tales como *New American*, *Comfort Food*, e *Indian Fusion* [source: 2].
* **Brecha de Volumen de Reseñas:** Existe una brecha significativa entre los competidores consolidados ($>2,500$ reseñas) [source: 2] y las nuevas aperturas ($<200$ reseñas) [source: 2]. Esto abre una ventana de oportunidad para una marca nueva que implemente estrategias agresivas de fidelización y recolección de feedback digital.

---

#### 3. Recomendaciones Estratégicas para la Apertura

* **Posicionamiento de Menú Flexitariano/Plant-Based:** Diseñar una propuesta enfocada en *Comfort Food* e influencias *New American* libre de proteína animal [source: 2], dirigida tanto a vegetarianos estrictos como al 67% de consumidores no vegetarianos de nivel socioeconómico alto [source: 3].
* **Estrategia Mix de Producto (Alimentos & Bebidas):** Incorporar barra de bebidas, cócteles de autor y bebidas funcionales para capturar el 61.61% de la demanda consumidora de alcohol [source: 3] y elevar el ticket promedio por encima de los $35 - $50 USD.
* **Estrategia de Ubicación:** Priorizar sectores céntricos o corredores gastronómicos de alto flujo (similares a *Ogden St*, *E 17th Ave* o *W 33rd Ave* [source: 2]), aprovechando las coordenadas geoespaciales de alta densidad obtenidas en el mapeo de Yelp [source: 2].

---

### Resumen de Métricas de Data Hygiene

| Métrica | Estado Inicial | Método de Imputación / Normalización | Resultado Final |
| :--- | :--- | :--- | :--- |
| **Registros Duplicados** | 0 duplicados detectados [source: 3] | Validación por combinatoria `id_persona` + `ciudad_residencia` [source: 3] | 30,000 registros únicos [source: 3] |
| **Outliers de Edad (300 años)** | 547 registros inconsistentes [source: 3] | Reemplazo directo por valor tipográfico correcto (30 años) [source: 3] | Rango de edad corregido [source: 3] |
| **Valores Nulos en Edad** | 101 registros ($0.33\%$) [source: 3] | Imputación por Mediana [source: 3] | 0 nulos [source: 3] |
| **Gasto Promedio Comida** | 145 registros ($0.48\%$) [source: 3] | Imputación por Mediana de `ciudad_residencia` + Mediana Global [source: 3] | 0 nulos [source: 3] |
| **Preferencias Alimenticias** | 1,403 registros ($4.67\%$) [source: 3] | Normalización de texto e Imputación por Moda (`'Carnes'`) [source: 3] | 0 nulos [source: 3] |
| **Filtro Ciudad Denver** | Base Nacional USA | Subconjunto `ciudad_residencia == 'Denver'` [source: 3] | **2,523 registros locales** [source: 3] |
