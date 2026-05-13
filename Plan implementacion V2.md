# PROMPT
Lenguaje flutter dart, actúa como creador y diseñador de software, quiero crear una aplicación multiplataforma. Mi negocio es una juguetería -“Juguetería Ivette”-. Quiero que generes cada detalle necesario para que este plan de implementación sea lo mejor posible. Hazlo lo más largo y DETALLADO posible para hacer el proyecto muy bien.

IMPORTANTE:NO proporcionar codigo

 El objetivo de esta aplicación es que los usuarios puedan acceder al Sitio, para así comprar diversos productos que la juguetería ofrece.
La paleta de colores y diseño de la app será en colores principalmente morados y demás colores que sean llamativos APROPIADOS para una juguetería. De preferencia, crear una tabla con los colores que se usarán para cada cosa (como fondo, botones, appbar, etc). Autenticación por correo electrónico y password. Diseño UI, UX.

Escribe TODAS las entidades numerado cada una de ellas (tablas) que te voy a proporcionar de acuerdo al negocio. Dame una lista numerada de todas las dependencias necesarias para el proyecto. Quiero carpetas para templates, models, etc.
Que models voy a utilizar. Quiero TODA la información posible de agregar para desarrollar este proyecto.

El entorno de trabajo que se usará en este proyecto será Antigravity que se vincula con una base de datos en Firebase Console, me proporcionarás la lista de dependencias que necesitaré en pubspec.yaml como ayuda para la generación de este proyecto. A continuación te dejo las tablas que planeo usar para este proyecto con sus campos, tipo y descripción.

También me vas a generar un árbol de la estructura del proyecto con todos los archivos para saber cómo quedó estructurado  Procedimiento paso a paso para crear el proyecto.

 
1. CATEGORIA 
Almacena las clasificaciones generales de los productos.
Campo
Tipo
Descripción
id
SERIAL
Identificador único (Clave primaria).
nombre
VARCHAR(100)
Nombre de la categoría (ej. Juguetes, Electrónica). Único.
descripcion
TEXT
Detalles adicionales sobre qué incluye la categoría.

2. MARCA
Registro de los fabricantes o marcas de los artículos.
Campo
Tipo
Descripción
id
SERIAL
Identificador único (Clave primaria).
nombre
VARCHAR(100)
Nombre comercial de la marca. Único.
pais_origen
VARCHAR(80)
País donde se fundó o reside la marca.

3. PROVEEDOR
Entidades externas que suministran la mercancía.
Campo
Tipo
Descripción
id
SERIAL
Identificador único (Clave primaria).
nombre
VARCHAR(150)
Razón social o nombre del proveedor.
contacto
VARCHAR(100)
Nombre de la persona de contacto.
email
VARCHAR(120)
Correo electrónico institucional. Único.
telefono
VARCHAR(20)
Número telefónico de contacto.

4. SUCURSAL
Diferentes puntos de venta o almacenes físicos.
Campo
Tipo
Descripción
id
SERIAL
Identificador único (Clave primaria).
nombre
VARCHAR(100)
Nombre de la sede.
direccion
VARCHAR(200)
Ubicación física detallada.
ciudad
VARCHAR(80)
Ciudad donde se encuentra.
telefono
VARCHAR(20)
Teléfono de la sucursal.

5. ROL
Define los niveles de acceso al sistema.
Campo
Tipo
Descripción
id
SERIAL
Identificador único (Clave primaria).
nombre
VARCHAR(50)
Nombre del rol (ej. Admin, Cajero). Único.
permisos
TEXT
Listado o descripción de qué acciones puede realizar.

6. USUARIO
Personal que accede al sistema.
Campo
Tipo
Descripción
id
SERIAL
Identificador único (Clave primaria).
nombre
VARCHAR(100)
Nombre completo del empleado.
email
VARCHAR(120)
Credencial de acceso. Único.
password_hash
VARCHAR(255)
Contraseña encriptada para seguridad.
rol_id
INTEGER
Referencia al rol asignado.
sucursal_id
INTEGER
Referencia a la sede donde labora.
activo
BOOLEAN
Estado de la cuenta (True = Vigente).

7. PRODUCTO
Catálogo maestro de artículos disponibles.
Campo
Tipo
Descripción
id
SERIAL
Identificador único (Clave primaria).
nombre
VARCHAR(150)
Nombre del producto.
descripcion
TEXT
Ficha técnica o comercial.
precio
NUMERIC(10,2)
Valor de venta al público (no negativo).
stock
INTEGER
Cantidad global disponible.
categoria_id
INTEGER
Relación con la tabla CATEGORIA.
marca_id
INTEGER
Relación con la tabla MARCA.
proveedor_id
INTEGER
Relación con el proveedor principal.
imagen_url
VARCHAR(255)
Ruta a la fotografía del producto.
edad_minima
SMALLINT
Restricción de edad recomendada.
activo
BOOLEAN
Indica si el producto se sigue vendiendo.

8. INVENTARIO
Control de existencias específicas por sucursal.
Campo
Tipo
Descripción
id
SERIAL
Identificador único (Clave primaria).
producto_id
INTEGER
Referencia al producto.
sucursal_id
INTEGER
Referencia a la sucursal.
cantidad
INTEGER
Existencia actual en esa sucursal específica.
stock_minimo
INTEGER
Alerta para reposición (Default 5).
actualizado_at
TIMESTAMP
Última vez que se modificó el registro.

9. MOVIMIENTO_INVENTARIO
Historial de entradas, salidas y ajustes de stock.
Campo
Tipo
Descripción
id
SERIAL
Identificador único (Clave primaria).
inventario_id
INTEGER
Referencia al registro de inventario afectado.
tipo
VARCHAR(20)
Clasificación: 'entrada', 'salida' o 'ajuste'.
cantidad
INTEGER
Unidades que entraron o salieron.
motivo
VARCHAR(200)
Explicación del movimiento (ej. "Merma por rotura").
fecha
TIMESTAMP
Momento exacto del movimiento.
usuario_id
INTEGER
Persona que registró el movimiento.

10. CLIENTE
Personas que realizan compras.
Campo
Tipo
Descripción
id
SERIAL
Identificador único (Clave primaria).
nombre
VARCHAR(150)
Nombre completo o razón social.
email
VARCHAR(120)
Correo de contacto. Único.
telefono
VARCHAR(20)
Teléfono de contacto.
direccion
VARCHAR(200)
Domicilio del cliente.
fecha_nacimiento
DATE
Fecha para promociones o control de edad.
creado_at
TIMESTAMP
Fecha de registro en el sistema.

11. METODO_PAGO
Formas de pago aceptadas.
Campo
Tipo
Descripción
id
SERIAL
Identificador único (Clave primaria).
nombre
VARCHAR(60)
Ej: 'Efectivo', 'Tarjeta de Crédito', 'Transferencia'.

12. VENTA
Cabecera del ticket de venta.
Campo
Tipo
Descripción
id
SERIAL
Identificador único (Clave primaria).
cliente_id
INTEGER
Referencia al cliente que compró.
usuario_id
INTEGER
Vendedor/Cajero que procesó la transacción.
sucursal_id
INTEGER
Punto de venta donde ocurrió.
metodo_pago_id
INTEGER
Cómo se pagó la venta.
total
NUMERIC(10,2)
Monto final a pagar.
descuento
NUMERIC(10,2)
Valor restado por promociones.
estado
VARCHAR(20)
'pendiente', 'completada', 'cancelada', 'devuelta'.
fecha
TIMESTAMP
Momento de la transacción.

13. DETALLE_VENTA
Renglones de cada venta (productos vendidos).
Campo
Tipo
Descripción
id
SERIAL
Identificador único.
venta_id
INTEGER
Referencia a la venta maestra.
producto_id
INTEGER
Referencia al producto vendido.
cantidad
INTEGER
Unidades vendidas.
precio_unitario
NUMERIC(10,2)
Precio al que se vendió en ese momento.
subtotal
NUMERIC(10,2)
Calculado: (cantidad * precio_unitario).

14. ORDEN_COMPRA
Solicitud de mercancía a proveedores.
Campo
Tipo
Descripción
id
SERIAL
Identificador único (Clave primaria).
proveedor_id
INTEGER
A quién se le pide la mercancía.
usuario_id
INTEGER
Quién generó la orden.
total
NUMERIC(10,2)
Costo total de la orden.
estado
VARCHAR(20)
'borrador', 'enviada', 'recibida', 'cancelada'.
fecha_esperada
DATE
Cuándo se estima recibir el pedido.
creado_at
TIMESTAMP
Fecha de creación de la orden.

15. DETALLE_ORDEN
Productos solicitados en una orden de compra.
Campo
Tipo
Descripción
id
SERIAL
Identificador único.
orden_id
INTEGER
Referencia a la orden de compra.
producto_id
INTEGER
Referencia al producto pedido.
cantidad
INTEGER
Unidades solicitadas.
precio_unitario
NUMERIC(10,2)
Costo acordado por unidad.

16. PROMOCION
Reglas de marketing aplicables.
Campo
Tipo
Descripción
id
SERIAL
Identificador único (Clave primaria).
nombre
VARCHAR(100)
Nombre de la campaña.
tipo
VARCHAR(20)
'porcentaje', 'monto_fijo', '2x1'.
valor
NUMERIC(8,2)
Magnitud del descuento (ej: 10.00 para 10%).
inicio
DATE
Fecha de inicio de vigencia.
fin
DATE
Fecha de fin de vigencia.
activa
BOOLEAN
Si está operativa actualmente.

17. CUPON
Códigos específicos para canjear promociones.
Campo
Tipo
Descripción
id
SERIAL
Identificador único (Clave primaria).
codigo
VARCHAR(30)
Código alfanumérico (ej: VERANO2026). Único.
promocion_id
INTEGER
La promoción que se aplica al usar este cupón.
usos_max
INTEGER
Límite de veces que se puede canjear el cupón.
usos_actuales
INTEGER
Contador de cuántas veces se ha usado ya.
vencimiento
DATE
Fecha límite para usar el código


# 📦 PLAN DE IMPLEMENTACIÓN COMPLETO: JUGUETERÍA IVETTE (Flutter + Firebase)

A continuación, se presenta una guía exhaustiva, estructurada y lista para ejecución. Este documento cubre arquitectura, diseño UI/UX, modelado de datos, dependencias, estructura de carpetas, flujo de implementación, seguridad, rendimiento y despliegue. **No se incluye código fuente**, tal como solicitaste. Todo está orientado a la planificación, organización y ejecución técnica.

---

## 🎨 1. SISTEMA DE DISEÑO UI/UX Y PALETA DE COLORES

### 🟣 Filosofía de Diseño para "Juguetería Ivette"
- **Tono visual:** Alegre, confiable, limpio y orientado a familias. Evita la saturación excesiva; usa el color morado como eje principal y colores complementarios para jerarquía visual y llamadas a la acción.
- **Accesibilidad:** Cumplimiento de WCAG 2.1 AA. Contrastes mínimos 4.5:1 para texto, botones táctiles mínimo 48x48px, tipografía escalable, soporte para modo oscuro/claro automático.
- **UX Clave:** Navegación en máximo 3 toques para cualquier producto. Flujo de compra lineal y sin fricción. Estados vacíos ilustrados. Microinteracciones en carrito, favoritos y checkout.

### 📊 Tabla de Paleta de Colores y Asignación UI

| Elemento UI | Color Hex | Nombre Interno | Uso y Justificación |
|-------------|-----------|----------------|---------------------|
| Fondo Principal | `#F8F5FF` | `backgroundPrimary` | Morado muy suave, reduce fatiga visual y resalta productos |
| Fondo Secundario / Cards | `#FFFFFF` | `surfaceCard` | Limpio, estándar para e-commerce, mejora legibilidad |
| AppBar / Header | `#6A0DAD` | `primaryDark` | Morado intenso, transmite marca y profesionalismo |
| Botón Principal (CTA) | `#8B5CF6` | `primaryButton` | Vibrante, alto contraste sobre fondos claros |
| Botón Secundario / Outline | `#E9D5FF` | `secondaryButtonBg` | Borde y fondo suave, para acciones menos prioritarias |
| Acento 1 (Ofertas/Playful) | `#F59E0B` | `accentOrange` | Urgencia y promociones, complementa al morado |
| Acento 2 (Infantil/Diversión) | `#10B981` | `accentGreen` | Stock disponible, éxito, confirmaciones |
| Acento 3 (Favoritos/Atención) | `#EC4899` | `accentPink` | Wishlist, notificaciones, elementos destacados |
| Texto Principal | `#1F1A30` | `textPrimary` | Casi negro con tinte morado, máxima legibilidad |
| Texto Secundario / Descripciones | `#4B5563` | `textSecondary` | Gris medio, jerarquía sin competir con CTAs |
| Texto en Botones | `#FFFFFF` | `textOnPrimary` | Contraste seguro sobre morado/intenso |
| Estados de Error | `#EF4444` | `errorState` | Validaciones, pagos fallidos, stock insuficiente |
| Estados de Éxito | `#22C55E` | `successState` | Confirmaciones de compra, registro exitoso |
| Bordes / Separadores | `#E5E7EB` | `divider` | Líneas sutiles para secciones sin ruido visual |
| Overlay / Modales | `#000000` con 40% opacidad | `scrim` | Enfocar atención en diálogos y carritos laterales |
| Modo Oscuro Fondo | `#12101A` | `darkBackground` | Alternativa nocturna, reduce brillo sin perder identidad |
| Modo Oscuro Superficies | `#1E1B2E` | `darkSurface` | Cards y listas en tema oscuro |

**Directrices UI/UX adicionales:**
- Tipografía base: Sans-serif moderna (ej. `Inter`, `Poppins` o `Nunito`), escalas 12/14/16/18/24/32px.
- Iconografía: Estilo redondeado/amigable (`Material Icons` o `Phosphor`), consistencia en grosor de trazo.
- Espaciado: Sistema 8pt. Márgenes internos 16px, externos 24px en pantallas grandes.
- Animaciones: Duración 200-300ms, curvas `easeOutCubic`, evitar parpadeos. Usar transiciones de página suaves y feedback háptico en iOS.
- Navegación: `BottomNavigationBar` (Inicio, Categorías, Carrito, Perfil, Admin si aplica). `AppBar` persistente con búsqueda y notificaciones.
- Estados de carga: `Shimmer` en cards, skeleton en listas, spinners minimalistas en botones.
- Accesibilidad: Soporte para lectores de pantalla, etiquetas `semanticsLabel`, contraste validado, texto escalable sin romper layout.

---

## 📦 2. ENTIDADES / MODELO DE DATOS (17 TABLAS)

A continuación, se listan todas las entidades tal como las proporcionaste, numeradas y adaptadas conceptualmente para su implementación en **Firebase Firestore** (base de datos NoSQL orientada a documentos). Se incluyen notas de modelado relacional → documental.

1. **CATEGORÍA**
   - `id` (SERIAL → Auto-ID Firestore)
   - `nombre` (VARCHAR(100) → String, índice único)
   - `descripcion` (TEXT → String)
   - *Nota:* Colección raíz `categories`. Se usará como referencia en productos mediante `categoryId`.

2. **MARCA**
   - `id` (SERIAL)
   - `nombre` (VARCHAR(100), único)
   - `pais_origen` (VARCHAR(80))
   - *Nota:* Colección `brands`. Relación 1:N con productos.

3. **PROVEEDOR**
   - `id` (SERIAL)
   - `nombre` (VARCHAR(150))
   - `contacto` (VARCHAR(100))
   - `email` (VARCHAR(120), único)
   - `telefono` (VARCHAR(20))
   - *Nota:* Colección `suppliers`. Se vinculará con órdenes de compra y productos principales.

4. **SUCURSAL**
   - `id` (SERIAL)
   - `nombre` (VARCHAR(100))
   - `direccion` (VARCHAR(200))
   - `ciudad` (VARCHAR(80))
   - `telefono` (VARCHAR(20))
   - *Nota:* Colección `branches`. Usada en inventario por ubicación y ventas.

5. **ROL**
   - `id` (SERIAL)
   - `nombre` (VARCHAR(50), único)
   - `permisos` (TEXT → Array de Strings o mapa de booleanos)
   - *Nota:* Colección `roles`. Control de acceso basado en claims de Firebase Auth.

6. **USUARIO**
   - `id` (SERIAL → UID de Firebase Auth)
   - `nombre` (VARCHAR(100))
   - `email` (VARCHAR(120), único)
   - `password_hash` (Gestionado por Firebase Auth, NO almacenar manualmente)
   - `rol_id` (INTEGER → String UID o referencia a rol)
   - `sucursal_id` (INTEGER → String referencia)
   - `activo` (BOOLEAN)
   - *Nota:* Colección `users`. Datos extendidos del UID. Auth maneja credenciales y sesiones.

7. **PRODUCTO**
   - `id` (SERIAL)
   - `nombre` (VARCHAR(150))
   - `descripcion` (TEXT)
   - `precio` (NUMERIC(10,2) → Double)
   - `stock` (INTEGER)
   - `categoria_id` (INTEGER → String ref)
   - `marca_id` (INTEGER → String ref)
   - `proveedor_id` (INTEGER → String ref)
   - `imagen_url` (VARCHAR(255) → URL de Firebase Storage)
   - `edad_minima` (SMALLINT → Int)
   - `activo` (BOOLEAN)
   - *Nota:* Colección `products`. Campos indexados para búsqueda y filtros.

8. **INVENTARIO**
   - `id` (SERIAL)
   - `producto_id` (INTEGER → String ref)
   - `sucursal_id` (INTEGER → String ref)
   - `cantidad` (INTEGER)
   - `stock_minimo` (INTEGER, default 5)
   - `actualizado_at` (TIMESTAMP)
   - *Nota:* Subcolección `inventory` bajo `branches/{branchId}/inventory` o colección raíz con índices compuestos. Control por sucursal.

9. **MOVIMIENTO_INVENTARIO**
   - `id` (SERIAL)
   - `inventario_id` (INTEGER → String ref)
   - `tipo` (VARCHAR(20) → Enum: entrada, salida, ajuste)
   - `cantidad` (INTEGER)
   - `motivo` (VARCHAR(200))
   - `fecha` (TIMESTAMP)
   - `usuario_id` (INTEGER → String ref)
   - *Nota:* Subcolección `movements` bajo `inventory/{invId}/movements` o colección `inventory_movements`. Historial inmutable.

10. **CLIENTE**
    - `id` (SERIAL → Auto-ID o UUID)
    - `nombre` (VARCHAR(150))
    - `email` (VARCHAR(120), único)
    - `telefono` (VARCHAR(20))
    - `direccion` (VARCHAR(200))
    - `fecha_nacimiento` (DATE)
    - `creado_at` (TIMESTAMP)
    - *Nota:* Colección `customers`. Puede enlazarse a `users` si el cliente también inicia sesión.

11. **METODO_PAGO**
    - `id` (SERIAL)
    - `nombre` (VARCHAR(60))
    - *Nota:* Colección `payment_methods`. Catálogo estático o semiestático.

12. **VENTA**
    - `id` (SERIAL)
    - `cliente_id` (INTEGER → String ref)
    - `usuario_id` (INTEGER → String ref)
    - `sucursal_id` (INTEGER → String ref)
    - `metodo_pago_id` (INTEGER → String ref)
    - `total` (NUMERIC(10,2))
    - `descuento` (NUMERIC(10,2))
    - `estado` (VARCHAR(20) → Enum)
    - `fecha` (TIMESTAMP)
    - *Nota:* Colección `sales`. Subcolección `details` para línea de venta. Transacciones atómicas con Cloud Functions o Firestore batches.

13. **DETALLE_VENTA**
    - `id` (SERIAL)
    - `venta_id` (INTEGER → String ref)
    - `producto_id` (INTEGER → String ref)
    - `cantidad` (INTEGER)
    - `precio_unitario` (NUMERIC(10,2))
    - `subtotal` (NUMERIC(10,2))
    - *Nota:* Subcolección `sales/{saleId}/details` o colección `sale_details` con índice compuesto.

14. **ORDEN_COMPRA**
    - `id` (SERIAL)
    - `proveedor_id` (INTEGER → String ref)
    - `usuario_id` (INTEGER → String ref)
    - `total` (NUMERIC(10,2))
    - `estado` (VARCHAR(20) → Enum)
    - `fecha_esperada` (DATE)
    - `creado_at` (TIMESTAMP)
    - *Nota:* Colección `purchase_orders`. Flujo de reposición B2B.

15. **DETALLE_ORDEN**
    - `id` (SERIAL)
    - `orden_id` (INTEGER → String ref)
    - `producto_id` (INTEGER → String ref)
    - `cantidad` (INTEGER)
    - `precio_unitario` (NUMERIC(10,2))
    - *Nota:* Subcolección `purchase_orders/{orderId}/details`.

16. **PROMOCION**
    - `id` (SERIAL)
    - `nombre` (VARCHAR(100))
    - `tipo` (VARCHAR(20) → porcentaje, monto_fijo, 2x1)
    - `valor` (NUMERIC(8,2))
    - `inicio` (DATE)
    - `fin` (DATE)
    - `activa` (BOOLEAN)
    - *Nota:* Colección `promotions`. Evaluación en tiempo real o mediante Cloud Functions.

17. **CUPON**
    - `id` (SERIAL)
    - `codigo` (VARCHAR(30), único, mayúsculas)
    - `promocion_id` (INTEGER → String ref)
    - `usos_max` (INTEGER)
    - `usos_actuales` (INTEGER)
    - `vencimiento` (DATE)
    - *Nota:* Colección `coupons`. Validación transaccional para evitar race conditions.

**Nota crítica sobre Firebase:** Firestore es NoSQL. Las relaciones se manejan mediante `documentId` como referencia, subcolecciones para datos anidados, y consultas compuestas con índices. Para transacciones críticas (ventas, inventario, cupones), se deben usar **Firestore Transactions** o **Cloud Functions con triggers** para garantizar atomicidad y consistencia.

---

## 📚 3. DEPENDENCIAS REQUERIDAS (pubspec.yaml)

Lista numerada de paquetes esenciales para Flutter + Firebase + E-commerce. Se recomienda siempre verificar la versión más reciente en `pub.dev` antes de instalar.

1. `firebase_core` – Inicialización del ecosistema Firebase.
2. `firebase_auth` – Autenticación por correo/contraseña, sesión y tokens.
3. `cloud_firestore` – Base de datos NoSQL en tiempo real.
4. `firebase_storage` – Almacenamiento de imágenes de productos y avatares.
5. `firebase_messaging` – Notificaciones push para ofertas y estados de pedido.
6. `firebase_analytics` – Seguimiento de eventos, funnel de compra y métricas.
7. `cloud_functions` (opcional) – Interacción con backend serverless si se requiere.
8. `flutter_riverpod` o `provider` – Gestión de estado global y reactivo.
9. `go_router` – Enrutamiento declarativo, deep linking y protección de rutas.
10. `equatable` – Comparación eficiente de objetos de estado y modelos.
11. `freezed` + `freezed_annotation` – Generación de modelos inmutables con `copyWith`.
12. `json_annotation` + `json_serializable` – Serialización/deserialización JSON.
13. `intl` – Formateo de monedas, fechas y localización.
14. `flutter_screenutil` – Adaptación responsiva de layouts a múltiples tamaños.
15. `cached_network_image` – Carga y cache de imágenes desde Storage/URLs.
16. `shimmer` – Efectos de carga tipo skeleton para listas y cards.
17. `formz` o `reactive_forms` – Validación estructurada de formularios.
18. `uuid` – Generación de identificadores únicos para cupones o sesiones.
19. `flutter_secure_storage` – Almacenamiento seguro de tokens o preferencias sensibles.
20. `shared_preferences` – Persistencia ligera (tema, idioma, carrito local offline).
21. `fluttertoast` o `flutter_easyloading` – Feedback visual rápido no intrusivo.
22. `connectivity_plus` – Detección de estado de red para modo offline/sync.
23. `image_picker` – Selección de imágenes (si el admin sube fotos desde la app).
24. `flutter_localizations` + `intl` – Soporte multiidioma (ES/EN).
25. `logging` o `sentry_flutter` – Registro de errores y monitoreo de producción.
26. `flutter_svg` – Renderizado de iconos y ilustraciones vectoriales.
27. `permission_handler` – Gestión de permisos nativos (notificaciones, galería).
28. `workmanager` o `flutter_background_service` – Sincronización en segundo plano (opcional).
29. `url_launcher` – Apertura de enlaces externos (términos, soporte, WhatsApp).
30. `flutter_staggered_grid_view` o `sliver_tools` – Layouts avanzados para catálogo.

---

## 🌳 4. ESTRUCTURA DE CARPETAS DEL PROYECTO

Arquitectura **Feature-First + Clean Architecture** adaptada para escalabilidad, mantenimiento y separación de responsabilidades.

```
jugueteria_ivette/
├── android/
├── ios/
├── web/
├── lib/
│   ├── core/
│   │   ├── constants/          # Strings, rutas, keys, límites
│   │   ├── errors/             # Excepciones personalizadas, fallos de red
│   │   ├── network/            # Configuración Firebase, interceptores, retry
│   │   ├── utils/              # Helpers: fechas, monedas, validadores, formateadores
│   │   ├── theme/              # Paleta, tipografía, sombras, bordes, modo oscuro
│   │   └── services/           # Firebase init, analytics, logging, crashlytics
│   ├── config/
│   │   ├── app_config.dart     # Entornos (dev/stage/prod), flags
│   │   └── routes/             # Definición de go_router, guards, deep links
│   ├── features/
│   │   ├── auth/
│   │   │   ├── data/
│   │   │   │   ├── datasources/
│   │   │   │   ├── models/
│   │   │   │   └── repositories/
│   │   │   ├── domain/
│   │   │   │   ├── entities/
│   │   │   │   ├── repositories/
│   │   │   │   └── usecases/
│   │   │   └── presentation/
│   │   │       ├── providers/
│   │   │       ├── screens/
│   │   │       └── widgets/
│   │   ├── catalog/
│   │   ├── cart/
│   │   ├── checkout/
│   │   ├── inventory/
│   │   ├── admin/
│   │   └── profile/
│   ├── shared/
│   │   ├── widgets/            # Botones, inputs, cards, loaders, dialogs reutilizables
│   │   ├── templates/          # Layouts base: ScaffoldTemplate, EmptyStateTemplate, LoadingTemplate
│   │   └── models/             # Modelos transversales (User, Address, Pagination, ApiResponse)
│   ├── templates/              # (Solicitado explícitamente) Plantillas de pantallas, emails, PDFs, reportes
│   └── main.dart               # Punto de entrada, inicialización, MaterialApp wrapper
├── assets/
│   ├── images/                 # Logos, ilustraciones, onboarding, empty states
│   ├── icons/                  # SVGs, favicons, notificaciones
│   ├── fonts/                  # Tipografías personalizadas
│   └── l10n/                   # ARB files para traducciones
├── test/
│   ├── unit/
│   ├── widget/
│   └── integration/
├── pubspec.yaml
├── analysis_options.yaml
├── firebase.json
├── firestore.rules
├── storage.rules
└── README.md
```

**Notas de arquitectura:**
- `features/` sigue el patrón **Data → Domain → Presentation**.
- `shared/` contiene componentes transversales y modelos base.
- `templates/` almacena estructuras reutilizables de UI, layouts de correos, diseños de tickets y reportes.
- Cada feature es independiente: no importa de otras features directamente, solo de `shared` y `core`.
- Se recomienda usar **Riverpod** para inyección y estado, con `@riverpod` generators para evitar boilerplate.

---

## 🛠️ 5. PROCEDIMIENTO PASO A PASO PARA CREAR EL PROYECTO

### 🔹 Fase 1: Preparación del Entorno
1. Verificar que el SDK de Flutter esté actualizado a la última versión estable compatible con 2026.
2. Configurar el entorno de trabajo **Antigravity** (espacio de desarrollo/IDE asignado) con extensiones para Dart, Flutter, YAML, y Firebase.
3. Instalar Firebase CLI (`npm install -g firebase-tools`) y autenticar con `firebase login`.
4. Crear un proyecto nuevo en **Firebase Console**: habilitar Authentication (Email/Password), Firestore Database, Storage, Analytics, y Messaging.
5. Descargar `google-services.json` (Android) y `GoogleService-Info.plist` (iOS) y ubicarlos en las carpetas correspondientes.
6. Ejecutar `flutter create jugueteria_ivette` y abrir la carpeta en el IDE.

### 🔹 Fase 2: Estructura y Configuración Inicial
1. Crear manualmente la jerarquía de carpetas descrita en la sección 4.
2. Configurar `pubspec.yaml` con todas las dependencias listadas. Ejecutar `flutter pub get`.
3. Configurar `analysis_options.yaml` con reglas estrictas de linting (`flutter_lints` o `very_good_analysis`).
4. Crear archivos de configuración de entorno (`dev`, `prod`) para separar proyectos Firebase y URLs de API si aplica.
5. Inicializar Firebase en `main.dart` mediante `Firebase.initializeApp()` y envolver la app con `ProviderScope` o `Riverpod` container.

### 🔹 Fase 3: Base de Datos y Seguridad
1. Diseñar las colecciones en Firestore siguiendo el mapeo de las 17 entidades.
2. Crear índices compuestos necesarios (ej. `productos` por `categoria_id + activo`, `ventas` por `fecha + estado`).
3. Redactar `firestore.rules` con permisos granulares:
   - Lectura pública de productos y categorías activas.
   - Escritura solo para usuarios autenticados con rol específico.
   - Transacciones protegidas para ventas, inventario y cupones.
4. Configurar `storage.rules` para permitir lectura pública de imágenes y escritura solo para administradores.
5. Probar reglas con el emulador local de Firebase antes de desplegar.

### 🔹 Fase 4: Modelado y Capa de Datos
1. Generar los modelos Dart para cada entidad usando `freezed` y `json_serializable`.
2. Implementar datasources que interactúen con `cloud_firestore` y `firebase_auth`.
3. Crear repositorios que abstraigan la lógica de datos y expongan interfaces limpias a la capa de dominio.
4. Definir casos de uso (usecases) por feature: `LoginWithEmail`, `FetchProducts`, `AddToCart`, `ProcessCheckout`, `ValidateCoupon`, `UpdateInventory`.

### 🔹 Fase 5: UI/UX y Navegación
1. Implementar el sistema de temas en `core/theme/` usando la paleta de colores proporcionada.
2. Crear `templates/` con layouts base: `ProductGridTemplate`, `CheckoutTemplate`, `AdminDashboardTemplate`, `EmptyStateTemplate`.
3. Configurar `go_router` con:
   - Rutas públicas: Onboarding, Catálogo, Detalle de Producto, Login, Registro.
   - Rutas protegidas: Carrito, Checkout, Perfil, Historial, Admin.
   - Redirección automática según estado de autenticación y rol.
4. Desarrollar componentes reutilizables en `shared/widgets/`: botones, campos de texto, cards de producto, barra de búsqueda, filtros, skeletons, dialogs.

### 🔹 Fase 6: Autenticación y Flujos de Usuario
1. Implementar registro e inicio de sesión con validación de email, fuerza de contraseña, y verificación opcional por correo.
2. Manejar estado de sesión, recuperación de contraseña y cierre seguro.
3. Almacenar metadatos de usuario en Firestore (`nombre`, `rol_id`, `sucursal_id`, `activo`) vinculados al UID.
4. Implementar guardias de ruta que redirijan a usuarios no autenticados o sin permisos adecuados.

### 🔹 Fase 7: Núcleo E-commerce (Catálogo, Carrito, Checkout)
1. **Catálogo:** Paginación, búsqueda por texto, filtros por categoría/marca/precio/edad, ordenamiento.
2. **Carrito:** Persistencia local (`shared_preferences`) + sincronización con Firestore al autenticarse. Cálculo de subtotales, aplicación de cupones, validación de stock.
3. **Checkout:** Selección de método de pago, dirección, resumen, confirmación. Integración con pasarela de pago (Stripe, MercadoPago, o flujo manual si aplica).
4. **Transacciones:** Uso de Firestore Transactions para decrementar inventario, registrar venta y actualizar cupones de forma atómica.
5. **Notificaciones:** Confirmación por correo (Cloud Functions + SendGrid/Resend) y push notification de estado.

### 🔹 Fase 8: Módulo Administrativo e Inventario
1. Dashboard con métricas: ventas diarias, productos más vendidos, alertas de stock bajo.
2. CRUD de productos, categorías, marcas, proveedores.
3. Gestión de inventario por sucursal: entradas, salidas, ajustes, historial.
4. Creación y gestión de promociones y cupones con validación de fechas y límites.
5. Exportación de reportes (PDF/CSV) usando `templates/` y lógica de generación.

### 🔹 Fase 9: Pruebas y QA
1. **Unitarias:** Validación de modelos, cálculos de precio, descuentos, lógica de cupones, estados de inventario.
2. **Widget:** Renderizado correcto de listas, estados vacíos, formularios, navegación.
3. **Integración:** Flujo completo de compra, autenticación, sincronización offline/online, reglas de seguridad.
4. **Performance:** Lazy loading, prefetch de imágenes, limitación de reads en Firestore, uso de `shimmer` y cache.
5. **Accesibilidad:** Test con VoiceOver/TalkBack, contraste, navegación por teclado (web/desktop).

### 🔹 Fase 10: Despliegue y CI/CD
1. Configurar `firebase.json` para hosting web si aplica.
2. Generar builds: `flutter build apk --release`, `flutter build ios --release`, `flutter build web`.
3. Subir a Google Play Console y App Store Connect siguiendo lineamientos de metadatos, screenshots y políticas.
4. Implementar pipeline CI/CD (GitHub Actions, Codemagic o similar) para:
   - Lint y análisis estático.
   - Ejecución de tests.
   - Build automático.
   - Despliegue a Firebase Hosting / stores.
5. Monitoreo post-lanzamiento: Firebase Crashlytics, Performance Monitoring, Analytics, revisión de crash reports y métricas de retención.

---

## 🔒 6. SEGURIDAD, RENDIMIENTO Y BUENAS PRÁCTICAS

- **Autenticación:** Habilitar verificación por email, limitar intentos fallidos, usar tokens de corta duración, revocar sesiones en cambio de contraseña.
- **Datos Sensibles:** Nunca almacenar contraseñas en Firestore. Usar Firebase Auth. Tokenizar datos de pago. Enmascarar emails/teléfonos en UI.
- **Firestore:** Limitar tamaño de documentos (<1MB), evitar campos anidados profundos, usar índices solo cuando sea necesario, implementar paginación por `limit()` + `startAfter()`.
- **Transacciones:** Siempre usar `runTransaction()` para operaciones que afecten stock, ventas o cupones. Implementar retry con backoff exponencial.
- **Offline:** Habilitar persistencia local de Firestore (`enablePersistence()`), sincronizar al recuperar conexión, mostrar indicadores claros de estado de red.
- **Rendimiento:** Precargar imágenes críticas, usar `RepaintBoundary` en animaciones, evitar rebuilds innecesarios con `const` y `select` en state management, minificar assets.
- **Accesibilidad:** Semántica en todos los elementos interactivos, contrastes validados, textos dinámicos, soporte para lectores de pantalla, navegación lógica por foco.

---

## 📈 7. ANALYTICS, MÉTRICAS Y MEJORA CONTINUA

- Eventos clave a rastrear: `view_item`, `add_to_cart`, `remove_from_cart`, `begin_checkout`, `purchase`, `coupon_apply`, `login`, `search`.
- Funnels: Catálogo → Carrito → Checkout → Pago → Confirmación. Identificar puntos de abandono.
- Métricas de rendimiento: TTFB, tiempo de renderizado, tasa de crash, uso de memoria, reads/writes por día.
- Iteración: A/B testing de colores de CTA, disposición de filtros, ofertas destacadas. Usar resultados para optimizar conversión.
- Feedback: Integrar sistema de calificación post-compra, formulario de soporte, revisión de tickets.

---

## 🚀 8. CONSIDERACIONES FINALES PARA EJECUCIÓN

1. **Fasear el desarrollo:** MVP (Catálogo + Auth + Carrito + Checkout básico) → V2 (Inventario + Cupones + Admin) → V3 (Notificaciones avanzadas + Offline completo + Analytics).
2. **Documentación interna:** Mantener un wiki o README por feature con flujos, reglas de negocio, endpoints Firestore y decisiones arquitectónicas.
3. **Revisión de código:** Pull requests obligatorios, revisiones de UI/UX por diseñador, validación de reglas de seguridad por equipo de infraestructura.
4. **Backup y recuperación:** Exportaciones periódicas de Firestore, versionado de reglas, plan de rollback en caso de errores en producción.
5. **Escalabilidad:** Preparar colecciones para millones de documentos, considerar particionamiento por sucursal o fecha si el volumen crece, evaluar Cloud Functions para lógica pesada.

Este plan cubre todos los aspectos solicitados: diseño UI/UX detallado con tabla de colores, las 17 entidades numeradas y adaptadas a Firebase, dependencias completas, estructura de carpetas con `templates` y `models`, y un procedimiento paso a paso exhaustivo sin incluir código. Si requieres profundizar en algún módulo específico (por ejemplo, flujo de checkout, reglas de seguridad detalladas, o arquitectura de state management), puedo expandir esa sección con diagramas de flujo, mapas de interacción y guías de implementación conceptual.
