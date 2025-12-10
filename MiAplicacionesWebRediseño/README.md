# Music Player - Rediseño Moderno 🎵

[![Angular](https://img.shields.io/badge/Angular-20.2-red)](https://angular.io/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind-3.x-blue)](https://tailwindcss.com/)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)

> Reproductor de música moderno con diseño completamente renovado, inspirado en las mejores prácticas de UI/UX 2025.

## 🎨 Características del Rediseño

### Diseño Visual
- ✨ **Glassmorphism**: Efectos de vidrio esmerilado en navbar y componentes
- 🌈 **Paleta de Colores Moderna**: Índigo (#6366f1) + Emerald (#10b981)
- 🌓 **Dark/Light Mode**: Toggle funcional con persistencia en localStorage
- 📱 **100% Responsivo**: Mobile-first design con breakpoints optimizados
- 🎭 **Animaciones Suaves**: Transiciones y micro-interacciones fluidas

### Tecnologías
- **Framework**: Angular 20.2 (Standalone Components)
- **Estilos**: Tailwind CSS 3.x via CDN
- **Tipografía**: Poppins + Inter (Google Fonts)
- **Iconos**: SVG personalizados
- **Build**: Angular CLI con Vite

## 🚀 Inicio Rápido

### Prerrequisitos
- Node.js 18+ 
- npm 9+

### Instalación

```bash
# Clonar el repositorio
git clone https://github.com/tuusuario/AplicacionesWeb-Rediseño.git
cd AplicacionesWeb-Rediseño

# Instalar dependencias
npm install

# Iniciar servidor de desarrollo
npm start
```

La aplicación estará disponible en `http://localhost:4200/`

## 📦 Scripts Disponibles

```bash
npm start          # Servidor de desarrollo
npm run build      # Build de producción
npm test           # Ejecutar tests
npm run watch      # Build en modo watch
```

## 🎯 Estructura del Proyecto

```
src/
├── app/
│   ├── app.component.ts          # Componente principal con dark mode
│   ├── sidebar/                  # Sidebar rediseñado
│   ├── player-controls/          # Controles del reproductor
│   ├── search-bar/               # Barra de búsqueda
│   ├── search-results/           # Resultados de búsqueda
│   ├── player-view/              # Vista del reproductor
│   ├── song/                     # Componente de canción
│   └── track-list/               # Lista de tracks
├── styles.css                    # Estilos globales + utilidades
└── index.html                    # HTML principal con Tailwind CDN
```

## 🎨 Paleta de Colores

### Light Mode
- **Primary**: Indigo 500 (#6366f1)
- **Secondary**: Emerald 500 (#10b981)
- **Background**: Slate 50 (#f8fafc)
- **Surface**: White (#ffffff)

### Dark Mode
- **Primary**: Indigo 400 (#818cf8)
- **Secondary**: Emerald 400 (#34d399)
- **Background**: Slate 900 (#0f172a)
- **Surface**: Slate 800 (#1e293b)

## ✨ Características Principales

### Navbar Moderno
- Fixed top con glassmorphism
- Logo con gradiente animado
- Dark mode toggle con iconos SVG
- Hamburger menu responsivo para mobile
- Links con hover effects

### Sidebar (Desktop)
- Diseño minimalista con iconos grandes
- Active states con gradientes
- Hover effects con scale
- Footer decorativo

### Responsive Design
- **Mobile** (< 640px): Hamburger menu, layout vertical
- **Tablet** (640px - 1024px): Sidebar colapsable
- **Desktop** (> 1024px): Sidebar fijo, layout completo

## 🔧 Personalización

### Cambiar Colores
Edita la configuración de Tailwind en `src/index.html`:

```javascript
tailwind.config = {
  theme: {
    extend: {
      colors: {
        primary: { /* tus colores */ },
        secondary: { /* tus colores */ }
      }
    }
  }
}
```

### Agregar Animaciones
Las animaciones personalizadas están en `src/styles.css`:

```css
@keyframes tuAnimacion {
  /* ... */
}
```

## 📱 Compatibilidad

- ✅ Chrome 90+
- ✅ Firefox 88+
- ✅ Safari 14+
- ✅ Edge 90+

## 🤝 Contribuir

Las contribuciones son bienvenidas! Por favor:

1. Fork el proyecto
2. Crea una rama (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add: nueva característica'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

## 📄 Licencia

Este proyecto está bajo la Licencia MIT - ver el archivo [LICENSE](LICENSE) para detalles.

## 🙏 Agradecimientos

- Diseño original: [edsantm/AplicacionesWeb](https://github.com/edsantm/AplicacionesWeb)
- Inspiración UI/UX: Spotify, Apple Music, Deezer
- Iconos: Heroicons
- Fuentes: Google Fonts

## 📸 Screenshots

### Dark Mode
![Dark Mode](screenshots/dark-mode.png)

### Light Mode
![Light Mode](screenshots/light-mode.png)

### Mobile View
![Mobile](screenshots/mobile.png)

---

**Desarrollado con ❤️ usando Angular y Tailwind CSS**
