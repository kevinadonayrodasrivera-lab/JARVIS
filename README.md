WORKSPACE LAUNCHER

Lanzador automático de entorno de trabajo para Windows. Inicia aplicaciones, navegadores y terminales configurados, ubicándolos en los monitores seleccionados — todo con un solo gesto.

MÉTODOS DE LANZAMIENTO:
- Doble aplauso (detección de sonido con red neuronal PANNs CNN14)
- Comando de voz (reconocimiento de voz sin conexión vía Vosk)
- Atajo de teclado (ej. Win+Shift+W)
- Icono en la bandeja del sistema

----------------------------------------------------------------------
CARACTERÍSTICAS
----------------------------------------------------------------------
- Perfiles: prepara diferentes conjuntos de aplicaciones (ej. "Trabajo", "Casa", "Proyecto X") y cambia entre ellos.
- Posicionamiento de ventanas: asigna aplicaciones a monitores específicos, mitades de pantalla (izquierda/derecha) y capas (superpuesta / de fondo).
- Lanzamiento inteligente: detecta aplicaciones en ejecución y simplemente las reposiciona en lugar de iniciarlas de nuevo.
- Reconocimiento de sonido: la red neuronal PANNs CNN14 clasifica sonidos (aplausos, chasquidos, silbidos, golpes y más).
- Comando de voz: sin conexión, sin datos enviados a la nube (modelo Vosk).
- Soporte UWP: detecta e inicia automáticamente aplicaciones de Microsoft Store (Teams, Spotify, etc.).
- GUI de Configuración: editor gráfico para perfiles, aplicaciones y ajustes (customtkinter).
- Inicio automático: inicio opcional al arrancar Windows.

----------------------------------------------------------------------
REQUISITOS
----------------------------------------------------------------------
- Windows 10/11
- Python 3.10+ (para ejecutar desde el código fuente)
- Micrófono (para detección de aplausos y comandos de voz)
- Opcional: Git Bash, AutoHotkey v2

----------------------------------------------------------------------
INSTALACIÓN
----------------------------------------------------------------------
OPCIÓN A: Desde el código fuente (recomendado para desarrolladores)

  git clone https://github.com/YOUR-USER/workspace-launcher.git
  cd workspace-launcher
  pip install -r requirements.txt
  python config_gui.py
  python workspace.py

OPCIÓN B: .exe compilado

  build.bat

  (Salida en la carpeta dist/: WorkspaceLauncher.exe y workspace-config.json. Copia ambos a cualquier computadora, no requiere Python).

----------------------------------------------------------------------
USO
----------------------------------------------------------------------
1. CONFIGURACIÓN (GUI)
Ejecuta: python config_gui.py (o WorkspaceConfig.exe)

Pestañas:
- Apps: añade aplicaciones instaladas o busca el .exe.
- Terminals: añade terminales (Git Bash, PowerShell, CMD) con comandos.
- Settings: sensibilidad del micrófono, atajos, sonido activador, voz.

Opciones por aplicación/terminal:
- Pantalla: Número de monitor (1, 2, 3...)
- Posición: 'full' (completa), 'left' (mitad izquierda), 'right' (mitad derecha)
- Capa: 'Normal', 'On top' (Superpuesta), 'Behind' (De fondo)
- Orden: Prioridad de lanzamiento (mayor = más temprano)
- Minimizar: Iniciar minimizado

2. EJECUTAR EL LANZADOR
Ejecuta: python workspace.py (o WorkspaceLauncher.exe)

La aplicación inicia en la bandeja, carga el modelo de sonido, escucha el micrófono y activa el perfil tras detectar el aplauso/comando.

3. ACTIVACIÓN DEL ESPACIO DE TRABAJO
- Aplauso: 2x aplausos con las manos (por defecto)
- Atajo de teclado: Win+Shift+W (por defecto)
- Comando de voz: Establecido en configuración (ej. "launch")
- Icono de la bandeja: Clic derecho > "Launch: [perfil]"

4. MENÚ DE LA BANDEJA (Clic derecho)
- Launch: [perfil]: inicia el perfil seleccionado.
- Close workspace: cierra todos los procesos iniciados.
- Configuration: abre la GUI de configuración.
- Quit: cierra Workspace Launcher.

----------------------------------------------------------------------
CONFIGURACIÓN (JSON)
----------------------------------------------------------------------
El archivo workspace-config.json es creado por la GUI. 

Opciones principales:
- czulosc_klasniecia: Umbral de volumen del micrófono en dB (40-95)
- hotkey: Atajo de teclado (ej. Win+Shift+W)
- zdarzenie_dzwiekowe: Tipo de sonido (Clapping, Whistling, Knock, etc.)
- liczba_zdarzen: Cuántas veces repetir el sonido (1-3)
- cooldown: Pausa entre lanzamientos en segundos (0-30)
- czulosc_nn: Umbral de confianza de red neuronal (menor = más sensible)
- slowa_kluczowe: Comandos de voz separados por comas
- jezyk_mowy: Idioma de reconocimiento ('pl' o 'en')

----------------------------------------------------------------------
SCRIPTS ADICIONALES
----------------------------------------------------------------------
- clap-trigger.py: Activador de aplauso independiente (sin red neuronal)
- voice-trigger.py: Activador de voz independiente (Google Speech)
- workspace-launcher.ps1: Lanzador de PowerShell
- workspace-hotkey.ahk: Atajos de AutoHotkey v2
- create-shortcut.vbs: Crea acceso directo de inicio
- build.bat: Compila .exe usando PyInstaller

EJEMPLO ACTIVADOR DE APLAUSO:
  python clap-trigger.py
  python clap-trigger.py --calibrate
  python clap-trigger.py --threshold 65 --profile praca --debug

----------------------------------------------------------------------
COMPILACIÓN DE .exe
----------------------------------------------------------------------
Usando PyInstaller directamente:
  pip install pyinstaller
  pyinstaller --onefile --name WorkspaceLauncher --console workspace.py
  pyinstaller --onefile --name WorkspaceConfig --windowed config_gui.py

O usando el script:
  build.bat

----------------------------------------------------------------------
LICENCIA
----------------------------------------------------------------------
MIT