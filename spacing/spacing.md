# Sistema de Espaciado — Tema editorial AtomSN

> **Versión:** 2.0 · **Plataforma:** Flutter (mobile-first + web) · **Unidad base:** 4px

## Dirección visual

Sistema de espaciado basado en múltiplos de 4px. Garantiza ritmo visual consistente entre elementos, secciones y pantallas de la app.

El espaciado debe sentirse cómodo, predecible y estructural. La densidad por defecto es media: ni demasiado comprimida para pantallas de datos, ni demasiado abierta para una app de consulta rápida de resultados.

En AtomSN el espaciado adopta el lenguaje del periódico: la maquetación se ordena con reglas (filos hairline 1px, regla de sección 2px), columnas con un gutter fijo y kickers/overlines pegados a su titular. Las esquinas tienden a lo recto: el periódico prefiere el filo, y `radius.none` es el borde editorial por defecto de reglas, sellos y tablas. `radius.md` se mantiene como el estándar de cards.

---

## Principios

- Todo el espaciado proviene de la escala base de 4px; no se usan valores arbitrarios.
- Los componentes consumen tokens semánticos de espaciado, no valores crudos directamente.
- La densidad visual puede ajustarse cambiando los tokens semánticos sin tocar la escala base.
- El padding horizontal de pantalla es fijo y uniforme en toda la app.
- El radio de borde pertenece a este sistema: consistencia visual de cards, botones e inputs.
- Editorial: las esquinas tienden a lo recto. Reglas, sellos ("FINAL") y tablas de clasificación usan `radius.none`. Los radios redondeados se reservan para superficies de interacción (cards, sheets, botones).
- Las reglas (reglas hairline y de sección) son elementos de maquetación: su grosor sale de `border.*`, no de la escala de espaciado.
- Los layouts multi-columna (tablas, grids, web) usan un gutter de columna único y fijo.

---

## Restricciones base

- Valor mínimo de espaciado: `space.1` (4px)
- Valor máximo del sistema: `space.20` (80px)
- No usar valores fuera de la escala (ej: 6px, 10px, 15px)
- El radio de borde máximo para elementos rectangulares: `radius.xl` (24px)
- `radius.full` se reserva para elementos circulares (avatares, dots de estado, badges, pills)
- `radius.none` es el borde por defecto del utillaje editorial (reglas, sellos, tablas)
- Grosores de regla: solo `border.hairline` (1px) y `border.section` (2px); no inventar grosores intermedios

---

## Convención de nombres

```text
# Escala base de espaciado:
space.{n}       → n × 4px

# Radio de borde:
radius.{nivel}

# Grosor de regla editorial:
border.{nivel}

# Tokens semánticos de componente:
spacing.{componente}.{propiedad}.{tamaño}
```

Ejemplos: `space.4` (16px), `space.6` (24px), `radius.md`, `radius.none`, `border.hairline`, `spacing.card.padding.md`, `spacing.column.gap`, `spacing.overline.gap`

---

## Escala base

```yaml
raw_spacing:
  - token: space.1
    value: 4px
    role: micro espacio
    usage: separación entre icono y texto; entre elementos muy próximos; gap overline → titular

  - token: space.2
    value: 8px
    role: espacio compacto
    usage: padding de chips, badges y botones pequeños

  - token: space.3
    value: 12px
    role: espacio medio-compacto
    usage: padding vertical de inputs y botones

  - token: space.4
    value: 16px
    role: unidad base
    usage: padding horizontal estándar de pantalla en mobile; padding general de componentes; gutter de columna

  - token: space.5
    value: 20px
    role: espacio generoso
    usage: separación entre elementos de lista

  - token: space.6
    value: 24px
    role: separación de sección
    usage: separación entre secciones dentro de una pantalla

  - token: space.8
    value: 32px
    role: separación mayor
    usage: separación entre bloques de contenido

  - token: space.10
    value: 40px
    role: espacio de respiro
    usage: layouts de dashboard o pantallas de detalle

  - token: space.12
    value: 48px
    role: separación grande
    usage: padding vertical de secciones hero o cabeceras de pantalla

  - token: space.16
    value: 64px
    role: espaciado muy grande
    usage: separación entre secciones en empty states o onboarding

  - token: space.20
    value: 80px
    role: espacio máximo
    usage: padding superior/inferior en pantallas de presentación
```

---

## Radio de borde

Editorial: radios contenidos. El periódico prefiere esquinas rectas o levemente redondeadas. `radius.md` sigue siendo el estándar de cards; `radius.none` es el borde recto del utillaje editorial (reglas, sellos, tablas).

```yaml
border_radius:
  - token: radius.none
    value: 0px
    role: sin redondeo — borde recto editorial
    usage: reglas/filos, sellos de tinta ("FINAL"), tablas de clasificación, celdas; el filo recto del periódico

  - token: radius.xs
    value: 4px
    role: redondeo mínimo
    usage: chips compactos, badges, etiquetas pequeñas

  - token: radius.sm
    value: 8px
    role: redondeo bajo
    usage: inputs, botones secundarios, tooltips

  - token: radius.md
    value: 12px
    role: redondeo estándar
    usage: cards, sheets y modales — el más frecuente del sistema

  - token: radius.lg
    value: 16px
    role: redondeo amplio
    usage: cards grandes, bottom sheets, paneles destacados

  - token: radius.xl
    value: 24px
    role: redondeo pronunciado
    usage: cards hero, elementos con protagonismo visual fuerte

  - token: radius.2xl
    value: 32px
    role: redondeo muy pronunciado
    usage: elementos de onboarding o marketing interno

  - token: radius.full
    value: 9999px
    role: redondeo completo
    usage: avatares, dots de estado, badges circulares, botones pill
```

### Guía editorial de radios

- Reglas, filos y separadores: `radius.none`. Una regla redondeada no existe en un periódico.
- Sellos de tinta (`accent.ink`, p. ej. "FINAL"): `radius.none`. El sello es un bloque recto.
- Tablas de clasificación y sus celdas/filas: `radius.none`. Los líderes punteados y las cifras tabulares viven en una rejilla recta.
- Cards, sheets, modales: `radius.md`.
- Inputs y botones secundarios: `radius.sm`. Botones primarios pueden usar `radius.sm`/`radius.md` según peso visual.
- Elementos circulares (avatares, dots, pills): `radius.full`.

---

## Grosores de regla (border)

Las reglas son la herramienta de maquetación del periódico. Su grosor vive en `border.*` y su color en los tokens semánticos `border.hairline` / `border.section` (ver color.md). El grosor es independiente del color y de la escala de espaciado.

```yaml
border_width:
  - token: border.hairline
    value: 1px
    role: filo fino editorial
    color: border.hairline   # paper.300 (light) / paper.700 (dark)
    usage: separadores entre filas de tabla, divisores de lista, bordes de card, reglas finas internas

  - token: border.section
    value: 2px
    role: regla de sección
    color: border.section    # ink.500 (light) / paper.400 (dark)
    usage: regla bajo masthead/nameplate de sección; separación de bloques editoriales mayores

raw_spacing usage note: |
  El grosor de la regla NO consume la escala de espaciado. El AIRE alrededor de la
  regla (margen superior/inferior) sí: usar space.* (p. ej. space.4 sobre/bajo una
  regla de sección). Combinar siempre border.* (grosor) + radius.none (recto) + space.* (aire).
```

---

## Tokens semánticos

Espaciado listo para usar en producto. Los componentes deben consumir estos tokens.

```yaml
semantic_spacing:

  screen:
    # Nota: estos tokens se aplican DENTRO del área segura del dispositivo.
    # SafeArea (status bar, home indicator, notch) es responsabilidad del
    # sistema/Scaffold y se gestiona por separado. Ver sección SafeArea más abajo.
    - token: spacing.screen.horizontal
      description: padding lateral de todas las pantallas, dentro del área segura
      value: space.4   # 16px

    - token: spacing.screen.vertical.top
      description: padding superior del body, después de que AppBar o SafeArea resuelven el status bar
      value: space.4   # 16px

    - token: spacing.screen.vertical.bottom
      description: padding inferior del body, antes de NavigationBar o SafeArea resuelven el home indicator
      value: space.6   # 24px

    - token: spacing.screen.section.gap
      description: separación entre secciones dentro de una pantalla
      value: space.6   # 24px

  card:
    - token: spacing.card.padding.sm
      description: padding interno de cards compactas (listas de partidos, filas de tabla)
      horizontal: space.3  # 12px
      vertical: space.3    # 12px

    - token: spacing.card.padding.md
      description: padding interno de cards estándar
      horizontal: space.4  # 16px
      vertical: space.4    # 16px

    - token: spacing.card.padding.lg
      description: padding interno de cards destacadas o de detalle
      horizontal: space.5  # 20px
      vertical: space.5    # 20px

    - token: spacing.card.gap
      description: separación entre cards en listas o grids
      value: space.3   # 12px

  list:
    - token: spacing.list.item.gap
      description: separación entre ítems de lista
      value: space.1   # 4px — la separación la da el padding del ítem (y el filo hairline), no el gap entre ellos

    - token: spacing.list.item.padding.horizontal
      description: padding horizontal de un ítem de lista
      value: space.4   # 16px

    - token: spacing.list.item.padding.vertical
      description: padding vertical de un ítem de lista
      value: space.3   # 12px

  button:
    - token: spacing.button.padding.sm
      description: padding de botones pequeños y compactos
      horizontal: space.3  # 12px
      vertical: space.2    # 8px

    - token: spacing.button.padding.md
      description: padding de botones estándar
      horizontal: space.4  # 16px
      vertical: space.3    # 12px

    - token: spacing.button.padding.lg
      description: padding de botones grandes o CTA principales
      horizontal: space.6  # 24px
      vertical: space.4    # 16px

    - token: spacing.button.icon.gap
      description: separación entre icono y texto dentro de un botón
      value: space.2   # 8px

  input:
    - token: spacing.input.padding.horizontal
      description: padding lateral de campos de texto e inputs
      value: space.4   # 16px

    - token: spacing.input.padding.vertical
      description: padding vertical de campos de texto
      value: space.3   # 12px

  navigation:
    - token: spacing.navigation.bottom.height
      description: altura de la bottom navigation bar
      value: space.16  # 64px — referencia, el sistema Flutter define la altura final

    - token: spacing.navigation.item.gap
      description: separación entre ítems de bottom nav (gestionado por NavigationBar)
      value: space.1   # 4px — ajustar según densidad del dispositivo

  inline:
    - token: spacing.inline.xs
      description: separación mínima entre elementos en línea (icono + label)
      value: space.1   # 4px

    - token: spacing.inline.sm
      description: separación compacta entre elementos en línea
      value: space.2   # 8px

    - token: spacing.inline.md
      description: separación estándar entre elementos en línea
      value: space.3   # 12px

  # --- Tokens editoriales AtomSN ---

  column:
    - token: spacing.column.gap
      description: >
        gutter entre columnas en layouts multi-columna (tablas de clasificación,
        grids de partidos, maquetación web a 2+ columnas). Único y fijo, como el
        medianil de un periódico.
      value: space.4   # 16px

  overline:
    - token: spacing.overline.gap
      description: >
        separación entre un kicker/overline en mayúsculas (text.overline: "GRUPO A",
        "EN VIVO", "JORNADA 12") y el titular o bloque que encabeza. El overline se
        pega a su titular para leerse como una unidad editorial.
      value: space.1   # 4px
```

---

## SafeArea y zonas del sistema

`SafeArea` y los tokens `spacing.screen.*` son **capas distintas y complementarias**. No se reemplazan entre sí.

---

## Integración Flutter

### EdgeInsets desde la escala

```dart
// Equivalentes directos de los tokens base
const double space1 = 4;
const double space2 = 8;
const double space3 = 12;
const double space4 = 16;
const double space6 = 24;

// Padding estándar de pantalla (spacing.screen.horizontal)
const EdgeInsets screenPadding = EdgeInsets.symmetric(horizontal: space4);

// Padding de card estándar (spacing.card.padding.md)
const EdgeInsets cardPaddingMd = EdgeInsets.all(space4);

// Padding de botón estándar (spacing.button.padding.md)
const EdgeInsets buttonPaddingMd = EdgeInsets.symmetric(
  horizontal: space4,
  vertical: space3,
);
```

### BorderRadius desde la escala

```dart
// radius.none — borde recto editorial: reglas, sellos, tablas
const BorderRadius radiusNone = BorderRadius.zero;

// radius.sm — inputs y botones secundarios
const BorderRadius radiusSm = BorderRadius.all(Radius.circular(8));

// radius.md — el más frecuente (cards estándar)
const BorderRadius radiusMd = BorderRadius.all(Radius.circular(12));

// radius.full — avatares y elementos circulares
const BorderRadius radiusFull = BorderRadius.all(Radius.circular(9999));
```

### Reglas editoriales (border)

```dart
// border.hairline — filo fino (1px). Color: border.hairline (paper.300 light)
// Separador entre filas de tabla / divisor de lista.
const double borderHairline = 1;
const Divider hairlineRule = Divider(
  height: 1,
  thickness: borderHairline,
  // color: tomar de border.hairline en el theme activo
);

// border.section — regla de sección (2px). Color: border.section (ink.500 light)
// Bajo masthead/nameplate. Recta (radius.none) y con aire space.4 alrededor.
const double borderSection = 2;
const Border sectionRule = Border(
  bottom: BorderSide(width: borderSection /*, color: border.section */),
);
```

### SizedBox y gaps

```dart
// Separación vertical entre secciones (spacing.screen.section.gap)
const SizedBox sectionGap = SizedBox(height: 24);

// Separación entre icono y texto (spacing.inline.sm)
const SizedBox inlineGapSm = SizedBox(width: 8);

// Separación entre cards (spacing.card.gap)
const SizedBox cardGap = SizedBox(height: 12);

// Gutter de columna en layouts multi-columna (spacing.column.gap)
const SizedBox columnGap = SizedBox(width: 16);

// Separación overline → titular (spacing.overline.gap)
const SizedBox overlineGap = SizedBox(height: 4);
```

---

## Relación entre espaciado y tipografía

| Contexto | Token tipográfico | Padding / gap recomendado |
|---|---|---|
| Botón con `text.label.lg` | 14px / medium | `spacing.button.padding.md` |
| Ítem de lista con `text.body.md` | 14px / regular | `spacing.list.item.padding.*` |
| Card con `text.title.lg` | 20px / semibold | `spacing.card.padding.md` |
| Chip con `text.label.md` | 12px / medium | `spacing.button.padding.sm` |
| Input con `text.body.lg` | 16px / regular | `spacing.input.padding.*` |
| Overline `text.overline` sobre titular `text.headline.*` | 12px / semibold mayúsculas | `spacing.overline.gap` (4px) |
| Columnas de `text.stat.*` / tabla de clasificación | tabular | `spacing.column.gap` (16px) + `radius.none` |
| Masthead `text.masthead.*` con regla inferior | serif display | `border.section` (2px) + `space.4` de aire |
```
