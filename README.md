# 🏃‍♂️ Proyecto de Aprendizaje Automático: Maratón de Tokyo (2015-2017)

¡Hola!

Aquí tenéis nuestra web oficial del proyecto (actualizada en tiempo real):
🌐 **[Web del Proyecto en GitHub Pages](https://bedatasportlab.github.io/aprendizaje-automatico-maraton/)**

---

## 🛠️ Paso 1: Configurar tu Entorno de Trabajo (Solo la primera vez)

Para asegurarnos de que a todos nos corre exactamente el mismo código con las mismas librerías sin que dé errores, vamos a usar **Conda**. Sigue estos tres pasos sencillos en tu terminal:

1. **Clona el repositorio** en tu ordenador (si no lo has hecho ya):
   ```bash
   git clone https://github.com/bedatasportlab/aprendizaje-automatico-maraton.git
   ```

2. **Crea el entorno de Conda** a partir de nuestro archivo de configuración. Esto instalará automáticamente Python 3.10, Pandas, Scikit-Learn, XGBoost, SHAP, Seaborn y todo lo necesario:
   ```bash
   conda env create -f environment.yml
   ```

---

## 📝 Paso 2: ¿Dónde y cómo escribimos el código?

Trabajamos de forma **modular**. No hacemos un archivo gigante; dividimos el trabajo en capítulos dentro de la carpeta `notebooks/`:

* 📂 **`notebooks/01_eda.qmd`**: Carga de datos crudos (`data/raw/`), análisis exploratorio, tratamiento de nulos, gráficos y exportación del dataset limpio.
* 📂 **`notebooks/02_unsupervised.qmd`**: Modelos de Clustering (Aprendizaje No Supervisado).
* 📂 **`notebooks/03_supervised.qmd`**: Árboles de decisión, Redes Neuronales, Regresiones, XGBoost y análisis SHAP.

### 🔄 La Regla de Oro: Flujo de Datos Modular
Para poder trabajar en el Capítulo 2 o 3 sin tener que volver a ejecutar todo el EDA (que puede tardar mucho en cargar), haremos lo siguiente:
1. Al final del **Capítulo 1 (EDA)**, guardamos los datos limpios en formato rápido `.parquet` (no uses CSV para pasos intermedios, el parquet mantiene los tipos de datos perfectos):
   ```python
   df_limpio.to_parquet('../data/processed/maraton_limpio.parquet')
   ```
2. Al inicio del **Capítulo 2 (Clustering)**, simplemente cargamos ese archivo procesado:
   ```python
   import pandas as pd
   df = pd.read_parquet('../data/processed/maraton_limpio.parquet')
   ```


---

## 🚀 Paso 3: ¿Cómo probar tu código en local?

* **Vista previa rápida de un solo capítulo:** Si quieres ver cómo está quedando maquetado un capítulo en concreto como página HTML, ejecuta en tu consola activa:
   ```bash
   quarto render notebooks/01_eda.qmd
   ```

---

## 🌐 Paso 4: Cómo actualizar la Web y el PDF de la entrega (¡MUY IMPORTANTE!)

⚠️ **¡CUIDADO!** Si solo editas el código del archivo `.qmd` y haces un `git push`, **la página web NO se actualizará**.

Para que la web de GitHub Pages y el PDF final que se descarga el profesor se actualicen con tus cambios, tienes que seguir **obligatoriamente** estos tres pasos en tu terminal (con tu entorno de Conda activado):

1. **Compilar el libro entero (Renderizar):**
   ```bash
   quarto render
   ```
   *(Este comando lee todos nuestros capítulos, genera la web interactiva en la carpeta `/docs` y une todo en un único PDF para entregar al profesor).*

2. **Añadir y guardar los cambios en Git:**
   ```bash
   git add .
   git commit -m "Añadidos cambios y actualización de la web/PDF"
   ```

3. **Subir al repositorio:**
   ```bash
   git push origin main
   ```

¡Y listo! En **1 o 2 minutos**, GitHub Pages detectará la actualización de la carpeta `docs/` y publicará los cambios automáticamente en nuestra web.

---

## 📁 Estructura del repositorio para no perderse
```text
aprendizaje-automatico-Maraton-Tokyo/
├── _quarto.yml          # Configuración global del libro (menú, PDF, etc.)
├── index.qmd            # Introducción y objetivos (Portada de la web)
├── environment.yml      # Receta de nuestro entorno de Conda
├── style.css            # El diseño personalizado de la web (¡con logos URJC/MUSA!)
├── MUSA.png             # Logo del Máster
├── URJC_logo.svg.png    # Logo de la Universidad
├── docs/                # Carpeta mágica que GitHub Pages lee para la web y PDF
├── data/
│   ├── raw/             # Pon aquí tus CSV originales (¡No los subas a Git si pesan mucho!)
│   └── processed/       # Parquets de checkpoints intermedios
└── notebooks/
    ├── 01_eda.qmd
    ├── 02_unsupervised.qmd
    └── 03_supervised.qmd
```