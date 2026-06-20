# PLAN — Movimiento en Agua · CRM & Landing

> Documento vivo. Actualizar cada vez que se complete una fase, cambie una decisión o se agregue un módulo.  
> Última actualización: 2026-06-19

---

## 1. Estado actual del proyecto

### Lo que existe (funcional)
El proyecto es un único archivo `index.html` auto-contenido con CSS embebido y JavaScript vanilla. Incluye:

| Módulo | Estado | Notas |
|--------|--------|-------|
| Landing page | ✅ Completa | Hero, beneficios, about, horarios, CTA, footer |
| Login | ✅ Funcional | Autenticación por localStorage, rol admin / alumna |
| Dashboard admin | ✅ Funcional | KPIs, vista semanal, ranking, embudo, P&L |
| Módulo Alumnas | ✅ Funcional | CRUD, drawer detalle, historial asistencia |
| Módulo Clases | ✅ Funcional | Horario fijo, registro de asistencia por sesión |
| Planificación | ✅ Funcional | Editor mensual de contenido, export PDF |
| Finanzas | ✅ Funcional | Pagos, gastos, estado de resultado, gráfico anual |
| Documentos | ✅ Funcional | Links/docs compartidos |
| Perfil | ✅ Funcional | Editar bio pública, cambiar contraseña |
| Capital Abeja | ✅ Funcional | Planificador subsidio Sercotec $3.5M |
| Chat asistente | ✅ Funcional | Bot local con respuestas basadas en datos |
| Portal alumna | ✅ Funcional | Mi perfil, mis clases, reservas, documentos |

### Limitaciones actuales
- **Todo en un archivo**: difícil de mantener a largo plazo (>3000 líneas)
- **Sin backend**: datos en localStorage — se pierden al limpiar el browser, no sincronizan entre dispositivos
- **Sin autenticación real**: contraseñas en texto plano en localStorage
- **Sin multiusuario real**: una sola sesión de admin, alumnos con usuarios fijos
- **Sin notificaciones push**: el asistente no puede alertar proactivamente

---

## 2. Arquitectura de la solución

### Decisión de stack: mantenerse en HTML puro (sin framework)
**Razón**: el negocio es pequeño (una instructora, ~20 alumnas), la velocidad de desarrollo es la prioridad, y la app ya funciona. Migrar a React/Vue añadiría complejidad sin beneficio proporcional en este estadio.

**Cuándo reconsiderar**: si se llega a +5 instructoras o se necesita app móvil nativa.

### Persistencia de datos
| Fase | Solución | Cuándo |
|------|----------|--------|
| Actual | `localStorage` | Ya implementado |
| Fase 2 | `Supabase` (Postgres + Auth) | Al tener >1 dispositivo o necesitar backup |
| Fase 3 | API propia | Al escalar a múltiples centros |

### Estructura de archivos objetivo
```
movimiento-en-agua/
├── index.html          # Landing page pública
├── crm/
│   ├── index.html      # App CRM (login → admin/alumna)
│   ├── css/
│   │   └── tokens.css  # Design tokens (variables CSS)
│   └── js/
│       ├── data.js     # Modelo de datos + localStorage
│       ├── auth.js     # Login / roles / sesión
│       ├── dashboard.js
│       ├── students.js
│       ├── classes.js
│       ├── finance.js
│       └── chat.js
├── PLAN.md
├── DESIGN_SYSTEM.md
└── CNAME
```

> **Por ahora**: seguimos en el archivo único hasta que el volumen de código lo justifique. La separación en módulos se hará gradualmente.

---

## 3. Modelo de datos

### Alumna
```json
{
  "id": "uuid",
  "nombre": "string",
  "usuario": "string",
  "password": "string (hash futuro)",
  "email": "string",
  "telefono": "string",
  "fechaIngreso": "YYYY-MM-DD",
  "plan": "clase_suelta | plan_4 | plan_8 | sin_plan",
  "notas": "string",
  "condicionMedica": "string",
  "activo": "boolean"
}
```

### Pago (por mes)
```json
{
  "alumnaId": "uuid",
  "mes": "YYYY-MM",
  "plan": "string",
  "monto": "number",
  "pagado": "boolean",
  "fechaPago": "YYYY-MM-DD | null"
}
```

### Clase / Sesión
```json
{
  "id": "uuid",
  "fecha": "YYYY-MM-DD",
  "hora": "HH:MM",
  "asistentes": ["alumnaId"],
  "notas": "string"
}
```

### Planificación de clase
```json
{
  "fecha": "YYYY-MM-DD",
  "contenido": "string (texto libre)",
  "ejercicios": ["string"]
}
```

### Gasto
```json
{
  "mes": "YYYY-MM",
  "concepto": "string",
  "monto": "number"
}
```

---

## 4. Módulos y features — roadmap detallado

### FASE 1 — Estabilización y UX (prioridad alta) ✍️
> Objetivo: el CRM actual queda pulido, sin bugs, con buena UX en móvil.

- [ ] **Separar landing de CRM** en archivos distintos (`index.html` = landing, `crm/index.html` = app)
- [ ] **Responsive completo del CRM** — sidebar colapsable en móvil, tablas con scroll horizontal
- [ ] **Validación de formularios** — todos los campos requeridos con feedback visual
- [ ] **Confirmaciones de destructivo** — modal de confirmación antes de borrar alumna, clase, gasto
- [ ] **Feedback de guardado** — toast/snackbar al guardar cualquier cambio
- [ ] **Estados vacíos** — pantallas amigables cuando no hay datos (no tabla vacía)
- [ ] **Búsqueda global** — buscador en header del admin para encontrar alumnas rápido
- [ ] **Filtros en listado alumnas** — por plan, estado de pago, actividad reciente
- [ ] **Exportar listado alumnas** — CSV descargable

### FASE 2 — Módulo de comunicaciones
> Objetivo: Martina puede contactar alumnas directamente desde el CRM.

- [ ] **Plantillas WhatsApp** — botones que abren WA con texto pre-armado por cada alumna
  - "Te echamos de menos" (sin clase hace +14 días)
  - "Recordatorio de pago" (morosas)
  - "Felicitaciones por X meses"
  - "Nueva clase disponible"
- [ ] **Log de mensajes enviados** — registro de cuándo se contactó a cada alumna
- [ ] **Notificaciones programadas** — recordatorio en browser (Notification API) para cobros del 1 de cada mes
- [ ] **Resumen semanal** — PDF/impresión de la semana: asistencia + ingresos + alertas

### FASE 3 — Portal alumna mejorado
> Objetivo: alumnas ven su información y reservan clases.

- [ ] **Reserva de clases** — alumna puede reservar su lugar en la próxima sesión (con cupos)
- [ ] **Historial de asistencia visual** — calendario de meses pasados con días asistidos
- [ ] **Estado de cuenta** — alumna ve su plan actual, cuántas clases le quedan, si debe
- [ ] **Perfil editable** — alumna puede actualizar teléfono, condición médica, contraseña
- [ ] **Documentos** — alumna ve los docs que Martina le compartió
- [ ] **Notificación de próxima clase** — recordatorio 24hs antes (browser notification)

### FASE 4 — Analytics y business intelligence
> Objetivo: Martina toma decisiones con datos.

- [ ] **Retención mensual** — % de alumnas que renovaron vs mes anterior
- [ ] **Churn rate** — quiénes no pagaron 2 meses seguidos
- [ ] **LTV por alumna** — ingresos acumulados por alumna
- [ ] **Mejor día/hora** — qué sesión tiene más asistencia
- [ ] **Proyección de ingresos** — si mantiene plan actual, cuánto recauda en 3/6 meses
- [ ] **Comparativa anual** — gráfico mes a mes vs año anterior

### FASE 5 — Infraestructura (cuando el negocio crezca)
> Activar si: +3 instructoras, o se necesita acceso desde múltiples dispositivos.

- [ ] **Backend Supabase** — migrar localStorage a base de datos real
- [ ] **Autenticación segura** — Supabase Auth con JWT
- [ ] **Backups automáticos** — export mensual automático a Google Drive
- [ ] **PWA** — instalar como app en el celular
- [ ] **Múltiples instructoras** — roles: superadmin, instructora, alumna
- [ ] **Múltiples ubicaciones** — Hotel MAE + otros centros
- [ ] **App móvil** — React Native si hay demanda

---

## 5. Flujo de usuario

### Admin (Martina)
```
Landing → "Portal alumnos" → Login → Dashboard
  ├── Ver KPIs del mes
  ├── Alumnas → Ver listado → Abrir drawer → Editar / ver historial
  ├── Clases → Ver próximas → Pasar lista de asistencia
  ├── Planificación → Escribir contenido → Descargar PDF
  ├── Finanzas → Registrar pagos → Ver estado de resultado
  ├── Comunicaciones → Enviar WhatsApp a morosas
  └── Documentos → Subir links
```

### Alumna
```
Landing → "Portal alumnos" → Login → Portal alumna
  ├── Ver perfil y plan actual
  ├── Ver próximas clases
  ├── Reservar clase (Fase 3)
  ├── Ver historial de asistencia
  └── Ver documentos compartidos
```

---

## 6. Estándares de código

### CSS
- Todos los colores, tamaños y sombras deben usar **variables CSS** definidas en `:root` (ver DESIGN_SYSTEM.md)
- Nunca escribir colores hex en línea en el HTML — siempre `var(--token)`
- Clases BEM-like: `.modulo-elemento--modificador`

### JavaScript
- Funciones pequeñas con nombres descriptivos en camelCase
- Todo dato que se guarda en localStorage pasa por `saveData(key, value)` y `loadData(key, default)`
- Nunca acceder a `localStorage` directamente en la lógica de UI

### HTML
- Atributos `id` solo para referencias JS
- Clases CSS para estilos
- `aria-label` en todos los botones de ícono
- Imágenes con `alt` descriptivo

---

## 7. Decisiones de diseño

- **Paleta**: azules derivados de `#0EA5E9` — representa el agua, la frescura, la salud
- **Fuente**: sistema (`-apple-system, BlinkMacSystemFont, 'Segoe UI'`) — sin dependencia externa
- **Bordes**: `border-radius: 12px` (cards), `border-radius: 50px` (pills/botones)
- **Sombras**: dos niveles — `--sh` (sutil) y `--sh2` (elevada)
- **Iconos**: SVG inline o emojis — sin librería externa
- **Breakpoints**: solo un punto de quiebre en `768px`

---

## 8. Convenciones de naming (localStorage)

| Key | Contenido |
|-----|-----------|
| `mea_students` | Array de alumnas |
| `mea_sessions` | Array de sesiones/asistencia |
| `mea_pagos_YYYY-MM` | Pagos del mes |
| `mea_gastos_YYYY-MM` | Gastos del mes |
| `mea_plan_YYYY-MM` | Planificación clases del mes |
| `mea_docs` | Documentos compartidos |
| `mea_bio` | Bio pública de Martina |
| `mea_pass_admin` | Password admin |
| `mea_abeja` | Presupuesto Capital Abeja |
| `mea_logged` | Sesión activa (`admin` / `alumnaId`) |

---

## 9. Checklist antes de cada push a GitHub

- [ ] Probar en Safari (Mac) y Chrome
- [ ] Probar en móvil (iPhone) — resize a 375px
- [ ] No hay console.error en producción
- [ ] Todos los links de WhatsApp tienen el número correcto `56940608592`
- [ ] Las imágenes `hero-pool.jpg`, `martina-foto.jpg`, `logo-mea.png` existen en la raíz
- [ ] El archivo CNAME existe con `movimientoenagua.cl`
- [ ] El DESIGN_SYSTEM.md está actualizado si hubo cambios visuales

---

## 10. Historial de decisiones (ADR ligeros)

| Fecha | Decisión | Razón |
|-------|----------|-------|
| 2026-05 | Un solo archivo HTML | Simplicidad, cero infraestructura |
| 2026-06 | GitHub Pages + Cloudflare | Free tier, HTTPS automático, CDN |
| 2026-06 | Dominio `movimientoenagua.cl` en NIC.cl | Identidad de marca, dominio .cl local |
| 2026-06 | Separar landing de CRM (pendiente) | Mantenibilidad, carga más rápida de landing |
