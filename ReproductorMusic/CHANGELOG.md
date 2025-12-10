# Changelog

Todos los cambios notables en este proyecto serán documentados en este archivo.

El formato está basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/),
y este proyecto adhiere a [Semantic Versioning](https://semver.org/lang/es/).

## [2.0.0] - 2025-12-09

### 🎨 Rediseño Completo de UI/UX

#### Agregado
- **Dark/Light Mode**: Toggle funcional con persistencia en localStorage
- **Glassmorphism**: Efectos de vidrio esmerilado en navbar y componentes clave
- **Navbar Moderno**: Fixed top con blur effect, logo animado y navegación responsiva
- **Mobile Menu**: Hamburger menu con animación slide-down
- **Nueva Paleta de Colores**: 
  - Primary: Indigo (#6366f1)
  - Secondary: Emerald (#10b981)
  - Reemplaza el esquema púrpura original
- **Tipografía Moderna**: Google Fonts (Poppins + Inter)
- **Animaciones**: Transiciones suaves, hover effects, micro-interacciones
- **Sidebar Rediseñado**: Iconos grandes, active states con gradientes
- **Scrollbar Personalizado**: Diseño minimalista con soporte dark mode
- **Responsive Design**: Mobile-first con breakpoints optimizados
- **SEO Mejorado**: Meta tags, descripción, theme-color
- **Accesibilidad**: Focus states, ARIA labels, contraste WCAG AA

#### Cambiado
- **Framework CSS**: Migrado de CSS vanilla a Tailwind CSS 3.x (CDN)
- **Estructura de Layout**: De flexbox básico a grid moderno con glassmorphism
- **Componente App**: Agregada lógica para dark mode y mobile menu
- **Sidebar**: De diseño simple a diseño con cards y efectos hover
- **Colores**: De morado oscuro (#A020F0) a índigo/emerald
- **Fuentes**: De Inter básico a Poppins + Inter con pesos variables
- **Background**: De gradiente simple a gradiente multi-color con blur

#### Mejorado
- **Performance**: Lazy loading, optimización de assets
- **UX**: Feedback visual en todas las interacciones
- **Responsive**: Breakpoints más granulares (sm/md/lg/xl/2xl)
- **Navegación**: Active states más visibles, transiciones suaves
- **Contraste**: Mejor legibilidad en ambos modos (light/dark)

### 🛠️ Cambios Técnicos

#### Agregado
- Tailwind CSS 3.x via CDN
- Configuración personalizada de Tailwind en index.html
- Utilidades CSS custom (glass, card, gradient-text)
- Animaciones con @keyframes (fadeIn, slideUp, scaleIn)
- RouterModule para mejor compatibilidad con Angular 20

#### Cambiado
- Angular actualizado a v20.2
- Componentes standalone (sin NgModules)
- Imports optimizados en app.component.ts
- Estructura de estilos: de variables CSS a clases de Tailwind

#### Removido
- Dependencias locales de Tailwind (conflicto con Angular 20)
- PostCSS config (incompatible con nuevo builder)
- CSS variables antiguas (--bg-color, --sidebar-bg, etc.)
- Estilos inline en index.html

### 📝 Documentación

#### Agregado
- README.md completamente reescrito
- CHANGELOG.md (este archivo)
- ANALISIS_UI.md con análisis del diseño original
- Badges de tecnologías en README
- Sección de screenshots (pendiente de agregar imágenes)
- Guía de contribución
- Instrucciones de personalización

### 🐛 Correcciones

#### Solucionado
- Conflicto de PostCSS con Angular 20 builder
- RouterOutlet import error (cambiado a RouterModule)
- Warnings de Tailwind directives
- Compatibilidad con Node.js 24.x

---

## [1.0.0] - 2024-XX-XX (Original)

### Características Originales
- Reproductor de música básico
- Búsqueda de canciones
- Lista de tracks
- Vista de reproductor
- Diseño con tema púrpura oscuro
- CSS vanilla con variables
- Sidebar básico
- Responsive limitado

---

## Tipos de Cambios

- `Agregado` para nuevas características
- `Cambiado` para cambios en funcionalidad existente
- `Obsoleto` para características que serán removidas
- `Removido` para características removidas
- `Solucionado` para corrección de bugs
- `Seguridad` para vulnerabilidades

---

**Nota**: Este changelog documenta el rediseño completo (v2.0.0) basado en el proyecto original de [edsantm/AplicacionesWeb](https://github.com/edsantm/AplicacionesWeb).
