[README.md](https://github.com/user-attachments/files/31317805/README.md)
# TLP
pagina web TLP
# TLP — Sitio web

Landing page de **TLP, transporte privado de pasajeros en la Región de Coquimbo**,
construida a partir de los diseños de Stitch.

Sitio estático: HTML + CSS + JavaScript sin dependencias ni paso de compilación.
Se puede publicar tal cual en GitHub Pages.

## Estructura

```
index.html              Página completa (una sola página con anclas)
assets/css/styles.css   Estilos, tokens de color y responsive
assets/js/main.js       Menú móvil, acordeón FAQ, carrusel, contadores y formularios
assets/img/             Logo e imágenes (las fotos son marcadores de posición)
```

## Ver el sitio en local

No necesita servidor, pero el mapa embebido funciona mejor sobre HTTP:

```bash
python3 -m http.server 8000
# abrir http://localhost:8000
```

## Secciones

Hero con formulario de cotización · Confían en nosotros · Servicios · Por qué elegirnos ·
Cifras · Cómo funciona · Flota (carrusel) · Cobertura con mapa · Seguridad y confort ·
Testimonios · FAQ · Contacto · Footer.

## Qué hay que reemplazar antes de publicar

El contenido de ejemplo viene del diseño y **debe reemplazarse por los datos reales**:

| Qué | Dónde |
|---|---|
| Teléfono `+56 9 3284 2799` | `index.html` (topbar, contacto, footer, botón WhatsApp) y `CONFIG.whatsapp` en `main.js` |
| Email `contacto@tlp.cl` | `index.html` y `CONFIG.email` en `main.js` |
| Dirección | `index.html` (contacto, footer y bloque JSON-LD del `<head>`) |
| Cifras (50.000+, 15 años, etc.) | atributos `data-count` en la sección `.stats` |
| Testimonios y caso de éxito | secciones "Testimonios" y "Seguridad y confort" |
| Logos de "Confían en nosotros" | sección `.trust` — hoy son marcas de texto genéricas |
| Fotos | `assets/img/*.svg` — son ilustraciones de relleno, reemplazar por fotos reales (`.jpg`/`.webp`) y actualizar el `src` |
| Enlaces legales | footer, hoy apuntan a `#` |
| Redes sociales | footer, hoy apuntan a `#` |
| `<link rel="canonical">` | `index.html`, poner el dominio final |

## Cómo se envían los formularios

Los dos formularios (hero y contacto) validan en el navegador y luego entregan la
solicitud según `CONFIG.method`, al inicio de `assets/js/main.js`:

- `'whatsapp'` *(por defecto)* — abre WhatsApp con el mensaje ya redactado.
- `'email'` — abre el cliente de correo con el mensaje.
- `'endpoint'` — hace `POST` a `CONFIG.endpoint` (Formspree, Getform, Basin, etc.).

```js
var CONFIG = {
  whatsapp: '56932842799',
  email: 'contacto@tlp.cl',
  method: 'whatsapp',
  endpoint: ''
};
```

Al ser un sitio estático no hay backend propio: para recibir las solicitudes por
correo hay que usar la opción `endpoint` con algún servicio de formularios.

## Paleta

| Token | Valor | Uso |
|---|---|---|
| `--navy-900` | `#0f2438` | Fondos oscuros, hero, footer |
| `--navy-800` | `#16314b` | Footer, botones secundarios |
| `--orange` | `#f2911f` | Acento, botones principales |
| `--bg-soft` | `#f5f7fa` | Fondo de secciones alternas |

Se editan en el bloque `:root` de `assets/css/styles.css`.

## Publicar en GitHub Pages

En el repositorio: **Settings → Pages → Source: Deploy from a branch**, elegir la
rama y la carpeta `/ (root)`.

## Notas técnicas

- Responsive en tres cortes: 1024px, 860px (menú hamburguesa) y 680px.
- Accesibilidad: navegación por teclado, `aria-expanded` en menú y FAQ, enlace de
  salto al contenido, foco visible y respeto por `prefers-reduced-motion`.
- SEO: meta description, Open Graph y datos estructurados `LocalBusiness`.
- El mapa de cobertura usa el embed de OpenStreetMap (sin API key). Si no carga,
  se muestra un texto de respaldo con las comunas.
