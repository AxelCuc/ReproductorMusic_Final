# 📚 Documentación Completa del Proyecto - Music Player App

## 📋 Índice
1. [Estructura General del Proyecto](#estructura-general)
2. [Carpeta `/src`](#carpeta-src)
3. [Carpeta `/src/app`](#carpeta-srcapp)
4. [Carpeta `/src/app/services`](#carpeta-services)
5. [Carpeta `/src/app/models`](#carpeta-models)
6. [Componentes de la Aplicación](#componentes)
7. [Carpeta `/src/environments`](#carpeta-environments)
8. [Archivos de Configuración Raíz](#archivos-configuracion)
9. [Flujo de Datos Completo](#flujo-datos)

---

## 🏗️ Estructura General del Proyecto {#estructura-general}

```
MiAplicacionesWebRediseño/
├── src/                          # Código fuente de la aplicación
│   ├── app/                      # Lógica de la aplicación Angular
│   ├── environments/             # Configuración de entornos
│   ├── index.html                # HTML principal
│   ├── main.ts                   # Punto de entrada de la app
│   └── styles.css                # Estilos globales
├── public/                       # Archivos públicos estáticos
├── node_modules/                 # Dependencias instaladas (npm)
├── package.json                  # Configuración del proyecto y dependencias
├── angular.json                  # Configuración de Angular CLI
├── tsconfig.json                 # Configuración de TypeScript
└── README.md                     # Documentación del proyecto
```

---

## 📁 Carpeta `/src` {#carpeta-src}

**Propósito**: Contiene todo el código fuente de la aplicación.

### Archivos Principales:

#### 1. **`index.html`** - Página HTML Principal
```html
<!doctype html>
<html lang="es">
<head>
  <title>Music Player - Reproductor Moderno</title>
  <!-- Tailwind CSS via CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body>
  <app-root></app-root>  <!-- Componente raíz de Angular -->
</body>
</html>
```

**Función**: 
- Es el único archivo HTML que se carga en el navegador
- Contiene el tag `<app-root>` donde Angular inyecta toda la aplicación
- Incluye Tailwind CSS para estilos modernos
- Define meta tags para SEO y responsive design

---

#### 2. **`main.ts`** - Punto de Entrada
```typescript
import { bootstrapApplication } from '@angular/platform-browser';
import { appConfig } from './app/app.config';
import { AppComponent } from './app/app.component';

bootstrapApplication(AppComponent, appConfig)
  .catch((err) => console.error(err));
```

**Función**:
- **Primer archivo** que se ejecuta cuando inicia la app
- Arranca (bootstrap) la aplicación Angular
- Carga el componente raíz `AppComponent`
- Aplica la configuración global `appConfig`

---

#### 3. **`styles.css`** - Estilos Globales
```css
@import url('https://fonts.googleapis.com/css2?family=Poppins...');

/* Utilidades personalizadas */
.glass { /* Efecto glassmorphism */ }
.card { /* Estilos de tarjetas */ }
.gradient-text { /* Texto con gradiente */ }

/* Scrollbar personalizado */
::-webkit-scrollbar { /* ... */ }
```

**Función**:
- Define estilos que aplican a **toda la aplicación**
- Importa fuentes de Google (Poppins, Inter)
- Crea clases utilitarias reutilizables
- Personaliza scrollbars, selección de texto, etc.

---

## 📂 Carpeta `/src/app` {#carpeta-srcapp}

**Propósito**: Contiene toda la lógica de la aplicación Angular.

```
app/
├── services/              # Servicios (lógica de negocio)
├── models/                # Modelos de datos (interfaces/clases)
├── search-bar/            # Componente de búsqueda
├── search-results/        # Componente de resultados
├── sidebar/               # Componente de menú lateral
├── player-controls/       # Componente de controles de reproducción
├── player-view/           # Componente de vista del reproductor
├── song/                  # Componente de canción individual
├── track-list/            # Componente de lista de canciones
├── app.component.ts       # Componente raíz
├── app.config.ts          # Configuración de la app
└── app.routes.ts          # Definición de rutas
```

### Archivos Raíz de `/app`:

#### **`app.component.ts`** - Componente Principal
```typescript
export class AppComponent implements OnInit {
  isDarkMode = true;           // Estado del tema oscuro/claro
  isMobileMenuOpen = false;    // Estado del menú móvil

  ngOnInit() {
    // Carga tema guardado en localStorage
    const savedTheme = localStorage.getItem('theme');
    // Aplica dark mode si corresponde
  }

  toggleDarkMode() {
    // Cambia entre tema claro y oscuro
  }
}
```

**Función**:
- **Componente raíz** que contiene toda la aplicación
- Maneja el estado global del dark mode
- Controla el menú móvil (hamburger menu)
- Se ejecuta primero cuando la app carga

---

#### **`app.routes.ts`** - Configuración de Rutas
```typescript
export const routes: Routes = [
  { path: '', component: TrackList },           // Página principal
  { path: 'search', component: SearchResults }, // Página de búsqueda
  { path: 'player', component: PlayerView },    // Página del reproductor
  { path: '**', redirectTo: '/search' }         // Ruta por defecto
];
```

**Función**:
- Define las **URLs** de la aplicación
- Asocia cada URL con un componente
- Ejemplo: `/search` → muestra `SearchResultsComponent`
- `**` captura rutas no encontradas (404)

---

#### **`app.config.ts`** - Configuración Global
```typescript
export const appConfig: ApplicationConfig = {
  providers: [
    provideRouter(routes),           // Habilita routing
    provideHttpClient(),             // Habilita HTTP requests
    provideAnimations()              // Habilita animaciones
  ]
};
```

**Función**:
- Configura **servicios globales** de Angular
- Habilita el sistema de rutas
- Habilita peticiones HTTP (para llamar a Spotify API)
- Habilita animaciones

---

## 🔧 Carpeta `/src/app/services` {#carpeta-services}

**Propósito**: Contiene la **lógica de negocio** y comunicación con APIs externas.

```
services/
├── auth.ts              # Autenticación con Spotify
├── spotify-api.ts       # Llamadas a la API de Spotify
└── music-state.ts       # Estado global de la música
```

---

### 1. **`auth.ts`** - Servicio de Autenticación

```typescript
@Injectable({ providedIn: 'root' })
export class AuthService {
  private accessTokenSubject = new BehaviorSubject<string>('');
  public accessToken$ = this.accessTokenSubject.asObservable();

  constructor(private http: HttpClient) {
    this.initializeAuth();  // Se autentica automáticamente al iniciar
  }

  authenticate(): Observable<SpotifyTokenResponse> {
    // Envía CLIENT_ID y CLIENT_SECRET a Spotify
    // Recibe access_token válido por 1 hora
    // Programa renovación automática
  }
}
```

**Responsabilidades**:
1. **Autenticación Automática**: Se conecta a Spotify al iniciar la app
2. **Gestión de Tokens**: Guarda y comparte el access token
3. **Renovación Automática**: Renueva el token cada 59 minutos
4. **Manejo de Errores**: Detecta tokens expirados o credenciales inválidas

**Flujo**:
```
App inicia → AuthService constructor
    ↓
initializeAuth()
    ↓
authenticate()
    ↓
POST https://accounts.spotify.com/api/token
Headers: Authorization: Basic [CLIENT_ID:CLIENT_SECRET]
Body: grant_type=client_credentials
    ↓
Spotify responde: { access_token: "BQD4...", expires_in: 3600 }
    ↓
accessTokenSubject.next(token)  ← Otros servicios pueden usarlo
    ↓
scheduleTokenRefresh(3600)  ← Programa renovación en 59 min
```

---

### 2. **`spotify-api.ts`** - Servicio de API de Spotify

```typescript
@Injectable({ providedIn: 'root' })
export class SpotifyApiService {
  private readonly API_URL = 'https://api.spotify.com/v1';

  constructor(
    private http: HttpClient,
    private authService: AuthService
  ) {}

  // Métodos públicos:
  search(query: string, limit: number): Observable<SearchResult>
  getTrack(trackId: string): Observable<Track | null>
  getAlbum(albumId: string): Observable<Album | null>
  getArtist(artistId: string): Observable<Artist | null>
  getAlbumTracks(albumId: string): Observable<Track[]>
  getArtistTopTracks(artistId: string): Observable<Track[]>
}
```

**Responsabilidades**:
1. **Búsqueda**: Buscar canciones, álbumes, artistas
2. **Detalles**: Obtener información específica de tracks/albums/artists
3. **Espera de Token**: No hace peticiones sin token válido
4. **Transformación**: Convierte JSON de Spotify a objetos simples
5. **Manejo de Errores**: Retry automático, mensajes de error claros

**Ejemplo de Uso**:
```typescript
// En cualquier componente:
constructor(private spotifyApi: SpotifyApiService) {}

buscarCanciones() {
  this.spotifyApi.search('Coldplay', 10).subscribe({
    next: (results) => {
      console.log('Canciones:', results.tracks);
      console.log('Álbumes:', results.albums);
      console.log('Artistas:', results.artists);
    },
    error: (error) => console.error('Error:', error)
  });
}
```

---

### 3. **`music-state.ts`** - Servicio de Estado Global

```typescript
@Injectable({ providedIn: 'root' })
export class MusicStateService {
  private currentTrackSubject = new BehaviorSubject<Track | null>(null);
  private currentPlaylistSubject = new BehaviorSubject<Track[]>([]);
  
  public currentTrack$ = this.currentTrackSubject.asObservable();
  public currentPlaylist$ = this.currentPlaylistSubject.asObservable();

  selectTrack(track: Track): void {
    this.currentTrackSubject.next(track);
  }

  selectAlbum(album: Album): void {
    // Obtiene canciones del álbum y las guarda
  }
}
```

**Responsabilidades**:
1. **Estado Compartido**: Comparte datos entre componentes
2. **Canción Actual**: Guarda qué canción está seleccionada
3. **Playlist Actual**: Guarda lista de reproducción
4. **Búsqueda Actual**: Guarda término de búsqueda
5. **Comunicación**: Permite que componentes se comuniquen sin conocerse

**Patrón de Diseño**: **Observer Pattern** con RxJS
```
SearchBar selecciona canción
    ↓
musicState.selectTrack(track)
    ↓
currentTrackSubject.next(track)
    ↓
PlayerView está suscrito a currentTrack$
    ↓
PlayerView recibe la canción automáticamente
    ↓
PlayerView muestra la canción
```

---

## 📊 Carpeta `/src/app/models` {#carpeta-models}

**Propósito**: Define la **estructura de datos** que usa la aplicación.

```
models/
├── track.models.ts        # Modelo de Canción
├── album.model.ts         # Modelo de Álbum
├── artist.model.ts        # Modelo de Artista
└── search-result.model.ts # Modelo de Resultados de Búsqueda
```

---

### **`track.models.ts`** - Modelo de Canción

```typescript
// Interfaz: Define la estructura de una canción
export interface Track {
  id: string;              // "3AJwUDP919kvQ9QcozQPxg"
  name: string;            // "Yellow"
  artistName: string;      // "Coldplay"
  artistId: string;        // "4gzpq5DPGxSnKTe4SA8HAU"
  albumName: string;       // "Parachutes"
  albumId: string;         // "0RHX9XECH8IVI3LNgWDpmQ"
  albumImage: string;      // "https://i.scdn.co/image/..."
  duration: number;        // 266773 (milisegundos)
  previewUrl: string | null; // "https://p.scdn.co/mp3-preview/..."
  uri: string;             // "spotify:track:3AJwUDP919kvQ9QcozQPxg"
  explicit: boolean;       // false
}

// Mapper: Convierte JSON de Spotify a objeto Track
export class TrackMapper {
  static fromSpotifyTrack(spotifyTrack: any): Track {
    return {
      id: spotifyTrack.id,
      name: spotifyTrack.name,
      artistName: spotifyTrack.artists?.[0]?.name || 'Unknown',
      // ... extrae todos los campos del JSON complejo
    };
  }
}
```

**Función**:
- **Interface**: Define qué campos tiene una canción
- **Mapper**: Convierte JSON complejo de Spotify a objeto simple
- **Type Safety**: TypeScript valida que los datos sean correctos

**Ventajas**:
```typescript
// ❌ Sin modelo:
const cancion = response.tracks.items[0].album.images[0].url; // Confuso

// ✅ Con modelo:
const cancion: Track = TrackMapper.fromSpotifyTrack(response);
console.log(cancion.albumImage); // Claro y seguro
```

---

## 🧩 Componentes de la Aplicación {#componentes}

Cada componente tiene 3-4 archivos:
- `.ts` - Lógica (TypeScript)
- `.html` - Interfaz (HTML)
- `.css` - Estilos (CSS)
- `.spec.ts` - Tests (opcional)

---

### 1. **`search-bar/`** - Barra de Búsqueda

**Archivos**:
- `search-bar.ts` - Lógica de búsqueda
- `search-bar.html` - Input y dropdown de resultados
- `search-bar.css` - Estilos del search bar

**Responsabilidades**:
1. Capturar texto que escribe el usuario
2. Hacer búsquedas con debounce (300ms)
3. Mostrar resultados en dropdown
4. Navegar a página de reproductor al seleccionar

**Características Técnicas**:
- **RxJS Operators**: `debounceTime`, `distinctUntilChanged`, `switchMap`
- **Auto-complete**: Muestra resultados mientras escribes
- **Cancelación**: Cancela búsquedas anteriores si escribes rápido

---

### 2. **`search-results/`** - Resultados de Búsqueda

**Responsabilidades**:
1. Mostrar resultados completos de búsqueda
2. Grid responsivo de canciones/álbumes/artistas
3. Filtros y ordenamiento
4. Paginación (si hay muchos resultados)

---

### 3. **`sidebar/`** - Menú Lateral

**Responsabilidades**:
1. Navegación principal (Inicio, Buscar)
2. Logo de la aplicación
3. Links activos (highlight en ruta actual)
4. Responsive (se oculta en mobile)

---

### 4. **`player-controls/`** - Controles de Reproducción

**Responsabilidades**:
1. Botones: Play/Pause, Anterior, Siguiente
2. Barra de progreso de la canción
3. Control de volumen
4. Tiempo actual / duración total

---

### 5. **`player-view/`** - Vista del Reproductor

**Responsabilidades**:
1. Mostrar información de la canción actual
2. Imagen del álbum grande
3. Nombre, artista, álbum
4. Letras (si disponible)
5. Botones de acción (like, compartir, etc.)

---

### 6. **`track-list/`** - Lista de Canciones

**Responsabilidades**:
1. Mostrar lista/tabla de canciones
2. Ordenar por nombre, artista, duración
3. Seleccionar canción para reproducir
4. Mostrar duración, número de pista

---

### 7. **`song/`** - Componente de Canción Individual

**Responsabilidades**:
1. Card de una canción
2. Imagen miniatura
3. Nombre y artista
4. Botón de reproducción
5. Hover effects

---

## 🌍 Carpeta `/src/environments` {#carpeta-environments}

**Propósito**: Configuración específica por entorno (desarrollo/producción).

```
environments/
└── environment.ts
```

### **`environment.ts`**
```typescript
export const environment = {
  production: false,  // ¿Es producción?
  spotify: {
    API_URL: 'https://api.spotify.com/v1',
    AUTH_API_URL: 'https://accounts.spotify.com/api/token',
    CLIENT_ID: 'b340427f88a9479ca7ff7378d87cc306',
    CLIENT_SECRET: '2b7dcfb1d32c4e23a563dd80a7eecb47'
  }
};
```

**Función**:
- **Centraliza configuración**: Todas las URLs y credenciales en un lugar
- **Fácil de cambiar**: Solo editas este archivo para cambiar credenciales
- **Seguridad**: En producción, usarías variables de entorno reales

**Uso en código**:
```typescript
import { environment } from '../../environments/environment';

const apiUrl = environment.spotify.API_URL;  // 'https://api.spotify.com/v1'
```

---

## ⚙️ Archivos de Configuración Raíz {#archivos-configuracion}

### 1. **`package.json`** - Configuración del Proyecto

```json
{
  "name": "music-app-redesign",
  "version": "0.0.0",
  "scripts": {
    "start": "ng serve",      // Inicia servidor de desarrollo
    "build": "ng build",      // Compila para producción
    "test": "ng test"         // Ejecuta tests
  },
  "dependencies": {
    "@angular/core": "^20.2.0",  // Framework Angular
    "rxjs": "~7.8.0",            // Programación reactiva
    "aos": "^2.3.4"              // Animaciones
  }
}
```

**Función**:
- Define **nombre y versión** del proyecto
- Lista **dependencias** necesarias
- Define **scripts** para ejecutar comandos
- Configuración de **prettier** (formateo de código)

---

### 2. **`angular.json`** - Configuración de Angular CLI

```json
{
  "projects": {
    "music-app-redesign": {
      "architect": {
        "build": {
          "options": {
            "browser": "src/main.ts",     // Punto de entrada
            "styles": ["src/styles.css"], // Estilos globales
            "assets": [{ "glob": "**/*", "input": "public" }]
          }
        }
      }
    }
  }
}
```

**Función**:
- Configura cómo Angular CLI **compila** el proyecto
- Define **archivos de entrada** (main.ts, styles.css)
- Configura **optimizaciones** para producción
- Define **budgets** (límites de tamaño de archivos)

---

### 3. **`tsconfig.json`** - Configuración de TypeScript

```json
{
  "compilerOptions": {
    "target": "ES2022",           // Versión de JavaScript objetivo
    "module": "ES2022",           // Sistema de módulos
    "strict": true,               // Modo estricto (más seguro)
    "esModuleInterop": true       // Compatibilidad con módulos
  }
}
```

**Función**:
- Configura cómo TypeScript **compila** a JavaScript
- Define **nivel de strictness** (validaciones)
- Configura **paths** para imports

---

## 🔄 Flujo de Datos Completo {#flujo-datos}

### Escenario: Usuario busca "Coldplay" y reproduce una canción

```
┌─────────────────────────────────────────────────────────────┐
│ 1. INICIO DE LA APLICACIÓN                                 │
└────────────────────┬────────────────────────────────────────┘
                     ↓
┌─────────────────────────────────────────────────────────────┐
│ main.ts                                                     │
│ → bootstrapApplication(AppComponent, appConfig)            │
└────────────────────┬────────────────────────────────────────┘
                     ↓
┌─────────────────────────────────────────────────────────────┐
│ AppComponent (app.component.ts)                            │
│ → ngOnInit() carga tema dark/light                         │
│ → Renderiza navbar, sidebar, router-outlet                 │
└────────────────────┬────────────────────────────────────────┘
                     ↓
┌─────────────────────────────────────────────────────────────┐
│ AuthService (services/auth.ts)                             │
│ → constructor() ejecuta initializeAuth()                   │
│ → authenticate() llama a Spotify                           │
│ → Recibe token: "BQD4O9w3K..."                             │
│ → accessTokenSubject.next(token)                           │
└────────────────────┬────────────────────────────────────────┘
                     ↓
┌─────────────────────────────────────────────────────────────┐
│ 2. USUARIO INTERACTÚA                                      │
│ Usuario escribe "Coldplay" en SearchBar                    │
└────────────────────┬────────────────────────────────────────┘
                     ↓
┌─────────────────────────────────────────────────────────────┐
│ SearchBar (search-bar/search-bar.ts)                       │
│ → onSearch($event) captura texto                           │
│ → searchTerms.next("Coldplay")                             │
│ → Pipeline RxJS:                                           │
│   • debounceTime(300ms)                                    │
│   • distinctUntilChanged()                                 │
│   • switchMap → spotifyApi.search("Coldplay", 3)          │
└────────────────────┬────────────────────────────────────────┘
                     ↓
┌─────────────────────────────────────────────────────────────┐
│ SpotifyApiService (services/spotify-api.ts)                │
│ → search("Coldplay", 3)                                    │
│ → waitForToken() espera token de AuthService              │
│ → http.get('https://api.spotify.com/v1/search')           │
│   Headers: Authorization: Bearer [token]                   │
│   Params: q=Coldplay&type=track,album,artist&limit=3      │
└────────────────────┬────────────────────────────────────────┘
                     ↓
┌─────────────────────────────────────────────────────────────┐
│ Spotify API (externo)                                      │
│ → Procesa búsqueda en su base de datos                    │
│ → Retorna JSON con tracks, albums, artists                │
└────────────────────┬────────────────────────────────────────┘
                     ↓
┌─────────────────────────────────────────────────────────────┐
│ Mappers (models/*.model.ts)                                │
│ → SearchResultMapper.fromSpotifySearch(response)           │
│ → TrackMapper.fromSpotifyTrack() para cada canción        │
│ → AlbumMapper.fromSpotifyAlbum() para cada álbum          │
│ → ArtistMapper.fromSpotifyArtist() para cada artista      │
└────────────────────┬────────────────────────────────────────┘
                     ↓
┌─────────────────────────────────────────────────────────────┐
│ SearchBar recibe resultados                                │
│ → this.searchResults = { tracks: [...], albums: [...] }   │
│ → this.showResults = true                                  │
│ → Angular renderiza dropdown con resultados               │
└────────────────────┬────────────────────────────────────────┘
                     ↓
┌─────────────────────────────────────────────────────────────┐
│ 3. USUARIO SELECCIONA CANCIÓN                              │
│ Usuario hace click en "Yellow - Coldplay"                  │
└────────────────────┬────────────────────────────────────────┘
                     ↓
┌─────────────────────────────────────────────────────────────┐
│ SearchBar                                                   │
│ → selectTrack(track)                                       │
│ → musicState.selectTrack(track)                            │
│ → router.navigate(['/player'])                             │
└────────────────────┬────────────────────────────────────────┘
                     ↓
┌─────────────────────────────────────────────────────────────┐
│ MusicStateService (services/music-state.ts)                │
│ → selectTrack(track)                                       │
│ → currentTrackSubject.next(track)                          │
│ → Notifica a todos los suscriptores                        │
└────────────────────┬────────────────────────────────────────┘
                     ↓
┌─────────────────────────────────────────────────────────────┐
│ Router (app.routes.ts)                                     │
│ → Detecta navegación a '/player'                           │
│ → Carga PlayerView component                              │
└────────────────────┬────────────────────────────────────────┘
                     ↓
┌─────────────────────────────────────────────────────────────┐
│ PlayerView (player-view/)                                  │
│ → ngOnInit() se suscribe a musicState.currentTrack$       │
│ → Recibe track: { name: "Yellow", artist: "Coldplay" }    │
│ → Renderiza información de la canción                      │
│ → Muestra imagen del álbum                                 │
│ → Carga preview de audio (si disponible)                   │
└────────────────────┬────────────────────────────────────────┘
                     ↓
┌─────────────────────────────────────────────────────────────┐
│ 4. REPRODUCCIÓN                                            │
│ Usuario hace click en Play                                 │
└────────────────────┬────────────────────────────────────────┘
                     ↓
┌─────────────────────────────────────────────────────────────┐
│ PlayerControls (player-controls/)                          │
│ → togglePlay()                                             │
│ → audioPlayer.src = track.previewUrl                       │
│ → audioPlayer.play()                                       │
│ → Reproduce preview de 30 segundos                         │
└─────────────────────────────────────────────────────────────┘
```

---

## 📝 Resumen para Presentación

### **Arquitectura del Proyecto**:

1. **Capa de Presentación** (Componentes):
   - `search-bar`, `player-view`, `sidebar`, etc.
   - Manejan la UI y eventos del usuario

2. **Capa de Servicios** (Services):
   - `AuthService`: Autenticación con Spotify
   - `SpotifyApiService`: Comunicación con API
   - `MusicStateService`: Estado global compartido

3. **Capa de Datos** (Models):
   - `Track`, `Album`, `Artist`
   - Mappers para transformar datos

4. **Configuración** (Environments):
   - Credenciales y URLs centralizadas

### **Flujo de Datos**:
```
Usuario → Componente → Servicio → API Externa → Mapper → Componente → UI
```

### **Tecnologías Clave**:
- **Angular 20**: Framework principal
- **RxJS**: Programación reactiva (Observables)
- **TypeScript**: Lenguaje tipado
- **Tailwind CSS**: Framework de estilos
- **Spotify Web API**: Fuente de datos

---

**Esta documentación cubre todos los aspectos importantes del proyecto para una presentación profesional a tu maestro.** 🎓
