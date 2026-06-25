# AtomSN — Design System · Tema editorial AtomSN

> **Versión:** 2.0
> **Estado:** En desarrollo
> **Plataforma:** Flutter · mobile-first · con soporte Flutter Web
> **Modos:** light ("AtomSN Light") · dark ("AtomSN Dark")
> **Stack:** Dart / Flutter · Hugeicons · ElmsSans (sans)

Sistema de diseño para la app de gestión de torneos de fútbol UScoreNow. Evoluciona el sistema minimalista de v1 hacia un aire de **periódico deportivo de verdad**: base apapelada crema sobre la que se imprime tinta cálida, con verde césped y negro tinta como únicos acentos. El contenido —marcadores, clasificaciones, crónicas— manda; el utillaje editorial (reglas hairline, kickers en mayúsculas, líderes punteados, cifras tabulares, sellos de tinta) le da voz de prensa sin ruido cromático.

---

## Principios generales

Restricciones duras del sistema. Aplican a todos los archivos y a toda decisión de implementación:

- **Tinta sobre papel.** La base es crema apapelada (`color.paper.*`); el texto y los destacados son tinta cálida (`color.ink.*`). No hay grises fríos.
- **Negros y blancos puros prohibidos.** `#000000` y `#FFFFFF` están vetados. El negro legal más oscuro es `color.ink.900` `#0E0D0A`; el papel más claro, `color.paper.50` `#FBF8F0`.
- **El verde es escaso.** `color.green.*` se reserva para acciones, estados activos/seleccionados y deltas positivos. Nunca como relleno decorativo.
- **Relleno vs. texto.** Los tokens `*.500` (green/yellow/red) son de RELLENO/ICONO; sus `*.700`/`*.800` son los de TEXTO sobre papel (cumplen AA). En dark, el texto de estado usa variantes más claras (`*.300`/`*.400`).
- **Tokens semánticos en producto.** Los tokens base son la capa fundacional; los componentes consumen SOLO tokens semánticos (`semantic.light.*` / `semantic.dark.*`).
- **Una librería de iconos.** Solo `Hugeicons`, estilo `strokeRounded` como base obligatoria.
- **Una excepción, una regla explícita.** Consistencia sobre expresividad: una semántica → un recurso visual. Toda desviación se documenta como excepción acotada (ver abajo).

---

## Excepciones a reglas duras

El sistema histórico imponía dos invariantes que v2 rompe de forma **explícita y acotada**:

- **Segunda familia tipográfica (serif).** v1 exigía una sola familia. v2 añade `Libre Caslon Display` como **excepción documentada**, restringida a `masthead`, `headline` y `display`-titulares. **Nunca** se usa por debajo de 20px, ni en cuerpo, UI, labels, captions o stats: todo eso sigue siendo `ElmsSans`. La serif solo tiene peso 400; se emplea a tamaño grande, donde el alto contraste de la Caslon ya da presencia.
- **Negro tinta `ink.900` permitido.** v1 trataba el negro como inalcanzable. v2 habilita `color.ink.900` `#0E0D0A` para destacados, sellos ("FINAL") y mastheads. **Esto no levanta la prohibición de `#000000` puro**, que sigue vetado: `ink.900` es el negro legal más oscuro, no el negro absoluto.

---

## Índice de artefactos

```
atom-sn-design-system/
├── tokens/
│   └── tokens.json       # FUENTE ÚNICA DE VERDAD (formato DTCG). Color, tipografía,
│                         #   espaciado, radios, reglas. Toda decisión sale de aquí.
├── colors/
│   └── colors.md         # Rampas paper/ink/green/yellow/red/indigo + semánticos light/dark
├── fonts/
│   └── typography.md     # Duotono serif/sans, escala, composiciones text.*, cifras tabulares
├── icons/
│   └── icons.md          # Sistema iconográfico con Hugeicons (strokeRounded)
├── spacing/
│   └── spacing.md        # Escala 4px, padding, gap, radios (radius.none editorial)
├── editorial/            # Capítulo nuevo: reglas hairline/section, kickers/overlines,
│                         #   líderes punteados, highlight marker, sellos de tinta
├── preview/
│   └── index.html        # Preview HTML del sistema para inspección en navegador
└── assets/
    └── fonts/
        └── elms_sans/    # ElmsSans variable (Regular + Italic) · OFL.txt
```

> Estado: `colors/`, `fonts/`, `icons/`, `spacing/` y `tokens/` están poblados. `editorial/` y `preview/` son directorios de la estructura objetivo, en construcción. `Libre Caslon Display` (serif, w400) se resuelve vía fuente del sistema/CDN; solo `ElmsSans` se versiona en `assets/fonts/`.

> **Repo solo de documentación.** Aquí vive la especificación del sistema (tokens DTCG, docs, marca, preview). La **implementación Flutter** (tema y componentes derivados de `tokens.json`) vive en el repo de código [`UScoreNow/atom-sn`](https://github.com/UScoreNow/atom-sn).

---

## Secciones del sistema

### Colores

Sistema cromático editorial: **papel crema** como base estructural, **tinta cálida** para texto, **verde césped** y **negro tinta** como únicos acentos.

- **Papel** (`color.paper.50` `#FBF8F0` → `color.paper.900` `#2B2820`): fondos, superficies, bordes y reglas hairline.
- **Tinta** (`color.ink.50` `#6E6A60` → `color.ink.900` `#0E0D0A`, más `color.ink.bg` `#16140F` para el fondo dark): texto, reglas de sección y sellos.
- **Verde** (`color.green.500` `#3E8E45`): acción primaria y estados activos. `green.700` `#27592C` para texto/enlaces sobre papel (AA).
- **Estado**: `red` (live/error), `yellow` (tarjeta/warning + highlight marker), `indigo` (solo `status.info`, uso escaso heredado de v1).
- **Highlight marker**: `highlight.mark` → wash `yellow.100` tras stats/records clave.
- Semánticos con mapeo explícito light ("AtomSN Light") / dark ("AtomSN Dark").

Convención: `color.{familia}.{escala}` (base) · `color.{categoría}.{rol}` y `text.{grupo}.{nivel}` (semánticos).

→ [Documentación de colores](colors/colors.md)

---

### Tipografía

Sistema **duotono**: serif editorial para titulares, sans para todo lo demás.

| Familia | Token | Uso |
|---|---|---|
| `Libre Caslon Display` | `font.family.serif` | Solo masthead/headline/display-titular. Peso 400. Nunca <20px ni en cuerpo. |
| `ElmsSans` (variable) | `font.family.sans` | Cuerpo, UI, labels, captions, stats (cifras tabulares). |

- **Cifras tabulares obligatorias** en marcadores, minutos y stats (`tabular: true` en `display.*`, `stat.*`).
- **Overline/kicker** (`text.overline`): mayúsculas, tracking `0.08em` → "GRUPO A", "EN VIVO", "JORNADA 12".
- Escala de `font.size.sm` (12px) a `font.size.7xl` (60px); pesos `regular` (400) a `black` (900).

Convención: `font.{categoría}.{nivel}` (base) · `text.{grupo}.{nivel}` (composiciones).

→ [Documentación de tipografía](fonts/typography.md)

---

### Iconografía

Librería única: **Hugeicons** (`package:hugeicons/hugeicons.dart`), estilo `strokeRounded`. Tamaño base `24.0`, trazo `1.5`. Estado seleccionado diferenciado por color, no por estilo.

Convención: `icon.{dominio}.{nombre}` — p.ej. `icon.navigation.home`, `icon.status.live`.

→ [Documentación de iconos](icons/icons.md)

---

### Espaciado

Escala en múltiplos de 4px para padding, gap, márgenes y radios.

| Token | Valor | Uso |
|---|---|---|
| `space.2` | 8px | Espacio interno compacto |
| `space.4` | 16px | Padding base de componentes |
| `space.6` | 24px | Separación entre secciones |
| `radius.none` | 0px | Reglas, sellos, tablas: borde recto editorial |
| `radius.md` | 12px | Borde estándar de cards |
| `border.hairline` | 1px | Regla fina editorial (`paper.300`) |
| `border.section` | 2px | Regla de sección bajo masthead (`ink.500`) |

El periódico prefiere esquinas rectas: `radius.none` para reglas, sellos y tablas; `radius.md` se mantiene como estándar de cards.

Convención: `space.{n}` (múltiplos de 4) · `radius.{nivel}` · `border.{grosor}`.

→ [Documentación de espaciado](spacing/spacing.md)

---

### Editorial

Capítulo nuevo de v2 con el utillaje de prensa: reglas/filos hairline y de sección, kickers/overlines en mayúsculas, líderes punteados (`paper.400`) en tablas de clasificación, highlight "marker" (`highlight.mark`), cifras tabulares y sellos de tinta `ink.900` ("FINAL"). En construcción en `editorial/`.

---

## Cómo consumir

### Flutter (producto)

Usar el tema generado en `lib/theme/` y registrar las fuentes en `pubspec.yaml`:

```yaml
# pubspec.yaml
flutter:
  fonts:
    - family: ElmsSans
      fonts:
        - asset: assets/fonts/elms_sans/ElmsSans-VariableFont.ttf
        - asset: assets/fonts/elms_sans/ElmsSans-Italic-VariableFont.ttf
          style: italic
  # Libre Caslon Display (serif, w400): vía google_fonts o fuente del sistema.
```

```dart
// main.dart
MaterialApp(
  theme: UScoreTheme.light,      // "AtomSN Light"
  darkTheme: UScoreTheme.dark,   // "AtomSN Dark"
);
```

### Web / otras plataformas

Consumir `tokens/tokens.json` (formato DTCG) directamente o vía pipeline de transformación (Style Dictionary u otro) para emitir CSS custom properties, JS, etc. `preview/index.html` sirve como referencia visual rápida en navegador.

---

> **Fuente única de verdad:** `tokens/tokens.json`. Ningún hex, nombre de token ni decisión tipográfica vive fuera de él. La documentación describe; los tokens deciden.

## Contributing

This repository follows the [UScoreNow contribution guidelines](https://github.com/UScoreNow/.github/blob/main/CONTRIBUTING.md): branching model, Conventional Commits, pull requests and releases.
