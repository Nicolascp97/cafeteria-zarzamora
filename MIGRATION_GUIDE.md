# 🛰️ Guía de Migración: de Vanilla HTML a SaaS Pro (Next.js 14+)

> **Propósito:** Este documento define las reglas exactas para transformar el proyecto "Cafetería Zarzamora" en una aplicación web moderna, escalable y profesional, sirviendo como "Base Maestra" para futuros proyectos.

---

## 🏗️ 1. Preparación del Entorno (Directorio de Trabajo)

Para mantener la base intacta para otros proyectos, los resultados de la migración se organizarán en una estructura modular.

### 📍 Ubicación de la Base (Templates)
Cualquier componente o lógica "base" se guardará en `components/shared/` para ser copiado fácilmente a otros SaaS.

---

## 🛠️ 2. Reglas de Conversión de Arquitectura

### A. De Archivos .html a Rutas Next.js
| Archivo Original | Nueva Ruta (App Router) | Propósito |
| :--- | :--- | :--- |
| `index.html` | `app/(marketing)/page.tsx` | Landing page principal |
| `menu.html` | `app/(shop)/menu/page.tsx` | Menú interactivo cliente |
| `admin.html` | `app/(dashboard)/admin/page.tsx` | ERP / Panel administrativo |

### B. Gestión de Assets (Animaciones)
*   **Frames de Animación:** Los archivos de `cafe_frames/` se moverán a `public/assets/animations/zarzamora/`.
*   **Regla de Oro:** Siempre usar el componente `<Image />` de Next.js para optimización automática.

---

## 🎨 3. Reglas de Diseño & Estilo

### A. Sistema de Diseño (Branding)
Cada proyecto debe iniciar con la creación de `.antigravity/branding.json`.
Para Zarzamora, extraeremos los tokens directamente de los estilos actuales:
*   **Primary:** `#ebb2ff` (Purple)
*   **Secondary:** `#ffdd74` (Gold)
*   **Surface:** `#131313` (Dark)

### B. Tailwind Estrictas
1.  **Eliminar CDN:** Se instala `@tailwindcss/postcss` y `@tailwindcss/forms`.
2.  **Configuración:** Los colores de `menu.html` se inyectan en `tailwind.config.ts`.
3.  **Fuentes:** Usar `next/font/google` para cargar *Noto Serif* e *Inter* sin latencia.

---

## ⚡ 4. Reglas de Lógica & Estado

### A. Carrito de Compras (Base Reutilizable)
Para evitar "código espagueti", el carrito de `menu.html` se migra a un **Store de Zustand**.
*   **Archivo:** `lib/store/use-cart.ts`
*   **Funcionalidades:** Multi-mesa, persistencia en `localStorage`, cálculo de total automático.

### B. Animación Canvas (Apple-Style)
El script de `menu.html` se encapsula en un **Custom Hook** de React:
*   **Archivo:** `hooks/use-scroll-animation.ts`
*   **Regla:** Usar `requestAnimationFrame` y LERP para suavidad cinematográfica.

---

## 🔐 5. Seguridad & Administración

### A. Panel Admin (Dashboard Pro)
El `admin.html` se descompone en:
1.  **Layout Protegido:** `app/(dashboard)/layout.tsx` (verifica login vía NextAuth).
2.  **Componentes shadcn/ui:**
    *   `StatsCard.tsx` (para flujo de barra).
    *   `TablesGrid.tsx` (para gestión de mesas).
    *   `InventoryTable.tsx` (con filtros y estados críticos).

### B. Base de Datos (Persistencia Real)
Sustituir los arrays de JS por **Prisma & Supabase**:
*   **Modelos:** `Order`, `Table`, `Product`, `InventoryItem`.

---

## 📦 6. Guardado de Resultados "Base"

Para que este proyecto sirva de plantilla, seguiremos estas reglas de backup:

1.  **Componentes Atómicos:** Cualquier componente UI generado (ej. un botón premium o una card de producto) se guardará con el prefijo `Base-` en una carpeta de respaldo local.
2.  **Documentación de Lógica:** Cada hook complejo tendrá su propio `README.md` explicando cómo portarlo a otro negocio (ej. Restaurantes, Barberías, etc.).

---

## ✅ Checklist de Ejecución (No Iniciar cambios aún)

1. [ ] Crear nuevo proyecto Next.js en carpeta paralela `zarzamora-pro/`.
2. [ ] Copiar `branding.json` y `designinspo/`.
3. [ ] Instalar `lucide-react`, `framer-motion`, `shadcn/ui`.
4. [ ] Migrar el Hook de Animación Canvas (El corazón visual del menú).
5. [ ] Configurar Rutas y Auth.

---

**Nota Final:** Al seguir estas reglas, transformamos una "página web" en una **Plataforma de Software (SaaS)** profesional que cumple con los estándares globales de Antigravity.
