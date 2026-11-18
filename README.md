# Lazeta Fragancias: tienda online con GitHub como base de datos

Toda la web está en un solo archivo, `index.html`, más la carpeta `datos` con el catálogo y las fotos. Los productos, precios, textos y fotos se guardan **en el mismo repositorio de GitHub**, así que no hace falta ningún otro servicio.

- **Tienda:** `https://TU-USUARIO.github.io/lazeta/`
- **Panel del personal:** la misma dirección con `#admin` al final. **No hay ningún link visible para los clientes.**
  - Acceso rápido para el personal: tocar **5 veces seguidas el logo del pie de página**.
  - Aunque alguien llegue a la pantalla de ingreso, no puede entrar sin usuario y contraseña.

## Cómo funciona

1. El personal entra al panel con **usuario y contraseña**, desde cualquier celular o computadora. El **token de GitHub** se usa **una sola vez**, para crear esos usuarios.
2. Cuando guarda, el panel escribe el catálogo en `datos/catalogo.json` y las fotos en `datos/fotos/`, dentro del repositorio.
3. GitHub Pages publica el cambio solo, en **1 o 2 minutos**.
4. Los clientes lo ven al entrar a la página. Si ya la tenían abierta, se actualiza sola en el próximo minuto.

Si hacés varios cambios seguidos, como sumar stock de varios productos, el panel los junta y los sube en una sola publicación.

Abierta fuera de GitHub Pages (por ejemplo, con doble clic en el archivo), la página funciona en **modo demo**: el usuario es `admin` y la contraseña `lazeta2026`. Esos datos ya no se muestran en pantalla, y después de 5 intentos fallidos el ingreso se bloquea 1 minuto.

---

## Instalación (unos 10 minutos, una sola vez)

### 1. Crear el repositorio
1. Entrá a **github.com** y creá una cuenta gratis si no tenés.
2. Arriba a la derecha, hacé clic en **+**, elegí **New repository** y ponele de nombre `lazeta`. Dejalo **Public** y hacé clic en **Create repository**.
3. Hacé clic en **uploading an existing file** y arrastrá **`index.html` y la carpeta `datos`** completa (tiene el catálogo y las fotos de los perfumes). Apretá **Commit changes**.

### 2. Activar GitHub Pages
1. En el repositorio, andá a **Settings → Pages**.
2. En *Source* elegí **Deploy from a branch**, la rama **main** y la carpeta **/ (root)**, y apretá **Save**.
3. En 1 o 2 minutos la tienda va a estar en `https://TU-USUARIO.github.io/lazeta/`.

### 3. Crear el token del personal
1. En GitHub, hacé clic en tu foto y andá a **Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token**.
2. Completá así:
   - **Token name:** `Panel Lazeta`
   - **Expiration:** la duración más larga que te ofrezca. Cuando venza, se crea otro.
   - **Repository access:** **Only select repositories**, y elegí `lazeta`.
   - **Permissions → Repository permissions → Contents:** **Read and write**.
3. Apretá **Generate token** y **copiá el token**, que empieza con `github_pat_`. GitHub lo muestra una sola vez.

### 4. Primer ingreso y creación del usuario (una sola vez)
1. Entrá a `https://TU-USUARIO.github.io/lazeta/#admin`.
2. Tocá **"¿Primera vez? Ingresar con el token de GitHub"** y pegá el token.
3. El catálogo ya viene cargado con los 9 perfumes en `datos/catalogo.json`.
4. El panel te lleva solo a **Ajustes → Acceso del personal**. Creá tu **usuario y contraseña**, de al menos 10 caracteres.
5. Listo. En 1 o 2 minutos ya podés entrar desde cualquier dispositivo con usuario y contraseña, sin el token. Si es tu dispositivo, tildá "Recordar en este dispositivo" y no te lo va a volver a pedir.

Arriba del panel tiene que aparecer en verde: **"Conectado a GitHub"**.

---

## Preguntas frecuentes

**¿Es seguro?**
Sí, si usás contraseñas fuertes:
- El token se guarda en `datos/acceso.json` **cifrado con AES-256** usando la contraseña de cada usuario. Sin la contraseña correcta, ese archivo no sirve para nada.
- Como el repositorio es público, cualquiera podría intentar adivinar una contraseña. Por eso hay que usar **contraseñas largas y difíciles**: como mínimo 10 caracteres, mejor 14 o más, mezclando palabras y números (por ejemplo `AromaAzul-Lanus-2026`). No uses fechas de cumpleaños ni el nombre de la tienda solo.
- Cualquiera puede ver el catálogo, igual que la tienda, pero sin usuario y contraseña no puede modificarlo.
- Si sospechás que alguien sabe una contraseña, borrá el token en GitHub (Fine-grained tokens → Delete). Eso inutiliza todos los accesos al instante. Después creá un token nuevo y volvé a crear los usuarios.

**¿Cómo le doy acceso a otra persona del personal?**
En **Ajustes → Acceso del personal**, creá otro usuario con su propia contraseña. Para quitarle el acceso, tocá el 🗑 al lado de su nombre.

**¿Cómo cambio una contraseña?**
En **Ajustes → Acceso del personal**, escribí el mismo usuario con la contraseña nueva y apretá **Guardar usuario**.

**Mis cambios no aparecen en la tienda.**
- Esperá 1 o 2 minutos y recargá la página.
- En el repositorio, la pestaña **Actions** muestra cada publicación ("pages build and deployment").
- GitHub Pages tiene un límite de unas 10 publicaciones por hora. Si hacés muchísimos cambios en poco tiempo, los últimos pueden demorar un poco más, pero se publican igual.

**El panel dice que el token venció.**
Los tokens de GitHub tienen fecha de vencimiento. Cuando vence:
1. Creá un token nuevo (paso 3).
2. Entrá con **"Ingresar con el token de GitHub"**.
3. En **Ajustes → Acceso del personal**, volvé a guardar cada usuario con su contraseña.

**¿Uso un dominio propio, como www.lazeta.com.ar?**
Abrí `index.html`, buscá `GITHUB_REPO` y escribí `'TU-USUARIO/lazeta'`.

**¿Puedo pasar lo que cargué en modo demo?**
Sí, en dos pasos:
1. En la versión demo, andá a **Ajustes** y apretá **Descargar respaldo**.
2. Ya en GitHub Pages, volvé a **Ajustes**, usá **Importar** con ese archivo y se publica todo.

**¿Cómo cargo un perfume nuevo?**
En el panel: **Productos → + Nuevo producto**. Completá marca, nombre, precio en efectivo y por transferencia, notas y subí la foto. Para que quede igual que las demás, usá una foto con fondo liso: la página le pone el fondo con curvas azules y el podio. Si dejás el precio vacío, la tienda muestra **"Consultar precio"** con un botón a WhatsApp.
