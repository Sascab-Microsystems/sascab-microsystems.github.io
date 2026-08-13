# Sitio web — Sascab Microsystems

Sitio estático, bilingüe (EN/ES), sin dependencias ni build. Cada página es un archivo HTML
autocontenido (CSS y JS en línea), así que funciona en cualquier hosting estático.

**Paleta:** carbón cálido `#3E4243` + oro antiguo `#B09453`, tomados directamente del logotipo.

## Contenido — 12 páginas por idioma

| Archivo | Página |
|---|---|
| `index` | Inicio |
| `about` | Nosotros: quiénes somos, misión/visión/valores, compromiso de calidad, ubicación |
| `product` | BioRLE-1: producto + tabla de especificaciones + entregables |
| `technology` | Tecnología y núcleo open source |
| `licensing` | Licencias y modelo de negocio |
| `blog` | Índice del blog |
| `post-radio-power` | Artículo: por qué la radio define la autonomía |
| `post-lossless` | Artículo: sin pérdida vs. casi sin pérdida en ECG |
| `post-fabless` | Artículo: qué significa fabless para tu cadena de suministro |
| `contact` | Contacto |
| `legal` | Aviso legal |
| `privacy` | Aviso de privacidad |

Inglés en `nombre.html`, español en `nombre.es.html`. El inglés es el idioma por defecto porque
el cliente objetivo es el OEM internacional. Selector EN/ES arriba a la derecha.

Incluye además `sitemap.xml`, `robots.txt` y `logo-propuesta.svg`.

---

## ⚠️ Qué falta antes de publicar

**Todo lo que aparece en terracota con borde punteado es un marcador que debes reemplazar.**

### 1. Especificaciones técnicas de BioRLE-1
En `product`, las celdas `POR DEFINIR` / `TBD`: razón de compresión, reconstrucción, resolución,
frecuencia de muestreo, latencia, área, consumo, nodo de proceso e interfaz con el host. No se
inventó ninguna cifra. Si alguna va bajo NDA, borra la fila completa.

### 2. Dirección física
Falta la dirección en el footer y en `about`. **Ya están puestos:** el teléfono
+52 56 2766 8073 y los correos `contacto@`, `licencias@` y `legal@` en `sascabmicro.com`
— falta darlos de alta en el proveedor de correo.

### 3. Textos legales
`legal` y `privacy` son **plantillas** con la estructura de la LFPDPPP. **Requieren abogado.**
Completar razón social, RFC, domicilio fiscal, correo de privacidad, proveedores tecnológicos y
ciudad de jurisdicción. Cuando estén revisadas, borra el bloque de aviso de arriba.

### 4. Certificaciones
En `about`, la nota final de "Compromiso de calidad". No declares conformidad con una norma sin
tenerla documentada.

### 5. Formulario de contacto
Apunta a `https://formspree.io/f/FORM_ID`. Crea una cuenta en [Formspree](https://formspree.io)
y reemplaza `FORM_ID`.

### 6. Repositorio open source
En `technology`, el botón apunta a `#` para no dejar un enlace roto. Cámbialo por
`https://github.com/sascab-microsystems/biorle` **el día que el repositorio exista y sea
público**, no antes.

### 7. Dominio
Ya configurado como **sascabmicro.com** en `sitemap.xml`, `robots.txt`, los correos y el archivo
`CNAME` que GitHub Pages necesita. Falta **registrarlo** y apuntar el DNS.

### 8. Logotipo — decisión pendiente del CEO
El sitio usa una versión del emblema original **sin la banana**: se conserva el marco de 8
puntas, los triángulos dorados y las bandas paralelas al octágono, y en el centro va una **S de
Sascab** dibujada con el mismo lenguaje —chaflanes de 45°, mismo grosor de banda—. Archivos:

| Archivo | Uso |
|---|---|
| `emblema-sin-banana.svg` | Completo, fondos claros. Papelería, LinkedIn, portadas. |
| `emblema-sin-banana-oscuro.svg` | El mismo en versión clara, para fondos oscuros. |
| `emblema-reducido.svg` | Silueta llena para 16-34 px: favicon, header, avatares. |
| `logo-propuesta.svg` | Lockup completo: emblema + SASCAB + MICROSYSTEMS. |

**No uses el reducido en tamaños grandes** — está simplificado a propósito y a partir de unos
60 px conviene el completo. El header del sitio y el favicon usan el reducido; se sustituyen en
`MARK` y `FAVICON` dentro de `fuentes/build.py`.

---

## Publicar

**Cloudflare Pages** — Workers & Pages → Create → Pages → Upload assets, arrastra la carpeta,
luego Custom domains.

**Netlify** — [app.netlify.com/drop](https://app.netlify.com/drop), arrastra la carpeta, luego
Domain settings → Add custom domain.

**GitHub Pages** — sube los archivos a la raíz de `main`, Settings → Pages → Source `main`/`(root)`.

---

## Editar el sitio

`dist/` es generado. Para cambios estructurales, edita los fuentes y regenera:

```
fuentes/build.py         paletas, estilos, plantilla, navegación, footer, datos de contacto
fuentes/content_en.py    inglés de las 5 páginas originales
fuentes/content_es.py    español de las mismas
fuentes/extra_en.py      Nosotros, blog, artículos y legales en inglés
fuentes/extra_es.py      lo mismo en español
fuentes/main.py          genera dist/

python3 main.py
```

**Cambiar de paleta** sin tocar nada más:

```
SASCAB_THEME=navy  python3 main.py   # carbón + oro (actual)
SASCAB_THEME=cream python3 main.py   # crema + oro
SASCAB_THEME=tech  python3 main.py   # la primera versión, verde agua
```

Para añadir un artículo: agrégalo a `POSTS` en `build.py`, escribe el cuerpo con `_post()` en
`extra_es.py` y `extra_en.py`, y añade su miniatura SVG a `THUMBS`.
