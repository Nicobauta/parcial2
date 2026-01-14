# Sistema de Recolección y Procesamiento de Datos Inmobiliarios con AWS y Python

Este proyecto implementa un **sistema automatizado de recolección, almacenamiento y procesamiento de datos inmobiliarios**, utilizando **web scraping**, **AWS S3** y **Python**.

El sistema descarga páginas web de avisos de venta de apartamentos en Bogotá, almacena los archivos HTML en la nube, procesa la información relevante y genera archivos **CSV estructurados**, todo validado mediante **pruebas automatizadas**.  
El proyecto fue desarrollado con fines académicos como parte de un **parcial de Big Data / Computación en la Nube**.

---

## Características principales

- Descarga automática de páginas web inmobiliarias
- Web scraping usando **Requests** y **BeautifulSoup**
- Almacenamiento de datos crudos en **AWS S3**
- Procesamiento de HTML para extraer:
  - Barrio
  - Precio
  - Número de habitaciones
  - Número de baños
  - Metros cuadrados
- Generación de archivos **CSV**
- Ejecución en la nube mediante **AWS Lambda**
- Despliegue serverless con **Zappa**
- Pruebas unitarias automatizadas
- Integración con **GitHub Actions**

---

## Arquitectura del sistema

Portal inmobiliario  
↓  
Requests (Scraping Web)  
↓  
AWS S3 (HTML crudo)  
↓  
Parser de datos (Python)  
↓  
Archivo CSV en S3  
↓  
Pruebas automatizadas  

---

## Tecnologías utilizadas

- **Python 3**
- **AWS S3**
- **AWS Lambda**
- **Zappa**
- **Requests**
- **BeautifulSoup**
- **Boto3**
- **Pytest**
- **GitHub Actions**

---

## Estructura del proyecto
```

├── .github/
│ └── workflows/
│ └── blank.yml
│
├── pycache/
├── env/
│
├── parcial.py
├── punto2.py
├── test_script.py
│
├── requirements.txt
├── zappa_settings.json
├── .gitignore
└── README.md

```

---

## Descripción de los componentes

### `parcial.py`
Archivo principal del proyecto.

Funciones:
- Descarga páginas web de avisos inmobiliarios
- Organiza los archivos por fecha
- Sube los archivos HTML a un bucket de **AWS S3**
- Puede ejecutarse como **AWS Lambda**

---

### `punto2.py`
Módulo encargado del **procesamiento de los archivos HTML**.

Funciones principales:
- Parseo de HTML con **BeautifulSoup**
- Extracción de datos relevantes del inmueble
- Generación de un archivo CSV con el siguiente formato: FechaDescarga,Barrio,Valor,NumHabitaciones,NumBanos,mts2


- Subida del CSV a **AWS S3**

---

### `test_script.py`
Archivo de **pruebas unitarias**.

Funciones:
- Validación de la correcta extracción de datos
- Simulación de servicios AWS
- Verificación del contenido y formato del CSV generado

---

### `zappa_settings.json`
Archivo de configuración para el **despliegue serverless** del proyecto en **AWS Lambda** utilizando **Zappa**.

---

### `.github/workflows/blank.yml`
Workflow de **GitHub Actions** para integración continua (CI).

---

## Ejecución del proyecto

```bash
# 1. Crear entorno virtual
python -m venv env

# 2. Activar entorno virtual
# Linux / macOS
source env/bin/activate

# Windows
env\Scripts\activate

# 3. Instalar dependencias
pip install -r requirements.txt

# 4. Ejecutar pruebas
pytest

# 5. Ejecutar scraping de forma local
python parcial.py
