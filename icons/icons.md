# Sistema de Iconos — UScoreNow AtomSN

> **Versión:** 2.0 · **Tema:** AtomSN · **Plataforma:** Flutter (mobile-first + web) · **Librería:** Hugeicons

## Dirección visual

Sistema iconográfico editorial para una app de gestión de torneos de fútbol construida en Flutter con Hugeicons.

La iconografía debe sentirse ligera, clara y estructural, como el utillaje gráfico de un periódico deportivo: trazo de tinta fino sobre papel, sin relleno ni dramatismo. Los iconos acompañan navegación, acciones y estados del producto, pero nunca compiten con el contenido principal (titulares serif, marcadores tabulares, reglas hairline). En el lenguaje editorial de AtomSN el peso visual lo cargan la tipografía y las reglas; el icono es notación, no ilustración.

---

## Principios

- Toda la app debe usar Hugeicons como librería única de iconos.
- El estilo principal debe ser `strokeRounded`.
- Los iconos deben heredar color desde el sistema de tema de Flutter (tokens `semantic.*`) siempre que sea posible.
- El tamaño del icono debe depender del contexto de uso, no del gusto de cada pantalla.
- El grosor de trazo debe mantenerse estable en toda la app.
- Cada semántica importante del producto debe mapear a un único icono principal.
- Los iconos decorativos deben ser excepcionales; la mayoría deben tener función de navegación, acción, estado o representación de entidad.
- El icono nunca lleva color de acento por decoración: el verde (`action.primary`) marca interacción/activo y es escaso; los colores de estado (red/yellow/indigo) solo aparecen sobre iconos de estado real.

---

## Restricción principal de estilo

- Estilo único: `strokeRounded` — es el único estilo disponible y permitido en el sistema
- No mezclar `strokeRounded` con `sharp`, `standard`, `bulk`, `duotone` ni ningún otro estilo
- No usar varios estilos visuales para una misma semántica
- La diferenciación de estados (activo, seleccionado) se logra exclusivamente mediante color y opacidad, nunca mediante cambio de estilo
- El trazo `strokeRounded` (esquinas suaves) convive con los radios contenidos del tema; las reglas, sellos y tablas usan `radius.none`, pero eso afecta a contenedores, no al dibujo interno del icono

---

## Convención de nombres

```text
icon.{dominio}.{nombre}
```

Ejemplos:
- `icon.navigation.home`
- `icon.navigation.matches`
- `icon.navigation.standings`
- `icon.action.search`
- `icon.action.filter`
- `icon.status.live`
- `icon.status.warning`
- `icon.entity.team`
- `icon.entity.player`

---

## Fundamentos técnicos

```yaml
icon_foundation:
  library: "hugeicons"            # ^1.1.7
  flutter_package: "package:hugeicons/hugeicons.dart"
  primary_style: "strokeRounded"  # constantes HugeIcons.strokeRounded<Nombre>
  base_widget: "HugeIcon"
  token_map: "lib/theme/app_icons.dart"  # AppIcons: mapa canonico (semantica -> icono)
```

> **Fuente canónica del mapeo:** `lib/theme/app_icons.dart` (`AppIcons.*`). Los
> componentes referencian `AppIcons.navigationHome`, etc., nunca `HugeIcons.*` directo.
> Algunos identificadores reales de hugeicons 1.1.7 difieren de este catálogo (escrito con
> la convención antigua `HugeIconsStrokeRounded.home01`): p.ej. `trophy01`→`Champion`,
> `radioButton01`→`RadioButton`, `stadium`→`FootballPitch`, `user01`→`UserCircle`,
> `lock01`→`Lock`, `inbox01`→`Inbox`. `AppIcons` ya usa los nombres válidos.

---

## Roles semánticos

```yaml
semantic_roles:
  navigation:
    description: iconos para bottom navigation, tabs, app bar secundaria y cambio de vistas
    examples:
      - home
      - calendar
      - trophy
      - chart
      - user

  actions:
    description: iconos para acciones directas del usuario
    examples:
      - search
      - filter
      - notification
      - share
      - bookmark
      - edit

  status:
    description: iconos para estados de sistema y estados de partido
    examples:
      - live
      - time
      - check
      - alert
      - lock

  entities:
    description: iconos para representar objetos del dominio fútbol
    examples:
      - team
      - player
      - match
      - stadium
      - standings

  feedback:
    description: iconos para empty states, confirmaciones y mensajes informativos
    examples:
      - info
      - success
      - warning
      - error
```

---

## Catálogo de iconos aprobados

Inventario oficial del sistema. Antes de usar un icono, verificar que esté aquí o añadirlo siguiendo la lista de decisión.

> Los identificadores de Hugeicons deben verificarse contra el catálogo oficial en [hugeicons.com](https://hugeicons.com) antes de implementar.

```yaml
approved_icons:

  navigation:
    - semantic: icon.navigation.home
      stroke: HugeIconsStrokeRounded.home01

    - semantic: icon.navigation.matches
      stroke: HugeIconsStrokeRounded.calendar03

    - semantic: icon.navigation.standings
      stroke: HugeIconsStrokeRounded.chartLineData02

    - semantic: icon.navigation.competitions
      stroke: HugeIconsStrokeRounded.trophy01

    - semantic: icon.navigation.profile
      stroke: HugeIconsStrokeRounded.user01

  actions:
    - semantic: icon.action.search
      stroke: HugeIconsStrokeRounded.search01

    - semantic: icon.action.filter
      stroke: HugeIconsStrokeRounded.filterHorizontal

    - semantic: icon.action.notification
      stroke: HugeIconsStrokeRounded.notification03

    - semantic: icon.action.bookmark
      stroke: HugeIconsStrokeRounded.bookmark01

    - semantic: icon.action.share
      stroke: HugeIconsStrokeRounded.share01

    - semantic: icon.action.more
      stroke: HugeIconsStrokeRounded.moreVertical

    - semantic: icon.action.back
      stroke: HugeIconsStrokeRounded.arrowLeft01

    - semantic: icon.action.close
      stroke: HugeIconsStrokeRounded.cancel01

  status:
    - semantic: icon.status.live
      stroke: HugeIconsStrokeRounded.radioButton01
      note: >
        usar semantic.status.live (red.500 light / red.400 dark) como dot pulsante,
        acompañado del overline "EN VIVO" (text.overline). Ver nota editorial.

    - semantic: icon.status.time
      stroke: HugeIconsStrokeRounded.clock01

    - semantic: icon.status.check
      stroke: HugeIconsStrokeRounded.checkmarkCircle01

    - semantic: icon.status.alert
      stroke: HugeIconsStrokeRounded.alert02

    - semantic: icon.status.info
      stroke: HugeIconsStrokeRounded.informationCircle

    - semantic: icon.status.lock
      stroke: HugeIconsStrokeRounded.lock01

  entities:
    - semantic: icon.entity.team
      stroke: HugeIconsStrokeRounded.userGroup

    - semantic: icon.entity.player
      stroke: HugeIconsStrokeRounded.userStar01

    - semantic: icon.entity.stadium
      stroke: HugeIconsStrokeRounded.stadium

    - semantic: icon.entity.ball
      stroke: HugeIconsStrokeRounded.football

    - semantic: icon.entity.competition
      stroke: HugeIconsStrokeRounded.trophy01

  feedback:
    - semantic: icon.feedback.success
      stroke: HugeIconsStrokeRounded.checkmarkCircle02
      color: semantic.status.success

    - semantic: icon.feedback.warning
      stroke: HugeIconsStrokeRounded.alert02
      color: semantic.status.warning

    - semantic: icon.feedback.error
      stroke: HugeIconsStrokeRounded.cancelCircle
      color: semantic.status.error

    - semantic: icon.feedback.info
      stroke: HugeIconsStrokeRounded.informationCircle
      color: semantic.status.info

    - semantic: icon.feedback.empty
      stroke: HugeIconsStrokeRounded.inbox01
```

---

## Tamaños

```yaml
icon_sizes:
  xs:
    value: 16.0
    usage: metadata, chips, texto auxiliar, tablas densas (clasificación)

  sm:
    value: 20.0
    usage: trailing icons, inputs, botones compactos

  md:
    value: 24.0
    usage: tamaño base del sistema; navegación, acciones y uso general

  lg:
    value: 28.0
    usage: app bars internas, acciones destacadas, estados vacíos compactos

  xl:
    value: 32.0
    usage: onboarding, empty states, paneles destacados
```

---

## Grosor de trazo

El trazo fino es deliberado: sobre papel (`bg.base` = paper.50) el icono debe leerse como tinta, no como mancha. Preferir `1.5` como regla general; subir a `1.75` solo donde la densidad o el contraste lo exija (tablas de clasificación, líderes punteados).

```yaml
stroke_rules:
  default:
    strokeWidth: 1.5
    usage: regla general de producto; trazo de tinta fino sobre papel

  compact:
    strokeWidth: 1.75
    usage: >
      iconos pequeños (xs, sm), tablas densas de clasificación, o sobre
      superficies de contraste más difícil (raised, marker yellow.100)

  emphatic:
    strokeWidth: 2.0
    usage: accesibilidad o énfasis excepcional
```

---

## Color y tematización

Los iconos deben heredar color desde el tema siempre que sea posible. Solo usar color explícito para estados semánticos intencionados. Todos los valores se resuelven desde la capa `semantic.{light|dark}` de `tokens.json`; nunca usar hex literal.

El color por defecto del icono es la tinta sobre papel: `text.primary` resuelve a `ink.700` (#1A1814) en light y a `paper.100` (#F5F0E3) en dark. El estado interactivo lo marca el verde escaso de `action.primary`. Los colores de estado siguen la regla relleno-vs-texto del sistema: en iconos `strokeRounded` el trazo actúa como relleno/icono, por lo que se usan las variantes `*.500` (light) / `*.300`–`*.400` (dark) de `semantic.status.*`, no las variantes `*Text`.

```yaml
icon_color_behavior:
  default:
    source: "Theme.of(context).colorScheme.onSurface"
    semantic_token: semantic.text.primary
    resolves: { light: color.ink.700, dark: color.paper.100 }

  muted:
    source: "Theme.of(context).colorScheme.onSurfaceVariant"
    semantic_token: semantic.text.secondary
    resolves: { light: color.paper.700, dark: color.paper.400 }

  active:
    source: "Theme.of(context).colorScheme.primary"
    semantic_token: semantic.action.primary
    resolves: { light: color.green.500, dark: color.green.300 }
    note: acento verde escaso; solo interacción o estado activo

  selected:
    source: "Theme.of(context).colorScheme.primary"
    semantic_token: semantic.action.primary
    resolves: { light: color.green.500, dark: color.green.300 }

  live:
    source: "semantic.status.live"
    resolves: { light: color.red.500, dark: color.red.400 }
    note: dot pulsante junto al overline "EN VIVO"; ver nota editorial

  success:
    source: "semantic.status.success"
    resolves: { light: color.green.500, dark: color.green.300 }
    note: usar valor resuelto del token según tema activo

  warning:
    source: "semantic.status.warning"
    resolves: { light: color.yellow.500, dark: color.yellow.300 }
    note: doble función del amarillo (tarjeta/advertencia); usar valor resuelto del token

  danger:
    source: "semantic.status.error"
    resolves: { light: color.red.500, dark: color.red.400 }
    note: usar valor resuelto del token según tema activo

  info:
    source: "semantic.status.info"
    resolves: { light: color.indigo.500, dark: color.indigo.400 }
    note: indigo escaso, solo información neutral

  disabled:
    source: "Theme.of(context).disabledColor"
    semantic_token: semantic.text.disabled
    resolves: { light: color.paper.400, dark: color.paper.700 }
    opacity: 0.6
```

> Nota relleno-vs-texto: cuando un estado se comunica como **texto** adyacente (overline, label), ese texto sí usa las variantes AA `*Text` (`status.liveText` = red.700 light / red.300 dark, etc.). El icono usa la variante de relleno; el texto, la de lectura.

### Nota editorial — el icono "live"

`icon.status.live` (`radioButton01`) se trata como un **sello de directo**, no como un icono más:

- Color: `semantic.status.live` — `red.500` (#C5403A) en light, `red.400` (#CC554D) en dark. El rojo es ladrillo cálido de tinta, coherente con el papel.
- Forma: dot pulsante (animación de pulso/opacidad). Tamaño `xs` (16) cuando precede a un overline; `sm` (20) en cabeceras de partido.
- Acompañamiento obligatorio: overline "EN VIVO" en `text.overline` (ElmsSans, mayúsculas, `tracking.kicker` 0.08em). El estado en vivo nunca se comunica solo con el dot; el kicker editorial lo verbaliza.
- Trazo: `1.5` por defecto. En tablas/listas densas de partidos en curso, `1.75` para no perder el punto a tamaño `xs`.
- Maridaje: el dot rojo + overline rojo (`status.liveText` = red.700 light / red.300 dark) forman la unidad "kicker en vivo" sobre papel; no añadir relleno ni badge, basta la regla hairline si necesita separarse del marcador tabular contiguo.

---

## Reglas de uso

- En `BottomNavigationBar`, `NavigationBar` o tabs, usar tamaño `md` como base.
- En `IconButton`, usar `sm` o `md` según densidad visual.
- En listas, cards y tablas, todos los iconos del mismo nivel jerárquico deben compartir tamaño.
- En tablas de clasificación (densas, con líderes punteados), usar `xs` con trazo `1.75`.
- No usar color fijo salvo en estados semánticos intencionados; priorizar color heredado del tema.
- El verde (`action.primary`) es escaso: reservarlo a interacción y estado activo/seleccionado, nunca a decoración ni a iconos de entidad neutra.
- No introducir un nuevo icono si ya existe otro aprobado para la misma semántica.
- No usar más de un icono para expresar la misma acción en distintas pantallas.

---

## Reglas de estado

```yaml
interactive_states:
  default:
    style: strokeRounded
    color: semantic.text.secondary
    description: estado neutro del icono, sin interacción

  hover:
    style: strokeRounded
    color: semantic.text.primary
    description: aplica en Flutter Web y Desktop; ignorar en mobile (Android/iOS)

  focused:
    style: strokeRounded
    color: semantic.action.primary
    description: icono recibe foco por teclado o navegación por accesibilidad

  active:
    style: strokeRounded
    color: semantic.action.primary
    description: >
      estado momentáneo durante el gesto de tap — se restablece al soltar.
      Diferente de "selected": active es transición, selected es estado persistente.

  selected:
    style: strokeRounded
    color: semantic.action.primary
    description: >
      el elemento está marcado como seleccionado de forma persistente (ej: tab actual
      en bottom nav, ítem favorito, opción activa en filtro). La diferenciación visual
      se logra exclusivamente mediante color (verde action.primary, escaso),
      no mediante cambio de estilo.

  disabled:
    style: strokeRounded
    color: semantic.text.disabled
    opacity: 0.6
    description: icono no interactuable; reducir opacidad además de cambiar color
```

---

## Accesibilidad

- Todo icono que represente una acción debe tener etiqueta semántica con `Semantics(label: '...', child: ...)` en Flutter.
- Todo icono puramente decorativo debe excluirse con `ExcludeSemantics(child: ...)`.
- No depender solo del icono para expresar error, éxito, urgencia o estado en vivo — complementar con texto o color. En vivo: siempre dot + overline "EN VIVO".
- Mantener tamaño suficiente (mínimo `md: 24px`) y contraste adecuado en light y dark mode. Las variantes de estado en dark (`*.300`/`*.400`) están elegidas para AA sobre fondo tinta.
- El estado `disabled` debe reducir opacidad a `0.6` además de cambiar el color.
- Recordar que `#FFFFFF` y `#000000` puros están prohibidos: ningún icono debe forzar blanco o negro absoluto; usar `paper.*` / `ink.*` del tema.

---

## Patrones de implementación

### Uso base — herencia de color del tema

```dart
import 'package:flutter/material.dart';
import 'package:hugeicons/hugeicons.dart';

HugeIcon(
  icon: HugeIconsStrokeRounded.home01,
  size: 24.0,
  strokeWidth: 1.5,
  // sin color explícito: hereda de IconTheme.of(context).color (semantic.text.primary)
)
```

### Estado seleccionado — diferenciación por color (verde escaso)

```dart
HugeIcon(
  icon: HugeIconsStrokeRounded.home01,
  size: 24.0,
  strokeWidth: 1.5,
  color: isSelected
      ? Theme.of(context).colorScheme.primary       // semantic.action.primary (verde)
      : Theme.of(context).colorScheme.onSurfaceVariant, // semantic.text.secondary
)
```

### Icono "live" — dot pulsante + overline editorial

```dart
Row(
  mainAxisSize: MainAxisSize.min,
  children: [
    // dot pulsante (animar opacidad/escala); color = semantic.status.live
    HugeIcon(
      icon: HugeIconsStrokeRounded.radioButton01,
      size: 16.0,
      strokeWidth: 1.5,
      color: context.tokens.status.live, // red.500 light / red.400 dark
    ),
    const SizedBox(width: 8.0), // space.2
    // overline "EN VIVO" — text.overline, color status.liveText (AA)
    Text('EN VIVO', style: context.text.overline.copyWith(
      color: context.tokens.status.liveText,    // red.700 light / red.300 dark
    )),
  ],
)
```

### Color de estado explícito (warning / tabla densa)

```dart
HugeIcon(
  icon: HugeIconsStrokeRounded.alert02,
  size: 16.0,            // xs en tabla densa
  strokeWidth: 1.75,     // compact: no perder trazo a 16px
  color: context.tokens.status.warning, // yellow.500 light / yellow.300 dark
)
```

---

## Criterios de consistencia

- Una semántica, un icono.
- Un contexto, un tamaño dominante.
- Un sistema, un estilo base (`strokeRounded`).
- Una excepción, una regla explícita.
- Un tema, una fuente de color principal (la tinta sobre papel; el verde solo marca interacción).

---

## Lista de decisión

Antes de introducir un icono nuevo, validar:

1. ¿Representa una acción, entidad o estado real del producto?
2. ¿Ya existe otro icono aprobado para esa semántica?
3. ¿Pertenece al estilo base `strokeRounded`?
4. ¿Funciona correctamente a 16, 20, 24 y 28 con trazo 1.5 / 1.75?
5. ¿Hereda bien desde `Theme.of(context)` / los tokens `semantic.*`, sin hex literal?
6. ¿Respeta la escasez del verde y la regla relleno-vs-texto de los estados?
7. ¿Necesita semántica accesible (`Semantics` widget)?
8. ¿Es realmente necesario o el texto/overline ya comunica suficiente?
```
