---
source-git-commit: ef1c207922c1079117d8bd255dbfa32a1527b014
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---
# Plantilla de fila de catálogo de casos de uso

## Formato de fila

Cada fila de la tabla del catálogo de casos de uso sigue este formato exacto:

```
| <img src="assets/use-case-icons/{industry}/icon-{kebab-name}.png" alt="{Alt Text}" width="40"> | [{Use Case Title}]({industry}/{industry}-overview.md#{heading-anchor}) | {One-sentence description} | [!BADGE {Maturity}]{type={Type}} | [{Pattern Name}](/help/blueprints/use-case-patterns/{category}/{pattern-file}.md) |
```

### Fila sin icono (se utiliza cuando el icono aún no está disponible)

```
| | [{Use Case Title}]({industry}/{industry}-overview.md#{heading-anchor}) | {One-sentence description} | [!BADGE {Maturity}]{type={Type}} | [{Pattern Name}](/help/blueprints/use-case-patterns/{category}/{pattern-file}.md) |
```

## Referencia de campo

| Campo | Formato | Ejemplo |
| --- | --- | --- |
| industria | nombre del directorio kebab-case | comercio minorista, servicios financieros, viajes y hospitalidad |
| kebab-name | nombre del caso de uso de kebab-case para el icono | carro de compras abandonado, nutrición con plomo |
| Texto alternativo | Carcasa de título, corta | Carro abandonado, nutrición de plomo |
| anclaje de cabeza | kebab-case del encabezado ## en descripción general | abandonado-cart-email-recovery |
| Vencimiento + Tipo | Sintaxis de distintivo | `[!BADGE Foundational]{type=Neutral}`, `[!BADGE Emerging]{type=Informative}`, `[!BADGE Advanced]{type=Caution}` |

## Marcadores de pestaña del sector en el catálogo

El archivo de catálogo utiliza esta estructura de pestañas:

- `>[!TAB Retail]`
- `>[!TAB Automotive]`
- `>[!TAB Financial Services]`
- `>[!TAB Healthcare]`
- `>[!TAB Insurance]`
- `>[!TAB Media & Entertainment]`
- `>[!TAB Telecommunications]`
- `>[!TAB Travel & Hospitality]`
- `>[!TAB B2B]`

## Ordenación dentro de pestañas

Las filas se ordenan por nivel de vencimiento:

1. **Filas básicas** primero (type=Neutral)
2. **Emergente** filas en segundo lugar (type=Informativo)
3. **Avanzadas** filas en último lugar (type=Caution)

Dentro del mismo nivel de vencimiento, agregue nuevas filas al final de ese grupo.
