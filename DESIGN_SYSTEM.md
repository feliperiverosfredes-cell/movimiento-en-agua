# DESIGN SYSTEM — Movimiento en Agua

> Fuente de verdad para todos los tokens visuales del proyecto.  
> **Regla**: cualquier cambio visual en el código DEBE reflejarse aquí primero o inmediatamente después.  
> Última actualización: 2026-06-19

---

## 1. Tokens de color

Definidos en `:root` en el `<style>` del HTML. Nunca usar valores hex directamente en el markup.

### Paleta principal — Agua / Sky Blue
```css
:root {
  --blue:        #0EA5E9;  /* Azul principal — CTAs, íconos activos */
  --blue-dark:   #0284C7;  /* Azul oscuro — texto logo, hover botones */
  --blue-deeper: #0369A1;  /* Azul profundo — headers sidebar, gradientes */
  --blue-light:  #38BDF8;  /* Azul claro — acentos, trend lines */
  --blue-xlight: #BAE6FD;  /* Azul muy claro — backgrounds de chips */
  --blue-bg:     #F0F9FF;  /* Azul fondo — sections alternadas, cards info */
}
```

### Neutros
```css
:root {
  --white:      #FFFFFF;
  --gray-50:    #F8FAFC;   /* Fondo de página */
  --gray-100:   #F1F5F9;   /* Divisores suaves, fondos input */
  --gray-200:   #E2E8F0;   /* Bordes de cards, inputs */
  --gray-400:   #94A3B8;   /* Texto secundario, placeholders */
  --gray-500:   #64748B;   /* Texto body secundario */
  --gray-700:   #334155;   /* Texto body principal */
  --gray-900:   #0F172A;   /* Texto headings, fondo sidebar */
}
```

### Semánticos (estado)
```css
/* Éxito */
--success:        #10B981;
--success-bg:     #F0FDF4;
--success-border: #BBF7D0;

/* Advertencia */
--warn:           #F59E0B;
--warn-bg:        #FFFBEB;
--warn-border:    #FDE68A;

/* Peligro / Error */
--danger:         #EF4444;
--danger-bg:      #FEF2F2;
--danger-border:  #FECACA;

/* Info */
--info:           #3B82F6;
--info-bg:        #EFF6FF;
--info-border:    #BFDBFE;
```

### Colores de planes
```css
--plan-8:     #0284C7;   /* Plan 8 clases — azul fuerte */
--plan-8-bg:  #DBEAFE;
--plan-4:     #BAE6FD;   /* Plan 4 clases — azul claro */
--plan-4-txt: #0369A1;
--plan-suelta: #FDE68A;  /* Clase suelta — amarillo */
--plan-suelta-txt: #92400E;
--plan-inactivo: #F1F5F9; /* Sin plan */
--plan-inactivo-txt: #94A3B8;
```

### Colores financieros
```css
--fin-ingreso: #15803D;  /* Verde ingresos */
--fin-gasto:   #B91C1C;  /* Rojo gastos */
--fin-neto:    #1D4ED8;  /* Azul utilidad */
--fin-martina: #15803D;  /* 75% Martina */
--fin-mae:     #64748B;  /* 25% MAE */
```

---

## 2. Tipografía

### Fuente
```css
font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', system-ui, sans-serif;
```
Sin dependencias externas. Renderiza como SF Pro en Mac/iOS, Segoe UI en Windows.

### Escala tipográfica
| Token | Valor | Uso |
|-------|-------|-----|
| `--text-xs` | `10px` | Labels de leyenda, fechas secundarias |
| `--text-sm` | `12px` | Texto de tabla, badges, citas |
| `--text-base` | `14px` | Texto de interfaz, nav links |
| `--text-md` | `15-16px` | Párrafos de contenido |
| `--text-lg` | `17-18px` | Párrafos hero, subtítulos sección |
| `--text-xl` | `22-24px` | Títulos de card, subtítulos |
| `--text-2xl` | `28-30px` | Títulos de página, H3 |
| `--text-hero` | `clamp(48px, 8vw, 82px)` | H1 hero landing |
| `--text-section` | `clamp(28px, 4vw, 44px)` | H2 secciones landing |

### Pesos
| Peso | Uso |
|------|-----|
| `500` | Nav links, texto secundario |
| `600` | Labels de formulario, valores de card |
| `700` | Títulos de sección, botones, badges |
| `800` | H1, H2, números KPI, logo |

### Letter spacing
```css
--tracking-tight:  -3px;   /* H1 hero */
--tracking-snug:   -1px;   /* H2 secciones */
--tracking-normal:  0;
--tracking-wide:   1.5px;  /* Section labels mejorados */
--tracking-wider:  2.5px;  /* Section labels pequeños */
--tracking-widest: 2px;    /* Badges uppercase */
```

---

## 3. Espaciado

```css
--space-1:   4px;
--space-2:   8px;
--space-3:  12px;
--space-4:  16px;
--space-5:  20px;
--space-6:  24px;
--space-8:  32px;
--space-10: 40px;
--space-12: 48px;
--space-16: 64px;
--space-20: 80px;
--space-22: 88px;  /* Padding estándar de sección */
```

---

## 4. Border radius

```css
--r-sm:   8px;   /* Inputs, chips pequeños */
--r:      12px;  /* Cards, modales */
--r-lg:   16px;  /* Cards grandes, benefit-card */
--r-xl:   20px;  /* Cards hero, drawer */
--r-2xl:  24px;  /* Login card */
--r-full: 50px;  /* Botones pill, badges pill */
```

---

## 5. Sombras

```css
--sh:    0 4px 24px rgba(14, 165, 233, 0.10);   /* Sombra sutil — cards en reposo */
--sh2:   0 8px 40px rgba(14, 165, 233, 0.18);   /* Sombra elevada — cards hover */
--sh-sm: 0 1px 8px rgba(0, 0, 0, 0.06);         /* Sombra mínima — cards CRM */
--sh-dark: 0 24px 64px rgba(0, 0, 0, 0.25);     /* Sombra modal / login card */
```

---

## 6. Transiciones

```css
--t: 0.2s ease;        /* Hover estándar */
--t-slow: 0.3s ease;   /* Accordions, dropdowns */
--t-spring: 0.25s cubic-bezier(0.22, 1, 0.36, 1);  /* Drawer, modales */
```

---

## 7. Componentes base

### Botones

```css
/* Base */
.btn { padding: 12px 24px; border-radius: var(--r-full); font-size: 15px; font-weight: 600; }

/* Variantes */
.btn-primary { background: var(--blue); color: white; }
.btn-ghost   { background: transparent; color: var(--blue); border: 2px solid var(--blue); }
.btn-danger  { background: var(--danger); color: white; }
.btn-dark    { background: var(--gray-900); color: white; }

/* Tamaños */
.btn-sm  { padding: 8px 16px; font-size: 13px; }
.btn-lg  { padding: 16px 36px; font-size: 17px; }

/* Especiales */
.btn-whatsapp { background: #25D366; }
```

### Cards
```css
/* Landing */
.benefit-card { border-radius: 16px; padding: 22px 16px; box-shadow: var(--sh); }

/* CRM */
.card { background: white; border-radius: var(--r); padding: 28px; box-shadow: var(--sh-sm); }

/* KPI */
.kpi-card { border-radius: 14px; padding: 20px 22px; box-shadow: var(--sh-sm); }

/* Stat box (landing about) */
.stat-box { padding: 20px 10px; border-radius: var(--r); box-shadow: var(--sh); }
```

### Badges / Pills
```css
.badge-pill { padding: 4px 14px; border-radius: 50px; font-size: 12px; font-weight: 600; }

/* Planes */
.badge-plan-8     { background: var(--blue-bg); color: var(--blue-deeper); }
.badge-plan-4     { background: var(--blue-xlight); color: var(--blue-deeper); }
.badge-plan-suelta{ background: var(--warn-bg); color: #92400E; }
.badge-sin-plan   { background: var(--gray-100); color: var(--gray-400); }

/* Estado pago */
.badge-pagado     { background: var(--success-bg); color: var(--fin-ingreso); }
.badge-pendiente  { background: var(--warn-bg); color: #92400E; }
.badge-moroso     { background: var(--danger-bg); color: #991B1B; }
```

### Alerts / Banners
```css
.alert { border-radius: var(--r); padding: 14px 18px; font-size: 14px; border: 1px solid; }
.alert-info    { background: var(--info-bg);    border-color: var(--info-border);    color: #0C4A6E; }
.alert-success { background: var(--success-bg); border-color: var(--success-border); color: #14532D; }
.alert-warn    { background: var(--warn-bg);    border-color: var(--warn-border);    color: #92400E; }
.alert-danger  { background: var(--danger-bg);  border-color: var(--danger-border);  color: #991B1B; }
```

### Formularios
```css
.form-control {
  padding: 12px 16px;
  border: 2px solid var(--gray-200);
  border-radius: 10px;
  font-size: 15px;
  background: var(--gray-50);
}
.form-control:focus { border-color: var(--blue); background: white; }
```

### Section labels (landing)
```css
/* Estándar pequeño */
.section-label {
  font-size: 11px; font-weight: 700;
  letter-spacing: 2.5px; text-transform: uppercase;
  color: var(--blue);
}

/* Mejorado (¿Por qué el agua? / Fundadora) */
.section-label-lg {
  font-size: 16px; font-weight: 700;
  letter-spacing: 1.5px; text-transform: uppercase;
  color: var(--blue);
}
```

---

## 8. Layout

### Grid del dashboard (CRM)
```css
.dash-g3   { grid-template-columns: 1fr 1fr 1fr; }          /* 3 columnas iguales */
.dash-g2   { grid-template-columns: 1fr 1fr; }               /* 2 columnas iguales */
.dash-g32  { grid-template-columns: 1.6fr 1fr; }             /* 60/40 */
.dash-g23  { grid-template-columns: 1fr 1.6fr; }             /* 40/60 */
.kpi-grid-5{ grid-template-columns: repeat(5, 1fr); }        /* 5 KPIs */
```

### Sidebar CRM
```css
.sidebar { width: 250px; background: var(--gray-900); }
/* Móvil: width: 100%, horizontal scroll */
```

### Contenedor landing
```css
.container { max-width: 1080px; margin: 0 auto; }
/* Hero content: max-width: 680px */
/* Blockquotes: max-width: 760px */
```

### Breakpoints
```css
@media (max-width: 768px)  { /* Móvil principal */ }
@media (max-width: 1000px) { /* Tablet — dash colapsa a 2 col */ }
```

---

## 9. Animaciones

```css
/* Fade in (overlay) */
@keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

/* Slide in (drawer) */
@keyframes slideIn {
  from { transform: translateX(100%); }
  to   { transform: translateX(0); }
}

/* Chat panel */
@keyframes chatIn {
  from { opacity: 0; transform: translateY(16px) scale(0.97); }
  to   { opacity: 1; transform: none; }
}
```

---

## 10. Identidad de marca

### Logo
- Archivo: `logo-mea.png`
- **En hero** (fondo oscuro): `filter: brightness(0) invert(1)` — blanco
- **En nav** (fondo blanco): `filter: brightness(0) saturate(100%) invert(37%) sepia(93%) saturate(575%) hue-rotate(182deg) brightness(97%)` — azul igual a `--blue-dark`
- **En login card**: fondo `#0369a1` circular con padding

### Nombre de marca
- Siempre: **Movimiento en Agua** (mayúsculas en cada palabra)
- Abreviación interna: **MEA**
- Hashtag sugerido: `#MovimientoEnAgua`

### Voz y tono
- **Cercana pero profesional** — habla de "tú" a las alumnas
- **Positiva y motivadora** — enfocada en beneficios y bienestar
- **Sin tecnicismos** — el agua es accesible para todas

### Número de WhatsApp
- Siempre: `56940608592` (sin +, sin espacios en los links)
- Formato de display: `+56 9 4060 8592`

---

## 11. Changelog visual

| Fecha | Cambio | Afecta |
|-------|--------|--------|
| 2026-06-19 | Logo nav cambiado a filtro azul `--blue-dark` | nav `.nav-logo img` |
| 2026-06-19 | Section labels "¿Por qué el agua?" y "Fundadora" a 16px | `#beneficios`, `#about` |
| 2026-06-19 | Párrafo hero actualizado | `.hero p` |
| 2026-06-19 | Frase Martina: "El agua" → "El deporte" | Blockquote sección oscura |
| 2026-06-19 | Nav: agregado enlace "Beneficios" | `.nav-links` |
