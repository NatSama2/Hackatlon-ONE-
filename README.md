# ✈️ FlightOnTime — Data Science Module

## 📌 Descripción General
**FlightOnTime** es un proyecto de *Machine Learning* cuyo objetivo es predecir si un vuelo será **puntual (0)** o **retrasado (1)** utilizando datos históricos de vuelos. Este módulo corresponde a la parte de **Data Science**, donde se realizó el análisis exploratorio, limpieza de datos, ingeniería de características, entrenamiento de modelos y evaluación de métricas.

Este sistema está diseñado para integrarse con una API desarrollada en backend, permitiendo realizar predicciones en tiempo real.

---

## 🎯 Objetivo
Desarrollar un modelo de clasificación binaria capaz de predecir el estado de un vuelo:
- **0 → Puntual**
- **1 → Retrasado** (cuando el retraso es igual o mayor a 15 minutos)

---

## 🧠 Enfoque del Problema
Se aborda como un problema de *supervised learning*, específicamente de **clasificación binaria**, utilizando datos estructurados que incluyen:

- Aerolínea
- Origen
- Destino
- Fecha y hora de salida
- Distancia del vuelo
- Minutos de retraso

---

## 📊 Dataset
El dataset utilizado contiene información histórica de vuelos, incluyendo variables categóricas y numéricas.

### Variables principales:
- `airline`
- `origin`
- `destination`
- `departure_time`
- `distance`
- `delay_minutes`

### Etiquetado
Se creó una nueva variable objetivo llamada `delayed`:
- `0` → Puntual (delay < 15 min)
- `1` → Retrasado (delay ≥ 15 min)

---

## 🔍 Análisis Exploratorio (EDA)
Se realizó un análisis exploratorio para:
- Comprender la distribución de los datos
- Detectar valores nulos
- Identificar outliers
- Evaluar el balance de clases
- Analizar correlaciones

Se observó un **desbalance de clases**, donde la mayoría de los vuelos eran puntuales.

---

## 🧹 Limpieza de Datos
Las principales acciones realizadas fueron:
- Eliminación de valores nulos
- Conversión de fechas a formato `datetime`
- Eliminación de columnas irrelevantes
- Corrección de tipos de datos

---

## ⚙️ Feature Engineering
Se crearon nuevas variables a partir de la fecha:
- Hora de salida
- Día de la semana
- Mes
- Tramo horario (mañana, tarde, noche)

También se aplicó:
- One-Hot Encoding para variables categóricas
- Escalado con StandardScaler (solo para modelos que lo requieren)

---

## 🤖 Modelos Entrenados

### 1️⃣ Regresión Logística (Baseline)
Se utilizó como modelo base para establecer una línea de rendimiento.

### 2️⃣ Regresión Logística + SMOTE
Debido al desbalance de clases, se aplicó SMOTE para mejorar la detección de vuelos retrasados.

### 3️⃣ Random Forest
Se entrenó un modelo de Random Forest para capturar relaciones no lineales y mejorar el rendimiento general.

---

## 📈 Métricas de Evaluación
Los modelos fueron evaluados utilizando:
- Accuracy
- Precision
- Recall
- F1-score
- Matriz de confusión

Se dio especial importancia al **Recall de la clase retrasada (1)**, ya que es más crítico detectar vuelos con retraso.

---

## 🏆 Resultados
El modelo de **Random Forest** presentó el mejor equilibrio entre:
- Accuracy
- Recall
- F1-score

Por lo tanto, fue seleccionado como el modelo final.

---

## 📦 Exportación del Modelo
El modelo final fue exportado utilizando `joblib`, junto con todo el pipeline de preprocesamiento, para su uso en producción.

---

## 🔮 Función de Predicción
Se implementó una función `predict()` que recibe datos en formato JSON y retorna:

```json
{
  "prevision": "Retrasado",
  "probabilidad": 0.78
}
```

---

## 🔗 Integración con Backend
Este módulo de Data Science se conecta con una API REST desarrollada en Spring Boot, permitiendo realizar predicciones en tiempo real.

Actualmente:
- La conexión con la API **está implementada y funciona**.
- Sin embargo, la integración aún presenta **problemas de estabilidad** (caídas intermitentes), propios de una fase MVP.
- Para asegurar una conexión correcta y estable, el backend deberá cargar directamente el modelo serializado:

📦 **`flight_model_v1.0.0.joblib`**

Este archivo contiene el pipeline completo de preprocesamiento + modelo entrenado y es el que debe ser utilizado por el backend para garantizar consistencia entre entrenamiento e inferencia.

La integración definitiva se realizará consumiendo este archivo como fuente única de predicción.

---

### Contrato de Entrada
El contrato de entrada definido entre el módulo de Data Science y el Backend es el siguiente:

```json
{
  "aerolinea": "AZ",
  "origen": "GIG",
  "destino": "GRU",
  "fecha_partida": "2025-11-10T14:30:00",
  "distancia_km": 350
}
```
Este módulo está diseñado para integrarse con una API REST desarrollada en Spring Boot. El contrato de entrada es:

```json
{
  "aerolinea": "AZ",
  "origen": "GIG",
  "destino": "GRU",
  "fecha_partida": "2025-11-10T14:30:00",
  "distancia_km": 350
}
```

---

## 🛠️ Tecnologías Utilizadas
- Python
- Pandas
- NumPy
- Scikit-learn
- Imbalanced-learn (SMOTE)
- Matplotlib / Seaborn
- Joblib
- Google Colab

---

## 👩‍💻 Autores
Equipo Data Science — Proyecto FlightOnTime
- Giselle Cifuentes
- Karen Sofia Rodriguez
- Karen Guerrero González

---

## 📌 Conclusiones
Este proyecto demuestra cómo aplicar técnicas de Data Science para resolver un problema real del mundo de la aviación. A través del uso de ingeniería de características, manejo de desbalance de clases y evaluación de múltiples modelos, se logró construir un sistema capaz de predecir retrasos con un rendimiento sólido.

---

## 🚀 Trabajo Futuro
- Incorporar datos meteorológicos
- Agregar congestión aeroportuaria
- Implementar modelos más avanzados (XGBoost, LightGBM)
- Monitoreo de drift
- Reentrenamiento automático

---

