# Utillaje editorial — Tema AtomSN

> **Versión:** 2.0 · **Plataforma:** Flutter (mobile-first + web) · **Temas:** light "AtomSN Light" / dark "AtomSN Dark"

## Dirección visual

Este capítulo no existe en el sistema anterior. Documenta el **utillaje de periódico** (editorial devices) que AtomSN añade sobre la base de colores, tipografía y espaciado: las piezas concretas que hacen que una pantalla de resultados se lea como una página de prensa deportiva y no como una UI neutra.

Todo el utillaje resuelve sobre tokens existentes en `tokens.json`. No introduce tokens nuevos: combina reglas (`border.*`), tinta (`color.ink.*`), papel (`color.paper.*`), tipografía duotono (serif `text.masthead`/`text.headline` + sans `text.*`) y los semánticos editoriales (`accent.ink`, `highlight.mark`, `status.live`, `text.overline`, `spacing.column.gap`, `spacing.overline.gap`).

Principios transversales:

- El periódico ordena con **reglas**, no con sombras ni cajas. Lo que separa bloques es un filo, no una superficie elevada.
- Las cifras de competición (marcadores, minutos, stats, columnas de tabla) son **tabulares** siempre. La rejilla no debe bailar.
- La serif (`Libre Caslon Display`, w400) es exclusiva de masthead/headline a tamaño grande (≥20px). Kickers, labels, stats y cuerpo son sans (`ElmsSans`).
- El acento verde sigue siendo escaso; el utillaje editorial es mayormente **tinta sobre papel** (`ink.*` / `paper.*`), más rojo `status.live` y wash amarillo `highlight.mark` puntuales.
- Esquinas rectas: reglas, sellos y tablas usan `radius.none`.

---

## 1. Reglas / filos hairline

**Nombre:** regla hairline / regla de sección.
**Propósito:** separar filas, ítems y bloques editoriales con un filo de tinta en lugar de una caja o una sombra. Es la herramienta de maquetación primaria del periódico.

**Tokens implicados:**

| Elemento | Grosor | Color (light → dark) | Radio |
|---|---|---|---|
| Filo hairline | `border.hairline` (1px) | `border.hairline` = `paper.300` → `paper.700` | `radius.none` |
| Regla de sección | `border.section` (2px) | `border.section` = `ink.500` → `paper.400` | `radius.none` |

**Guía de uso en una app de fútbol:**

- **Hairline (1px):** separador entre filas de una tabla de clasificación, entre partidos de una jornada, entre líneas de un acta (goles, tarjetas, cambios), borde inferior de un header de lista. El aire alrededor lo da `space.*` (ver spacing.md), nunca el grosor.
- **Sección (2px):** bajo el masthead/nameplate de pantalla o de sección ("CLASIFICACIÓN", "JORNADA 12"), y para separar bloques editoriales mayores (p. ej. "PARTIDOS DE HOY" de "RESULTADOS DE AYER"). Siempre con `space.4` de aire por encima/debajo.
- No inventar grosores intermedios: solo `border.hairline` y `border.section`.
- En dark, el filo no desaparece: `paper.700` sobre `ink.bg` mantiene la separación; la regla de sección sube a `paper.400` para conservar presencia.

Ejemplo Flutter en el bloque de pseudocódigo de la sección final.

---

## 2. Masthead

**Nombre:** masthead / nameplate (cabecera de sección como mini-masthead).
**Propósito:** dar a cada pantalla o sección la cabecera de un periódico: un bloque serif de alto contraste, una regla de sección debajo y una línea de fecha/jornada que sitúa el contenido en el tiempo de la competición.

**Tokens implicados:**

- Bloque de título: `text.masthead.xl` (serif 6xl/48px, nameplate de pantalla) o `text.masthead.lg` (serif 4xl/32px). Color `text.primary` (`ink.700` light / `paper.100` dark) o `accent.ink` para máximo contraste.
- Regla bajo el masthead: `border.section` (2px) con color `border.section`.
- Línea de fecha/jornada: `text.overline` (kicker mayúsculas) o `text.caption`, color `text.secondary` / `text.tertiary`.
- Aire: `space.4` entre título y regla, `space.4`–`space.6` bajo la regla antes del contenido.

**Guía de uso en una app de fútbol:**

- **Masthead de pantalla:** la home de la competición o la cabecera de "Liga Local 2026" usa `text.masthead.xl`. Una sola por pantalla; es el nameplate.
- **Mini-masthead de sección:** cabeceras de pantalla secundaria ("CLASIFICACIÓN", "GOLEADORES", "CALENDARIO") usan `text.masthead.lg` + regla de sección + overline de contexto.
- **Línea de fecha/jornada:** justo bajo o sobre el masthead, en `text.overline`: "JORNADA 12 · 17 JUN 2026". Es lo que convierte la cabecera en portada de periódico.
- La serif nunca baja de 20px ni se usa en cuerpo: el masthead es su territorio. Subtítulos, descripciones y metadatos de la cabecera van en sans (`text.body.*`, `text.caption`, `text.overline`).

---

## 3. Kickers / overlines

**Nombre:** kicker (overline editorial en mayúsculas).
**Propósito:** etiquetar un titular o bloque con una línea corta en mayúsculas espaciadas, al estilo del antetítulo de prensa. Clasifica el contenido antes de leerlo.

**Tokens implicados:**

- Composición: `text.overline` — sans, 12px (`size.sm`), semibold, `lineHeight.tight`, `tracking.kicker` (0.08em), `transform: uppercase`.
- Color: `text.secondary` / `text.tertiary` para contexto neutro; `status.liveText` para "EN VIVO"; `accent.ink` para destacarlo como sello textual.
- Separación con el titular: `spacing.overline.gap` (= `space.1`, 4px). El overline se pega a su titular para leerse como una unidad.

**Guía de uso en una app de fútbol:**

- Etiquetas de agrupación: `"GRUPO A"`, `"GRUPO B"` sobre una tabla de clasificación.
- Estado temporal: `"EN VIVO"` (color `status.liveText`), `"FINALIZADO"`, `"DESCANSO"`.
- Contexto de calendario: `"JORNADA 12"`, `"CUARTOS DE FINAL"`, `"HOY"`.
- Siempre en mayúsculas con `tracking.kicker`; el espaciado de letras es lo que da el aire de antetítulo. No usar la serif aquí: el kicker es sans.
- Un kicker encabeza; no se usa como cuerpo ni como dato. Para datos numéricos usar `text.stat.*` (ver sección 5).

---

## 4. Líderes punteados en tablas de clasificación

**Nombre:** dotted leaders (líderes punteados).
**Propósito:** conectar el nombre de un equipo con su valor (puntos) mediante una línea de puntos que recorre el espacio sobrante, como un sumario o una ficha de prensa impresa. Guía el ojo a través de la fila sin necesidad de bordes verticales.

**Tokens implicados:**

- Relleno punteado: dotted en color `paper.400` (`border.strong` light), el token marcado en `tokens.json` como "líderes punteados".
- Nombre de equipo: `text.body.md` o `text.label.lg`, color `text.primary`.
- Valor (puntos): `text.stat.md` o `text.title.lg` con **cifras tabulares** (ver sección 5), color `text.primary` o `accent.ink`.
- Fila sobre rejilla recta: `radius.none`, separada de la siguiente por `border.hairline`.
- Gutter entre columnas de la tabla (PJ, G, E, P, GF, GC, Pts): `spacing.column.gap` (16px).

**Ejemplo de fila (clasificación):**

```text
1   ATLÉTICO LOCAL ······························  34
2   DEPORTIVO RÍO ······························   31
3   UNIÓN VALLE ································   29
```

El nombre se ancla a la izquierda, los puntos a la derecha, y el relleno dotted `paper.400` ocupa el medianil variable entre ambos. El número de posición y los puntos son tabulares para que las columnas no bailen entre filas.

Pseudocódigo Flutter en la sección final.

---

## 5. Cifras tabulares

**Nombre:** tabular figures (cifras tabulares).
**Propósito:** que todos los dígitos ocupen el mismo ancho, de modo que marcadores, minutos, stats y columnas de tabla queden perfectamente alineados en vertical y no "salten" al actualizarse en vivo.

**Tokens implicados:**

- Composiciones con `tabular: true` en `tokens.json`: `text.display.score` (marcador principal, sans extrabold 60px), `text.display.stat` (40px), `text.stat.lg` (24px), `text.stat.md` (18px).
- En Flutter se activa con `fontFeatures: [FontFeature.tabularFigures()]` sobre la familia sans `ElmsSans`.

**Guía de uso en una app de fútbol — obligatorio en:**

- **Marcadores:** `2 - 1` en la cabecera de partido (`text.display.score`).
- **Minutos / cronómetro:** `45'+2`, `90:00` (`text.stat.md`).
- **Stats:** posesión, tiros, faltas, goleadores (`text.stat.lg` / `text.display.stat`).
- **Columnas de tabla:** PJ, G, E, P, GF, GC, DG, Pts de la clasificación; cualquier columna numérica.
- La serif no lleva cifras tabulares: los números de competición son siempre sans. La serif solo titula.

---

## 6. Gutters de columna

**Nombre:** column gutter (medianil de columna).
**Propósito:** un único medianil fijo entre columnas, como el espacio entre columnas de un periódico. Aplica a tablas, grids de partidos y maquetación web a 2+ columnas.

**Tokens implicados:**

- `spacing.column.gap` = `space.4` (16px). Único y fijo (ver spacing.md).

**Guía de uso en una app de fútbol:**

- Separación entre las columnas de stats de una tabla de clasificación (PJ … Pts).
- Separación entre tarjetas de partido en un grid (vista web / tablet).
- En web a dos columnas (p. ej. clasificación + últimos resultados), el gutter entre columnas mayores es `spacing.column.gap`.
- No usar gutters variables ni arbitrarios: un solo medianil mantiene el ritmo de página.

---

## 7. Chip "LIVE"

**Nombre:** live chip (indicador en directo).
**Propósito:** señalar un partido en directo con un dot de tinta roja + un overline en mayúsculas, sin badge brillante ni glossy. Editorial, no de videojuego.

**Tokens implicados:**

- Dot: relleno `status.live` (`red.500` light / `red.400` dark), forma circular `radius.full`.
- Texto: `text.overline` en color `status.liveText` (`red.700` light / `red.300` dark) — el valor de TEXTO sobre papel que cumple AA, no el de relleno.
- Separación dot ↔ texto: `spacing.inline.xs` (4px) o `spacing.inline.sm` (8px).

**Guía de uso en una app de fútbol:**

- Composición: `● EN VIVO` o `● EN VIVO · 67'`, el minuto en `text.stat.md` tabular.
- El dot puede pulsar (animación de opacidad), pero el chip no lleva fondo de color saturado, ni borde redondeado tipo pill relleno, ni gradiente. El énfasis lo da el rojo del dot + el overline, sobre papel.
- Regla de color: el dot usa `status.live` (relleno), el texto usa `status.liveText` (texto AA). No pintar el texto con `red.500`.

---

## 8. Highlight "marker"

**Nombre:** marker highlight (subrayado de marcador editorial).
**Propósito:** resaltar un dato clave con un wash amarillo suave por detrás, como pasar un marcador (highlighter) sobre un recorte de periódico. Para records, líderes y stats destacados.

**Tokens implicados:**

- Wash de fondo: `highlight.mark` (`yellow.100` light / `yellow.700` dark, atenuado para fondo oscuro).
- Texto encima: mantiene su token normal (`text.primary` / `accent.ink`); el wash no debe reducir el contraste por debajo de AA.
- Forma: bloque tras el texto; esquinas rectas o `radius.xs` como mucho — es un trazo de marcador, no una pill.

**Guía de uso en una app de fútbol:**

- Detrás del máximo goleador de la tabla, del récord de imbatibilidad, de la racha de victorias, del "Pichichi" de la jornada.
- Tras una stat destacada en la ficha de partido (p. ej. el jugador con más pases completados).
- Escaso: si todo está marcado, nada está marcado. Uno o dos por pantalla.
- En dark, `highlight.mark` resuelve a `yellow.700` (wash atenuado) para no quemar sobre `ink.bg`; verificar que el texto encima siga en AA.
- No confundir con la tarjeta amarilla: la tarjeta usa `status.warning` (`yellow.500` relleno) / `status.warningText`. El marker es `yellow.100`, función highlight.

---

## 9. Sellos de tinta

**Nombre:** ink stamp (sello de tinta).
**Propósito:** estampar un estado definitivo con un bloque sólido de tinta y texto invertido, como el sello "FINAL" o "PAGADO" de un periódico/documento impreso. Máximo contraste, esquinas rectas.

**Tokens implicados:**

- Relleno del sello: `accent.ink` (`ink.900` light / `paper.100` dark — en dark el sello de alto contraste es papel).
- Texto sobre el sello: invertido — `text.inverse` (`paper.50` light / `ink.900` dark), en `text.overline` (mayúsculas, tracking kicker).
- Forma: `radius.none` (bloque recto), padding `spacing.button.padding.sm` (12×8).

**Guía de uso en una app de fútbol:**

- `"FINAL"` sobre un partido terminado, `"HOY"` sobre la jornada del día, `"APLAZADO"`, `"DESCANSO"`.
- El sello es un bloque recto sólido; no redondear, no añadir sombra ni gradiente. Su fuerza es la tinta plena + la inversión de texto.
- Uno por elemento: el sello marca el estado dominante de la tarjeta de partido, no se acumula con otros sellos.
- Diferencia con el chip LIVE (sección 7): LIVE es dot + overline sin fondo (estado en curso); el sello es bloque relleno (estado cerrado/definitivo).

---

## 10. Textura / halftone (OPCIONAL — off por defecto)

**Nombre:** textura editorial / halftone (opcional).
**Propósito:** insinuar la trama de impresión del papel de periódico con un grano o semitono muy tenue sobre el fondo. Es un acabado, no un componente.

**Estado:** **opcional y desactivado por defecto.** No forma parte del render base y no debe activarse si compromete el contraste.

**Tokens implicados:**

- No hay token de textura en `tokens.json`: es un overlay de acabado, no una decisión cromática del sistema.
- Si se aplica, el overlay debe construirse con la familia de papel/tinta del modo activo (p. ej. mota de `paper.300`/`ink.500`) a **≤3–4% de opacidad**, nunca con un color ajeno a la paleta.

**Guía de uso en una app de fútbol:**

- Como mucho, un grano sutil en fondos amplios de cabecera o en empty states; jamás sobre tablas, marcadores ni texto de cuerpo.
- Restricción dura: la textura **nunca** va a costa del contraste. Si reduce la legibilidad de texto/cifras por debajo de AA, no se usa.
- Off por defecto: debe ser una preferencia explícita, no el estado base del tema. La legibilidad de resultados manda sobre el efecto.

---

## Ejemplos en pseudocódigo Flutter

> Los colores se toman del theme activo (light "AtomSN Light" / dark "AtomSN Dark") resolviendo el token semántico correspondiente; aquí se anotan como comentario.

### Regla hairline entre filas

```dart
// border.hairline (1px) · color border.hairline (paper.300 light / paper.700 dark)
// Recta (radius.none implícito en Divider) y sin sombra.
final Divider hairline = Divider(
  height: 1,
  thickness: 1, // border.hairline
  color: theme.borderHairline, // paper.300 light / paper.700 dark
);

// Regla de sección bajo un masthead: border.section (2px) + space.4 de aire.
final Container sectionRule = Container(
  margin: const EdgeInsets.symmetric(vertical: 16), // space.4 de aire
  height: 2, // border.section
  color: theme.borderSection, // ink.500 light / paper.400 dark
);
```

### Fila de clasificación con líder punteado y cifras tabulares

```dart
// Tabla recta (radius.none), filas separadas por hairline, puntos tabulares,
// relleno dotted en paper.400 entre nombre y puntos.
Widget standingsRow({
  required int position,
  required String team,
  required int points,
}) {
  const tabular = TextStyle(
    fontFamily: 'ElmsSans',
    fontFeatures: [FontFeature.tabularFigures()], // cifras tabulares obligatorias
  );

  return Padding(
    padding: const EdgeInsets.symmetric(horizontal: 16, vertical: 12), // spacing.card.padding.sm-ish
    child: Row(
      children: [
        // Posición — tabular, text.stat.md
        Text('$position', style: tabular.copyWith(/* text.stat.md, text.primary */)),
        const SizedBox(width: 16), // spacing.column.gap
        // Nombre del equipo — text.label.lg / text.body.md, ink.700
        Text(team.toUpperCase(), style: const TextStyle(/* text.label.lg, text.primary */)),
        // Líder punteado: relleno dotted paper.400 que ocupa el medianil variable
        Expanded(
          child: Padding(
            padding: const EdgeInsets.symmetric(horizontal: 8),
            child: DottedLeader(color: theme.paper400), // dotted, paper.400 (border.strong)
          ),
        ),
        // Puntos — tabular, text.stat.md / accent.ink
        Text('$points', style: tabular.copyWith(/* text.stat.md, accent.ink */)),
      ],
    ),
  );
}

// DottedLeader: línea de puntos repetidos (CustomPaint o fila de '·').
// El color sale de paper.400; el grosor del punto es hairline.
```

### Chip LIVE (dot + overline, sin glossy)

```dart
// Dot status.live (red.500) + text.overline en status.liveText (red.700, AA).
Widget liveChip(String minute) => Row(
  mainAxisSize: MainAxisSize.min,
  children: [
    Container(
      width: 8, height: 8,
      decoration: BoxDecoration(
        color: theme.statusLive, // red.500 light / red.400 dark (RELLENO)
        shape: BoxShape.circle,  // radius.full
      ),
    ),
    const SizedBox(width: 4), // spacing.inline.xs
    Text('EN VIVO · $minute', style: const TextStyle(
      /* text.overline: sans 12px semibold, tracking.kicker, uppercase */
      /* color: status.liveText (red.700 light / red.300 dark) — TEXTO AA */
    )),
  ],
);
```

### Sello de tinta "FINAL"

```dart
// Bloque relleno accent.ink (ink.900), texto invertido, radius.none.
Widget inkStamp(String label) => Container(
  padding: const EdgeInsets.symmetric(horizontal: 12, vertical: 8), // spacing.button.padding.sm
  decoration: BoxDecoration(
    color: theme.accentInk,      // ink.900 light / paper.100 dark
    borderRadius: BorderRadius.zero, // radius.none
  ),
  child: Text(label.toUpperCase(), style: const TextStyle(
    /* text.overline: sans semibold, tracking.kicker, uppercase */
    /* color: text.inverse (paper.50 light / ink.900 dark) */
  )),
);
// inkStamp('FINAL') · inkStamp('HOY')
```

---

## Resumen del utillaje

| # | Device | Tokens clave | Radio |
|---|---|---|---|
| 1 | Reglas hairline / sección | `border.hairline` (paper.300), `border.section` (ink.500) | `radius.none` |
| 2 | Masthead | `text.masthead.*` (serif), `border.section`, `text.overline` | `radius.none` (regla) |
| 3 | Kicker / overline | `text.overline`, `tracking.kicker`, `spacing.overline.gap` | — |
| 4 | Líderes punteados | dotted `paper.400`, `text.stat.*` tabular, `spacing.column.gap` | `radius.none` |
| 5 | Cifras tabulares | `text.display.score/stat`, `text.stat.lg/md` (`tabular: true`) | — |
| 6 | Gutter de columna | `spacing.column.gap` (space.4) | — |
| 7 | Chip LIVE | `status.live` (dot) + `status.liveText` (texto) + `text.overline` | `radius.full` (dot) |
| 8 | Highlight marker | `highlight.mark` (yellow.100 / yellow.700 dark) | `radius.none`/`xs` |
| 9 | Sello de tinta | `accent.ink` (ink.900) + `text.inverse` + `text.overline` | `radius.none` |
| 10 | Textura halftone (opcional) | sin token; overlay ≤3–4% con paper/ink del modo | — |
```
