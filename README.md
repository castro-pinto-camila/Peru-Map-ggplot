## Cómo crear mapas en R (coroplético y bivariado)

Este repositorio presenta una guía reproducible para construir mapas geográficos 
en R usando datos abiertos y `ggplot2`.

Se incluyen:
- Un **mapa coroplético**
- Un **mapa bivariado (2 variables simultáneas)**

El flujo es adaptable a cualquier país y conjunto de datos.

---

### Resultado ! 
👉 **Ver resultado completo aquí:**  
[🔗 Abrir visualización](mapa_anemia_peru.html)

Ejemplo aplicado:
- **Anemia infantil (6–35 meses)**
- **Desnutrición crónica (<5 años)**
- Perú, 2024 (INEI)

---

### Metodología

Se sigue un enfoque progresivo:

1. Importación de datos espaciales (shapefile externo o librería de R)
2. Limpieza y unión de datos
3. Construcción de un mapa coroplético
4. Extensión a un mapa bivariado (análisis multivariable visual)

---

### Requisitos:

R 4.0 o superior con los siguientes paquetes:
```
# Instalar desde la Consola de R (solo la primera vez)
install.packages(c("sf", "ggplot2", "dplyr", "geodata", "cowplot"))
```

---

### ¿Cómo replicarlo?

1. Clona el repositorio
```
git clone https://github.com/tu-usuario/tu-repo.git
```
3. Abre mapa.qmd en RStudio
4. Renderiza

---

### ¿Cómo adaptarlo a otro país o variables?

1. Cambiar país
```
peru_sf <- gadm(country = "PER", level = 1, path = tempdir()) |>
  st_as_sf()```
```
Ejemplos:

MEX = México, COL = Colombia, ARG = Argentina, BRA = Brasil, etc...

2. Usar tus propios datos
```
datos <- data.frame(
  region    = c("Región 1", "Región 2"),
  variable1 = c(...),
  variable2 = c(...)
)
```  
3. Ajustar títulos
```
labs(
  title    = "Título de tu mapa",
  subtitle = "Descripción · Fuente y año"
)
```
---

### Tipos de mapas
#### Mapa coroplético

Pasos:

1. Cargar shapefile
2. Unir datos
3. Visualizar con ggplot2

> Nota:
> Los mapas coropléticos pueden ser engañosos cuando las regiones tienen tamaños muy diferentes o poblaciones desiguales.
   
#### Mapa bivariado

Permite visualizar dos variables simultáneamente usando una paleta 2D, cada región del mapa recibe un color según en qué celda de esta grilla cae.   

> Nota:
> Los mapas bivariados permiten explorar posibles asociaciones espaciales entre variables,
lo cual es útil para generar hipótesis en estudios epidemiológicos o económicos.
Resultado: 
---

### Hallazgos de ejemplo aplicado (Perú 2024)

Se encontró que, en la sierra y selva concentran mayores niveles de anemia y desnutrición. Por otra parte, la costa sur presenta niveles más bajos y existen regiones con patrones mixtos, lo que sugiere que ambas variables no siguen una relación perfectamente paralela.

### Limitaciones

- Clasificación relativa (no clínica)
- Nivel de agregación departamental
- Análisis descriptivo (no causal)

### Referencias

INEI (2024). Encuesta Demográfica y de Salud Familiar — ENDES 2024. Lima: Instituto Nacional de Estadística e Informática.
