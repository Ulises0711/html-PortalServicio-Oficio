# CraftConnect · Portal de Servicios Profesional y Clasificados de Oficios

**Segundo Parcial Práctico · Interfaz del Usuario 2026 · Caso 9**
Alumno: Ulises · Prototipo Figma: _(pegar acá el enlace, con permisos de lectura y prototipo activo)_

Plataforma que conecta usuarios del hogar con profesionales independientes (plomería, electricidad, pintura, gas) para pedir presupuestos.

## Cómo ver el sitio

No necesita instalación ni JavaScript. Abrí `index.html` en el navegador (doble clic) o publicá la carpeta en GitHub Pages / Vercel.

## Estructura del proyecto

```
craftconnect-web/
├── index.html              Directorio de profesionales (buscador por rubro y zona)
├── perfil.html             Perfil profesional (galería, opiniones, cobertura, tarifas)
├── solicitud.html          Formulario guiado de pedido de presupuesto
├── confirmacion.html       Confirmación de mensaje enviado al profesional
├── mis-solicitudes.html    Seguimiento de solicitudes (con cancelación confirmada)
├── estilos.css             Hoja de estilos única, ordenada en 12 secciones
├── imagenes/               Fotos de profesionales y de trabajos realizados
└── README.md
```

## Cobertura del Caso 9

| Requerimiento | Dónde se resuelve |
|---|---|
| Directorio: buscador por rubro y zona, listado con estrellas | `index.html`: filtros por rubro y zona que ocultan/muestran tarjetas con valoración en estrellas |
| Perfil: galería, opiniones, zona de cobertura, tarifas de visita | `perfil.html`: todas las secciones, con panel lateral de cobertura y tarifa |
| Solicitud: formulario guiado, adjuntos, confirmación de envío | `solicitud.html` (5 secciones, adjunto de fotos) → `confirmacion.html` |
| Pantallas adicionales para un flujo completo | `mis-solicitudes.html`, cancelación con modal, avisos y salidas en cada pantalla |

## Responsive

- Diseño **mobile first**: se escribe para celular y se amplía con `@media` a 720 px (tablet) y 1040 px (escritorio).
- Etiqueta `viewport`, imágenes fluidas y cuadrículas (`grid`) con `minmax(0, 1fr)`.
- Verificado sin scroll horizontal en anchos de 320, 360, 768 y 1280 px.
- Listado: 1 columna (celular), 2 (tablet), 3 (escritorio). El perfil pasa de una columna a dos con panel lateral fijo.

## Flujo de navegación (cerrado, sin callejones)

```
Directorio ──► Perfil ──► Solicitud ──► Confirmación ──► Mis solicitudes
    ▲            │            │               │                │
    └────────────┴────────────┴───────────────┴────────────────┘
      (logo, menú superior y enlaces "Volver" disponibles en todas las páginas)
```

- Avanzar: botones "Ver perfil", "Pedir presupuesto", "Enviar solicitud".
- Retroceder: "← Volver al directorio / al perfil" en cada página interna.
- Cancelar: botón "Cancelar" en el formulario, y "Cancelar solicitud" con ventana de confirmación en "Mis solicitudes".
- Volver al inicio: el logo y el menú están en todas las páginas.

## Heurísticas de Nielsen aplicadas

### 1. Visibilidad del estado del sistema
El usuario siempre sabe dónde está y qué pasó.
- El menú marca la página actual (`aria-current="page"`, fondo resaltado).
- Los filtros muestran el chip activo en verde y la lista cambia al instante.
- El formulario tiene un indicador de pasos (Tu pedido › Confirmación › Respuesta) y secciones numeradas del 1 al 5.
- Al enviar, `confirmacion.html` informa que el mensaje llegó, con número de referencia y línea de "Próximos pasos".
- Al cancelar una solicitud, aparece un aviso de éxito y la etiqueta cambia de "En revisión" a "Cancelada".
- Botones y tarjetas responden con `:hover`, `:active` y aro de foco `:focus-visible` (también al navegar con teclado).

### 2. Prevención de errores
- Campos con validación nativa: `required`, `minlength="20"`, `maxlength="500"`, `type="date"`, `type="tel"` con `pattern`.
- Los mensajes de error aparecen solo tras interactuar con el campo (`:user-invalid`), con borde rojo y texto que explica cómo corregirlo.
- Cancelar una solicitud exige confirmar en una ventana ("¿Cancelar esta solicitud? No se puede deshacer"); el botón seguro ("No, mantener") queda a la vista.
- El campo de zona limita las opciones a las zonas con cobertura.

### 3. Consistencia y estándares
- Una sola hoja de estilos, con variables de color y tipografía compartidas por todas las páginas.
- Mismo encabezado, pie y botones (principal, verde, suave, contorno, peligro) en cada pantalla.
- Convenciones conocidas: logo lleva al inicio, enlaces "← Volver", estrellas ámbar solo para valoraciones, rojo solo para urgencias y errores.

### 4. Reconocer en lugar de recordar
- Los filtros muestran todas las opciones como chips visibles, sin escribir.
- El tipo de problema y la franja horaria son tarjetas seleccionables con estado visible.
- La confirmación repite el resumen de lo enviado, para que no haya que recordarlo.

### 5. Control y libertad del usuario
- Salida en cada pantalla: "Volver", "Cancelar", logo y menú.
- El pedido puede cancelarse antes de enviarlo (formulario) y después de enviarlo (Mis solicitudes).

### 6. Diseño estético y minimalista
- Una acción principal por pantalla, en color destacado; las secundarias en estilo suave o de contorno.
- Jerarquía tipográfica clara y espacios consistentes (escala de 4/8 px).

## Decisiones y límites

- **Sin JavaScript:** los filtros, el modal de cancelación y los avisos usan solo CSS (`:has()`, `:target`, `:user-invalid`). Requiere un navegador actual (Chrome, Edge, Firefox o Safari recientes).
- **Es un prototipo estático:** los datos son de ejemplo y el envío del formulario no se guarda en ningún servidor.
- **Imágenes:** las fotos de perfil y de la galería están en la carpeta `imagenes/`. Todas tienen texto alternativo (`alt`) y carga diferida (`loading="lazy"`).
- **Perfil único:** todos los botones "Ver perfil" llevan al perfil de ejemplo de Mike Tremblay.

## Herramientas utilizadas

_(Completar según corresponda: Figma, Google Stitch para el diseño inicial, asistente de IA para el código, etc.)_
