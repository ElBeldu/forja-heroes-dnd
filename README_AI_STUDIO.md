# Integración en Google AI Studio (Creador de Personajes D&D 5e / 2024)

## Estructura de archivos (< 2 MB cada uno)
Colocá estos JSON en la carpeta `public/data/` de tu app en Google AI Studio:
- `00_manifest.json`: Índice general y conteo de elementos.
- `01_motor_y_config.json`: Reglas del motor (`aurora_config`), compatibilidad 2014↔2024 (`compatibility`) y 35 parches activos (`appends`).
- `02_razas_y_trasfondos.json`: 418 elementos (Razas, Subrazas, Trasfondos, Idiomas).
- `03_clases_y_subclases.json`: 1.371 elementos (13 Clases, 106 Subclases/Arquetipos, Rasgos).
- `04_dotes_y_mejoras.json`: 489 elementos (Dotes, ASI, Competencias).
- `05_conjuros.json`: 507 conjuros.
- `06_equipo_y_objetos_magicos.json`: 1.176 elementos (Armas, Armaduras, Equipo, Objetos Mágicos).
- `07_reglas_companeros_e_interno.json`: 896 elementos (Grants internos, Compañeros, Condiciones).

## Saneamiento aplicado
- Se resolvieron **235 grants rotos** (226 conjuros del PHB 2014 + 9 competencias de armas de fuego) hacia sus IDs equivalentes de D&D 2024 (conservando el ID original en `legacy_id`).
- Se filtraron los `appends` a los **35 parches** con `target_id` válido en este compendio.

## Prompt sugerido para Google AI Studio
> Estoy construyendo un creador de personajes de D&D 5e/2024 en español usando los archivos JSON modulares ubicados en `/public/data/`.
> 1. Al iniciar la app, cargá `01_motor_y_config.json` y usá `aurora_config.root_character_element` (`ID_INTERNAL_GRANTS_CHARACTER_BASE`) como raíz.
> 2. Cargá los módulos `02_*` a `07_*` en un único diccionario `elementsById` en memoria (o bajo demanda por pestaña).
> 3. Resolvé las selecciones del personaje evaluando `rules.grants`, `rules.selects` (filtrando por `supports` y `requirements`) y `compatibility.superseded_by_2024`.
> 4. Calculá atributos, CA y bonos aplicando `aurora_config.stat_engine` (mismo `type` toma el máximo; sin tipo se suma).
