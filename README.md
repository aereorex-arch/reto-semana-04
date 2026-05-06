# reto-semana-04
hola, se me olvido hacer el push
Sistema Automatizado de Inventario
Reto Semana 4: Programación para Ciencia de Datos

Pipeline de procesamiento en Python diseñado para la ingesta, validación y análisis de datos de inventario. El sistema lee registros comerciales, identifica anomalías en el formato, detecta niveles críticos de existencias y genera un reporte de reabastecimiento priorizado.

La arquitectura del proyecto aplica separación de responsabilidades mediante los directorios models/ y utils/, garantizando escalabilidad y facilitando el mantenimiento del código bajo estándares de ingeniería de software.
Arquitectura y Flujo de Datos

    Ingesta: Lectura automatizada desde data/inventario.csv.

    Validación (utils/): Limpieza de datos y filtrado de registros corruptos en tiempo de ejecución.

    Lógica de Negocio (models/): Evaluación de la condición de reabastecimiento (stock<stock_minimo) y cálculo del valor del inventario faltante.

    Extracción: Generación del reporte consolidado en outputs/reporte_inventario.csv.

Instrucciones de Despliegue
Requisitos Previos

    Intérprete de Python 3.x instalado en el sistema.

    Ejecución estricta desde el directorio raíz del proyecto.

    El archivo de origen debe existir en la ruta: data/inventario.csv.

Ejecución del Pipeline

El proceso es completamente automatizado y no requiere interacción del usuario mediante la terminal.

    Linux / Mac:
    Bash

    python3 main.py

    Windows (PowerShell / CMD):

PowerShell

    python main.py
    ```

> **Nota:** Al finalizar, el script imprimirá un resumen de la operación en la salida estándar (consola) y persistirá el dataset resultante en el directorio `outputs/`.

---

## Especificación de Datos

### Estructura de Entrada Esperada (`data/inventario.csv`)
El archivo de origen debe ser un CSV separado por comas con los siguientes encabezados:
```csv
sku,nombre,categoria,precio,stock,stock_minimo
SKU001,Laptop HP,Electronica,15000.00,5,10
SKU002,Mouse Logitech,Accesorios,350.00,3,15

Estructura del Reporte Generado (outputs/reporte_inventario.csv)

El sistema exporta únicamente los registros que requieren atención inmediata, ordenados de forma descendente según la métrica unidades_faltantes.
Fragmento de código

sku,nombre,categoria,stock_actual,stock_minimo,unidades_faltantes,valor_inventario
SKU002,Mouse Logitech,Accesorios,3,15,12,1050.00
SKU005,Audifonos Sony,Accesorios,2,10,8,2400.00
SKU001,Laptop HP,Electronica,5,10,5,75000.00
SKU007,SSD 1TB,Almacenamiento,0,5,5,0.00

Tolerancia a Fallos y Validación

El sistema implementa un mecanismo de exclusión silenciosa para mantener la integridad del pipeline. Se detectan e ignoran automáticamente las filas que presenten las siguientes anomalías:

    Valores no numéricos en los campos precio o stock.

    Asimetría estructural (columnas faltantes o excedentes respecto al encabezado).

Cualquier discrepancia detectada durante la validación se registra en la consola como una advertencia (log), permitiendo la depuración sin interrumpir la ejecución del resto del lote de datos.

Desarrollador: Manuel Hernandez Rodriguez
