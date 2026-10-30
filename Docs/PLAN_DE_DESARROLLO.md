# HUELLAS DE LUZ — Plan de desarrollo

**Documento de seguimiento permanente.**
**Referencia de diseño:** [`GDD_Huellas_de_luz.md`](GDD_Huellas_de_luz.md) (v2.0). Si el plan y el GDD discrepan, prevalece el GDD; la discrepancia se anota en la sección 3.
**Creado:** 2026-10-29 (revisión inicial, sin implementación).
**Revisión 2:** 2026-10-29 — prioridades, recursos provisionales, arte temprano, pruebas continuas, paquetes, rutas y Git (sin implementación).
**Revisión 3:** 2026-10-29 — corrección de la dependencia circular H5/H6 y de prioridades en T-12.3, T-14.3 y T-15.3.7 (sin implementación).

---

## 0. Cómo usar este documento

### 0.1 Leyenda de estados

| Marca | Significado |
|---|---|
| `- [ ]` | Pendiente. |
| `- [x]` | Completada: cumple **todos** sus criterios de aceptación y las pruebas indicadas se ejecutaron. |
| `- [ ] EN PROGRESO` | Se está trabajando en ella. |
| `- [ ] PENDIENTE DE VERIFICACIÓN` | Implementada (o compila), pero falta la prueba en Unity / build. **No cuenta como completada.** |
| `- [ ] BLOQUEADA — motivo` | No puede avanzar; se indica el motivo y qué la desbloquea. |

Una tarea padre solo se marca `[x]` cuando todas sus subtareas **obligatorias** están `[x]` y las recomendadas u opcionales están `[x]`, `APLAZADA — motivo` o `DESCARTADA — motivo` (ver 0.1.1).

### 0.1.1 Prioridad

Las posibilidades que el GDD enumera como ejemplos o alternativas **no** son requisitos. Cada tarea lleva una etiqueta de prioridad; las subtareas heredan la de su tarea salvo que indiquen otra.

| Etiqueta | Significado |
|---|---|
| `OBL` | Obligatoria: el GDD la exige o sin ella el juego no cumple sus criterios de calidad (GDD §16). |
| `REC` | Recomendada: mejora clara de calidad, robustez o sensación de control; se implementa salvo que el tiempo lo impida. |
| `OPC` | Opcional: alternativa o mejora que solo se implementa si una decisión de diseño la aprueba o sobra tiempo. |

Las tareas `REC` y `OPC` pueden marcarse `APLAZADA` o `DESCARTADA` con motivo y fecha; nunca se eliminan. Las alternativas de diseño (tipos de acertijo, tipos de transformación, etc.) se eligen por región o por ficha; solo se implementan las elegidas.

### 0.2 Reglas de actualización

1. Consultar este plan antes de empezar cualquier trabajo e identificar las tareas relacionadas.
2. Actualizar el estado **solo después** de implementar y verificar.
3. Marcar como completada únicamente si se cumplen todos los criterios de aceptación.
4. Algo que solo está escrito o que compila, pero que requiere prueba de ejecución, queda como `PENDIENTE DE VERIFICACIÓN`.
5. Si una tarea se divide, añadir las nuevas subtareas con identificadores derivados (p. ej. `T-4.2.5`).
6. Si aparece una tarea necesaria nueva, incorporarla en la etapa que corresponda con el siguiente identificador libre. **Los identificadores no se reutilizan.**
7. No eliminar tareas pendientes. Si una tarea se descarta por decisión de diseño, se marca `DESCARTADA — motivo y fecha` y se mantiene en el documento.
8. Al final de cada sesión, añadir una entrada al **Registro de sesiones** (sección 4).
9. Las decisiones de diseño que se tomen se anotan en la sección 2 y, si afectan al diseño, también en el GDD.

### 0.3 Convenciones del proyecto (estado real verificado)

- Editor: **Unity 6000.5.5f1** (Unity 6), URP 17.5.0. Plataforma objetivo: Windows.
- Estructura de carpetas real: `Assets/00_Scenes`, `Assets/01_Scripts/{Camera,Checkpoints,Interaction,Player,Procedural,Quests,Save,World}`, `Assets/02_Prefabs`, `Assets/03_Materials`, `Assets/04_Models`, `Assets/05_Audio`, `Assets/06_UI`, `Assets/07_ScriptableObjects`. Equivale a la organización conceptual del GDD §14 con prefijos numéricos; **no se renombra ninguna carpeta**.
- La documentación vive en **`Docs/`** (D mayúscula), que es como está registrada en Git. El GDD §14 la escribe `docs`; en este plan siempre se usa `Docs/`.
- Sistema de entrada: **Input System 1.19.0**, `activeInputHandler: 1` (solo Input System nuevo). Las APIs de `UnityEngine.Input` antiguas no funcionarán.
- Cinemachine **3.1.7** (API 3.x: `CinemachineCamera`, `CinemachineOrbitalFollow`, etc.; no usar la API 2.x `CinemachineVirtualCamera` / `FreeLook`).

### 0.4 Skills de apoyo por etapa

| Skill | Etapas |
|---|---|
| Unity 6 + C# Developer | 1, 2, 3, 4, 5, 6, 7, 8, 15 |
| Procedural World Generation | 9, 10 |
| Art Director de fantasía 3D | 1.5 y 11 (greybox con T-13.10), 7 (visual), 13; revisión breve en cada hito |
| Level Designer | 3 (ubicación), 8, 11, 12 |
| QA y optimización | Todas (pruebas), 16, 17 |
| Git y gestión del proyecto | 0, 19 (transversal) |

### 0.5 Recursos provisionales

- Movimiento, cámara, checkpoints, guardado, interacción, misiones, acertijos, generador y greyboxes se desarrollan y prueban con **recursos provisionales**: cápsula o maniquí para el protagonista, formas simples para guardián y almas, geometría ProBuilder, materiales de greybox (T-13.10) y sonidos temporales.
- La falta de modelos, animaciones o audio definitivos (D-11) **no bloquea** ningún prototipo ni los hitos H1–H3. Solo bloquea la sustitución por recursos finales (T-2.4.2–T-2.4.4, T-13.7, T-13.8, T-12.4.2) y el acabado de H4 en adelante.
- Los provisionales respetan la **escala y dimensiones** del personaje definitivo previsto (altura y radio de cápsula documentados en T-2.2.10), para que las métricas de nivel no cambien al sustituirlos.
- Todo provisional vive en carpetas o con nombres identificables (sufijo `_Temp`) para poder localizarlo y sustituirlo; los provisionales externos también se registran en `Docs/LICENCIAS.md`.

### 0.6 Dirección artística desde el primer prototipo

- La producción visual definitiva es posterior, pero la **identidad visual y la legibilidad** se consideran desde el greybox: la versión inicial de la guía de arte (T-13.1) y el kit de greybox (T-13.10) se preparan en paralelo a las etapas 1–2.
- Todo greybox usa el código de colores del kit (ruta principal, plataformas obligatorias, interactuables, peligros, zonas apagadas/restauradas), una niebla e iluminación de prueba acordes con el tono frío inicial y vistas lejanas que sugieran destinos.
- Cada hito incluye una revisión breve de legibilidad y coherencia visual con la Skill *Art Director de fantasía 3D*.

### 0.7 Pruebas continuas

- Las pruebas **no empiezan en la etapa 17**. Cada tarea tiene sus pruebas y no se marca completada sin ejecutarlas.
- El registro de errores (T-17.1) y la lista de pruebas funcionales (T-17.3) existen desde la etapa 0 y crecen con cada sistema.
- Cada hito exige una **prueba de regresión** de lo ya terminado (T-17.7) y, desde H2, una **build de verificación** de Windows (T-18.4).
- La etapa 17 agrupa las tareas transversales de calidad y el cierre de calidad previo a H5.

---

## 1. Resumen de etapas y orden de implementación

El orden prioriza construir pronto la **columna vertebral persistente** (identificadores estables + guardado) para que checkpoints, misiones, mecanismos y transformaciones se integren con el guardado desde su creación, y no al final.

| # | Etapa | Depende de | Hito |
|---|---|---|---|
| 0 | Preparación y organización del proyecto | — | |
| 1 | Arquitectura base: estado de juego, IDs estables, eventos, escenas | 0 | |
| 2 | Protagonista: movimiento, salto y cámara (con recursos provisionales) | 1 | **H1: escena de pruebas jugable** |
| 3 | Checkpoints, caídas y reaparición | 2 | |
| 4 | Guardado, carga y continuación (núcleo) | 1, 3 | **H2: salir y continuar desde checkpoint** |
| 5 | Interacción y sistema de diálogos | 2, 4 | |
| 6 | Encargos, objetos y progreso de almas animales | 4, 5 | |
| 7 | Mecanismos, rutas y transformaciones ambientales persistentes | 4, 6 | |
| 8 | Acertijos | 5, 7 | **H3: bucle completo en un prototipo (encargo → transformación → guardado)** |
| 9 | Generador propio de islas flotantes | 2 (para probar), 1 | |
| 10 | Generación procedural secundaria y validaciones | 9, 11.1 | |
| 11 | Diseño de niveles y regiones | 2–8 | **H4: vertical slice (El despertar + Ruinas olvidadas)** |
| 12 | Guardián, narrativa y escenas clave | 5, 6; se desarrolla junto a 11 (cada región integra su parte narrativa) | |
| 13 | Dirección artística, iluminación, materiales y efectos | Guía y kit de greybox (T-13.1, T-13.10): 0. Producción: 7, 11 | |
| 14 | Audio y música | 5, 7, 11 | |
| 15 | Interfaz, menú principal, pausa y opciones | 4 (mínimo), 5, 6 | |
| 16 | Optimización y rendimiento | Medición desde H1; optimización: 11, 13 | |
| 17 | Calidad transversal: registro de errores, regresión, casos límite y cierre | Transversal desde 0; cierre: etapas 0–16 y build candidata T-18.4.4 | **H5: versión completa candidata a entrega** |
| 18 | Build Windows: builds de verificación por hito y entrega final | Builds por hito desde H2; final: H5 | **H6: entrega** |
| 19 | Documentación y control de versiones | Transversal | |

Definición de los hitos:

| Hito | Contenido | Condición para darlo por alcanzado |
|---|---|---|
| H1 | Escena de pruebas jugable con protagonista provisional, salto y cámara. | Criterios de T-2.1–T-2.3 verificados en Play Mode; regresión T-17.7. |
| H2 | Salir del juego y continuar desde el último checkpoint. | Verificado en una build de Windows (T-18.4); regresión. |
| H3 | Bucle completo en un prototipo: encargo → acertijo/mecanismo → transformación → guardado → continuar. | Verificado en build; primera ronda breve con un jugador externo (T-17.5); regresión. |
| H4 | Vertical slice: El despertar + Ruinas olvidadas con identidad visual inicial. | Completable en build; revisión de arte; prueba con jugadores; revisión de alcance. |
| H5 | **Versión completa candidata a entrega**: todas las regiones aprobadas jugables, todas las tareas `OBL` de **desarrollo y contenido** completadas, es decir, todas salvo T-18.1–T-18.3 y el cierre de T-19.1 y T-19.4; recursos definitivos integrados. | Build candidata generada y verificada (T-18.4.4); checklist T-17.3 y casos límite T-17.4 pasados en esa build; regresión completa (T-17.7.5); sin errores críticos ni bloqueantes abiertos; partida completa desde Nueva partida hasta el final. |
| H6 | **Entrega**: configuración final de la build, verificación en equipo limpio y paquete definitivo. | T-18.1, T-18.2 y T-18.3 completadas; cierre de T-19.1 y T-19.4 (etiqueta de la versión entregada). |

Orden de cierre: las tareas `OBL` que **dependen de H5** (T-18.1 → T-18.2 → T-18.3) y el cierre de las tareas transversales que se mantienen hasta la entrega (T-19.1, T-19.4) pertenecen a H6 y no se exigen para declarar H5. Si la verificación de H6 encuentra un error crítico, se corrige en T-17.6, se repite la build candidata (T-18.4.4) y se vuelve a T-18.2; H5 no se reabre salvo que el error obligue a cambiar contenido.

Notas sobre el orden:
- La etapa 15 tiene una parte **mínima temprana** (T-15.1, menú principal con Continuar/Nueva partida) que se desarrolla junto a la etapa 4, porque sin ella no se puede probar la continuación de partida.
- La etapa 9 puede desarrollarse en paralelo a las etapas 3–8 como prototipo aislado.
- Las etapas 13 y 14 tienen tareas tempranas de definición (paletas, referencias, licencias) que pueden empezar ya; la producción de recursos va después del greybox. T-13.1 (versión inicial) y T-13.10 se hacen en paralelo a las etapas 1–2 para que el primer greybox ya sea legible (ver 0.6).
- La ausencia de recursos definitivos no bloquea las etapas 1–10 (ver 0.5).
- Las pruebas son continuas (ver 0.7): las etapas 17 y 18 incluyen tareas que se ejecutan en cada hito, no solo al final.

---

## 2. Decisiones pendientes y decisiones tomadas

### 2.1 Pendientes (bloquean o condicionan tareas)

| ID | Decisión | Afecta a | Estado |
|---|---|---|---|
| D-01 | Significado de «por lo menos un día jugando» (ciclo día/noche, jornada de juego o duración extensa). Confirmar con el docente. | 11, 13 (posible ciclo día/noche), 17 | Pendiente |
| D-02 | Número, tamaño y duración objetivo de las regiones. | 11, 12 | Pendiente |
| D-03 | Estructura de escenas: una escena por región con carga simple, o escena persistente + regiones aditivas. | 1, 4, 11 | Pendiente (propuesta en T-1.4) |
| D-04 | Formato y ubicación del guardado (propuesta: JSON en `Application.persistentDataPath`, una sola partida). | 4 | Pendiente (propuesta en T-4.1) |
| D-05 | Activación de checkpoints: al tocarlos o al interactuar. | 3 | Pendiente |
| D-06 | Interacción: pulsación simple o mantener. El asset de entrada actual define `Interact` con interacción **Hold**, lo que contradice la regla del GDD §6.3 de «una vez por activación». | 2, 5 | Pendiente |
| D-07 | Controles definitivos: solo teclado y ratón, o también mando. | 2, 15 | Pendiente |
| D-08 | Fichas narrativas: guardián, cada alma animal, sus encargos, nombres y diálogos. | 6, 12 | Pendiente |
| D-09 | Cómo y por qué muere el protagonista (el GDD §4.1 dice «después de su muerte, despierta…»). Debe definirse respetando §4.3 (sin presentar el suicidio como solución). | 12 | Pendiente |
| D-10 | Escena final del reencuentro: duración, forma, cámaras. | 12 | Pendiente |
| D-11 | Fuentes de modelos 3D (protagonista, perro, guardián, almas, ruinas), animaciones, texturas, música y efectos, y sus licencias. **No bloquea prototipos** (ver 0.5). | 2.4, 12, 13, 14 | Pendiente |
| D-12 | Comportamiento de cada acertijo al reaparecer/cargar (qué persiste y qué se reinicia). | 3, 4, 8 | Pendiente (se decide por acertijo) |
| D-13 | Plataformas móviles: aprobadas o no, y en qué zonas (el GDD §6.6 las condiciona a aprobación). | 2.2.8, 8, 11 | Pendiente |
| D-14 | Idioma(s) del juego (¿solo español?). | 5, 15 | Pendiente |
| D-15 | Opciones definitivas de audio, vídeo, controles y accesibilidad. | 15 | Pendiente |
| D-16 | Uso de los paquetes instalados que el GDD no menciona (AI Navigation, Timeline, Test Framework, Visual Scripting, Multiplayer Center, collab-proxy) y si Splines debe declararse como dependencia directa. Ningún paquete se añade ni se retira sin aprobación (ver T-0.2). | 0.2, 10.1.4, 12.3, 17.2 | Pendiente |
| D-17 | Si el perro u otras almas acompañan/siguen al jugador (necesitaría navegación/IA). | 6, 12 | Pendiente |
| D-18 | Coleccionables/secretos: si existen, cuántos y si persisten. | 6, 10, 11 | Pendiente |
| D-19 | Equipo objetivo para medir rendimiento y objetivo de FPS/resolución. | 16, 18 | Pendiente |
| D-20 | Qué tipos de acertijo (GDD §6.5) y de transformación (GDD §2) se usarán y en qué región. Son alternativas: solo se implementan las elegidas. | 7.2, 8.1, 11 | Pendiente |
| D-21 | Subcarpetas de scripts adicionales (`Core`, `UI`, `Editor`) y escenas de prueba (`00_Scenes/Tests`): aprobar antes de crearlas (ver T-0.3.5). | 0.3, 1 | Pendiente |
| D-22 | Uso de Git LFS para modelos, texturas y audio. Decidir antes de importar recursos pesados. | 0.6, 13, 14 | Pendiente |
| D-23 | Sistema de UI: uGUI o UI Toolkit (ambos disponibles). | 15 | Pendiente |

### 2.2 Decisiones tomadas

| ID | Decisión | Fecha | Fuente |
|---|---|---|---|
| — | Motor Unity 6, URP, C#, PC Windows, un jugador, tercera persona. | — | GDD |
| — | Sin combate como sistema principal; sin experiencia/niveles/estadísticas. | — | GDD §6.6, §6.7 |
| — | Generador de islas propio en C#; no se usa el asset comercial. | — | GDD §9.4, §13.3 |
| — | Ruta principal, checkpoints, personajes, acertijos principales y transformaciones narrativas se diseñan a mano. | — | GDD §9.2 |
| — | Guardado basado en eventos (no cada frame), con identificadores estables y escritura segura (temporal + reemplazo). | — | GDD §8 |

---

## 3. Hallazgos de la revisión inicial (2026-10-29)

### 3.1 Estado real del repositorio

Comprobado por inspección de archivos (no se abrió el Editor ni se ejecutó Play Mode):

- Proyecto Unity 6000.5.5f1 con URP 17.5.0, dos perfiles de render (`PC_RPAsset`, `Mobile_RPAsset`) y dos niveles de calidad (Mobile, PC; activo por defecto el índice 1 = PC).
- Paquetes (según `Packages/manifest.json` y `Packages/packages-lock.json`):

  | Categoría | Paquetes | Observación |
  |---|---|---|
  | Instalados directamente y previstos por el GDD | Cinemachine 3.1.7, ProBuilder 6.1.4, Terrain Tools 5.3.3, URP 17.5.0, Input System 1.19.0 | Base de las etapas 2, 11 y 13. |
  | Dependencia indirecta | **Splines 2.9.0** (llega por Cinemachine; profundidad 1 en `packages-lock.json`) | Está disponible, pero no figura en el manifiesto. Si Cinemachine se retirara, Splines desaparecería. |
  | Instalados con uso por decidir | Timeline 1.8.12 (posible uso en escenas, T-12.3), Test Framework 1.7.0 (posible uso en T-17.2), uGUI 2.5.0 (posible UI, D-23), AI Navigation 2.0.14 (solo si D-17 lo requiere), Visual Scripting 1.9.11, Multiplayer Center 1.0.1, collab-proxy 2.13.3 | El GDD no los menciona. Ver D-16. |
  | Herramientas de editor | IDE Rider 3.0.38, IDE Visual Studio 2.0.26 | Sin efecto en el juego. |
  | Módulos integrados | `com.unity.modules.*` | Estándar de Unity. |
- Una única escena: `Assets/00_Scenes/SampleScene.unity` (plantilla URP: Main Camera, Directional Light, Global Volume).
- Carpetas de scripts, prefabs, materiales, modelos, audio, UI y ScriptableObjects **creadas pero vacías**. No existe ningún script de juego. Los únicos scripts son los de la plantilla (`Assets/TutorialInfo`).
- `Assets/InputSystem_Actions.inputactions`: asset por defecto de Unity con mapas `Player` (Move, Look, Attack, Interact, Crouch, Jump, Previous, Next, Sprint) y `UI`.
- Git: rama `main`, 2 commits, `.gitignore` de Unity estándar. Remoto `origin` configurado (`https://github.com/molguinf/Huellas-de-luz.git`) y `main` sigue a `origin/main` en el mismo commit según las referencias locales (comprobado con `git remote -v` y `git branch -vv`, sin `fetch`). El push inicial lo indicó la usuaria; no se consultó GitHub directamente.
- Unity: `Asset Serialization: Force Text` (`EditorSettings.asset`, `m_SerializationMode: 2`) y `Visible Meta Files` (`VersionControlSettings.asset`), comprobado por inspección.
- GDD en `Docs/GDD_Huellas_de_luz.md` y `.docx`.

**Nada del GDD está implementado todavía** salvo la preparación base del proyecto (ver etapa 0).

### 3.2 Problemas, contradicciones y riesgos detectados

| # | Tipo | Hallazgo | Acción propuesta |
|---|---|---|---|
| H-01 | Configuración | `EditorBuildSettings` apunta a `Assets/Scenes/SampleScene.unity`, pero la escena está en `Assets/00_Scenes/`. El GUID coincide, por lo que Unity probablemente lo resuelva, pero hay que verificarlo en el Editor. | T-0.3 |
| H-02 | Organización | Existe la carpeta vacía `Assets/Scenes` duplicando a `Assets/00_Scenes`. | T-0.3 |
| H-03 | Dependencias | El GDD §13.2 presenta Splines como instalado; solo llega de forma indirecta por Cinemachine. Funciona, pero si se usa directamente conviene **decidir** si declararlo en el manifiesto (no se cambia sin aprobación). | T-0.2, D-16 |
| H-04 | Entrada | `Interact` usa interacción **Hold**; el GDD pide una activación por pulsación salvo diseño específico. Hay acciones sobrantes (Attack, Crouch, Previous, Next) que no corresponden al diseño. | T-2.1, D-06 |
| H-05 | Dependencias | Paquetes no previstos por el GDD (Visual Scripting, Multiplayer Center, collab-proxy, AI Navigation). El GDD pide evitar dependencias innecesarias. | D-16, T-0.2 |
| H-06 | Configuración | `companyName: DefaultCompany`; afecta a la ruta de `persistentDataPath` y del registro. Debe fijarse **antes** de implementar el guardado para no cambiar la ruta de las partidas después. | T-0.4 |
| H-07 | Residuos | Contenido de plantilla (`Assets/TutorialInfo`, `Readme.asset`, `SampleSceneProfile`) y perfil Mobile, que no es objetivo. | T-0.3 (con aprobación) |
| H-08 | Narrativa | «Después de su muerte» (§4.1) es ambiguo y delicado; debe definirse respetando §4.3. | D-09 |
| H-09 | Alcance | Requisito «un día jugando» indefinido; podría implicar un ciclo día/noche que el GDD no contempla como sistema. | D-01, T-13.9 |
| H-10 | Riesgo técnico | Los IDs estables pueden duplicarse al copiar objetos en el Editor; sin validación, el guardado se corrompe silenciosamente. | T-1.2 (validador) |
| H-11 | Riesgo técnico | Colisionadores de malla de islas generadas: coste y fiabilidad (personaje atascado, bordes). | T-9.5, T-9.7 |
| H-12 | Riesgo de producción | Dependencia de modelos y animaciones externos (personajes, perro). Los prototipos avanzan con provisionales (0.5); sin recursos definitivos solo se bloquea el acabado de H4 en adelante. | D-11, T-13.2, 0.5 |
| H-13 | Riesgo de alcance | Seis regiones con narrativa, acertijos, transformaciones, audio y arte es un alcance grande para un proyecto académico. | Vertical slice (H4) antes de producir más regiones. |
| H-14 | Falta en el GDD | No se definen: animaciones del protagonista, pantalla de carga/transiciones, registro de tiempo jugado, gestión de pérdida de foco de la ventana, comportamiento de diálogos durante la pausa, objetivo actual visible o no. | Tareas en etapas 2, 4, 5, 15 |
| H-15 | Rutas | El GDD §14 escribe la carpeta de documentación como `docs`; en el repositorio es `Docs/`. El plan usa `Docs/`; no se renombra nada. | — |

---

## ETAPA 0 — Preparación y organización del proyecto

### [ ] T-0.1 — Verificación del entorno base
- **Prioridad:** `OBL`
- **Descripción:** Confirmar versión de editor, pipeline, plataforma y que el proyecto abre sin errores.
- **Subtareas:**
  - [x] T-0.1.1 Confirmar versión de editor (6000.5.5f1) en `ProjectVersion.txt`.
  - [x] T-0.1.2 Confirmar URP asignado en Graphics/Quality (`PC_RPAsset`, `Mobile_RPAsset`).
  - [x] T-0.1.3 Confirmar Input System activo como único manejador (`activeInputHandler: 1`).
  - [ ] T-0.1.4 Abrir el proyecto en el Editor y comprobar consola sin errores ni advertencias.
  - [ ] T-0.1.5 Confirmar que la plataforma activa de build es Windows (Standalone).
- **Dependencias:** —
- **Criterios de aceptación:** El proyecto abre sin errores en la consola; plataforma Windows activa.
- **Pruebas:** Abrir el Editor, limpiar consola, entrar y salir de Play Mode con `SampleScene`.

### [ ] T-0.2 — Revisión de paquetes
- **Prioridad:** `OBL`
- **Descripción:** Distinguir paquetes instalados, dependencias indirectas y herramientas cuyo uso falta decidir (ver tabla en 3.1). **No se añade ni se elimina ningún paquete automáticamente**: cualquier cambio del manifiesto requiere aprobación explícita y se anota en 2.2.
- **Subtareas:**
  - [x] T-0.2.1 Inventariar paquetes y versiones, clasificados por categoría (ver 3.1).
  - [ ] T-0.2.2 Decidir si Splines se declara como dependencia directa cuando se use directamente (H-03, D-16). Hasta entonces se usa la versión indirecta 2.9.0.
  - [ ] T-0.2.3 Decidir, paquete por paquete, el uso de Timeline, Test Framework, uGUI, AI Navigation, Visual Scripting, Multiplayer Center y collab-proxy (D-16). Mantener, usar o proponer retirar; retirar solo con aprobación.
  - [ ] T-0.2.4 Verificar en el Editor que Cinemachine, ProBuilder, Terrain Tools y Splines cargan sin errores (abrir sus menús/ventanas).
- **Dependencias:** T-0.1
- **Criterios de aceptación:** Cada paquete tiene un uso decidido y anotado (usado / por usar en una tarea concreta / propuesto para retirar); ningún cambio del manifiesto se hizo sin aprobación; sin errores de paquetes en consola.
- **Pruebas:** Revisar consola y Package Manager. Si se aprueba un cambio del manifiesto: reabrir el proyecto, revisar consola y repetir la build de humo (T-0.5).

### [ ] T-0.3 — Limpieza y organización de escenas y carpetas
- **Prioridad:** `OBL`
- **Descripción:** Corregir la referencia de Build Settings y eliminar duplicados/residuos con aprobación.
- **Subtareas:**
  - [x] T-0.3.1 Crear estructura de carpetas numeradas en `Assets/` (existente).
  - [ ] T-0.3.2 Verificar en Build Settings qué ruta muestra la escena (H-01) y corregirla.
  - [ ] T-0.3.3 Decidir y, con aprobación, eliminar `Assets/Scenes` vacía (H-02).
  - [ ] T-0.3.4 Decidir y, con aprobación, eliminar contenido de plantilla `TutorialInfo`/`Readme.asset` (H-07).
  - [ ] T-0.3.5 Subcarpetas adicionales mínimas (D-21). Se conservan todas las carpetas existentes y se reparte el código según el GDD §14: diálogos en `01_Scripts/Interaction`; mecanismos, acertijos y transformaciones en `01_Scripts/World`; islas y decoración procedural en `01_Scripts/Procedural`. Solo se proponen, y se crean **cuando se necesite el primer archivo** y con aprobación:
    - `01_Scripts/Core`: arranque, estado de juego, identificadores persistentes, eventos, escenas y servicio de audio. El GDD no prevé carpeta para estos servicios transversales y no encajan en ninguna existente.
    - `01_Scripts/UI`: lógica de menús y HUD. `06_UI` es para recursos de interfaz (GDD §14), no para scripts.
    - `01_Scripts/Editor`: herramientas de Editor (validadores, botones del generador). Unity exige que el código de Editor esté en una carpeta `Editor` para excluirlo de la build.
    - `00_Scenes/Tests`: escenas de prueba (sandbox, generador) separadas de las escenas que entran en la build. Las regiones van directamente en `00_Scenes`.
    - No se crean `Dialogue`, `Audio` ni `Regions`: su contenido cabe en carpetas existentes.
  - [ ] T-0.3.6 Definir convención de nombres (scripts, prefabs, IDs persistentes, escenas) y documentarla en `Docs/CONVENCIONES.md`.
- **Dependencias:** T-0.1
- **Criterios de aceptación:** Build Settings apunta a escenas existentes; carpetas duplicadas resueltas según la decisión aprobada; ninguna carpeta existente renombrada; convención documentada.
- **Pruebas:** Abrir Build Settings; hacer una build de prueba vacía (T-0.5).

### [ ] T-0.4 — Configuración del Player
- **Prioridad:** `OBL`
- **Descripción:** Fijar identidad del producto antes de implementar el guardado (H-06).
- **Subtareas:**
  - [ ] T-0.4.1 Definir `companyName` y `productName` definitivos.
  - [ ] T-0.4.2 Configurar resolución por defecto, modo ventana/pantalla completa, `Run In Background` según diseño.
  - [ ] T-0.4.3 Icono provisional y versión (`bundleVersion`, actualmente 0.1.0).
- **Dependencias:** T-0.1
- **Criterios de aceptación:** Valores fijados y anotados en la sección 2.2.
- **Pruebas:** Comprobar `Application.persistentDataPath` en un log de prueba.

### [ ] T-0.5 — Build de humo temprana
- **Prioridad:** `OBL`
- **Descripción:** Comprobar desde el inicio que el proyecto genera un ejecutable Windows.
- **Subtareas:**
  - [ ] T-0.5.1 Generar build de la escena vacía en una carpeta ignorada (`Builds/`).
  - [ ] T-0.5.2 Ejecutar el `.exe` y cerrar sin errores.
- **Dependencias:** T-0.3, T-0.4
- **Criterios de aceptación:** El ejecutable abre y cierra correctamente.
- **Pruebas:** Ejecución manual de la build; revisar `Player.log`.

### [ ] T-0.6 — Flujo de Git
- **Prioridad:** `OBL`
- **Descripción:** Establecer forma de trabajo con ramas y commits.
- **Subtareas:**
  - [x] T-0.6.1 Repositorio Git con `.gitignore` de Unity y commits iniciales.
  - [x] T-0.6.2 Remoto en GitHub configurado y push inicial realizado. *Evidencia:* `origin` → `https://github.com/molguinf/Huellas-de-luz.git` y `main` sigue a `origin/main` en `683eeae` según las referencias locales (`git remote -v`, `git branch -vv`, 2026-10-29). El push lo indicó la usuaria; no se hizo `fetch` ni se consultó GitHub.
  - [ ] T-0.6.3 Evaluar Git LFS para modelos, texturas y audio antes de importar recursos pesados (D-22).
  - [x] T-0.6.4 Unity configurado con `Asset Serialization: Force Text` y `Version Control: Visible Meta Files`. *Evidencia:* inspección de `ProjectSettings/EditorSettings.asset` (`m_SerializationMode: 2`) y `ProjectSettings/VersionControlSettings.asset` (`m_Mode: Visible Meta Files`).
  - [ ] T-0.6.5 Acordar convención de ramas (`feature/…`, `fix/…`) y mensajes de commit.
  - [ ] T-0.6.6 Primer push desde una rama de trabajo (p. ej. este plan) para confirmar el flujo completo rama → push → integración en `main`.
- **Dependencias:** —
- **Criterios de aceptación:** Convención documentada; remoto operativo; LFS decidido.
- **Pruebas:** Crear rama de prueba, commit y push (T-0.6.6).

---

## ETAPA 1 — Arquitectura base

### [ ] T-1.1 — Arranque y estado global del juego
- **Prioridad:** `OBL`
- **Descripción:** Punto de entrada único con servicios básicos (estado de juego, pausa, guardado, escenas).
- **Subtareas:**
  - [ ] T-1.1.1 Escena o prefab de arranque (`Bootstrap`) que inicializa servicios persistentes (`DontDestroyOnLoad` o escena persistente según D-03).
  - [ ] T-1.1.2 Máquina de estados de juego: `MainMenu`, `Loading`, `Playing`, `Paused`, `Dialogue`, `Cutscene`.
  - [ ] T-1.1.3 Política de `Time.timeScale` y bloqueo de entrada por estado.
  - [ ] T-1.1.4 Garantizar que entrar en Play Mode desde cualquier escena de región funciona (inicialización automática para pruebas).
- **Dependencias:** T-0.3
- **Criterios de aceptación:** Un único conjunto de servicios existe en cualquier flujo; cambiar de estado bloquea/desbloquea la entrada correctamente.
- **Pruebas:** Play desde la escena de arranque y desde una escena de región; recargar escena y comprobar que no se duplican servicios.

### [ ] T-1.2 — Identificadores persistentes estables
- **Prioridad:** `OBL`
- **Descripción:** Componente de ID estable para todo elemento persistente (checkpoint, misión, mecanismo, transformación, objeto). Base de todo el guardado (GDD §8.3).
- **Subtareas:**
  - [ ] T-1.2.1 Componente `PersistentId` con ID serializado (GUID o texto legible) que no cambia al recargar.
  - [ ] T-1.2.2 Herramienta de Editor que detecta IDs vacíos o duplicados en las escenas (H-10).
  - [ ] T-1.2.3 `REC` Regenerar ID automáticamente al duplicar un objeto en el Editor, sin cambiarlo en instancias existentes. Sin esta mejora, el validador T-1.2.2 permite corregir duplicados a mano.
  - [ ] T-1.2.4 IDs de datos (misiones, objetos) definidos en ScriptableObjects con ID propio.
- **Dependencias:** T-1.1
- **Criterios de aceptación:** Los IDs sobreviven a cerrar/abrir el Editor; el validador informa de duplicados; si se implementa T-1.2.3, duplicar un objeto genera un ID nuevo.
- **Pruebas:** Duplicar objetos, reabrir escena, ejecutar validador con un duplicado forzado.

### [ ] T-1.3 — Bus de eventos de juego
- **Prioridad:** `OBL`
- **Descripción:** Eventos desacoplados para checkpoint activado, misión actualizada, transformación completada, ruta desbloqueada, región entrada, hito narrativo. El guardado automático se suscribe a ellos.
- **Subtareas:**
  - [ ] T-1.3.1 Definir eventos (C# events o canales ScriptableObject).
  - [ ] T-1.3.2 Registrar/desregistrar correctamente en `OnEnable`/`OnDisable`.
- **Dependencias:** T-1.1
- **Criterios de aceptación:** Los suscriptores reciben eventos sin referencias directas entre sistemas; sin fugas al cambiar de escena.
- **Pruebas:** Prueba en Play Mode con suscriptor de log; cambiar de escena y verificar que no hay llamadas a objetos destruidos.

### [ ] T-1.4 — Gestión de escenas y transiciones
- **Prioridad:** `OBL`
- **Descripción:** Cargar regiones, transiciones con fundido y punto de entrada por región (D-03).
- **Subtareas:**
  - [ ] T-1.4.1 Proponer y aprobar estructura de escenas (D-03).
  - [ ] T-1.4.2 Servicio de carga asíncrona con pantalla/fundido de transición.
  - [ ] T-1.4.3 Puntos de entrada/salida de región con ID estable.
  - [ ] T-1.4.4 Bloquear guardado y entrada durante la carga.
- **Dependencias:** T-1.1, T-1.2
- **Criterios de aceptación:** Se puede pasar de una región a otra y volver sin errores ni objetos duplicados.
- **Pruebas:** Ir y volver entre dos escenas de prueba varias veces; revisar consola.

### [ ] T-1.5 — Escena de pruebas (sandbox)
- **Prioridad:** `OBL`
- **Descripción:** Escena greybox con ProBuilder para probar movimiento, saltos de distancias conocidas, pendientes, escaleras, bordes, vacío.
- **Subtareas:**
  - [ ] T-1.5.1 Plataformas a distancias y alturas medidas (tabla de medidas).
  - [ ] T-1.5.2 Pendientes de distintos ángulos, escalones, paredes, techo bajo.
  - [ ] T-1.5.3 Zona de caída al vacío.
  - [ ] T-1.5.4 Aplicar el kit de greybox (T-13.10): colores de lectura, niebla e iluminación de prueba, fondo con contraste suficiente.
  - [ ] T-1.5.5 Protagonista provisional (cápsula o maniquí) con las dimensiones previstas (ver 0.5).
- **Dependencias:** T-0.3, T-13.10 (para T-1.5.4; mientras no exista, se usan materiales neutros y se aplica después)
- **Criterios de aceptación:** Escena en `00_Scenes/Tests` (o la ubicación aprobada en D-21) con medidas documentadas; plataformas y bordes distinguibles del fondo y del vacío.
- **Pruebas:** Se usará en T-2.x.

---

## ETAPA 2 — Protagonista, movimiento, salto y cámara

### [ ] T-2.1 — Configuración de entrada
- **Prioridad:** `OBL`
- **Descripción:** Adaptar el asset de acciones al diseño (GDD §6.1, §6.3).
- **Subtareas:**
  - [ ] T-2.1.1 Definir acciones: Move, Look, Jump, Sprint, Interact, Pause; retirar o ignorar Attack/Crouch/Previous/Next (H-04).
  - [ ] T-2.1.2 Resolver D-06: cambiar `Interact` de Hold a Press salvo decisión contraria.
  - [ ] T-2.1.3 Esquemas Teclado+Ratón y, según D-07, Mando.
  - [ ] T-2.1.4 Generar clase C# del asset o usar `PlayerInput`; documentar la elección.
- **Dependencias:** T-0.1, D-06, D-07
- **Criterios de aceptación:** Cada acción responde a su tecla; Interact se dispara una vez por pulsación.
- **Pruebas:** Input Debugger + log en Play Mode.

### [ ] T-2.2 — Controlador del protagonista
- **Prioridad:** `OBL`
- **Descripción:** Caminar, correr, saltar, control aéreo, gravedad, pendientes (GDD §6.1).
- **Subtareas:**
  - [ ] T-2.2.1 Elegir base (`CharacterController` o `Rigidbody`) y justificar.
  - [ ] T-2.2.2 Movimiento relativo a la cámara, aceleración/deceleración, giro suave.
  - [ ] T-2.2.3 Correr (Sprint).
  - [ ] T-2.2.4 Salto con altura configurable.
  - [ ] T-2.2.11 `REC` *Coyote time* (margen breve para saltar justo después de dejar el borde).
  - [ ] T-2.2.12 `REC` *Jump buffer* (registrar el salto pulsado justo antes de tocar el suelo).
  - [ ] T-2.2.5 Control en el aire (obligatorio, GDD §6.1); gravedad aumentada en caída `REC`.
  - [ ] T-2.2.6 Detección de suelo fiable, pendientes máximas, escalones.
  - [ ] T-2.2.7 Evitar quedar atrapado en geometría (deslizamiento por paredes, techos).
  - [ ] T-2.2.8 `OPC` Soporte para plataformas móviles (solo si D-13 las aprueba).
  - [ ] T-2.2.9 `REC` Parámetros en ScriptableObject para ajustar sin recompilar (como mínimo, parámetros expuestos en el Inspector, que es obligatorio para el ajuste por pruebas).
  - [ ] T-2.2.10 Documentar alcance real del salto (distancia horizontal y altura máximas) y dimensiones de la cápsula para el diseño de niveles.
- **Dependencias:** T-2.1, T-1.5. **No depende de modelos ni animaciones definitivos** (se desarrolla con la cápsula provisional, ver 0.5).
- **Criterios de aceptación:** En la escena de pruebas el personaje no atraviesa el suelo, no se atasca en esquinas, sube pendientes permitidas, no sube las no permitidas y alcanza las distancias documentadas de forma consistente. Las subtareas `REC`/`OPC` no implementadas se anotan como `APLAZADA` o `DESCARTADA`.
- **Pruebas:** Recorrer la escena sandbox; 20 saltos por distancia medida; pruebas a 30, 60 y 144 FPS (o con `Application.targetFrameRate`) para verificar independencia del framerate.

### [ ] T-2.3 — Cámara de tercera persona (Cinemachine 3)
- **Prioridad:** `OBL`
- **Descripción:** Cámara detrás y por encima, suave, con control del ratón y sin atravesar geometría (GDD §6.2).
- **Subtareas:**
  - [ ] T-2.3.1 `CinemachineBrain` + `CinemachineCamera` con `OrbitalFollow` y `RotationComposer`.
  - [ ] T-2.3.2 Entrada de Look por Input System; sensibilidad e inversión configurables.
  - [ ] T-2.3.3 `CinemachineDeoccluder` / colisión para no atravesar paredes.
  - [ ] T-2.3.4 Límites verticales de órbita para leer saltos.
  - [ ] T-2.3.5 `REC` Sistema de cámaras especiales con prioridad (guardián, transformaciones, final) y mezcla suave. El GDD §6.2 las prevé como posibilidad («pueden utilizarse»); el reencuentro final probablemente la requiera (D-10).
  - [ ] T-2.3.6 Bloqueo y ocultación del cursor en juego; liberación en menús.
- **Dependencias:** T-2.2 (con protagonista provisional)
- **Criterios de aceptación:** La cámara sigue sin tirones, no atraviesa muros, permite ver el destino de un salto y, si existe T-2.3.5, vuelve al control tras una cámara especial.
- **Pruebas:** Recorrer sandbox junto a paredes y bajo techos; activar cámara especial de prueba y salir.

### [ ] T-2.4 — Modelo y animaciones del protagonista
- **Prioridad:** `OBL`
- **Descripción:** Integrar modelo y animaciones. Se trabaja en dos fases: provisional (no bloquea nada) y definitiva (depende de D-11). La lógica del controlador no debe depender del modelo: el modelo es un hijo visual sustituible.
- **Subtareas:**
  - [ ] T-2.4.1 Fase provisional: cápsula/maniquí con orientación visible y dimensiones previstas. Es suficiente para H1–H3.
  - [ ] T-2.4.5 `REC` Animaciones provisionales gratuitas (p. ej. maniquí con ciclo de caminar/correr/saltar) para validar el Animator antes de tener el modelo definitivo.
  - [ ] T-2.4.2 Fase definitiva: obtener modelo y animaciones con licencia adecuada (D-11).
  - [ ] T-2.4.3 Animator: reposo, caminar, correr, saltar, caer, aterrizar (obligatorias); interactuar `REC`.
  - [ ] T-2.4.4 Sincronizar parámetros con el controlador.
  - [ ] T-2.4.6 Al sustituir el modelo, comprobar que las dimensiones de la cápsula y las métricas de T-2.2.10 no cambian.
- **Dependencias:** T-2.4.1: T-2.2. T-2.4.2–T-2.4.4 y T-2.4.6: D-11. **H1 no depende de la fase definitiva.**
- **Criterios de aceptación:** Las animaciones corresponden al estado real sin deslizamiento evidente; sustituir el modelo no altera colisiones ni métricas.
- **Pruebas:** Observación en Play Mode de cada transición; repetir la batería de saltos de T-2.2 tras sustituir el modelo.

**Hito H1:** escena de pruebas jugable con protagonista provisional, movimiento, salto y cámara verificados en Play Mode; regresión T-17.7 y revisión breve de legibilidad del greybox.

---

## ETAPA 3 — Checkpoints, caídas y reaparición

### [ ] T-3.1 — Checkpoint
- **Prioridad:** `OBL`
- **Descripción:** Punto seguro con ID estable, activación y registro del último activado (GDD §7.1).
- **Subtareas:**
  - [ ] T-3.1.1 Componente `Checkpoint` con `PersistentId` y punto/orientación de aparición.
  - [ ] T-3.1.2 Activación según D-05 (trigger o interacción).
  - [ ] T-3.1.3 Respuesta visual/sonora y aviso en UI (T-15.4). Con efectos y sonidos provisionales hasta las etapas 13–14; la forma y el color del checkpoint siguen el kit de greybox (T-13.10) para que sea reconocible desde el primer prototipo.
  - [ ] T-3.1.4 Emitir evento `CheckpointActivated` (para guardado automático, T-4.4).
  - [ ] T-3.1.5 No re-disparar guardado si se reactiva el mismo checkpoint (o definir política).
  - [ ] T-3.1.6 `REC` Validador de Editor: el punto de aparición está sobre suelo y sin solapes. Sin él, la comprobación se hace a mano en cada checkpoint (T-3.2).
- **Dependencias:** T-1.2, T-1.3, T-2.2, D-05
- **Criterios de aceptación:** Activar un checkpoint lo registra como último; todo punto de aparición está sobre suelo seguro (comprobado con el validador T-3.1.6 o a mano).
- **Pruebas:** Activar varios en distinto orden; volver a uno anterior y comprobar la política definida.

### [ ] T-3.2 — Caídas y zonas de fallo
- **Prioridad:** `OBL`
- **Descripción:** Detectar caída al vacío o fallo y reaparecer.
- **Subtareas:**
  - [ ] T-3.2.1 Volúmenes `KillZone` y límite de altura global de seguridad.
  - [ ] T-3.2.2 Fundido a negro, desactivar control, teletransportar y reactivar.
  - [ ] T-3.2.3 Reinicio de velocidad y estado del controlador al reaparecer.
  - [ ] T-3.2.4 Reposición correcta de la cámara (sin barrido desde la posición de caída).
  - [ ] T-3.2.5 Checkpoint inicial por defecto de cada región si no hay ninguno activado.
- **Dependencias:** T-3.1, T-2.3
- **Criterios de aceptación:** Al caer, el jugador reaparece en el último checkpoint válido, sobre suelo, mirando en la dirección definida, sin quedar dentro de geometría.
- **Pruebas:** Caer desde varios puntos; caer durante un salto; caer repetidamente; caer antes de activar ningún checkpoint.

### [ ] T-3.3 — Política de qué se conserva al reaparecer
- **Prioridad:** `OBL`
- **Descripción:** Aplicar GDD §7.2: se conserva progreso confirmado; los acertijos temporales pueden reiniciarse.
- **Subtareas:**
  - [ ] T-3.3.1 Interfaz `IResettableOnRespawn` para elementos temporales.
  - [ ] T-3.3.2 Documentar por acertijo/mecanismo qué se reinicia (D-12).
- **Dependencias:** T-3.2; se completa con etapa 8.
- **Criterios de aceptación:** Tras reaparecer, misiones, transformaciones y rutas permanentes siguen igual; los elementos temporales se reinician según su ficha.
- **Pruebas:** Completar algo permanente, caer y comprobar; empezar un acertijo temporal, caer y comprobar reinicio.

---

## ETAPA 4 — Guardado, carga y continuación de partida (núcleo)

> El guardado se construye aquí con checkpoints, y **cada sistema posterior (misiones, objetos, mecanismos, transformaciones, acertijos) incluye su propia subtarea de integración con el guardado**.

### [ ] T-4.1 — Modelo de datos de la partida
- **Prioridad:** `OBL`
- **Descripción:** Estructura serializable separada de los objetos de escena (GDD §8.3, §8.5).
- **Subtareas:**
  - [ ] T-4.1.1 Decidir formato y ubicación (D-04; propuesta JSON en `persistentDataPath`, una partida).
  - [ ] T-4.1.2 `SaveData` con: versión de formato, fecha, tiempo jugado, región/escena, último checkpoint, posición/orientación segura, progreso de historia, estado de misiones, objetos, transformaciones, mecanismos/rutas, secretos.
  - [ ] T-4.1.3 `REC` Ajustes del jugador en archivo separado del de la partida. Es uno de los mecanismos posibles para la persistencia obligatoria de T-15.3.7; la alternativa es `PlayerPrefs`.
  - [ ] T-4.1.4 Interfaz `ISaveable` (capturar/restaurar estado por ID) para que cada sistema se registre.
- **Dependencias:** T-1.2, T-0.4
- **Criterios de aceptación:** El modelo cubre todos los datos de GDD §8.3 sin referencias a objetos de escena.
- **Pruebas:** Pruebas de unidad (Test Framework) de serializar → deserializar con datos completos.

### [ ] T-4.2 — Escritura y lectura seguras
- **Prioridad:** `OBL`
- **Descripción:** Escribir en archivo temporal, validar y reemplazar; mantener copia de respaldo.
- **Subtareas:**
  - [ ] T-4.2.1 Escritura a `.tmp` + reemplazo del archivo principal solo al terminar correctamente (GDD §8.5).
  - [ ] T-4.2.2 Validación al leer: JSON válido, versión soportada, campos obligatorios.
  - [ ] T-4.2.3 `REC` Copia de respaldo `.bak` y recuperación desde ella si el principal está dañado.
  - [ ] T-4.2.4 `REC` Migración de versiones de formato. Obligatorio en cualquier caso: guardar el identificador de versión (T-4.1.2) y rechazar con aviso las versiones no soportadas.
  - [ ] T-4.2.5 Manejo de excepciones de E/S (disco lleno, permisos) sin bloquear el juego.
- **Dependencias:** T-4.1
- **Criterios de aceptación:** Un archivo corrupto no bloquea el inicio; se informa y se ofrece alternativa; nunca se pierde el último archivo válido por un fallo de escritura.
- **Pruebas:** Unidad: archivo vacío, truncado, JSON inválido, versión futura, ausente. Manual: borrar/editar el archivo entre sesiones.

### [ ] T-4.3 — Carga y reconstrucción del mundo
- **Prioridad:** `OBL`
- **Descripción:** Cargar escena, aplicar estado por ID, colocar al jugador (GDD §8.2, §8.4).
- **Subtareas:**
  - [ ] T-4.3.1 Orden de carga: escena → registrar `ISaveable` → aplicar estado → colocar jugador → habilitar control.
  - [ ] T-4.3.2 Validar que región, checkpoint e IDs existen; si no, usar el punto seguro por defecto de la región y registrar advertencia.
  - [ ] T-4.3.3 Aplicar transformaciones en su estado final sin repetir animaciones ni recompensas.
  - [ ] T-4.3.4 Idempotencia: cargar varias veces no duplica objetos ni recompensas.
- **Dependencias:** T-4.2, T-1.4, T-3.1
- **Criterios de aceptación:** Tras Continuar, el jugador aparece en el último checkpoint y el mundo refleja el progreso guardado.
- **Pruebas:** Guardar, cerrar Play Mode, reabrir y Continuar; cargar dos veces seguidas; guardado con ID de checkpoint inexistente.

### [ ] T-4.4 — Guardado automático por eventos
- **Prioridad:** `OBL`
- **Descripción:** Guardar en eventos seguros (GDD §8.1).
- **Subtareas:**
  - [ ] T-4.4.1 Suscribirse a: checkpoint activado, encargo completado, transformación confirmada, ruta desbloqueada, región entrada, hito narrativo, salida desde menú.
  - [ ] T-4.4.2 `REC` Agrupar varios eventos del mismo frame en una escritura.
  - [ ] T-4.4.3 No guardar durante cargas, transiciones, caídas ni en el aire (posición insegura → usar checkpoint).
  - [ ] T-4.4.4 Indicador discreto de guardado en UI (T-15.4).
- **Dependencias:** T-4.2, T-1.3, T-3.1
- **Criterios de aceptación:** Cada evento listado produce un guardado; no hay escrituras por frame (con T-4.4.2, eventos simultáneos producen una sola escritura).
- **Pruebas:** Log de escrituras durante un recorrido; activar dos eventos simultáneos.

### [ ] T-4.5 — Salir y continuar
- **Prioridad:** `OBL`
- **Descripción:** Guardar antes de cerrar y continuar al reabrir (GDD §8.2).
- **Subtareas:**
  - [ ] T-4.5.1 «Salir al escritorio» guarda y espera a terminar antes de `Application.Quit`.
  - [ ] T-4.5.2 Gestión de `Application.quitting` / cierre por la X de la ventana.
  - [ ] T-4.5.3 Detección de partida válida para habilitar Continuar.
  - [ ] T-4.5.4 Nueva partida con confirmación si existe progreso; no confundirla con Continuar.
- **Dependencias:** T-4.3, T-15.1
- **Criterios de aceptación:** En una **build**, salir y reabrir permite continuar en el mismo estado.
- **Pruebas:** Build Windows: jugar, salir por menú, reabrir, Continuar. Cerrar con Alt+F4 / Administrador de tareas y comprobar que se conserva el último guardado automático.

### [ ] T-4.6 — Herramientas de depuración del guardado
- **Prioridad:** `REC`
- **Subtareas:**
  - [ ] T-4.6.1 Menú de Editor: abrir carpeta de guardado, borrar partida, ver JSON.
  - [ ] T-4.6.2 Comandos de depuración en desarrollo (guardar/cargar forzado).
- **Dependencias:** T-4.2
- **Criterios de aceptación:** Disponibles solo en Editor / Development Build.
- **Pruebas:** Usarlas durante T-4.3–T-4.5; build Release sin ellas.

**Hito H2:** salir del juego y continuar desde el último checkpoint, verificado en una build de Windows (T-18.4); regresión T-17.7 de H1.

---

## ETAPA 5 — Interacciones y sistema de diálogos

### [ ] T-5.1 — Sistema de interacción
- **Prioridad:** `OBL`
- **Descripción:** Detección de interactuables en rango, señal visual, aviso en UI y ejecución única (GDD §6.3).
- **Subtareas:**
  - [ ] T-5.1.1 Interfaz `IInteractable` (texto de acción, puede interactuar, interactuar).
  - [ ] T-5.1.2 Detección por rango y elección predecible del objetivo (el más cercano). Tener en cuenta también el ángulo de cámara: `REC`.
  - [ ] T-5.1.3 Resaltado visual del objeto enfocado.
  - [ ] T-5.1.4 Aviso de acción en UI con la tecla real del esquema activo.
  - [ ] T-5.1.5 Antirrebote: una ejecución por activación.
  - [ ] T-5.1.8 `OPC` Interacción de «mantener pulsado», solo si un diseño concreto la requiere (GDD §6.3, D-06).
  - [ ] T-5.1.6 Respuesta visual, sonora o textual por interacción (al menos una; provisional hasta las etapas 13–14).
  - [ ] T-5.1.7 Desactivar interacción en pausa, diálogo, caída y carga.
- **Dependencias:** T-2.1, T-2.2, T-1.1
- **Criterios de aceptación:** Con dos interactuables cerca, se elige de forma predecible; pulsar una vez ejecuta una vez.
- **Pruebas:** Interactuar repetidamente rápido; interactuar en el borde del rango; dos objetos superpuestos.

### [ ] T-5.2 — Sistema de diálogos
- **Prioridad:** `OBL`
- **Descripción:** Diálogos breves con subtítulos legibles, avance manual y eventos.
- **Subtareas:**
  - [ ] T-5.2.1 Datos de diálogo en ScriptableObject (hablante, líneas, condiciones, eventos al terminar).
  - [ ] T-5.2.2 UI de diálogo/subtítulos con tamaño legible y tiempo suficiente (GDD §12.4).
  - [ ] T-5.2.3 Avanzar línea y bloquear movimiento durante el diálogo. Completar la línea actual al pulsar (saltar la animación de texto): `REC`.
  - [ ] T-5.2.4 Diálogos condicionados al estado de misión (antes/durante/después).
  - [ ] T-5.2.5 Disparar eventos (iniciar misión, entregar objeto, cámara especial).
  - [ ] T-5.2.6 Registro de diálogos ya vistos (persistente si afecta a la narrativa).
  - [ ] T-5.2.7 Comportamiento definido con pausa (T-15.2).
  - [ ] T-5.2.8 `OPC` Preparar textos para localización (solo si D-14 lo requiere).
- **Dependencias:** T-5.1, T-1.3, T-4.1
- **Criterios de aceptación:** Un diálogo condicionado muestra la variante correcta según el estado guardado; no se puede mover durante el diálogo; pausar no rompe el diálogo.
- **Pruebas:** Diálogo antes/durante/después de una misión; pausar en mitad; guardar/cargar y comprobar variante.

### [ ] T-5.3 — Interactuables base
- **Prioridad:** `OBL`
- **Subtareas:**
  - [ ] T-5.3.1 `REC` Objeto narrativo (lectura/recuerdo). El GDD §4.2 pide que el escenario aporte narrativa; este es el medio más directo, pero no el único.
  - [ ] T-5.3.2 Objeto recogible (con ID persistente; no reaparece tras cargar).
  - [ ] T-5.3.3 Palanca/interruptor (conecta con T-7.1).
  - [ ] T-5.3.4 Personaje con diálogo.
- **Dependencias:** T-5.1, T-5.2, T-4.1
- **Criterios de aceptación:** Cada tipo funciona como prefab reutilizable y persiste según su ficha.
- **Pruebas:** Recoger un objeto, guardar, cargar: no reaparece.

---

## ETAPA 6 — Encargos y progreso de las almas animales

### [ ] T-6.1 — Modelo de misión
- **Prioridad:** `OBL`
- **Descripción:** Encargos principales y secundarios con estados (GDD §6.4).
- **Subtareas:**
  - [ ] T-6.1.1 `QuestDefinition` (ScriptableObject) con ID, tipo (principal/secundario), objetivos, recompensa/transformación asociada.
  - [ ] T-6.1.2 Estados: NoIniciado, Activo, ObjetivoCumplido (pendiente de entrega), Completado.
  - [ ] T-6.1.3 Tipos de objetivo. El GDD §4.2 y §6.4 dan como ejemplos recuperar/entregar un objeto, llegar a un lugar, activar algo o completar una tarea. **Solo se implementan los tipos que requieran los encargos aprobados (T-6.5)**; el sistema debe permitir añadir tipos sin rehacerlo. Para el encargo de prueba de H3 basta un tipo (propuesta: recoger y entregar un objeto).
  - [ ] T-6.1.4 `QuestManager` que reacciona a eventos y emite `QuestUpdated`/`QuestCompleted`.
- **Dependencias:** T-1.2, T-1.3, T-5.2
- **Criterios de aceptación:** Un encargo de prueba recorre los 8 pasos del ciclo GDD §6.4.
- **Pruebas:** Unidad para transiciones de estado; Play Mode del ciclo completo.

### [ ] T-6.2 — Inventario de objetos importantes
- **Prioridad:** `OBL`
- **Subtareas:**
  - [ ] T-6.2.1 Registro de objetos obtenidos/entregados por ID.
  - [ ] T-6.2.2 Entrega de objetos a almas.
  - [ ] T-6.2.3 Evitar entregar dos veces o recoger duplicados.
- **Dependencias:** T-5.3, T-6.1
- **Criterios de aceptación:** No es posible duplicar ni perder objetos importantes al cargar.
- **Pruebas:** Recoger → guardar → cargar → entregar; entregar → cargar → intentar entregar otra vez.

### [ ] T-6.3 — Integración de misiones con el guardado
- **Prioridad:** `OBL`
- **Subtareas:**
  - [ ] T-6.3.1 `QuestManager` implementa `ISaveable`.
  - [ ] T-6.3.2 Completar encargo dispara guardado automático.
  - [ ] T-6.3.3 Al cargar, restaurar estado sin repetir recompensas ni diálogos de cierre.
- **Dependencias:** T-6.1, T-6.2, T-4.4
- **Criterios de aceptación:** Cerrar en cualquier punto del ciclo y continuar conserva el estado exacto confirmado.
- **Pruebas:** Guardar/cargar en cada estado; caer y reaparecer con misión activa; cargar dos veces.

### [ ] T-6.4 — Presentación del objetivo actual
- **Prioridad:** `OBL`
- **Subtareas:**
  - [ ] T-6.4.1 `REC` Recordatorio breve del objetivo (UI discreta; el GDD §12.1 dice que la interfaz «puede mostrar» el objetivo actual).
  - [ ] T-6.4.2 Confirmación de misión completada.
  - [ ] T-6.4.3 Pistas del entorno (luces, sonidos) para guiar sin marcadores invasivos.
- **Dependencias:** T-6.1, T-15.4
- **Criterios de aceptación:** Un probador nuevo sabe qué hacer sin ayuda externa (verificar en T-17.5).
- **Pruebas:** Observación de jugadores.

### [ ] T-6.5 — Fichas de cada alma animal y encargo
- **Prioridad:** `OBL`
- **Descripción:** Contenido concreto; requiere D-08. **No inventar contenido definitivo sin validación.**
- **Subtareas:**
  - [ ] T-6.5.1 Plantilla de ficha (`Docs/fichas/`): alma, historia, necesidad, objetivo, pistas, región, transformación, persistencia.
  - [ ] T-6.5.2 Redactar y aprobar fichas por región.
  - [ ] T-6.5.3 Implementar cada encargo aprobado (se añadirán subtareas por encargo).
- **Dependencias:** D-08, T-6.1
- **Criterios de aceptación:** Cada encargo implementado tiene ficha aprobada y pasa el ciclo completo con guardado.
- **Pruebas:** Por encargo: completar, abandonar y volver, guardar en cada estado.

---

## ETAPA 7 — Mecanismos, rutas y transformaciones ambientales persistentes

### [ ] T-7.1 — Mecanismos y rutas
- **Prioridad:** `OBL`
- **Subtareas:**
  - [ ] T-7.1.1 Componente de mecanismo con estados (inactivo/activo) y ID persistente.
  - [ ] T-7.1.2 Tipos de mecanismo: puertas, puentes que aparecen, plataformas que se elevan, barreras que desaparecen. Son alternativas: **solo se implementan los que usen las regiones y acertijos aprobados** (D-20). Para H3 basta uno (propuesta: puente o puerta).
  - [ ] T-7.1.3 Marcado de mecanismo **permanente** o **temporal** (GDD §7.2).
  - [ ] T-7.1.4 Atajos que se desbloquean (emiten `RouteUnlocked`).
  - [ ] T-7.1.5 Colisiones coherentes con el estado visual (un puente invisible no tiene colisión).
- **Dependencias:** T-5.3.3, T-1.2, T-1.3
- **Criterios de aceptación:** El estado visual y de colisión siempre coinciden; los permanentes persisten.
- **Pruebas:** Activar → guardar → cargar; activar → caer → reaparecer.

### [ ] T-7.2 — Sistema de transformaciones ambientales
- **Prioridad:** `OBL`
- **Descripción:** Propuesta distintiva del juego (GDD §2): cambios visibles, persistentes, con causa comprensible.
- **Subtareas:**
  - [ ] T-7.2.1 `EnvironmentTransformation` con ID, causa (misión/evento), escala (local/zona/región) y estados inicial/restaurado.
  - [ ] T-7.2.2 Efectos combinables. El GDD §2 da ejemplos (color/saturación, vegetación/flores, luces/cristales, reconstrucción, puente o isla que se conecta, niebla que se disipa, atajo, cambio de ambiente sonoro). Son alternativas: **solo se implementan las que elijan las fichas** (D-20). Para H3 bastan dos combinadas que cumplan T-7.2.7 (propuesta: cambio de color/luz + aparición de un elemento físico).
  - [ ] T-7.2.3 Transición animada al activarse en juego.
  - [ ] T-7.2.4 Aplicación instantánea al cargar (sin repetir la animación).
  - [ ] T-7.2.5 `REC` Cámara especial para transformaciones importantes (requiere T-2.3.5).
  - [ ] T-7.2.8 Prototipar la transformación con los estados apagado/restaurado del kit de greybox (T-13.10), de modo que el cambio ya sea perceptible antes del arte definitivo.
  - [ ] T-7.2.6 `REC` Volumen de post-procesado por zona (local Volume) que cambia con la restauración.
  - [ ] T-7.2.7 Cambio que no dependa solo del color (forma, luz, sonido o ruta; GDD §10.2).
- **Dependencias:** T-7.1, T-6.1, T-4.3
- **Criterios de aceptación:** Completar la causa activa la transformación una vez, se percibe claramente y se conserva tras cerrar y continuar.
- **Pruebas:** Activar → salir → continuar; cargar dos veces; activar varias transformaciones en la misma zona.

### [ ] T-7.3 — Integración con el guardado
- **Prioridad:** `OBL`
- **Subtareas:**
  - [ ] T-7.3.1 Mecanismos y transformaciones implementan `ISaveable`.
  - [ ] T-7.3.2 Guardado automático al confirmar una transformación importante o desbloquear ruta principal.
- **Dependencias:** T-7.1, T-7.2, T-4.4
- **Criterios de aceptación:** Ver T-7.2.
- **Pruebas:** Cierre inesperado justo después de una transformación.

---

## ETAPA 8 — Acertijos

### [ ] T-8.1 — Piezas de acertijo reutilizables
- **Prioridad:** `OBL` (el controlador y las piezas que usen los acertijos aprobados)
- **Descripción:** Los tipos del GDD §6.5 son **alternativas**, no una lista obligatoria. Cada ficha de acertijo (T-8.2, D-20) elige sus tipos y solo se implementan esos. T-8.1.1–T-8.1.5 son candidatas; las no elegidas se marcarán `DESCARTADA` o quedarán como `OPC`.
- **Subtareas:**
  - [ ] T-8.1.6 `OBL` Controlador de acertijo que combina piezas y emite `PuzzleSolved`.
  - [ ] T-8.1.1 Candidata: interruptor/placa de presión (propuesta para el primer acertijo de Ruinas olvidadas, por ser la más fácil de enseñar).
  - [ ] T-8.1.2 Candidata: secuencia de encendido en orden (con reinicio al fallar).
  - [ ] T-8.1.3 Candidata: relacionar símbolos.
  - [ ] T-8.1.4 Candidata: mover/colocar objetos (empujar o recoger y colocar).
  - [ ] T-8.1.5 `OPC` Candidata: mecanismos temporizados (el GDD §6.6 los cita como posible obstáculo).
- **Dependencias:** T-5.1, T-7.1, D-20
- **Criterios de aceptación:** Cada pieza implementada funciona aislada y combinada; un acertijo resuelto queda resuelto según su ficha; los tipos no elegidos están anotados como descartados u opcionales.
- **Pruebas:** Resolver, fallar, reintentar, caer en mitad, guardar en mitad, cargar resuelto.

### [ ] T-8.2 — Fichas y comunicación de reglas
- **Prioridad:** `OBL`
- **Subtareas:**
  - [ ] T-8.2.1 Ficha por acertijo: reglas, pistas visuales/sonoras, solución, qué persiste (D-12).
  - [ ] T-8.2.2 Retroalimentación de acierto/error.
- **Dependencias:** T-8.1
- **Criterios de aceptación:** Probadores resuelven sin pistas externas (T-17.5).
- **Pruebas:** Observación de jugadores.

### [ ] T-8.3 — Integración con reaparición y guardado
- **Prioridad:** `OBL`
- **Subtareas:**
  - [ ] T-8.3.1 Estado resuelto persistente; estado intermedio según ficha.
  - [ ] T-8.3.2 Objetos movibles: posición restaurada o reiniciada según ficha; evitar que queden fuera de alcance.
- **Dependencias:** T-8.1, T-3.3, T-4.3
- **Criterios de aceptación:** Ningún acertijo queda irresoluble tras caer, cargar o empujar un objeto al vacío.
- **Pruebas:** Tirar un objeto movible al vacío; cargar con acertijo a medias.

**Hito H3:** en una escena prototipo con recursos provisionales y kit de greybox, encargo → acertijo/mecanismo → transformación → guardado → salir → continuar funciona de extremo a extremo; verificado en build (T-18.4), con regresión T-17.7 y primera prueba breve con un jugador externo (T-17.5).

---

## ETAPA 9 — Generador propio de islas flotantes

> Prototipo aislado (GDD §9.4). No se considera terminado sin probar malla, colisiones, rendimiento, repetibilidad y que se pueda caminar y saltar.

### [ ] T-9.1 — Prototipo de malla
- **Prioridad:** `OBL`
- **Subtareas:**
  - [ ] T-9.1.1 Escena de prueba aislada en `00_Scenes/Tests` (o la ubicación aprobada en D-21).
  - [ ] T-9.1.2 Generación de contorno irregular (ruido sobre radio) con semilla.
  - [ ] T-9.1.3 Superficie superior transitable (ruido suave, pendiente máxima limitada).
  - [ ] T-9.1.4 Parte inferior (cono/estalactita) con profundidad configurable.
  - [ ] T-9.1.5 Normales, UV y tangentes correctas.
  - [ ] T-9.1.6 Material de greybox del kit (T-13.10) desde el primer prototipo, con superficie superior transitable visualmente distinta de los laterales para leer dónde se puede pisar.
- **Dependencias:** T-1.5
- **Criterios de aceptación:** Malla sin agujeros ni normales invertidas para cualquier semilla probada.
- **Pruebas:** 20+ semillas; inspección de wireframe y normales.

### [ ] T-9.2 — Parámetros e Inspector
- **Prioridad:** `OBL`
- **Subtareas:**
  - [ ] T-9.2.1 Radio, dimensiones, altura, profundidad, irregularidad, ruido, resolución, semilla.
  - [ ] T-9.2.2 `REC` Presets en ScriptableObject.
  - [ ] T-9.2.3 Botones Generar / Limpiar / Regenerar en el Inspector.
  - [ ] T-9.2.4 Límites de valores para evitar mallas degeneradas o enormes.
- **Dependencias:** T-9.1
- **Criterios de aceptación:** Los parámetros tienen efecto predecible y están acotados.
- **Pruebas:** Valores extremos de cada parámetro.

### [ ] T-9.3 — Reproducibilidad
- **Prioridad:** `OBL`
- **Subtareas:**
  - [ ] T-9.3.1 Misma semilla + parámetros = misma malla (sin `UnityEngine.Random` global).
  - [ ] T-9.3.2 Comparación automática de hash de vértices.
- **Dependencias:** T-9.1
- **Criterios de aceptación:** Hash idéntico entre ejecuciones y entre Editor y build.
- **Pruebas:** Prueba de unidad (Test Framework) de reproducibilidad.

### [ ] T-9.4 — Persistencia de la malla
- **Prioridad:** `OBL`
- **Subtareas:**
  - [ ] T-9.4.1 Guardar la malla como asset para islas de la ruta principal (no regenerar en runtime).
  - [ ] T-9.4.2 Limpiar solo objetos del generador.
- **Dependencias:** T-9.2
- **Criterios de aceptación:** Islas validadas no cambian al reabrir la escena ni en la build.
- **Pruebas:** Reabrir escena; comparar en build.

### [ ] T-9.5 — Colisiones
- **Prioridad:** `OBL`
- **Subtareas:**
  - [ ] T-9.5.1 `MeshCollider` de malla simplificada (o de la superior) para el personaje.
  - [ ] T-9.5.2 Verificar que el personaje no se atasca en bordes ni cae a través.
- **Dependencias:** T-9.1, T-2.2
- **Criterios de aceptación:** Se puede caminar y saltar sobre las islas sin atravesarlas ni quedar atrapado.
- **Pruebas:** Recorrer bordes, saltar entre dos islas generadas a distancias medidas.

### [ ] T-9.6 — Material y aspecto
- **Prioridad:** `REC`
- **Subtareas:**
  - [ ] T-9.6.1 Material superior (hierba/roca) y lateral (roca) por normales o vertex color.
  - [ ] T-9.6.2 Variante apagada y restaurada (enlace con T-7.2).
- **Dependencias:** T-9.1, T-13.1
- **Criterios de aceptación:** Coherente con la guía de arte.
- **Pruebas:** Revisión visual con la paleta.

### [ ] T-9.7 — Rendimiento del generador
- **Prioridad:** `OBL`
- **Subtareas:**
  - [ ] T-9.7.1 Medir tiempo de generación, nº de vértices y coste del colisionador por resolución.
  - [ ] T-9.7.2 Definir resolución máxima recomendada.
- **Dependencias:** T-9.5
- **Criterios de aceptación:** Datos medidos y anotados (no estimados).
- **Pruebas:** Profiler.

---

## ETAPA 10 — Generación procedural secundaria y validaciones

### [ ] T-10.1 — Distribuidor de decoración
- **Prioridad:** `REC` (la decoración procedural aporta variedad; el GDD no la exige en todas las zonas)
- **Subtareas:**
  - [ ] T-10.1.1 Distribución de rocas, vegetación y restos de ruinas en un área con semilla.
  - [ ] T-10.1.2 Raycast al suelo, alineación a la normal, pendiente máxima.
  - [ ] T-10.1.3 Separación mínima y límite de cantidad.
  - [ ] T-10.1.4 `OPC` Distribución a lo largo de Splines (bordes de caminos). Requiere decidir T-0.2.2.
  - [ ] T-10.1.5 Contenedor propio: limpiar/regenerar solo lo generado.
- **Dependencias:** T-9.3 (patrón de semillas); T-0.2.2 solo para T-10.1.4
- **Criterios de aceptación:** Resultados reproducibles; no se borra nada ajeno.
- **Pruebas:** Regenerar varias veces con la misma semilla; limpiar con objetos manuales en el mismo padre.

### [ ] T-10.2 — Zonas protegidas
- **Prioridad:** `OBL` si se usa T-10.1 o T-10.4 (reglas de seguridad del GDD §9.3)
- **Subtareas:**
  - [ ] T-10.2.1 Volúmenes de exclusión: ruta principal, plataformas, checkpoints, personajes, objetivos, interactuables, cámaras.
  - [ ] T-10.2.2 Exclusión automática alrededor de todos los `PersistentId` y `Checkpoint`.
  - [ ] T-10.2.3 `OPC` Exclusión a lo largo de splines de caminos (si se usan splines; si no, volúmenes de T-10.2.1).
- **Dependencias:** T-10.1, T-3.1
- **Criterios de aceptación:** Ningún objeto generado dentro de una zona protegida.
- **Pruebas:** Validador (T-10.3) con 10+ semillas.

### [ ] T-10.3 — Validador
- **Prioridad:** `OBL` si se usa T-10.1 o T-10.4 (reglas de seguridad del GDD §9.3)
- **Subtareas:**
  - [ ] T-10.3.1 Detectar objetos flotantes, enterrados o solapados.
  - [ ] T-10.3.2 Detectar bloqueos de ruta (cápsula del jugador a lo largo de la ruta).
  - [ ] T-10.3.3 Informe en consola/ventana con objetos problemáticos seleccionables.
  - [ ] T-10.3.4 Registro de semillas validadas por zona.
- **Dependencias:** T-10.1, T-10.2
- **Criterios de aceptación:** El validador detecta casos forzados de cada tipo.
- **Pruebas:** Casos sembrados a propósito.

### [ ] T-10.4 — Islas secundarias y secretos
- **Prioridad:** `OPC` (el GDD §9.1 las considera aptas para generación, no obligatorias)
- **Subtareas:**
  - [ ] T-10.4.1 Colocación de islas opcionales en zonas autorizadas.
  - [ ] T-10.4.2 Validar distancias de salto con el alcance documentado (T-2.2.10).
  - [ ] T-10.4.3 Secretos en zonas autorizadas, con ID persistente estable por semilla (D-18).
- **Dependencias:** T-9, T-10.3, D-18
- **Criterios de aceptación:** Toda isla opcional declarada como alcanzable lo es en ejecución.
- **Pruebas:** Saltar a cada isla opcional en Play Mode.

---

## ETAPA 11 — Diseño de niveles y regiones

### [ ] T-11.1 — Plan de regiones
- **Prioridad:** `OBL`
- **Subtareas:**
  - [ ] T-11.1.1 Resolver D-01 y D-02 (duración y número de regiones).
  - [ ] T-11.1.2 Documento por región (`Docs/regiones/`): objetivo, ruta principal, desvíos, checkpoints, encargos, acertijos, transformaciones, entradas/salidas.
  - [ ] T-11.1.3 Mapa esquemático y ritmo (enseñar → practicar → combinar).
  - [ ] T-11.1.4 Métricas de nivel basadas en T-2.2.10.
- **Dependencias:** T-2.2.10, D-01, D-02
- **Criterios de aceptación:** Documentos aprobados antes de construir cada región.
- **Pruebas:** Revisión de diseño.

### [ ] T-11.2 — Región: El despertar
- **Prioridad:** `OBL`
- **Subtareas:**
  - [ ] T-11.2.1 Greybox (ProBuilder/Terrain) con el kit de greybox (T-13.10) y la paleta inicial de la guía de arte (T-13.1): ruta legible, siluetas y puntos de interés, vistas lejanas que sugieran destinos, niebla de prueba que no oculte bordes.
  - [ ] T-11.2.2 Enseñanza de movimiento, salto y cámara.
  - [ ] T-11.2.3 Primer encuentro con el guardián (T-12.2).
  - [ ] T-11.2.4 Luces/señales que orientan a la salida.
  - [ ] T-11.2.5 Checkpoints y kill zones.
  - [ ] T-11.2.6 Sustituir provisionales por arte, audio e iluminación de producción (etapas 13–14).
- **Dependencias:** T-11.1, etapas 2–5
- **Criterios de aceptación:** Completable de principio a fin; todos los saltos probados en juego; guardado/continuar funciona en todos los checkpoints.
- **Pruebas:** Recorrido completo; caer en cada sección; salir/continuar en cada checkpoint.

### [ ] T-11.3 — Región: Ruinas olvidadas
- **Prioridad:** `OBL`
- **Subtareas:**
  - [ ] T-11.3.1 Greybox con el kit de greybox (T-13.10) y la guía de arte inicial (ver T-11.2.1).
  - [ ] T-11.3.2 Primeros acertijos y mecanismos que habilitan caminos.
  - [ ] T-11.3.3 Encargos aprobados de la región.
  - [ ] T-11.3.4 Transformaciones (mecanismos antiguos vuelven a funcionar).
  - [ ] T-11.3.5 Checkpoints, arte, audio.
- **Dependencias:** T-11.2, etapas 6–8
- **Criterios de aceptación:** Igual que T-11.2 + acertijos resolubles y transformaciones persistentes.
- **Pruebas:** Igual que T-11.2 + pruebas de acertijos.

**Hito H4: vertical slice** (El despertar + Ruinas olvidadas) completo con identidad visual inicial, probado en build (T-18.4); regresión T-17.7; revisión de arte y legibilidad; prueba con jugadores (T-17.5); primera medición formal de rendimiento (T-16.1). Revisar alcance antes de seguir.

### [ ] T-11.4 — Región: Camino de las almas
- **Prioridad:** `OBL` según el plan de regiones aprobado (T-11.1, D-02)
- **Subtareas:** Greybox con kit (T-13.10); varias almas y encargos; restauraciones elegidas en sus fichas (D-20; el GDD §5 sugiere color, vegetación y luces); checkpoints; arte y audio.
- **Dependencias:** H4, T-6.5
- **Criterios de aceptación / Pruebas:** Como T-11.3.

### [ ] T-11.5 — Región: Umbral celestial
- **Prioridad:** `OBL` según el plan de regiones aprobado (T-11.1, D-02)
- **Subtareas:** Greybox con kit (T-13.10) e islas (etapa 9); desafío de plataformas mayor; puentes, mecanismos o islas que se activan (según fichas, D-20); checkpoints frecuentes; arte y audio.
- **Dependencias:** H4, etapa 9; etapa 10 solo si se usa decoración o islas secundarias procedurales
- **Criterios de aceptación / Pruebas:** Como T-11.3 + todas las islas obligatorias revisadas manualmente.

### [ ] T-11.6 — Región: Reino de los perritos
- **Prioridad:** `OBL` según el plan de regiones aprobado (T-11.1, D-02)
- **Subtareas:** Greybox con kit (T-13.10); entorno cálido; encargos finales; checkpoints; arte y audio.
- **Dependencias:** H4
- **Criterios de aceptación / Pruebas:** Como T-11.3.

### [ ] T-11.7 — Región: Reencuentro
- **Prioridad:** `OBL`
- **Subtareas:** Espacio final; escena del reencuentro (T-12.4); créditos.
- **Dependencias:** T-12.4
- **Criterios de aceptación:** El juego puede terminarse; el estado final se guarda (partida completada).
- **Pruebas:** Completar el juego desde una partida nueva.

### [ ] T-11.8 — Conexiones entre regiones
- **Prioridad:** `OBL`
- **Subtareas:** Transiciones; puntos de entrada; guardado al entrar en región; impedir volver a estados imposibles.
- **Dependencias:** T-1.4, T-4.4
- **Criterios de aceptación:** Recorrer todas las regiones en orden sin errores.
- **Pruebas:** Partida completa.

---

## ETAPA 12 — Guardián, narrativa y escenas clave

### [ ] T-12.1 — Guion y fichas narrativas
- **Prioridad:** `OBL`
- **Subtareas:**
  - [ ] T-12.1.1 Resolver D-09 (muerte del protagonista) cumpliendo GDD §4.3.
  - [ ] T-12.1.2 Ficha del guardián: rol, aspecto, apariciones, líneas.
  - [ ] T-12.1.3 Arco narrativo por región y diálogos aprobados.
  - [ ] T-12.1.4 Revisión de sensibilidad del tratamiento del duelo.
- **Dependencias:** D-08, D-09
- **Criterios de aceptación:** Guion aprobado y revisado.
- **Pruebas:** Lectura y revisión.

### [ ] T-12.2 — Guardián en juego
- **Prioridad:** `OBL`
- **Subtareas:** Placeholder (forma simple reconocible) para prototipos y modelo definitivo cuando exista (D-11); diálogos; cámara especial `REC`; apariciones por región; persistencia de lo conversado.
- **Dependencias:** T-12.1, T-5.2; T-2.3.5 solo para la cámara especial. El placeholder permite probar todo el flujo sin el modelo definitivo.
- **Criterios de aceptación:** Aparece en los momentos definidos y sus diálogos reflejan el progreso.
- **Pruebas:** Guardar/cargar entre apariciones.

### [ ] T-12.3 — Escenas narrativas
- **Prioridad:** `OBL` (las subtareas indican su propia prioridad)
- **Descripción:** El GDD §4.2 presenta la historia «mediante escenas, diálogos breves, encuentros, objetos del entorno y cambios en los lugares». Lo obligatorio es el **resultado narrativo**, no la herramienta: cada escena puede hacerse con Timeline, con secuencias por script o con diálogo y cámara en juego.
- **Subtareas:**
  - [ ] T-12.3.1 `OBL` Presentación inicial del despertar y del primer encuentro con el guardián (forma libre: escena con cámara, diálogo en juego o combinación).
  - [ ] T-12.3.2 `OBL` Bloqueo de entrada y comportamiento con pausa definidos para toda escena que quite el control.
  - [ ] T-12.3.3 `OBL` Cada escena se reproduce una vez, se registra como vista y no se repite tras cargar; guardado tras los hitos narrativos (T-4.4).
  - [ ] T-12.3.4 `REC` Escenas para transformaciones clave.
  - [ ] T-12.3.5 `REC` Posibilidad de saltar escenas.
  - [ ] T-12.3.6 `OPC` Usar Timeline (instalado; decisión de uso en D-16). Si no se usa, las escenas se resuelven por script sin pérdida de requisitos.
- **Dependencias:** T-1.1, T-4.4, T-5.2; T-2.3.5 si la escena usa cámaras especiales; D-16 solo para T-12.3.6
- **Criterios de aceptación:** La presentación inicial comunica la situación del protagonista; toda escena se reproduce una vez y no se repite tras cargar; si existe T-12.3.5, saltar no rompe el estado; la elección de herramienta está anotada.
- **Pruebas:** Saltar escena; cerrar el juego en mitad de una escena y continuar.

### [ ] T-12.4 — Reencuentro final
- **Prioridad:** `OBL`
- **Subtareas:** Resolver D-10; escena final con perro provisional para validar flujo y cámara; modelo y animaciones definitivos del perro (D-11); créditos; vuelta al menú.
- **Dependencias:** T-12.3.2 y T-12.3.3 (mecanismo de escenas), D-10. D-11 solo para la versión definitiva (necesaria para H5).
- **Criterios de aceptación:** El final se dispara solo al cumplir la progresión principal.
- **Pruebas:** Partida completa; intentar llegar al final sin completar requisitos.

---

## ETAPA 13 — Dirección artística, iluminación, materiales y efectos

### [ ] T-13.1 — Guía de arte
- **Prioridad:** `OBL`
- **Descripción:** Se hace en dos pasos. **Versión inicial** en paralelo a las etapas 1–2, antes del primer greybox de región, para que los prototipos ya respeten la identidad visual (ver 0.6). **Versión completa** antes de la producción de recursos.
- **Subtareas:**
  - [ ] T-13.1.1 Versión inicial: paleta apagada y restaurada general, tono de niebla e iluminación de prueba, escala de referencia del protagonista, reglas de legibilidad (contraste plataformas/fondo, peligros visibles).
  - [ ] T-13.1.2 Versión completa: referencias propias (sin copiar *Sky*), paletas por región, escala de arquitectura e islas, materiales y estilo de modelos.
  - Documento: `Docs/GUIA_DE_ARTE.md`.
- **Dependencias:** —
- **Criterios de aceptación:** Versión inicial aprobada antes de T-11.2.1; versión completa aprobada antes de T-13.7.
- **Pruebas:** Revisión.

### [ ] T-13.2 — Recursos y licencias
- **Prioridad:** `OBL`
- **Subtareas:** Lista de recursos necesarios; búsqueda de recursos gratuitos con licencia adecuada; registro `Docs/LICENCIAS.md` (origen, autor, licencia, uso).
- **Dependencias:** D-11
- **Criterios de aceptación:** Todo recurso externo del proyecto aparece en el registro con licencia compatible.
- **Pruebas:** Auditoría del registro frente a `Assets/`.

### [ ] T-13.3 — Materiales y shaders
- **Prioridad:** `OBL`
- **Subtareas:** Materiales URP base (roca, ruinas, vegetación, cristal); parámetro de «restauración» (saturación/emisión) controlable por T-7.2; posible Shader Graph de transición.
- **Dependencias:** T-13.1, T-7.2
- **Criterios de aceptación:** Los materiales cambian de estado con la transformación.
- **Pruebas:** Activar transformaciones de prueba.

### [ ] T-13.4 — Iluminación
- **Prioridad:** `OBL`
- **Subtareas:** Iluminación por región; decidir baked/mixta/realtime; luces que guían; reflection probes `REC`; coste medido.
- **Dependencias:** T-11.x (greybox)
- **Criterios de aceptación:** Puntos de interés legibles; rendimiento dentro del objetivo (T-16).
- **Pruebas:** Revisión visual; Profiler.

### [ ] T-13.5 — Post-procesado y niebla
- **Prioridad:** `OBL`
- **Subtareas:** Volumen global con los efectos que la guía de arte elija (candidatos: tonemapping, color adjustments, bloom, vignette); volúmenes locales `REC`; niebla que no oculta peligros (obligatorio).
- **Dependencias:** T-13.1
- **Criterios de aceptación:** Plataformas y peligros visibles en todos los estados.
- **Pruebas:** Recorrido de legibilidad en cada región.

### [ ] T-13.6 — Efectos (VFX)
- **Prioridad:** `REC`
- **Subtareas:** Efectos para checkpoint, interacción y transformación `REC`; partículas de luz/huellas `REC`; ambiente (polvo, luciérnagas) `OPC`.
- **Dependencias:** T-13.1
- **Criterios de aceptación:** Efectos coherentes y sin coste excesivo.
- **Pruebas:** Profiler con varios efectos activos.

### [ ] T-13.7 — Modelos de entorno
- **Prioridad:** `OBL`
- **Subtareas:** Ruinas, puentes, rocas, vegetación, faroles, cristales, símbolos (modelos externos o ProBuilder detallado).
- **Dependencias:** T-13.2
- **Criterios de aceptación:** Escala coherente; colisiones adecuadas.
- **Pruebas:** Recorrido con el personaje.

### [ ] T-13.8 — Personajes
- **Prioridad:** `OBL`
- **Subtareas:** Protagonista, guardián, almas animales, perro (modelos y animaciones).
- **Dependencias:** D-11, T-13.2
- **Criterios de aceptación:** Integrados con licencias registradas.
- **Pruebas:** Revisión en juego.

### [ ] T-13.9 — Ciclo día/noche (condicional)
- **Prioridad:** `OPC` (condicional a D-01)
- **Descripción:** Solo si D-01 lo requiere.
- **Dependencias:** D-01
- **Estado:** `BLOQUEADA — depende de D-01`.

### [ ] T-13.10 — Kit de greybox legible
- **Prioridad:** `OBL`
- **Descripción:** Conjunto mínimo de materiales y reglas para que todos los prototipos y greyboxes respeten la legibilidad y el tono del juego desde el principio (ver 0.6). No es arte final.
- **Subtareas:**
  - [ ] T-13.10.1 Materiales URP simples con código de colores: suelo transitable de la ruta principal, plataformas obligatorias, desvíos, interactuables, checkpoints, peligros/vacío, elementos que se transformarán.
  - [ ] T-13.10.2 Variantes «apagado» y «restaurado» de los materiales de greybox para prototipar transformaciones (T-7.2.8).
  - [ ] T-13.10.3 Perfil de niebla e iluminación de prueba coherente con el estado inicial frío y desaturado (GDD §10.2), sin ocultar bordes ni peligros.
  - [ ] T-13.10.4 Prefabs de referencia de escala (protagonista provisional, puerta, escalón, salto máximo).
  - [ ] T-13.10.5 Leyenda del código de colores en `Docs/GUIA_DE_ARTE.md`. El código no debe depender solo del color (forma o patrón como apoyo, GDD §12.4).
- **Dependencias:** T-13.1.1 (puede empezar con una propuesta y ajustarse al aprobarla), T-0.3
- **Criterios de aceptación:** El sandbox (T-1.5) y el primer greybox de región usan el kit; un observador distingue ruta, plataformas, interactuables y peligros en capturas en escala de grises.
- **Pruebas:** Revisión con la Skill *Art Director de fantasía 3D*; captura en escala de grises para comprobar contraste.

---

## ETAPA 14 — Audio y música

### [ ] T-14.1 — Infraestructura de audio
- **Prioridad:** `OBL`
- **Subtareas:** AudioMixer con grupos (Música, Ambiente, Efectos, UI; Voz/Diálogo solo si hay voces); volúmenes expuestos para opciones; servicio de música con fundidos; pausa del audio de juego en el menú de pausa. Sonidos provisionales permitidos en los prototipos.
- **Dependencias:** T-1.1
- **Criterios de aceptación:** Los sliders de opciones afectan a cada grupo; la pausa silencia o atenúa lo definido.
- **Pruebas:** Cambiar volúmenes; pausar con música y efectos activos.

### [ ] T-14.2 — Efectos de sonido
- **Prioridad:** `OBL`
- **Subtareas:** Pasos (variación por superficie `REC`); salto/aterrizaje `REC`; interacción; mecanismos; acertijo acierto/error; checkpoint; misión completada; UI.
- **Dependencias:** T-14.1, T-2.2, T-5.1
- **Criterios de aceptación:** Cada acción importante tiene respuesta sonora sin saturar.
- **Pruebas:** Recorrido de escucha.

### [ ] T-14.3 — Ambiente y música por región
- **Prioridad:** `OBL`
- **Prioridad de subtareas:** el GDD §11 enumera los elementos previstos de audio; la regla del GDD §2 exige respuesta visual **o** sonora en cada transformación, y la visual ya es obligatoria en T-7.2. Por eso el cambio sonoro al restaurar es recomendado y la técnica es libre.
- **Subtareas:**
  - [ ] T-14.3.1 `OBL` Ambiente sonoro base por región (viento, espacios abiertos).
  - [ ] T-14.3.2 `OBL` Música ambiental por región (una pista por región como mínimo; se pueden compartir entre regiones afines).
  - [ ] T-14.3.3 `OBL` Música o sonido específico para el reencuentro final (momento narrativo principal, GDD §11).
  - [ ] T-14.3.4 `REC` Cambio suave de ambiente o música al restaurar una zona, con persistencia al cargar. Técnica libre: fundido entre pistas o capas `OPC`.
  - [ ] T-14.3.5 `REC` Música o sonido específico para otras escenas clave (guardián, transformaciones importantes).
- **Dependencias:** T-14.1; T-7.2 solo para T-14.3.4; T-12.4 para T-14.3.3
- **Criterios de aceptación:** Cada región tiene ambiente y música; el final tiene su tratamiento sonoro; si existe T-14.3.4, el cambio al restaurar es perceptible y persiste al cargar.
- **Pruebas:** Recorrido de escucha por región; si existe T-14.3.4: restaurar zona → guardar → cargar.

### [ ] T-14.4 — Licencias de audio
- **Prioridad:** `OBL`
- **Subtareas:** Registrar en `Docs/LICENCIAS.md`.
- **Dependencias:** T-13.2
- **Criterios de aceptación:** Todo el audio externo registrado.

### [ ] T-14.5 — Importación optimizada
- **Prioridad:** `REC`
- **Subtareas:** Load Type y compresión por tipo (música streaming, efectos cortos descomprimidos/ADPCM), mono para 3D.
- **Dependencias:** T-14.2, T-14.3
- **Criterios de aceptación:** Memoria de audio medida y razonable.
- **Pruebas:** Memory Profiler.

---

## ETAPA 15 — Interfaz, menú principal, menú de pausa y opciones

### [ ] T-15.1 — Menú principal (mínimo temprano)
- **Prioridad:** `OBL`
- **Descripción:** Continuar / Nueva partida / Opciones / Salir (GDD §12.2). Se desarrolla junto a la etapa 4.
- **Subtareas:**
  - [ ] T-15.1.1 Elegir sistema de UI (uGUI o UI Toolkit, D-23) y documentarlo.
  - [ ] T-15.1.2 Escena de menú principal.
  - [ ] T-15.1.3 Continuar habilitado solo con partida válida.
  - [ ] T-15.1.4 Nueva partida con confirmación si hay progreso.
  - [ ] T-15.1.5 Aviso de partida dañada sin bloquear el inicio (T-4.2).
  - [ ] T-15.1.6 Navegación con teclado/ratón (y mando si D-07).
- **Dependencias:** T-1.1, T-4.2
- **Criterios de aceptación:** Los cuatro botones hacen lo esperado en todos los estados del archivo (ausente, válido, dañado).
- **Pruebas:** Las tres situaciones del archivo de guardado; en build.

### [ ] T-15.2 — Menú de pausa
- **Prioridad:** `OBL`
- **Subtareas:**
  - [ ] T-15.2.1 Reanudar; Opciones; Volver al menú (confirmación + guardado); Salir al escritorio (guardado).
  - [ ] T-15.2.2 Gestión de tiempo, cámara, entrada, cursor y sonido al pausar.
  - [ ] T-15.2.3 Comportamiento definido durante diálogos y escenas (GDD §12.3).
  - [ ] T-15.2.4 `REC` Pausa automática al perder el foco de la ventana (Alt+Tab).
- **Dependencias:** T-1.1, T-4.5, T-14.1
- **Criterios de aceptación:** Pausar congela el juego y la cámara; reanudar no provoca saltos ni entradas fantasma.
- **Pruebas:** Pausar en el aire, en diálogo, durante transformación, durante caída; Alt+Tab (con o sin T-15.2.4, el juego no debe quedar en un estado incoherente al volver).

### [ ] T-15.3 — Opciones
- **Prioridad:** `OBL`
- **Descripción:** El GDD §12.2 deja las opciones definitivas para producción (D-15). Propuesta de mínimo obligatorio y extras clasificados:
- **Subtareas:**
  - [ ] T-15.3.1 `OBL` Volumen (al menos general, música y efectos).
  - [ ] T-15.3.2 `OBL` Pantalla completa/ventana y resolución.
  - [ ] T-15.3.3 `REC` Sensibilidad de cámara e invertir eje Y.
  - [ ] T-15.3.4 `REC` Calidad gráfica y VSync.
  - [ ] T-15.3.5 `REC` Tamaño y fondo de subtítulos (GDD §12.4 pide subtítulos legibles; el ajuste es una mejora).
  - [ ] T-15.3.6 `OPC` Reasignación de controles.
  - [ ] T-15.3.7 `OBL` Persistencia de **todas las opciones implementadas** entre sesiones (GDD §8.3: «ajustes de juego que deban persistir, si se implementan»; como T-15.3.1 y T-15.3.2 son obligatorias, hay ajustes que persistir). El mecanismo es libre: archivo de ajustes propio (T-4.1.3, `REC`) o `PlayerPrefs`. `REC`: que los ajustes sean independientes de la partida (Nueva partida no los borra).
- **Dependencias:** T-15.1, T-14.1, D-15
- **Criterios de aceptación:** Los ajustes se aplican al momento y se conservan al reiniciar.
- **Pruebas:** Cambiar cada opción, cerrar, reabrir (en build).

### [ ] T-15.4 — HUD discreto
- **Prioridad:** `OBL`
- **Subtareas:** Aviso de interacción; subtítulos; misión completada; aviso de error de guardado (obligatorios, GDD §6.3, §12.1, §16); objetivo actual `REC` (T-6.4.1); aviso de checkpoint `REC`; indicador de guardado `REC`. Sistema de UI según D-23.
- **Dependencias:** T-5.1, T-5.2, T-6.4
- **Criterios de aceptación:** Legible a 1080p y 720p; no tapa elementos importantes; no depende solo del color.
- **Pruebas:** Varias resoluciones y relaciones de aspecto.

### [ ] T-15.5 — Pantallas de transición y créditos
- **Prioridad:** `REC` (el fundido de carga de T-1.4.2 es obligatorio; esta tarea es su acabado y los créditos)
- **Subtareas:** Pantalla/fundido de carga; créditos con licencias.
- **Dependencias:** T-1.4, T-13.2
- **Criterios de aceptación:** Sin pantallazos de escena vacía durante las cargas.
- **Pruebas:** Cambios de región.

---

## ETAPA 16 — Optimización y rendimiento

### [ ] T-16.1 — Objetivo y medición base
- **Prioridad:** `OBL`
- **Subtareas:** Definir equipo y objetivo (D-19); primeras mediciones orientativas desde H1 (sandbox) y en cada build de hito (T-18.4); medición formal en build Development con Profiler (CPU, GPU, memoria, GC) en H4.
- **Dependencias:** H1 para las primeras mediciones; H4 y D-19 para la medición formal
- **Criterios de aceptación:** Cifras medidas y anotadas (no estimadas).
- **Pruebas:** Profiler en build.

### [ ] T-16.2 — Optimización de render
- **Prioridad:** `REC` (se aplica lo que la medición de T-16.1 justifique)
- **Subtareas:** Ajuste de `PC_RPAsset` (sombras, MSAA, render scale); LOD; occlusion culling; batching (SRP Batcher, GPU instancing para decoración); distancia de dibujo; reducir variantes de shader.
- **Dependencias:** T-16.1
- **Criterios de aceptación:** Objetivo alcanzado en la región más pesada.
- **Pruebas:** Profiler antes/después.

### [ ] T-16.3 — Optimización de CPU y memoria
- **Prioridad:** `REC` (se aplica lo que la medición de T-16.1 justifique)
- **Subtareas:** Eliminar asignaciones por frame; evitar `Find`/`GetComponent` en `Update`; coste de colisionadores de islas; compresión de texturas; audio (T-14.5).
- **Dependencias:** T-16.1
- **Criterios de aceptación:** Sin picos de GC perceptibles en recorrido normal.
- **Pruebas:** Profiler (GC Alloc), Memory Profiler.

### [ ] T-16.4 — Tiempos de carga y guardado
- **Prioridad:** `OBL`
- **Subtareas:** Medir carga de región y escritura de guardado; evitar tirones al guardar.
- **Dependencias:** T-4.4, T-16.1
- **Criterios de aceptación:** Guardar no produce un tirón perceptible.
- **Pruebas:** Profiler durante guardado automático.

---

## ETAPA 17 — Calidad transversal: errores, regresión, casos límite y cierre

> Las tareas de esta etapa **se ejecutan durante todo el desarrollo** (ver 0.7). Lo único que ocurre al final es el cierre de calidad previo a H5.

### [ ] T-17.1 — Registro de errores
- **Prioridad:** `OBL`
- **Subtareas:** Archivo `Docs/ERRORES.md` (o issues de GitHub) con: pasos, esperado, observado, gravedad, archivo/objeto, corrección, verificación. Se crea al empezar la implementación (etapa 0–1).
- **Dependencias:** —
- **Criterios de aceptación:** Todo error encontrado queda registrado.

### [ ] T-17.2 — Pruebas automatizadas
- **Prioridad:** `REC` (las pruebas manuales siguen siendo obligatorias)
- **Subtareas:** Edit Mode: serialización de guardado, validación, migración, estados de misión, reproducibilidad del generador. Play Mode: reaparición, carga idempotente.
- **Dependencias:** etapas 4, 6, 9; decisión de uso de Test Framework (instalado, D-16). Se escriben junto a cada sistema, no al final.
- **Criterios de aceptación:** Todas pasan en Test Runner.
- **Pruebas:** Ejecutar Test Runner.

### [ ] T-17.3 — Lista de pruebas funcionales
- **Prioridad:** `OBL`
- **Subtareas:** Checklist (`Docs/PRUEBAS.md`) que cubra GDD §16: movimiento, cámara, recorridos obligatorios, saltos, encargos, transformaciones, checkpoints, guardado/carga, procedural, errores de guardado, coherencia visual/sonora. **Crece de forma incremental**: cada sistema terminado añade sus pruebas al checklist.
- **Dependencias:** se inicia con la etapa 2; se completa con las etapas 2–15
- **Criterios de aceptación:** Para H5: checklist completo ejecutado en build con resultados anotados. En cada hito: las secciones existentes ejecutadas (T-17.7).

### [ ] T-17.4 — Casos límite
- **Prioridad:** `OBL`
- **Subtareas:**
  - [ ] T-17.4.1 Guardado: archivo ausente, dañado, vacío, versión antigua/futura, sin permisos; cierre durante la escritura; cierre inesperado; cargar dos veces; Nueva partida con partida existente.
  - [ ] T-17.4.2 Checkpoints: caer sin checkpoint; caer repetidamente; activar checkpoint durante una caída; checkpoint de otra región.
  - [ ] T-17.4.3 Misiones: completar fuera de orden; volver tras abandonar; entregar dos veces; recoger objeto y caer.
  - [ ] T-17.4.4 Interacción: pulsar repetidamente; interactuar durante pausa/diálogo/caída.
  - [ ] T-17.4.5 Pausa: en el aire, en transición, en escena, Alt+Tab.
  - [ ] T-17.4.6 Mundo: quedarse atascado en geometría, saltar fuera de los límites, secuencia rota (saltarse un mecanismo).
  - [ ] T-17.4.7 Procedural: múltiples semillas, rutas bloqueadas, objetos solapados.
  - [ ] T-17.4.8 Resoluciones y relaciones de aspecto distintas.
- **Dependencias:** T-17.3. Cada grupo de casos se prueba en cuanto existe su sistema (p. ej. T-17.4.1 al terminar la etapa 4, T-17.4.2 al terminar la etapa 3); antes de H5 se repiten todos.
- **Criterios de aceptación:** Cada caso probado con resultado anotado; errores registrados en T-17.1.

### [ ] T-17.5 — Pruebas con jugadores
- **Prioridad:** `OBL`
- **Subtareas:** Sesiones con personas que no conocen el juego; observar comprensión de objetivos, acertijos, ruta; medir duración real (para D-01).
- **Dependencias:** H3 (sesión breve del bucle principal), H4 (ronda del vertical slice), antes de H5 (ronda con el juego completo)
- **Criterios de aceptación:** Hallazgos documentados y priorizados.

### [ ] T-17.6 — Corrección de errores
- **Prioridad:** `OBL`
- **Subtareas:** Priorizar por gravedad; corregir errores reproducibles antes de añadir funciones (continuo); verificar cada corrección.
- **Dependencias:** T-17.1
- **Criterios de aceptación:** Sin errores críticos ni bloqueantes abiertos al declarar H5.

### [ ] T-17.7 — Prueba de regresión por hito
- **Prioridad:** `OBL`
- **Descripción:** Al alcanzar cada hito (H1–H5), volver a probar lo ya terminado para detectar roturas causadas por sistemas nuevos.
- **Subtareas:**
  - [ ] T-17.7.1 Regresión H1.
  - [ ] T-17.7.2 Regresión H2.
  - [ ] T-17.7.3 Regresión H3.
  - [ ] T-17.7.4 Regresión H4.
  - [ ] T-17.7.5 Regresión H5 (completa).
- **Dependencias:** T-17.3
- **Criterios de aceptación:** Secciones existentes del checklist ejecutadas con resultado anotado en el registro de sesiones; errores en T-17.1.
- **Pruebas:** Las del propio checklist.

**Hito H5: versión completa candidata a entrega.** Todas las tareas `OBL` de desarrollo y contenido completadas (todas salvo T-18.1–T-18.3 y el cierre de T-19.1 y T-19.4, que pertenecen a H6); regiones aprobadas jugables de principio a fin; recursos definitivos integrados con licencias registradas; build candidata verificada (T-18.4.4) con el checklist T-17.3 y los casos límite T-17.4 pasados en ella; sin errores críticos ni bloqueantes abiertos. Lo que reste hasta H6 es solo configuración final, verificación en equipo limpio y empaquetado.

---

## ETAPA 18 — Build para Windows: builds por hito y verificación de la entrega

### [ ] T-18.1 — Configuración de build final
- **Prioridad:** `OBL`
- **Descripción:** Primera tarea de H6. Parte de la build candidata de H5 y solo aplica la configuración final.
- **Subtareas:** Escenas en orden correcto en Build Profiles; desactivar herramientas de depuración; icono, nombre y versión finales; confirmar backend (IL2CPP o Mono) y arquitectura x64. El backend se decide y se usa **a más tardar en la build candidata T-18.4.4**, para que la build final no introduzca un cambio sin probar.
- **Dependencias:** H5
- **Criterios de aceptación:** Build Release generada sin errores, con la misma configuración técnica que la build candidata salvo los ajustes finales anotados.
- **Pruebas:** Log de build.

### [ ] T-18.2 — Verificación de la build
- **Prioridad:** `OBL`
- **Subtareas:** Partida completa en la build final; salir y continuar; opciones persistentes; sin errores en `Player.log`; probar en un equipo distinto al de desarrollo y sin Unity instalado; probar con ruta con espacios/acentos.
- **Dependencias:** T-18.1
- **Criterios de aceptación:** Todo el checklist T-17.3 pasa en la build final y en un equipo limpio. Un error crítico se corrige en T-17.6 y se repite desde T-18.4.4 (ver la tabla de hitos).

### [ ] T-18.3 — Paquete de entrega
- **Prioridad:** `OBL`
- **Subtareas:** Carpeta comprimida con el ejecutable y `_Data`; instrucciones de ejecución y controles; documentación requerida por la asignatura; etiqueta Git de la versión entregada.
- **Dependencias:** T-18.2
- **Criterios de aceptación:** Un tercero descomprime y juega sin ayuda.
- **Pruebas:** Prueba en equipo limpio.

### [ ] T-18.4 — Builds de verificación por hito
- **Prioridad:** `OBL`
- **Descripción:** Generar y probar una build de Windows en cada hito desde H2, para detectar pronto problemas que solo aparecen fuera del Editor (rutas de guardado, escenas no incluidas, código de Editor, shaders eliminados).
- **Subtareas:**
  - [ ] T-18.4.1 Build H2: salir y continuar.
  - [ ] T-18.4.2 Build H3: bucle completo.
  - [ ] T-18.4.3 Build H4: vertical slice.
  - [ ] T-18.4.4 Build H5: candidata a entrega. Se genera con todo el contenido terminado y con el backend definitivo; sobre ella se ejecutan T-17.3, T-17.4 y T-17.7.5. Forma parte de H5 (no depende de H5).
- **Dependencias:** T-0.5; para cada subtarea, el contenido de su hito. T-18.4.4 requiere todo el desarrollo y contenido de H5 salvo las pruebas que se ejecutan sobre ella (T-17.3, T-17.4, T-17.7.5); los errores que esas pruebas encuentren se corrigen en T-17.6 y se genera una nueva build candidata.
- **Criterios de aceptación:** La build abre, se juega el contenido del hito y `Player.log` no muestra errores.
- **Pruebas:** Ejecución manual de cada build; revisión de `Player.log`.

---

## ETAPA 19 — Documentación y control de versiones (transversal)

### [ ] T-19.1 — Mantenimiento de este plan
- **Prioridad:** `OBL`
- **Subtareas:** Actualizar estado tras cada sesión; registro de sesiones (sección 4).
- **Dependencias:** —
- **Criterios de aceptación:** El plan refleja el estado real al final de cada sesión.

### [ ] T-19.2 — Documentación técnica
- **Prioridad:** `OBL`
- **Subtareas:** `Docs/ARQUITECTURA.md` (servicios, eventos, guardado, IDs); `Docs/CONVENCIONES.md`; cómo usar el generador de islas y el distribuidor; formato del archivo de guardado.
- **Dependencias:** etapas 1, 4, 9, 10
- **Criterios de aceptación:** Un compañero puede configurar un checkpoint, una misión y una transformación leyendo la documentación.

### [ ] T-19.3 — Documentación de diseño
- **Prioridad:** `OBL`
- **Subtareas:** Fichas de almas, regiones, acertijos; actualizar el GDD con decisiones tomadas; `Docs/LICENCIAS.md`.
- **Dependencias:** etapas 6, 8, 11, 13, 14

### [ ] T-19.4 — Control de versiones
- **Prioridad:** `OBL`
- **Subtareas:** Commits pequeños por funcionalidad; ramas por funcionalidad; no subir `Library/`, builds ni datos de guardado; etiquetas en cada hito (H1–H6); revisar `.meta` en cada commit.
- **Dependencias:** T-0.6
- **Criterios de aceptación:** Historial trazable; cada hito etiquetado.

---

## 4. Registro de sesiones

Plantilla para cada sesión:

```
### Sesión AAAA-MM-DD
1. Implementado:
2. Probado realmente (cómo y dónde: Editor / Play Mode / build):
3. Pendiente:
4. Errores o bloqueos:
5. Siguiente tarea recomendada:
```

### Sesión 2026-10-29 — Revisión inicial
1. **Implementado:** nada de código ni escenas. Se creó este plan (`Docs/PLAN_DE_DESARROLLO.md`).
2. **Probado realmente:** solo inspección de archivos del repositorio (manifiesto, `packages-lock.json`, `ProjectSettings`, escena, asset de entrada, Git). No se abrió el Editor ni se ejecutó Play Mode ni build.
3. **Pendiente:** todo el desarrollo. Las únicas subtareas marcadas como completadas son verificaciones de configuración por inspección (T-0.1.1–T-0.1.3, T-0.2.1, T-0.3.1, T-0.6.1).
4. **Errores o bloqueos:** H-01 (ruta de escena en Build Settings), H-04 (Interact en Hold), H-06 (`companyName` por defecto). Decisiones pendientes D-01 a D-19.
5. **Siguiente tarea recomendada:** T-0.1.4 / T-0.3 / T-0.4 (abrir el proyecto, corregir Build Settings, fijar nombre de compañía) y resolver D-03, D-04, D-05 y D-06, necesarias para las etapas 1–4.

### Sesión 2026-10-29 — Revisión 2 del plan
1. **Implementado:** solo cambios en este documento. Sin cambios en scripts, escenas, prefabs, paquetes ni configuración de Unity.
   - Prioridades `OBL` / `REC` / `OPC` en todas las tareas (0.1.1) y en las subtareas que difieren de su tarea; las alternativas del GDD (tipos de acertijo, mecanismo, transformación y objetivo) pasan a ser candidatas que se eligen por ficha (D-20).
   - Nuevas secciones 0.5 (recursos provisionales), 0.6 (dirección artística desde el primer prototipo) y 0.7 (pruebas continuas).
   - T-0.3.5 reducido a cuatro subcarpetas propuestas y justificadas, pendientes de aprobación (D-21).
   - T-0.2 y 3.1: paquetes clasificados en instalados directos, dependencia indirecta (Splines) y uso por decidir; ningún cambio sin aprobación.
   - Hitos redefinidos (tabla en la sección 1); H5 = versión completa candidata a entrega.
   - Tareas nuevas: T-1.5.4, T-1.5.5, T-2.2.11, T-2.2.12, T-2.4.5, T-2.4.6, T-5.1.8, T-7.2.8, T-9.1.6, T-13.1.1, T-13.1.2, T-13.10, T-15.2.1–T-15.2.4, T-15.3.1–T-15.3.7, T-17.7, T-18.4, T-0.6.6. Decisiones nuevas D-20 a D-23. Hallazgo nuevo H-15.
   - Ninguna tarea eliminada.
2. **Probado realmente:** solo inspección: `git remote -v` y `git branch -vv` (remoto `origin` configurado; `main` sigue a `origin/main` en `683eeae`, sin `fetch`), `ProjectSettings/EditorSettings.asset` (Force Text) y `ProjectSettings/VersionControlSettings.asset` (Visible Meta Files). Con esa evidencia se marcaron T-0.6.2 y T-0.6.4. El push inicial lo indicó la usuaria; no se consultó GitHub.
3. **Pendiente:** todo el desarrollo; aprobación del plan.
4. **Errores o bloqueos:** los mismos de la revisión inicial. `Docs/PLAN_DE_DESARROLLO.md` aún no está en ningún commit.
5. **Siguiente tarea recomendada:** tras aprobar el plan, T-0.6.6 (rama de trabajo y commit del plan), T-0.1.4, T-0.3, T-0.4 y resolver D-03 a D-06; en paralelo, T-13.1.1 y T-13.10.

### Sesión 2026-10-29 — Revisión 3 del plan
1. **Implementado:** solo cambios en este documento.
   - H5/H6: H5 exige todas las tareas `OBL` salvo T-18.1–T-18.3 y el cierre de T-19.1 y T-19.4, más la build candidata verificada (T-18.4.4); H6 contiene la configuración final, la verificación en equipo limpio y el paquete. Se añadió el procedimiento si H6 encuentra un error crítico. El backend de compilación se fija a más tardar en T-18.4.4.
   - Tabla de etapas: la etapa 17 ya no depende de «todas» (incluía la 18) y la etapa 12 se desarrolla junto a la 11 (T-11.2.3 necesita T-12.2).
   - T-12.3 dividida en T-12.3.1–T-12.3.6 con prioridad explícita; Timeline pasa a `OPC`. T-12.4 depende ahora de T-12.3.2 y T-12.3.3.
   - T-14.3 dividida en T-14.3.1–T-14.3.5 con prioridad explícita.
   - T-15.3.7 pasa a `OBL` (persistencia de las opciones implementadas, mecanismo libre); T-4.1.3 se aclara como uno de los mecanismos posibles.
   - Ninguna tarea eliminada; ninguna marcada como completada.
2. **Probado realmente:** nada; solo revisión del documento.
3. **Pendiente:** aprobación del plan y todo el desarrollo.
4. **Errores o bloqueos:** sin cambios respecto a la revisión 2.
5. **Siguiente tarea recomendada:** la misma de la revisión 2.
