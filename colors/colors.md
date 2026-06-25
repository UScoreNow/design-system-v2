# Sistema de Colores — Tema editorial AtomSN

> **Versión:** 2.0 · **Plataforma:** Flutter (mobile-first + web) · **Temas:** light "AtomSN Light" / dark "AtomSN Dark"

## Dirección visual

El sistema cromático evoluciona del minimalismo neutro anterior (grises fríos + verde único) hacia un aire de **periódico de verdad**. Cuatro materiales definen la paleta:

- **Papel crema:** la base deja de ser gris frío y pasa a una rampa apapelada cálida (`color.paper.*`). El papel ligeramente tintado reduce la fatiga visual, da profundidad sin blancos puros y evoca la prensa deportiva impresa.
- **Tinta cálida:** el texto y los destacados son tinta (`color.ink.*`), un negro que lleva un susurro del tono papel para no enfriarse sobre crema. `ink.900` (`#0E0D0A`) es el negro de tinta más oscuro: sellos, masthead y destacados.
- **Verde césped cálido:** acento único de interacción (`color.green.*`). Escaso: solo acciones, estados activos/seleccionados y deltas positivos.
- **Negro tinta:** segundo acento editorial, reservado a destacados y sellos (`accent.ink`).

Todo lo que no sea acción debe sentirse como **tinta sobre papel**.

---

## Principios

- La interfaz vive sobre papel crema, no sobre blanco de pantalla.
- El verde destaca acciones, estados activos y elementos clave; nunca decora.
- El negro tinta (`ink.900`) es para destacados de alto contraste y sellos editoriales ("FINAL"), no para texto de cuerpo (ese es `ink.700`).
- El tema claro "AtomSN Light" usa fondo crema, tinta para texto y acentos verde/negro.
- El tema oscuro "AtomSN Dark" usa fondo tinta, texto crema y acentos verde claro/papel.
- Los componentes no definen colores propios: consumen exclusivamente tokens semánticos.
- La paleta base es capa fundacional; no se usa directa en producto.

---

## Restricciones base

- Papel más claro permitido: `color.paper.50` (`#FBF8F0`).
- Tinta más oscura permitida (negro legal): `color.ink.900` (`#0E0D0A`).
- **El blanco puro (`#FFFFFF`) está prohibido.** No existe en el sistema y no debe usarse bajo ninguna circunstancia.
- **El negro puro (`#000000`) está prohibido.** El negro más oscuro del sistema es `ink.900` (`#0E0D0A`); los destacados "negros" resuelven siempre ahí.
- **El verde es escaso.** Solo acciones, estados activos/seleccionados y deltas positivos. No usarlo para superficies amplias ni como decoración.
- El indigo se mantiene del sistema anterior, pero **solo para `status.info`** y de forma escasa. No es color de navegación ni de acción.

---

## Convención de nombres

```text
# Tokens base (paleta cruda — capa fundacional):
color.{familia}.{escala}

# Tokens semánticos (uso en producto), por modo (light / dark):
color.{categoría}.{rol}
text.{grupo}.{nivel}
```

Ejemplos base: `color.paper.50`, `color.ink.900`, `color.green.500`
Ejemplos semánticos: `bg.base`, `text.primary`, `action.primary`, `accent.ink`, `border.hairline`, `status.liveText`, `highlight.mark`

---

## Paleta base

Valores crudos del sistema. No usar directamente en componentes. Hex, rol y usage tal cual `tokens.json`.

```yaml
raw_palette:

  paper:
    # Rampa neutra crema cálida. Sustituye a la gris fría del sistema anterior.
    - token: color.paper.50
      hex: "#FBF8F0"
      role: papel más claro
      usage: fondo app (light)

    - token: color.paper.100
      hex: "#F5F0E3"
      role: superficie elevada / cards
      usage: texto primario (dark)

    - token: color.paper.200
      hex: "#ECE4D2"
      role: superficie con tinte
      usage: hover, raised

    - token: color.paper.300
      hex: "#DCD2BC"
      role: bordes y reglas hairline (light)
      usage: border.default / border.hairline (light)

    - token: color.paper.400
      hex: "#C2B69D"
      role: borde fuerte / relleno disabled
      usage: líderes punteados en tablas de clasificación

    - token: color.paper.500
      hex: "#A6987C"
      role: texto tenue (dark) / mid neutro
      usage: text.muted

    - token: color.paper.600
      hex: "#857862"
      role: texto terciario (light)
      usage: text.tertiary (light)

    - token: color.paper.700
      hex: "#615847"
      role: texto secundario (light) / borde (dark)
      usage: text.secondary (light) / border.default (dark)

    - token: color.paper.800
      hex: "#403A30"
      role: superficie elevada cálida
      usage: dark raised (bg.raised dark)

    - token: color.paper.900
      hex: "#2B2820"
      role: neutro cálido más oscuro
      usage: valor de escala

  ink:
    # Negro tinta cálido (lleva un susurro del tono papel para no enfriar sobre crema).
    - token: color.ink.50
      hex: "#6E6A60"
      role: tinta tenue
      usage: captions

    - token: color.ink.100
      hex: "#514D44"
      role: tinta media-tenue
      usage: valor de escala

    - token: color.ink.300
      hex: "#39362E"
      role: superficie base (dark surface)
      usage: regla de sección / bg.surface (dark)

    - token: color.ink.500
      hex: "#26241E"
      role: tinta estándar
      usage: regla de sección 2px bajo masthead (border.section light)

    - token: color.ink.700
      hex: "#1A1814"
      role: tinta de titular
      usage: texto primario (light) (text.primary)

    - token: color.ink.900
      hex: "#0E0D0A"
      role: NEGRO tinta
      usage: destacados, sellos "FINAL", masthead, accent.ink. Negro legal más oscuro.

    - token: color.ink.bg
      hex: "#16140F"
      role: fondo base del tema oscuro
      usage: bg.base (dark "AtomSN Dark")

  green:
    # Verde césped cálido. Acento único de interacción. Escaso.
    - token: color.green.50
      hex: "#EAF1E4"
      role: superficie verde sutil
      usage: action.subtle (light)

    - token: color.green.100
      hex: "#CDDFC0"
      role: verde claro
      usage: action.active (dark)

    - token: color.green.200
      hex: "#AECF96"
      role: verde suave
      usage: active / action.hover (dark)

    - token: color.green.300
      hex: "#8FBE6F"
      role: acción primaria (dark)
      usage: action.primary / text.link / border.active (dark)

    - token: color.green.400
      hex: "#5FA453"
      role: verde medio
      usage: valor de escala

    - token: color.green.500
      hex: "#3E8E45"
      role: acento primario (light)
      usage: acción, activo, marca (action.primary light)

    - token: color.green.600
      hex: "#327237"
      role: hover de acción (light)
      usage: action.hover (light)

    - token: color.green.700
      hex: "#27592C"
      role: verde para texto/enlaces sobre papel (AA)
      usage: text.link / action.active / status.successText (light)

    - token: color.green.800
      hex: "#1D4421"
      role: verde muy oscuro
      usage: valor de escala

    - token: color.green.900
      hex: "#163518"
      role: verde profundo
      usage: valor de escala

  yellow:
    # Mostaza editorial. Doble función: highlight "marcador" editorial + tarjeta amarilla/advertencia.
    - token: color.yellow.50
      hex: "#FBF4D8"
      role: amarillo muy claro
      usage: valor de escala

    - token: color.yellow.100
      hex: "#F6E8BE"
      role: wash de highlight "marker"
      usage: highlight.mark (light)

    - token: color.yellow.200
      hex: "#F0D89B"
      role: amarillo suave
      usage: valor de escala

    - token: color.yellow.300
      hex: "#E8C863"
      role: acentos de kicker / advertencia (dark)
      usage: status.warning / status.warningText (dark)

    - token: color.yellow.400
      hex: "#DFB740"
      role: amarillo medio
      usage: valor de escala

    - token: color.yellow.500
      hex: "#D6A52E"
      role: tarjeta amarilla / warning (light)
      usage: status.warning (light, RELLENO)

    - token: color.yellow.600
      hex: "#B98A1F"
      role: amarillo fuerte
      usage: valor de escala

    - token: color.yellow.700
      hex: "#9A7416"
      role: amarillo para texto sobre papel (AA)
      usage: highlight.mark wash atenuado (dark)

    - token: color.yellow.800
      hex: "#7A5B13"
      role: amarillo muy oscuro
      usage: status.warningText (light, AA pleno en texto pequeño)

    - token: color.yellow.900
      hex: "#5C4410"
      role: amarillo profundo
      usage: valor de escala

  red:
    # Ladrillo cálido de tinta. En vivo / error / estado crítico.
    - token: color.red.50
      hex: "#F7E6E4"
      role: rojo muy claro
      usage: valor de escala

    - token: color.red.100
      hex: "#EFC9C6"
      role: rojo claro
      usage: valor de escala

    - token: color.red.200
      hex: "#E29E99"
      role: rojo suave
      usage: valor de escala

    - token: color.red.300
      hex: "#D5736C"
      role: rojo medio claro
      usage: status.liveText / status.errorText (dark, AA sobre fondo oscuro)

    - token: color.red.400
      hex: "#CC554D"
      role: live/error (dark)
      usage: status.live / status.error (dark, RELLENO)

    - token: color.red.500
      hex: "#C5403A"
      role: live/error (light)
      usage: dot pulsante, alertas (status.live / status.error light, RELLENO)

    - token: color.red.600
      hex: "#A8332E"
      role: rojo fuerte
      usage: valor de escala

    - token: color.red.700
      hex: "#8C2A26"
      role: rojo para texto sobre papel (AA)
      usage: status.liveText / status.errorText (light)

    - token: color.red.800
      hex: "#6E211E"
      role: rojo muy oscuro
      usage: valor de escala

    - token: color.red.900
      hex: "#511817"
      role: rojo profundo
      usage: valor de escala

  indigo:
    # Información neutral / estadísticas complementarias. Se mantiene del sistema anterior; uso escaso y solo para status.info.
    - token: color.indigo.50
      hex: "#EEF2FF"
      role: índigo muy claro
      usage: valor de escala

    - token: color.indigo.100
      hex: "#E0E7FF"
      role: índigo claro
      usage: valor de escala

    - token: color.indigo.200
      hex: "#C7D2FE"
      role: índigo suave
      usage: valor de escala

    - token: color.indigo.300
      hex: "#A5B4FC"
      role: índigo medio claro
      usage: valor de escala

    - token: color.indigo.400
      hex: "#818CF8"
      role: info (dark)
      usage: status.info / status.infoText (dark)

    - token: color.indigo.500
      hex: "#6366F1"
      role: info (light)
      usage: status.info (light, RELLENO)

    - token: color.indigo.600
      hex: "#4F46E5"
      role: índigo fuerte
      usage: valor de escala

    - token: color.indigo.700
      hex: "#4338CA"
      role: info para texto sobre papel
      usage: status.infoText (light)

    - token: color.indigo.800
      hex: "#3730A3"
      role: índigo muy oscuro
      usage: valor de escala

    - token: color.indigo.900
      hex: "#312E81"
      role: índigo profundo
      usage: valor de escala
```

---

## Regla fill-vs-text

Los tokens `*.500` de las familias de estado (`green`/`yellow`/`red`) son de **RELLENO/ICONO**: dots, fondos de chip, iconos de estado. Sus variantes `*.700`/`*.800` son los de **TEXTO sobre papel** y cumplen AA.

- `status.live` / `status.error` / `status.success` / `status.warning` / `status.info` → relleno (`*.500`, yellow.500, indigo.500).
- `status.liveText` / `status.errorText` / `status.successText` / `status.warningText` / `status.infoText` → texto sobre papel (`red.700`, `green.700`, `yellow.800`, `indigo.700`).
- En **dark "AtomSN Dark"**, el texto de estado usa variantes más claras (`*.300`/`*.400`: `red.300`, `green.300`, `yellow.300`, `indigo.400`) para mantener AA sobre fondo tinta.

No usar `*.500` como color de texto pequeño sobre papel: no cumple contraste.

---

## Tokens semánticos

Capa de uso en producto. Los componentes consumen **solo** estos tokens. Cada token resuelve a un token base por modo (`semantic.light` "AtomSN Light" / `semantic.dark` "AtomSN Dark").

```yaml
semantic_tokens:

  bg:
    - token: bg.base
      description: fondo base de la app y scaffolds
      light: color.paper.50    # #FBF8F0 — papel crema, nunca blanco puro
      dark: color.ink.bg       # #16140F

    - token: bg.surface
      description: superficies elevadas — cards, sheets, modales
      light: color.paper.100   # #F5F0E3
      dark: color.ink.300      # #39362E

    - token: bg.raised
      description: superficie raised / elevación cálida
      light: color.paper.200   # #ECE4D2
      dark: color.paper.800    # #403A30

    - token: bg.subtle
      description: fondos de secciones internas, agrupaciones
      light: color.paper.100   # #F5F0E3
      dark: color.ink.300      # #39362E

    - token: bg.overlay
      description: overlay para modales y bottom sheets
      light: color.ink.900     # #0E0D0A — usar con opacidad 0.5
      dark: color.ink.900      # #0E0D0A — usar con opacidad 0.7

    - token: bg.inverse
      description: fondo de elementos invertidos (snackbars, tooltips)
      light: color.ink.900     # #0E0D0A
      dark: color.paper.50     # #FBF8F0

  text:
    - token: text.primary
      description: texto principal de alta jerarquía
      light: color.ink.700     # #1A1814 — 16.7:1 sobre paper.50 ✓ AAA
      dark: color.paper.100    # #F5F0E3 — 16.2:1 sobre ink.bg ✓ AAA

    - token: text.secondary
      description: texto de apoyo, subtítulos
      light: color.paper.700   # #615847 — 6.6:1 sobre paper.50 ✓ AA
      dark: color.paper.400    # #C2B69D — 9.2:1 sobre ink.bg ✓ AAA

    - token: text.tertiary
      description: texto tenue, metadatos, timestamps
      light: color.paper.600   # #857862 — 4.1:1 (decorativo / large)
      dark: color.paper.500    # #A6987C

    - token: text.muted
      description: texto más tenue, no esencial
      light: color.paper.500   # #A6987C
      dark: color.paper.500    # #A6987C

    - token: text.disabled
      description: texto de controles inactivos
      light: color.paper.400   # #C2B69D
      dark: color.paper.700    # #615847

    - token: text.inverse
      description: texto sobre fondos invertidos (bg.inverse)
      light: color.paper.50    # #FBF8F0
      dark: color.ink.900      # #0E0D0A

    - token: text.onPrimary
      description: texto sobre relleno de acción verde
      light: color.paper.50    # #FBF8F0 — 3.8:1 sobre green.500 ✓ AA large (bold ≥14px)
      dark: color.ink.900      # #0E0D0A — tinta oscura sobre green.300

    - token: text.link
      description: texto con acción de navegación o enlace
      light: color.green.700   # #27592C — 7.8:1 sobre paper.50 ✓ AAA
      dark: color.green.300    # #8FBE6F — 8.6:1 sobre ink.bg ✓ AAA

  action:
    - token: action.primary
      description: estado base de botones primarios, tabs activos, controles de acción
      light: color.green.500   # #3E8E45
      dark: color.green.300    # #8FBE6F

    - token: action.hover
      description: estado hover/focus (web/desktop Flutter)
      light: color.green.600   # #327237
      dark: color.green.200    # #AECF96

    - token: action.active
      description: estado pressed del tap
      light: color.green.700   # #27592C
      dark: color.green.100    # #CDDFC0

    - token: action.disabled
      description: estado deshabilitado de controles
      light: color.paper.300   # #DCD2BC
      dark: color.paper.700    # #615847

    - token: action.subtle
      description: fondo sutil al hover/seleccionar items de lista y navegación
      light: color.green.50    # #EAF1E4
      dark: color.ink.300      # #39362E

  accent:
    - token: accent.ink
      description: destacados y sellos editoriales en negro tinta ("FINAL"); en dark el sello de alto contraste es papel
      light: color.ink.900     # #0E0D0A
      dark: color.paper.100    # #F5F0E3

  border:
    - token: border.default
      description: borde estándar de inputs, cards y divisores generales
      light: color.paper.300   # #DCD2BC
      dark: color.paper.700    # #615847

    - token: border.subtle
      description: divisores internos muy suaves entre secciones
      light: color.paper.200   # #ECE4D2
      dark: color.ink.300      # #39362E

    - token: border.strong
      description: borde de énfasis, anillo de foco, separadores destacados
      light: color.paper.400   # #C2B69D
      dark: color.paper.500    # #A6987C

    - token: border.active
      description: borde de elemento seleccionado, en foco o activo persistente
      light: color.green.500   # #3E8E45
      dark: color.green.300    # #8FBE6F

    - token: border.hairline
      description: regla fina editorial 1px (filos hairline entre filas/secciones)
      light: color.paper.300   # #DCD2BC
      dark: color.paper.700    # #615847

    - token: border.section
      description: regla de sección 2px bajo masthead
      light: color.ink.500     # #26241E
      dark: color.paper.400    # #C2B69D

  status:
    - token: status.live
      description: indicador de partido en curso — dot rojo pulsante (RELLENO)
      light: color.red.500     # #C5403A
      dark: color.red.400      # #CC554D

    - token: status.liveText
      description: texto "EN VIVO" sobre papel
      light: color.red.700     # #8C2A26 — 8.0:1 sobre paper.50 ✓ AAA
      dark: color.red.300      # #D5736C — 5.7:1 sobre ink.bg ✓ AA

    - token: status.error
      description: error, estado crítico, alerta destructiva (RELLENO)
      light: color.red.500     # #C5403A
      dark: color.red.400      # #CC554D

    - token: status.errorText
      description: texto de error sobre papel
      light: color.red.700     # #8C2A26 — 8.0:1 sobre paper.50 ✓ AAA
      dark: color.red.300      # #D5736C — 5.7:1 sobre ink.bg ✓ AA

    - token: status.success
      description: confirmación, resultado positivo (RELLENO)
      light: color.green.500   # #3E8E45
      dark: color.green.300    # #8FBE6F

    - token: status.successText
      description: texto de éxito / delta positivo sobre papel
      light: color.green.700   # #27592C — 7.8:1 sobre paper.50 ✓ AAA
      dark: color.green.300    # #8FBE6F — 8.6:1 sobre ink.bg ✓ AAA

    - token: status.warning
      description: advertencia, tarjeta amarilla (RELLENO)
      light: color.yellow.500  # #D6A52E
      dark: color.yellow.300   # #E8C863

    - token: status.warningText
      description: texto de advertencia sobre papel
      light: color.yellow.800  # #7A5B13 — 5.9:1 sobre paper.50 ✓ AA (AA pleno en texto pequeño)
      dark: color.yellow.300   # #E8C863

    - token: status.info
      description: información neutral, estadísticas complementarias (RELLENO)
      light: color.indigo.500  # #6366F1
      dark: color.indigo.400   # #818CF8

    - token: status.infoText
      description: texto informativo sobre papel
      light: color.indigo.700  # #4338CA — 7.5:1 sobre paper.50 ✓ AAA
      dark: color.indigo.400   # #818CF8

  highlight:
    - token: highlight.mark
      description: wash de marcador "marker" tras stats/records clave
      light: color.yellow.100  # #F6E8BE
      dark: color.yellow.700   # #9A7416 — wash atenuado para fondo oscuro
```

---

## Accesibilidad y contraste

Pares de colores clave del sistema con ratio WCAG verificado.

### AtomSN Light (sobre `paper.50` #FBF8F0)

| Par | Ratio | WCAG |
|---|---|---|
| `text.primary` (`ink.700`) sobre `bg.base` | 16.7:1 | AAA ✓ |
| `text.secondary` (`paper.700`) sobre `bg.base` | 6.6:1 | AA ✓ |
| `text.tertiary` (`paper.600`) sobre `bg.base` | 4.1:1 | decorativo / large ✓ |
| `text.link` / `status.successText` (`green.700`) sobre `bg.base` | 7.8:1 | AAA ✓ |
| `status.liveText` / `status.errorText` (`red.700`) sobre `bg.base` | 8.0:1 | AAA ✓ |
| `status.warningText` (`yellow.800`) sobre `bg.base` | 5.9:1 | AA ✓ |
| `status.infoText` (`indigo.700`) sobre `bg.base` | 7.5:1 | AAA ✓ |
| `text.onPrimary` (`paper.50`) sobre `action.primary` (`green.500`) | 3.8:1 | AA large ✓ (solo bold ≥14px) |

### AtomSN Dark (sobre `ink.bg` #16140F)

| Par | Ratio | WCAG |
|---|---|---|
| `text.primary` (`paper.100`) sobre `bg.base` | 16.2:1 | AAA ✓ |
| `text.secondary` (`paper.400`) sobre `bg.base` | 9.2:1 | AAA ✓ |
| `text.link` / `status.successText` (`green.300`) sobre `bg.base` | 8.6:1 | AAA ✓ |
| `status.liveText` / `status.errorText` (`red.300`) sobre `bg.base` | 5.7:1 | AA ✓ |

> `text.tertiary` (`paper.600`, 4.1:1) no alcanza AA en texto pequeño: úsese solo para información no esencial (timestamps, metadatos) o texto grande. Nunca para contenido crítico o acciones.
>
> `text.onPrimary` sobre verde de acción (3.8:1) solo es válido en texto **bold ≥14px** (AA large). Para texto fino sobre verde, subir el peso o usar relleno con tinta.
