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
[🔗 Abrir visualización](mapa__anemia_peru.html)

### Metodología

Se sigue un enfoque progresivo:

1. Importación de datos espaciales (shapefile externo o librería de R)
2. Limpieza y unión de datos
3. Construcción de un mapa coroplético
4. Extensión a un mapa bivariado (análisis multivariable visual)

### Requisitos:

R 4.0 o superior con los siguientes paquetes:
```
# Instalar desde la Consola de R (solo la primera vez)
install.packages(c("sf", "ggplot2", "dplyr", "geodata", "cowplot"))
```

### ¿Cómo adaptarlo a otro país o variables?

1. El país del shapefile:
```
# Cambia "PER" por el código ISO de tu país
# MEX = México | COL = Colombia | ARG = Argentina | BRA = Brasil
peru_sf <- gadm(country = "PER", level = 1, path = tempdir()) |>
  st_as_sf()
```
2. Tus propios datos:
```
datos <- data.frame(
  region    = c("Región 1", "Región 2", ...),  # nombres exactos del shapefile
  variable1 = c(...),                           # primera variable
  variable2 = c(...)                            # segunda variable
)
```   
3. Los títulos:
```
labs(
  title    = "Título de tu mapa",
  subtitle = "Descripción · Fuente y año"
)
```
Lo demás funciona igual! :)

### Parte 1: Mapa coroplético

Se representa una variable continua en el espacio geográfico.

### Pasos:

1. Cargar shapefile
2. Unir datos
3. Visualizar con ggplot2

> Nota:
> Los mapas coropléticos pueden ser engañosos cuando las regiones tienen tamaños muy diferentes o poblaciones desiguales.
   
### Parte 2: ¿Qué es un mapa bivariado? 

Un mapa tradicional (coroplético) solo muestra una variable por región. Un mapa bivariado muestra dos al mismo tiempo usando una paleta de color 2D:

                         DESNUTRICIÓN
                  Baja      Media      Alta
               ┌─────────┬─────────┬─────────┐
    A    Baja  │ #e8e8e8 │ #dfb0d6 │ #be64ac │
    N          ├─────────┼─────────┼─────────┤
    E    Media │ #ace4e4 │ #a5b3cc │ #8c62aa │   
    M          ├─────────┼─────────┼─────────┤
    I    Alta  │ #5ac8c8 │ #5698b9 │ #3b4994 │ ← más crítico
    A          └─────────┴─────────┴─────────┘

Cada región del mapa recibe un color según en qué celda de esta grilla cae.   

Los mapas bivariados permiten explorar posibles asociaciones espaciales entre variables,
lo cual es útil para generar hipótesis en estudios epidemiológicos o económicos.

Resultado: 


### Hallazgos 

Se encontró que, en los departamentos con mayor concentración de ambos problemas (color azul oscuro #3b4994) son los que requieren intervención prioritaria en políticas de salud pública.

Los resultados muestran un claro patrón, los departamentos de la sierra y selva concentran los niveles más altos de anemia y desnutrición, mientras que los de la costa sur (Tacna, Moquegua, Ica) presentan los niveles más bajos.

### Referencias

INEI (2024). Encuesta Demográfica y de Salud Familiar — ENDES 2024. Lima: Instituto Nacional de Estadística e Informática.
