# App-IA — contexto del proyecto

App-IA (se pronuncia "ápia", App + IA) arma **apps a medida para comercios** de Mar del Plata: panaderías, gimnasios, almacenes, cafeterías. El dueño es Rami. El cliente prueba la app **7 días gratis**, pide mejoras cada día y, si le gusta, paga un abono mensual. Si no paga, la app se bloquea.

Eslogan: **"Tu negocio, en tu mano."** Todo lo que ve el cliente va en **español rioplatense, con voseo**.

## Qué hay en este repo

| Ruta | Qué es |
|---|---|
| `index.html` | Portada de App-IA con el logo y un enlace al brief |
| `brief/` | Brief interactivo (una pregunta por pantalla). Al terminar sugiere un plan y manda el resumen por WhatsApp a Rami (`WA_NUMBER`) |
| `corteza/` | Demo para **Corteza · Pastelería artesanal** (cliente piloto): caja, panel del dueño, equipo, productos y mejoras |
| `assets/` | Logos (variantes con círculo de circuito blanco y dorado) y la guía de venta en PDF |
| `logo-appia.jpg` | Logo que usa la portada |

Se publica con **GitHub Pages** desde `main` / raíz: `https://ramirodavalosmdq-dev.github.io/app-ia/`

## Convenciones

- **Un solo archivo HTML por app**, con CSS y JS adentro, sin paso de compilación. Las fuentes vienen de Google Fonts.
- Pensada para **tablet en el mostrador** y para celular; probar en los dos tamaños (1180×820 y 390×844).
- Antes de cada push, recorrer los flujos con Playwright y revisar que no haya errores en la consola.
- Validar todo lo que se carga (precios > 0, campos obligatorios) y mostrar los errores en la misma pantalla.
- Los documentos para imprimir llevan filas alternadas en gris claro.
- Seguridad: **la menor cantidad de accesos posible**. Cada acceso nuevo se justifica.

## Demo Corteza (estado actual)

- Los datos se guardan en `localStorage` (clave `appia-corteza-v1`), **en un solo dispositivo**.
- Códigos de la demo: Dueño `0000` · Lucía `1111` · Martín `2222` · Sofía `3333` · Carla `4444`.
- Panel → "Cargar una semana de ejemplo" y "▶ Simular ventas en vivo" sirven para mostrarla en el local.
- El catálogo se cargó a partir de fotos reales de las listas de Corteza. Falta confirmar: masas (¿¼ kg o bandeja?), budines, conservas y las etiquetas chicas de las bolsas.
- Identidad visual: verde salvia `#6F8565`, crema `#F7F3EA`, madera `#A47A4F`, tipografía Josefin Sans. Instagram: @cortezamdp.

## Decisiones de producto

- **Caja:** fila de "Más vendidos", categorías, buscador, orden (más vendidos / A–Z / precio / manual). Por kilo: botones de ¼, ½, ¾ y 1 kg, o gramos, o monto. Cobro en un toque con cálculo de vuelto. Plan B: cobrar solo el monto cuando hay fila. Meta: 4 productos en menos de 10 segundos.
- **Panel del dueño, en vivo:** total del día comparado con ayer a la misma hora, efectivo en caja, ventas por hora, ranking de productos, medios de pago, ventas por empleado.
- **Equipo en vivo:** fichaje en la tablet con código de 4 dígitos + foto automática, por sector (Mostrador, Producción, Pastelería, Limpieza). La huella de la tablet no sirve porque no identifica a la persona. Reconocimiento facial: módulo premium para más adelante.
- **Prueba de 7 días:** cartel "Día X de 7". Al vencer, pantalla de bloqueo con botón para activar por WhatsApp.
- **Mejoras diarias:** el cliente anota cambios todo el día. **Corte a las 20 h** y a la mañana siguiente están listos, con el aviso "✨ Tu app se actualizó". Entran ajustes; las funciones nuevas se cotizan aparte.
- **Precios desde una foto (Socio IA):** el dueño saca una foto a la lista y la IA detecta productos y precios. Se muestra antes/después con el %, se puede editar cada uno y se confirma con el botón verde "Realizar cambios".
- **Seguridad y datos:** los datos son del cliente, cifrados, exportables a Excel. Backup cada 24 h, ilimitado, en un almacenamiento separado con bloqueo de retención (planes Pro y Premium).
- **Bóveda Privada (extra):** se cifra en el dispositivo del cliente, se abre con passkey (huella o cara de su celular) y tiene un kit de recuperación impreso. Ni App-IA puede leerla.

## Planes (ARS por mes)

| Plan | Incluye | Precio |
|---|---|---|
| Base | Caja, panel en vivo, reportes | $35.000 |
| Pro | Base + Equipo en vivo + backup diario ilimitado | $50.000 |
| Premium | Pro + Socio IA | $75.000 |

Extras: stock e insumos +$15.000 · facturación ARCA +$12.000 · reconocimiento facial +$10.000 · Bóveda Privada +$9.000 · dispositivo adicional +$5.000. Instalación: $90.000. Pago anual: 2 meses gratis. Ajuste trimestral por IPC. Precio fundador para los primeros 10 comercios.

## Pendientes (por prioridad)

1. **Firebase** (Firestore + Auth): sincronizar en tiempo real la tablet del local y el celular del dueño. Licencias de prueba guardadas en Firestore para activar o bloquear sin tocar el código. Reglas de seguridad por negocio y por rol. Falta que Rami cree el proyecto y pase `firebaseConfig`.
2. **Service worker** con actualización automática y el aviso "✨ Tu app se actualizó", que no recargue en medio de una venta.
3. **Cuenta de GitHub nueva** (por ejemplo `app-ia`) con el repo `app-ia.github.io`, para que los links no muestren el usuario personal. Más adelante, dominio propio (por ejemplo `appia.com.ar`).
4. **Marca en el INPI — PRESENTADA:** "App-IA", acta **N.º 4834102**, fecha de presentación (prioridad) **25/11/2026 18:27** (trámite web 4237638; recibo de ingreso notificado el 26/11/2026). Arancel de una clase pagado el 25/11/2026 ($42.043). Hasta que se conceda: usar "Marca en trámite", no ®. Revisar las notificaciones del portal del INPI: los plazos corren desde el día siguiente a cada notificación. Pendiente: sumar la clase 9 (y la 35, opcional).
5. **Socio IA**: requiere una Cloud Function (plan Blaze) para no exponer la clave de la API. Resumen diario, consejos de producción, preguntas libres y lectura de listas de precios desde una foto.
6. Brief: subir la foto de la lista de precios cuando esté Firebase.
7. Videos institucionales: guiones listos para grabar con voz propia o CapCut.

## Contacto en la app

WhatsApp de App-IA para los briefs y la activación: `5492233467936`.
