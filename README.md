# Alex Boots · Giveaway Día del Padre — Ruleta

Herramienta interna standalone para correr el sorteo en vivo del giveaway de
Día del Padre de **Alex Boots (Ranchers Boot Co.)**. Una ruleta animada
muestra los participantes y, al detenerse, despliega el mensaje completo que
el ganador escribió para su papá.

Todo vive en **un solo archivo**: `alexboots-giveaway-ruleta.html`. Sin build,
sin Node, sin dependencias locales.

---

## Cómo abrir

Haz doble click en `alexboots-giveaway-ruleta.html` o ábrelo en cualquier
navegador moderno (Chrome, Edge, Safari, Firefox).

> Requiere conexión a internet la primera vez, ya que carga Google Fonts,
> los iconos de Lucide y `canvas-confetti` desde sus CDN.

---

## Formato esperado del CSV

Formato estándar de **Commentpicker**, dos columnas:

```csv
username,text
marcos_rdz,"Papá, gracias por enseñarme a trabajar duro."
lucia.fernandez,"Eres mi héroe, viejo. Feliz día."
```

- El encabezado (`username,text`) es opcional; se autodetecta. También se
  reconocen alias como `user/handle/usuario` y `comment/message/mensaje`.
- Se admiten comas, comillas y saltos de línea dentro del campo del mensaje.

### Filtros aplicados automáticamente al importar

1. Comentarios con texto vacío.
2. Comentarios que son **solo emojis**.
3. Comentarios que son **solo @menciones** sin mensaje real (< 3 caracteres
   útiles tras quitar las menciones).
4. Comentarios de la **cuenta del cliente** (`alexbootscollection` y variantes,
   configurable en `localStorage`).
5. **Duplicados** por username (se conserva el primero).

Antes de guardar verás un **modal de vista previa** con el desglose
(total leídos, válidos, y excluidos por cada motivo) para confirmar.

---

## Atajos de teclado

| Tecla | Acción |
|-------|--------|
| `Espacio` | Gira la ruleta |
| `Esc` | Cierra el modal del ganador / preview / sidebar |
| `D` `D` `D` | **Modo demo oculto**: con la lista vacía, carga 8 participantes de prueba con mensajes bonitos para screenshots |

---

## Funciones principales

- **Ruleta animada** en Canvas con desaceleración cinematográfica (ease-out),
  click de audio por segmento y aguja dorada. Si hay más de 30 participantes,
  los nombres se ocultan y solo se muestran los segmentos.
- **Modal de ganador** con confetti dorado/crema, el handle en grande y el
  mensaje al papá animado con efecto *typewriter* y comillas decorativas.
- **Girar de nuevo**: remueve al ganador actual y vuelve a girar.
- **Guardar ganador**: descarga un JSON `{ winner, runners_up, timestamp }`
  y lo agrega al histórico.
- **Sidebar** (icono ☰) con la lista completa, preview del mensaje, borrado
  manual y exportación a JSON.

---

## Persistencia (localStorage)

| Clave | Contenido |
|-------|-----------|
| `alexboots_participants` | Array de participantes válidos |
| `alexboots_winners` | Histórico de ganadores guardados |
| `alexboots_excluded_users` | Usernames a excluir (cuenta del cliente) |

### Cómo reiniciar / limpiar

- Desde la app: abre el sidebar (☰) → **VACIAR TODO**.
- Manualmente: abre la consola del navegador (`F12`) y ejecuta:

```js
localStorage.removeItem('alexboots_participants');
localStorage.removeItem('alexboots_winners');
localStorage.removeItem('alexboots_excluded_users');
location.reload();
```

O para borrar todo de una vez:

```js
localStorage.clear(); location.reload();
```
