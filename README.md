# 🏰 GreenAbyss — Imperio isométrico

Juego de construcción de reino en vista isométrica, hecho en un solo archivo HTML con Canvas, sin dependencias ni compilación.
Construye edificios, produce aldeanos y envíalos a recolectar madera, piedra, comida y oro en una isla que crece contigo.

## Cómo jugarlo

Abre `index.html` en el navegador. No necesita servidor.

| Acción | Cómo |
| --- | --- |
| Interactuar | Tocar con el clic (edificios, aldeanos, árboles, rocas, puerto, mina) |
| Mover el mapa | Arrastrar |
| Zoom | Rueda del ratón |
| Construir | Tocar una tarjeta de la barra inferior y luego una casilla libre |
| Salir del modo construir | Tocar la tarjeta otra vez, `Esc` o clic derecho |
| Renombrar el reino | Tocar el nombre de arriba a la izquierda |
| Ver qué hace un edificio | Pasar el cursor sobre su tarjeta (en móvil, tocarla): sale su descripción, precio y requisitos |

## Recursos

Empiezas con **500 de oro** y **50 de comida**. Los recursos suben cuando el aldeano **entrega** la carga. Arriba se muestran oro, comida, madera, piedra, aldeanos (máx. 10), cuarteles y el tiempo hasta el próximo rebrote.

## Edificios

| Edificio | Precio | Qué hace |
| --- | --- | --- |
| Casa | 30 oro | +1 oro por segundo |
| Granja | 40 oro | +1 comida por segundo |
| Cuartel | 80 oro | Cuenta en la barra superior (sin función todavía) |
| Camino | 5 oro | Se puede pisar; el modo construir sigue activo para trazar varios |
| Campamento | 60 oro | Produce un **aldeano** (20 comida, 3 s) |
| Casa vikinga | 90 oro | Produce un **aldeano vikingo** (25 comida, 4 s) |
| Puerto | 120 oro | Solo en la costa. Un aldeano pesca: +6 comida cada 2,6 s |
| Mina de oro | 150 oro | Solo en colinas. Un aldeano extrae: +10 oro cada 3,2 s |
| Almacén | 70 oro | Punto de entrega: los aldeanos dejan aquí lo que recolectan (el Campamento y la Casa vikinga también sirven) |
| Demoler | — | Devuelve el 50 % del oro |

**Aldeanos:** tocar el edificio, producir, tocar al aldeano y luego tocar un árbol (+5 madera), una roca (+5 piedra), el puerto o la mina.
Los aldeanos **cargan** lo que recolectan (15 de madera o piedra, 18 de comida, 20 de oro) y lo llevan al punto de entrega más cercano; una barra sobre su cabeza muestra cuánto llevan. Después vuelven solos al trabajo. Si no tienen tarea y llevan carga, van a entregarla. Construir un almacén junto al bosque o la mina acorta los viajes.
Los árboles aguantan 3 golpes y las rocas 4.

**Caza:** con un aldeano seleccionado, toca una vaca o una oveja. El animal se marca con un aro rojo, el aldeano va hasta él y lo abate en 1,4 s. Da **12 de carne** (vaca) u **8** (oveja), que cuenta como comida y se entrega igual que lo demás. Cada animal **reaparece a los 3 minutos** en su zona de origen. Cada 5 minutos el mapa repone árboles y rocas hasta la cantidad inicial.

## Guardado

Automático cada 10 segundos y al cerrar la pestaña, en `localStorage` (clave `imperio_save_v5`).
El botón **Nueva partida** borra el guardado.

## Para desarrollar

Todo está en `index.html`: estilos, iconos SVG y lógica.

- `N` — tamaño del mapa (máximo 63).
- `T` — catálogo de edificios; los iconos de las tarjetas están en `ICON`.
- `PR` — edificios que producen aldeanos.
- Si cambias la generación del terreno, **sube la versión de `KEY`** (`imperio_save_vN`) para no cargar partidas incompatibles.

### Guía de estilo para añadir cosas nuevas

- **Tarjeta en la barra inferior:** borde grueso de color, degradado, ilustración SVG de 64×64, nombre en blanco con sombra y precio con moneda. Define su color con `.k-nombre{--c1;--c2;--bd}`.
- **Descripción:** cada edificio tiene su texto en el objeto `INFO` (`d` = descripción, `r` = requisito opcional). Se muestra al pasar el cursor sobre la tarjeta.
- **Edificio en el mapa:** contorno oscuro redondeado, sombra suave y círculo de tierra debajo (salvo caminos y puerto).
- **Paleta:** hierba amarillo-verdosa, arena clara, mar turquesa con patrón de rombos y espuma blanca.
- **Roca:** el suelo rocoso es de losas irregulares en tonos marrón y beige (con grietas y manchas), y las plataformas elevadas son de losas gris oscuro biseladas. Las rocas picables son piedras con facetas, reflejos, musgo y guijarros alrededor, y encogen con cada golpe.
- **Diseño de edificios:** casas de madera con tejado de color propio (almacén naranja, casa vikinga marrón con escudos, puerto azul con muelle y bote), base de césped o arena, vallas bajas, farol, barril, caja y arbustos pequeños. Los accesorios van a escala reducida (`sc()`) para no tapar la casa.
- **Interfaz:** madera oscura con bordes dorados, barra de piedra con cápsulas oscuras e iconos grandes.

## Publicar con GitHub Pages

Settings → Pages → Branch `main` → carpeta `/ (root)`. El juego quedará en `https://TU-USUARIO.github.io/NOMBRE-DEL-REPO/`.
