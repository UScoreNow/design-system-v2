# Sistema Tipográfico — UScoreNow (tema editorial AtomSN)

> **Versión:** 2.1 · **Plataforma:** Flutter (mobile-first + web) · **Modelo:** FAMILIA ÚNICA (ElmsSans)

## Dirección visual

El sistema mantiene la **voz de periódico deportivo**: página de papel (crema cálido)
impresa con tinta cálida, jerarquía editorial nítida. Esa jerarquía nace del ritmo de
tamaño, peso, interlineado y tracking sobre una **única familia tipográfica, ElmsSans**.

La cabecera (masthead, titulares de crónica) y el aparato de interfaz (cuerpo, datos,
marcadores) comparten familia; la diferencia de voz la marcan el tamaño grande y el
tracking apretado de los titulares frente a la lectura tabular y neutra del resto.

> Cambio respecto a 2.0: el sistema unificó la tipografía en ElmsSans. La serif de
> cabecera (Libre Caslon Display, vía `google_fonts`) se retiró. El token
> `font.family.serif` permanece como alias histórico y resuelve a ElmsSans.

---

## La familia única

El sistema usa una sola familia, definida en `font.family.*` de `tokens.json`:

| Token | Familia | Stack | Uso |
|---|---|---|---|
| `font.family.sans` | **ElmsSans** | `["ElmsSans", "sans-serif"]` | Todo el sistema |
| `font.family.serif` | **ElmsSans** (alias) | `["ElmsSans", "sans-serif"]` | Alias histórico de cabecera; resuelve a ElmsSans w400 |

### Reparto por jerarquía (no por familia)

- **Cabecera (`text.masthead.*`, `text.headline.*`)** — ElmsSans a peso **400 (regular)**,
  tamaños ≥20px, con tracking apretado en masthead (`tight -0.02em`) y normal en headline.
  El tamaño grande y el tracking dan la presencia "impresa" del nameplate.
- **Interfaz y datos** — ElmsSans en el resto: títulos de card y UI (`text.title.*`),
  cuerpo (`text.body.*`), labels (`text.label.*`), overlines/kickers (`text.overline`),
  captions (`text.caption`), estadísticas (`text.stat.*`) y marcadores display
  (`text.display.*`). Los marcadores y stats usan **cifras tabulares**.

Regla operativa: una sola familia (ElmsSans); la jerarquía se construye con tamaño, peso,
interlineado y tracking. No se admiten otras familias.

---

## Registro de fuentes

ElmsSans es la única familia y se registra local desde assets (variable, con italic).
Ya no hay dependencia de `google_fonts`.

### ElmsSans — local desde assets (variable, con italic)

Archivos en `assets/fonts/elms_sans/` (licencia OFL incluida en `OFL.txt`):

- `ElmsSans-VariableFont.ttf`
- `ElmsSans-Italic-VariableFont.ttf`

Registro en `pubspec.yaml`:

```yaml
flutter:
  fonts:
    - family: ElmsSans
      fonts:
        - asset: assets/fonts/elms_sans/ElmsSans-VariableFont.ttf
        - asset: assets/fonts/elms_sans/ElmsSans-Italic-VariableFont.ttf
          style: italic
```

> **Fuente variable:** al registrar el variable font sin declarar `weight`, Flutter acepta
> cualquier `FontWeight` (incluidos intermedios como `FontWeight.w450`) y la fuente
> interpola el trazo. No hace falta registrar archivos estáticos por peso.

---

## Escala base

Valores crudos de `tokens.json` (`font.*`). No se usan directamente en componentes; se
componen vía `text.*`.

### `font.family`

| Token | Valor |
|---|---|
| `font.family.sans` | `["ElmsSans", "sans-serif"]` — todo el sistema |
| `font.family.serif` | `["ElmsSans", "sans-serif"]` — alias histórico, resuelve a ElmsSans |

### `font.size`

| Token | Valor |
|---|---|
| `font.size.sm` | 12px |
| `font.size.md` | 14px |
| `font.size.lg` | 16px |
| `font.size.xl` | 18px |
| `font.size.2xl` | 20px |
| `font.size.3xl` | 24px |
| `font.size.4xl` | 32px |
| `font.size.5xl` | 40px |
| `font.size.6xl` | 48px |
| `font.size.7xl` | 60px |

### `font.weight`

| Token | Valor |
|---|---|
| `font.weight.regular` | 400 |
| `font.weight.medium` | 500 |
| `font.weight.semibold` | 600 |
| `font.weight.bold` | 700 |
| `font.weight.extrabold` | 800 |
| `font.weight.black` | 900 |

> ElmsSans (variable) cubre todos los pesos `400`–`900`. La cabecera usa `400`;
> `800`/`900` quedan para cifras display de alto impacto (`display.score`, `stat`).

### `font.lineHeight`

| Token | Valor |
|---|---|
| `font.lineHeight.tight` | 1.1 |
| `font.lineHeight.snug` | 1.25 |
| `font.lineHeight.normal` | 1.5 |
| `font.lineHeight.relaxed` | 1.65 |

### `font.tracking`

| Token | Valor | Uso |
|---|---|---|
| `font.tracking.tight` | -0.02em | titulares grandes y cifras compactas |
| `font.tracking.normal` | 0em | uso general |
| `font.tracking.wide` | 0.02em | labels y texto en mayúsculas |
| `font.tracking.xwide` | 0.06em | metadata/categorías amplias |
| `font.tracking.kicker` | **0.08em** | overline/kicker en mayúsculas (`text.overline`) |

---

## Composiciones semánticas `text.*`

Composiciones exactas de `tokens.json`. Los componentes consumen SOLO estas. Toda la
columna `fam` es ElmsSans. `tab` = cifras tabulares obligatorias. `upper` = transform
uppercase.

| Token | fam | size | weight | lineHeight | tracking | tab | upper | Uso |
|---|---|---|---|---|---|---|---|---|
| `text.masthead.xl` | ElmsSans | 7xl / 60px | 400 | tight 1.1 | tight -0.02em | — | — | nameplate de pantalla/sección |
| `text.masthead.lg` | ElmsSans | 4xl / 32px | 400 | snug 1.25 | tight -0.02em | — | — | masthead secundario |
| `text.headline.xl` | ElmsSans | 4xl / 32px | 400 | snug 1.25 | normal 0em | — | — | titular editorial/crónica |
| `text.headline.lg` | ElmsSans | 3xl / 24px | 400 | snug 1.25 | normal 0em | — | — | titular menor |
| `text.display.score` | ElmsSans | 7xl / 60px | 800 | tight 1.1 | tight -0.02em | sí | — | marcador principal de partido |
| `text.display.stat` | ElmsSans | 5xl / 40px | 700 | tight 1.1 | tight -0.02em | sí | — | cifra display de stat |
| `text.title.lg` | ElmsSans | 2xl / 20px | 600 | snug 1.25 | normal 0em | — | — | título de card / dato |
| `text.title.md` | ElmsSans | xl / 18px | 500 | normal 1.5 | normal 0em | — | — | subtítulo / encabezado de lista |
| `text.body.lg` | ElmsSans | lg / 16px | 400 | normal 1.5 | — | — | — | cuerpo principal, descripciones |
| `text.body.md` | ElmsSans | md / 14px | 400 | normal 1.5 | — | — | — | interfaz estándar — el más frecuente |
| `text.body.sm` | ElmsSans | sm / 12px | 400 | normal 1.5 | — | — | — | texto auxiliar, metadatos |
| `text.label.lg` | ElmsSans | md / 14px | 500 | tight 1.1 | — | — | — | labels de botones/controles/nav |
| `text.label.md` | ElmsSans | sm / 12px | 500 | tight 1.1 | — | — | — | chips, badges, etiquetas compactas |
| `text.overline` | ElmsSans | sm / 12px | 600 | tight 1.1 | kicker 0.08em | — | **sí** | kicker: "GRUPO A", "EN VIVO", "JORNADA 12" |
| `text.stat.lg` | ElmsSans | 3xl / 24px | 700 | tight 1.1 | tight -0.02em | sí | — | stat mediana en cards de resumen |
| `text.stat.md` | ElmsSans | xl / 18px | 600 | tight 1.1 | normal 0em | sí | — | stat en listas/filas de tabla |
| `text.caption` | ElmsSans | sm / 12px | 400 | normal 1.5 | — | — | — | pie de foto, nota editorial breve |

Notas de composición:

- **Cabecera (`masthead.*`, `headline.*`)** a peso 400; la presencia la dan el tamaño y el
  tracking, no la negrita.
- **`tabular: true`** es obligatorio en `display.score`, `display.stat`, `stat.lg` y
  `stat.md`: marcadores, minutos y stats deben alinear cifras en columna (ver Flutter,
  `FontFeature.tabularFigures()`).
- **`text.overline`** es el único con `transform: uppercase` y usa `tracking.kicker`
  0.08em. Es el kicker editorial del sistema.
- `text.headline.*` comparte tamaño con `masthead.lg` (32px) pero con `tracking.normal`
  en vez de `tight`: el masthead aprieta, el titular respira.

---

## Integración Flutter

Mapeo de `text.*` a `TextStyle`. Una sola vía de familia: `fontFamily: 'ElmsSans'`.

> **`letterSpacing`** en Flutter va en píxeles lógicos, no en `em`. Fórmula:
> `valor_em × fontSize`. Ej.: `-0.02em` a 60px → `-1.2`; `0.08em` a 12px → `0.96`.

> **Cifras tabulares:** las composiciones marcadas `tab` exigen
> `fontFeatures: [FontFeature.tabularFigures()]` para que los dígitos no "bailen" al
> cambiar el marcador.

### TextStyle de ejemplo

```dart
import 'package:flutter/material.dart';

// text.masthead.xl — ElmsSans w400, tracking apretado
const TextStyle mastheadXl = TextStyle(
  fontFamily: 'ElmsSans',
  fontSize: 60,
  fontWeight: FontWeight.w400,
  height: 1.1,                 // lineHeight.tight
  letterSpacing: -1.2,         // -0.02em x 60px
);

// text.headline.xl — titular de crónica
const TextStyle headlineXl = TextStyle(
  fontFamily: 'ElmsSans',
  fontSize: 32,
  fontWeight: FontWeight.w400,
  height: 1.25,                // lineHeight.snug
  letterSpacing: 0,            // tracking.normal
);

// text.body.md — el más frecuente
const TextStyle bodyMd = TextStyle(
  fontFamily: 'ElmsSans',
  fontSize: 14,
  fontWeight: FontWeight.w400,
  height: 1.5,                 // lineHeight.normal
  letterSpacing: 0,
);

// text.display.score — marcador con cifras tabulares
const TextStyle displayScore = TextStyle(
  fontFamily: 'ElmsSans',
  fontSize: 60,
  fontWeight: FontWeight.w800,
  height: 1.1,
  letterSpacing: -1.2,         // -0.02em x 60px
  fontFeatures: [FontFeature.tabularFigures()],
);

// text.overline — kicker en mayúsculas (aplicar el uppercase en el String)
const TextStyle overline = TextStyle(
  fontFamily: 'ElmsSans',
  fontSize: 12,
  fontWeight: FontWeight.w600,
  height: 1.1,
  letterSpacing: 0.96,         // 0.08em x 12px (tracking.kicker)
);
// uso: Text('GRUPO A', style: overline)  // el transform uppercase se aplica al texto
```

### TextTheme recomendado

Todas las ranuras usan ElmsSans; las de cabecera (`displayLarge`, `headlineLarge/Medium`)
a peso 400, y las de cifras (`displayMedium` = score) llevan `fontFeatures` tabular.
La implementación real vive en `lib/theme/app_typography.dart`.

```dart
import 'package:flutter/material.dart';

const _tabular = [FontFeature.tabularFigures()];

const TextTheme appTextTheme = TextTheme(
  // --- Cabecera: masthead + headline (ElmsSans w400) ---
  displayLarge: TextStyle(
    fontFamily: 'ElmsSans', fontSize: 60, fontWeight: FontWeight.w400,
    height: 1.1, letterSpacing: -1.2),
  headlineLarge: TextStyle(
    fontFamily: 'ElmsSans', fontSize: 32, fontWeight: FontWeight.w400,
    height: 1.25, letterSpacing: 0),
  headlineMedium: TextStyle(
    fontFamily: 'ElmsSans', fontSize: 24, fontWeight: FontWeight.w400,
    height: 1.25, letterSpacing: 0),

  // --- Display de cifras (tabular) ---
  displayMedium: TextStyle(
    fontFamily: 'ElmsSans', fontSize: 60, fontWeight: FontWeight.w800,
    height: 1.1, letterSpacing: -1.2, fontFeatures: _tabular),
  displaySmall: TextStyle(
    fontFamily: 'ElmsSans', fontSize: 40, fontWeight: FontWeight.w700,
    height: 1.1, letterSpacing: -0.8, fontFeatures: _tabular),

  // --- Títulos UI ---
  titleLarge: TextStyle(
    fontFamily: 'ElmsSans', fontSize: 20, fontWeight: FontWeight.w600, height: 1.25),
  titleMedium: TextStyle(
    fontFamily: 'ElmsSans', fontSize: 18, fontWeight: FontWeight.w500, height: 1.5),

  // --- Cuerpo ---
  bodyLarge: TextStyle(
    fontFamily: 'ElmsSans', fontSize: 16, fontWeight: FontWeight.w400, height: 1.5),
  bodyMedium: TextStyle(
    fontFamily: 'ElmsSans', fontSize: 14, fontWeight: FontWeight.w400, height: 1.5),
  bodySmall: TextStyle(
    fontFamily: 'ElmsSans', fontSize: 12, fontWeight: FontWeight.w400, height: 1.5),

  // --- Labels ---
  labelLarge: TextStyle(
    fontFamily: 'ElmsSans', fontSize: 14, fontWeight: FontWeight.w500, height: 1.1),
  labelMedium: TextStyle(
    fontFamily: 'ElmsSans', fontSize: 12, fontWeight: FontWeight.w500, height: 1.1),
  labelSmall: TextStyle(
    fontFamily: 'ElmsSans', fontSize: 12, fontWeight: FontWeight.w600,
    height: 1.1, letterSpacing: 0.96),
);
```

> Material `TextTheme` tiene 15 ranuras y el sistema define 17 composiciones.
> `text.masthead.lg`, `text.stat.lg` y `text.stat.md` no tienen ranura directa: defínelas
> como `TextStyle` reutilizables o como extensión de tema, no las fuerces en ranuras
> semánticamente ajenas.

---

## Criterio de composición

El sistema se lee como un **periódico deportivo** con una sola voz tipográfica bien
graduada: cabecera de presencia (ElmsSans grande, tracking apretado) y un cuerpo de
trabajo silencioso y preciso (ElmsSans en lectura y datos). La coherencia la mantiene la
jerarquía, no la mezcla de familias:

- La cabecera "habla" en masthead y titular: aparece poco y grande, a peso 400.
- El resto se hace cargo de las cifras: marcadores, minutos y stats van en ElmsSans
  tabular para alinear en columna y no saltar al actualizarse.
- El kicker (`text.overline`, uppercase, `tracking.kicker` 0.08em) etiqueta secciones y
  estados ("EN VIVO", "JORNADA 12").

La personalidad nace de la jerarquía sobre una familia única. Todo es ElmsSans.
