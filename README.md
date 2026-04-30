# Cómo crear mapas coropléticos y bivariados en R (aplicable a cualquier país)

En este repositorio podrán encontrar una guía para construir mapas geográficos en R usando datos abiertos, desde un mapa coroplético básico hasta un mapa bivariado (una técnica de visualización que representa dos variables simultáneamente mediante una paleta de color 2D).

El flujo es reproducible y adaptable a cualquier país utilizando datos geoespaciales (shapefiles) y variables de interés. Como ejemplo, se visualiza la relación entre anemia infantil y desnutrición crónica en los 25 departamentos del Perú usando datos oficiales del INEI (ENDES 2024). 

## Resultado ! 


## Metodología

Se sigue un enfoque progresivo:

1. Importación de datos espaciales (shapefile externo o librería de R)
2. Limpieza y unión de datos
3. Construcción de un mapa coroplético
4. Extensión a un mapa bivariado (análisis multivariable visual)

## ¿Qué es un mapa bivariado? 

Un mapa tradicional (coroplético) solo muestra una variable por región. Un mapa bivariado muestra dos al mismo tiempo usando una paleta de color 2D:

                         DESNUTRICIÓN
                  Baja      Media      Alta
               ┌─────────┬─────────┬─────────┐
         Baja  │ #e8e8e8 │ #dfb0d6 │ #be64ac │
               ├─────────┼─────────┼─────────┤
  ANEMIA Media │ #ace4e4 │ #a5b3cc │ #8c62aa │
               ├─────────┼─────────┼─────────┤
         Alta  │ #5ac8c8 │ #5698b9 │ #3b4994 │ ← más crítico
               └─────────┴─────────┴─────────┘

Cada región del mapa recibe un color según en qué celda de esta grilla cae.          
