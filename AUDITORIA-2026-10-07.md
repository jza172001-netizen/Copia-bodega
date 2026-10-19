# Auditoría final — 7-oct-2026 (cerrada el 19-oct)

## Qué se probó y cómo

1. **Pruebas automáticas:** `npm run test` (827 pasan, 0 fallan), `node verificar-lint.cjs`, `npm run build` y `node supabase/verificar-baseline.cjs` (28/28 migraciones sobre una base en blanco más las comprobaciones de accesos, Kardex y `APLICAR-3-OCT.sql`). Todo salió con código 0.
2. **Revisión de código por defectos** en el bloque, los accesos, la cola de escrituras y la API.
3. **Producción, en solo lectura:** políticas, permisos, funciones, migraciones instaladas y Kardex. Los ensayos terminaron en `raise` y se deshicieron solos.
4. **Navegador real** (`tests/navegador/`): Chromium del tamaño de un celular contra un Supabase falso, nunca la base real. Se probaron cuatro recorridos:
   - la entrada a la app;
   - el bloque del 3-oct con FECHA;
   - una FECHA futura, que no envía nada;
   - el formato viejo del bloque.

## Hallazgos, del más grave al menor

1. **CRÍTICO, en producción: las 3 migraciones del 3-oct nunca se aplicaron.** CLAUDE.md, el HANDOFF y yo las dimos por hechas. La última instalada es `accesos_por_el_servidor` (2-oct). Lo que se vio en la base:
   - las tablas tienen `service_access`, así que la llave pública lee y escribe;
   - `authenticate_user` sigue viva;
   - hay 3 claves en texto plano;
   - `anon` puede ejecutar las funciones de stock, `restore_user` y la papelera;
   - el Kardex tiene ítems descuadrados.
2. **Doble envío:** dos escrituras seguidas se mandaban dos veces, porque `withSync` corría al lado de la cola. Lo encontró el recorrido en navegador.
3. **«tubos de 4» se creaba como un ítem llamado «4».**
4. **Se perdía la pulgada** en «brocha de 2», «disco de 7» o «varilla de 3/8».
5. **Dentro de una ENTREGA**, renglones como `OBSERVACIONES:`, `[ACCESORIOS]` o «Juan: 2 palas» se volvían elementos.
6. **`HORA: mañana` se botaba en silencio** y la entrega salía con la hora del momento.
7. **El aviso de categoría salía aunque no cambiara Préstamo/Gasto.**
8. **El renglón 📍 del bloque no mostraba la FECHA.**
9. **El botón «Sí, crear» se escondía** cuando había ítems parecidos.
10. **En el celular, el menú lateral tapaba la pantalla** al entrar.
11. **El indicador «Ítems» contaba solo los que tienen stock.** Ahora se llama «Con stock».
12. **El 19-oct el proyecto de Supabase estaba PAUSADO**, a pesar del latido diario. Se reactivó.

Los hallazgos 2 a 11 están arreglados, cada uno con su prueba. Los de reglas tienen además una prueba de mutación: se deshizo el arreglo a propósito y la prueba se puso roja.

## Producción (lectura del 7-oct)

- 130 ítems, 238 movimientos vivos y 22 préstamos abiertos. El último movimiento es del 2-oct.
- No hay stock negativo.
- **Ensayo del Kardex**, deshecho al terminar: los asientos pasan de 261 a 286 (18 devoluciones viejas más 7 regularizaciones), el stock total sigue en 94 y no queda ningún ítem descuadrado.
- Las 5 funciones de stock de la migración 2 son idénticas, letra por letra, a las instaladas; solo les agrega la guarda.

## Por qué no se aplicó desde acá

El conector de Supabase pide confirmar a mano cada `DROP`. Esa confirmación no aparece en una sesión remota y la orden se corta a los 60 s. Se probó con un `drop policy if exists` de una política que no existía.

Por eso existe **`supabase/APLICAR-3-OCT.sql`**: las tres migraciones textuales en una transacción que se revisa a sí misma. Si algo no queda bien, aborta y no deja nada. Se probó en una base en blanco:

- aborta cuando el Kardex no cuadra;
- aplica todo cuando está bien;
- correrlo dos veces no duplica nada;
- si se le quita a propósito el cierre de la llave pública sobre `app_users`, aborta y lo dice.

## Lo que queda abierto

1. **Juli pega `APLICAR-3-OCT.sql`** en el editor SQL de Supabase. Después hay que comprobarlo en la base.
2. **Revisar el latido** (`/api/latido` y el cron de Vercel), porque el proyecto se pausó igual.
3. **Juli genera los códigos de Kate y Camilo.** Después del paso 1, la clave vieja de Kate deja de servir.
4. **Decisiones de Juli:**
   - la pistola de Héctor;
   - los dos «Estuco tipo 3» gemelos;
   - los 2 préstamos de la lijadora Stanley a nombre de Diego;
   - la Lista 5;
   - la prueba A1–A7 del asistente.
5. **Sin probar en navegador:** Organizar bodega, que queda cubierto por `reorganizar.test`, las devoluciones y dos teléfonos a la vez.
6. **`npm audit`:** 14 avisos. Los que van dentro de la app son `pdfjs-dist` y `mammoth`.
