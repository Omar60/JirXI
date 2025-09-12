# JirX

Visualización animada en Canvas de un clúster de girasoles a partir de datos JSON. Al hacer clic en el botón, el script carga un archivo JSON con regiones (contornos y color) y las dibuja progresivamente en pantalla. Al terminar, muestra un mensaje de cierre.

## Características
- Canvas a pantalla completa con redimensionado automático.
- Renderizado progresivo (animado) de miles de regiones para un efecto de “pintado” suave.
- Mensaje de finalización cuando termina de dibujar.
- Sin dependencias externas: puro HTML, CSS y JS.

## Requisitos
- Un navegador moderno (Chrome, Edge, Firefox...).
- Servir los archivos por HTTP (necesario para `fetch`). Abrir `index.html` con `file://` no funcionará.

## Estructura del proyecto
- `index.html`: página principal, lógica JavaScript embebida y canvas.
- `styles.css`: estilos de la UI (título, botón, canvas y mensaje final).
- `resources/sunflower_cluster.json`: dataset con los contornos y colores de cada región (archivo grande).

## Puesta en marcha (Windows, PowerShell)
Desde la carpeta del proyecto (`JirXI`), inicia un servidor HTTP sencillo.

Opción A — Python (recomendado si tienes Python instalado):
```powershell
# Desde la carpeta JirXI
python -m http.server 5500
# Luego abre en el navegador
# http://localhost:5500/
```

Opción B — VS Code (extensión Live Server):
- Instala la extensión “Live Server”.
- Abre `index.html` y haz clic en “Go Live”.

Opción C — Node.js http-server (si tienes Node):
```powershell
# Instala una vez (global)
npm install -g http-server
# Ejecuta el servidor
http-server -p 5500
# Abre en el navegador
# http://localhost:5500/
```

Luego visita `http://localhost:5500/` en tu navegador.

## Uso
1. Abre la página servida por HTTP (ver pasos anteriores).
2. Pulsa el botón “¡Hey... aquí, da click aquí!” para iniciar la carga del dataset y el dibujo animado.
3. Espera a que el proceso termine; se mostrará un mensaje de finalización.

Notas importantes:
- El archivo JSON es grande; la primera carga puede tardar varios segundos.
- Durante el renderizado el botón queda deshabilitado para evitar múltiples cargas.

## Ruta del JSON (importante)
En `index.html` la función `loadCluster()` usa `fetch` para cargar el JSON. Asegúrate de que la ruta apunte a la carpeta `resources` del proyecto. Dado que `index.html` está en la raíz del proyecto junto a la carpeta `resources/`, la ruta correcta debería ser:

```
resources/sunflower_cluster.json
```

Si mueves archivos o publicas en una subcarpeta, ajusta la ruta según la ubicación relativa de `index.html`.

## Personalización
- Texto principal y mensaje final: edítalos directamente en `index.html`.
- Velocidad de animación: cambia la constante `ANIMATION_SPEED` en el script de `index.html` (valor 1 = máximo detalle, más alto = más rápido).
- Estilos: ajusta colores, tipografías y posiciones en `styles.css`.

## Rendimiento y consejos
- El dataset es muy grande (muchas regiones y puntos). En equipos modestos, la animación completa puede tardar.
- Mantén otras pestañas/cargas al mínimo mientras se dibuja.
- Si necesitas un arranque más rápido, puedes aumentar `ANIMATION_SPEED` para procesar más regiones por frame.

## Solución de problemas
- “No se pudo cargar el archivo del cluster…”: 
  - Asegúrate de estar sirviendo por HTTP (no abrir con `file://`).
  - Verifica que la ruta del `fetch` apunte a `resources/sunflower_cluster.json`.
- Pantalla negra o tarda mucho: el renderizado está en progreso; espera unos segundos/minutos según el equipo.
- El canvas no llena la ventana: el tamaño se ajusta en `resizeCanvas()`; revisa que no haya errores en la consola.

## Despliegue
- Puedes publicar el sitio en GitHub Pages, Netlify, Vercel, etc. Solo asegúrate de mantener la estructura de carpetas (`index.html` en la raíz y `resources/` junto a él), o ajusta la ruta en `fetch` si cambia.

## Licencia
No se ha especificado una licencia para este proyecto.

---
Hecho con cariño 💚
