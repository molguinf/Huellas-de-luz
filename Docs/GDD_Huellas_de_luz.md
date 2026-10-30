# HUELLAS DE LUZ
## Game Design Document (GDD)
**Versión:** 2.0  
**Estado:** Documento de diseño base  
**Género:** Aventura narrativa 3D, exploración y plataformas ligeras  
**Plataforma objetivo:** PC Windows  
**Motor:** Unity 6  
**Renderizado:** Universal Render Pipeline (URP)  
**Lenguaje:** C#  
**Modo:** Un jugador  
**Perspectiva:** Tercera persona

---

## 1. Visión general

*Huellas de luz* es una aventura narrativa 3D en tercera persona sobre el vínculo entre una persona y su perro, el duelo, la esperanza y la posibilidad de seguir adelante. El jugador controla a un hombre que, después de perder a su perro y atravesar un periodo de profundo dolor, despierta en un mundo extraño y oscuro situado entre distintos reinos.

Al principio cree que ha llegado al infierno. Un guardián le explica que se encuentra en uno de los niveles de ese mundo y que el camino hacia los reinos superiores será difícil. El protagonista descubre que su perro está en un reino celestial y emprende un viaje para encontrarlo.

Durante el recorrido atraviesa ruinas, precipicios, caminos antiguos e islas flotantes. Conoce almas de animales que conservan recuerdos, afectos o asuntos pendientes. Al ayudarlas, descubre fragmentos de sus historias y devuelve vida a lugares que habían quedado apagados.

La aventura combina exploración, movimiento, saltos, acertijos sencillos, interacción con personajes y objetos, encargos opcionales o principales y cambios persistentes en el entorno. Su identidad no depende del combate: el centro de la experiencia es explorar, ayudar, descubrir y transformar.

### 1.1 Experiencia que se busca transmitir

- Asombro ante paisajes amplios, misteriosos y mágicos.
- Curiosidad por descubrir qué ocurrió en cada lugar.
- Empatía hacia las almas animales y sus historias.
- Satisfacción al observar que las acciones del jugador restauran el mundo.
- Sensación de avance y esperanza, desde un entorno frío y oscuro hacia espacios más vivos y cálidos.
- Un cierre emocional centrado en el vínculo entre el protagonista y su perro.

### 1.2 Público y tono

La experiencia está dirigida a jugadores que disfrutan de aventuras narrativas, exploración, plataformas moderadas y mundos atmosféricos. El tono es emotivo, contemplativo y esperanzador. Puede tratar temas difíciles, pero no debe recurrir al impacto gratuito ni presentar el suicidio como una solución o como un medio deseable para reunirse con alguien fallecido.

---

## 2. Propuesta distintiva

La característica central de *Huellas de luz* es la **transformación visible y persistente del mundo a partir de las acciones del jugador**.

Ayudar a un alma animal no debe limitarse a mostrar un mensaje de misión completada o entregar un objeto. La acción debe producir una consecuencia reconocible en el escenario. Por ejemplo:

- Una zona gris y apagada recupera color.
- Aparecen flores, hierba o árboles luminosos.
- Se encienden faroles, cristales o símbolos antiguos.
- Una estructura rota se reconstruye.
- Un puente aparece o vuelve a ser transitable.
- Una isla suspendida se activa y se conecta con otra.
- La niebla se disipa y revela un camino.
- Se abre un atajo o una zona que antes era inaccesible.
- Cambia suavemente el ambiente sonoro o musical de una región.

La escala de la transformación depende de la importancia de la acción. Algunas misiones producen cambios pequeños y locales; otras pueden modificar una zona completa o habilitar la progresión principal.

**Regla de diseño:** cada transformación importante debe tener una causa comprensible, una respuesta visual o sonora y un estado que pueda conservarse al guardar y cargar la partida.

---

## 3. Pilares de diseño

1. **Exploración con propósito:** cada zona ofrece algo que descubrir, comprender, resolver o ayudar.
2. **Transformación ambiental:** el mundo responde de forma visible a las decisiones y acciones del jugador.
3. **Narrativa emocional:** personajes, escenarios, objetos y sonido refuerzan el viaje del protagonista.
4. **Progresión legible:** el jugador entiende su objetivo actual, los caminos disponibles y las consecuencias de sus acciones.
5. **Desafío justo:** saltos, acertijos y obstáculos se enseñan mediante el propio juego y no dependen de adivinar.
6. **Mundo diseñado y controlado:** los elementos narrativos y las rutas obligatorias se construyen manualmente; la generación procedural añade variedad secundaria sin comprometer la jugabilidad.
7. **Continuidad de la partida:** el progreso importante se conserva mediante checkpoints y guardado.

---

## 4. Historia y estructura narrativa

### 4.1 Premisa

El protagonista ha perdido a su perro, un compañero muy importante en su vida. La pérdida lo deja emocionalmente devastado. Después de su muerte, despierta en un reino oscuro y desconocido. Interpreta ese lugar como el infierno, pero un guardián le explica que se encuentra en uno de los niveles de ese mundo.

Más adelante descubre que su perro está en un reino celestial. Decide emprender el camino para encontrarlo. El viaje no consiste únicamente en avanzar físicamente: también le permite conocer las historias de otras almas animales, comprender el valor de los vínculos y atravesar un proceso emocional.

### 4.2 Desarrollo del viaje

La historia se presenta mediante escenas, diálogos breves, encuentros, objetos del entorno y cambios en los lugares. No es necesario explicar todo mediante largas conversaciones. El escenario debe aportar información narrativa.

El guardián introduce las reglas generales del mundo y orienta al protagonista. Las almas animales tienen historias y necesidades propias. Algunas pueden necesitar recuperar un objeto significativo, encontrar algo perdido, llegar a un lugar o completar una pequeña tarea.

La historia concreta de cada alma, sus diálogos, nombres y encargos se definirán durante el diseño de cada región. No se deben inventar como contenido definitivo sin validación de diseño.

### 4.3 Tratamiento emocional

El duelo debe tratarse con sensibilidad. El juego no debe presentar el suicidio como una solución deseable, una recompensa ni una vía recomendada para reunirse con un ser querido. El foco está en el dolor de la pérdida, el valor del vínculo, las consecuencias de las decisiones y la esperanza.

### 4.4 Final

El viaje culmina al llegar al reino celestial y reencontrarse con el perro. El cierre debe sentirse merecido y emotivo, apoyado por el recorrido y por las transformaciones que el jugador ayudó a producir. Los detalles de la escena final, su duración y la forma exacta del reencuentro quedan por definir durante la producción narrativa.

---

## 5. Mundo y regiones

El mundo está compuesto por regiones conectadas mediante caminos, ruinas, plataformas, precipicios e islas flotantes. La progresión principal debe ser diseñada manualmente y debe permitir que el jugador comprenda hacia dónde avanzar.

| Región | Función narrativa y jugable | Transformación característica |
|---|---|---|
| El despertar | Presentar al protagonista, el movimiento, la cámara y la sensación del reino oscuro. | Pequeñas luces o señales orientan hacia la salida. |
| Ruinas olvidadas | Introducir exploración, interacción y primeros acertijos. | Mecanismos antiguos vuelven a funcionar y habilitan caminos. |
| Camino de las almas | Presentar varias almas animales y sus encargos. | Regresan colores, vegetación y luces a zonas apagadas. |
| Umbral celestial | Elevar el desafío de plataformas y conectar rutas entre islas. | Puentes, mecanismos o islas se activan. |
| Reino de los perritos | Acercar al jugador al destino y ofrecer un entorno más cálido. | El paisaje alcanza un estado más vivo y luminoso. |
| Reencuentro | Resolver el arco emocional y cerrar el viaje. | El entorno transmite calma, calidez y cierre. |

Esta tabla expresa una estructura conceptual. La cantidad final de niveles, su tamaño, duración, orden definitivo y contenido detallado se concretarán mediante prototipos y planificación.

### 5.1 Lectura del espacio

- Los puntos de interés deben distinguirse por silueta, iluminación, color, movimiento o sonido.
- Las vistas lejanas deben sugerir destinos, rutas, secretos o lugares narrativamente importantes.
- La ruta principal debe ser reconocible sin eliminar la posibilidad de explorar.
- Los desvíos pueden contener coleccionables, recuerdos, vistas, pequeñas historias o secretos.
- La decoración no debe saturar la escena ni ocultar plataformas, personajes u objetos interactivos.

---

## 6. Mecánicas de juego

### 6.1 Movimiento del protagonista

El jugador controla al protagonista desde una cámara en tercera persona.

Acciones previstas:
- Caminar.
- Correr.
- Saltar.
- Desplazarse por plataformas y superficies de distinta altura.
- Interactuar con objetos, mecanismos y personajes.

El control debe ser responsivo y predecible. La aceleración, velocidad, altura del salto, control en el aire y tolerancia de los saltos deben ajustarse mediante pruebas de jugabilidad. Los valores numéricos definitivos no están fijados en este documento.

El personaje debe respetar colisiones, no atravesar el suelo y no quedar atrapado fácilmente en geometría del escenario. Debe existir una forma de recuperarse de caídas accidentales, normalmente mediante el checkpoint correspondiente.

### 6.2 Cámara

La cámara principal es de tercera persona, situada detrás y ligeramente por encima del protagonista. Debe permitir leer el camino, anticipar saltos y apreciar el paisaje sin ocultar obstáculos importantes.

Se prevén movimientos suaves y ajustes de encuadre para situaciones narrativas. Las cámaras especiales pueden utilizarse en encuentros con el guardián, transformaciones importantes y el reencuentro final. La cámara no debe quitar el control al jugador de forma innecesaria.

### 6.3 Interacción

La interacción se realiza mediante una acción sencilla, por ejemplo la tecla **E**, siempre que coincida con el sistema de entrada configurado en el proyecto.

Cuando el jugador se encuentre dentro del rango:
- El objeto o personaje debe mostrar una señal visual de que puede interactuarse.
- La interfaz debe indicar la acción disponible.
- La interacción debe ejecutarse una sola vez por activación, salvo que el diseño requiera mantener pulsado.
- Debe existir una respuesta visual, sonora o textual.

Los elementos interactivos pueden ser personajes, objetos narrativos, mecanismos, puertas, palancas, símbolos y puntos de activación.

### 6.4 Encargos de las almas animales

El ciclo general de un encargo es:

1. El jugador encuentra un alma animal.
2. Se presenta su situación mediante diálogo, animación o pistas del entorno.
3. El jugador recibe un objetivo comprensible.
4. Explora la zona para localizar un objeto, activar algo o completar una tarea.
5. El juego reconoce el cumplimiento del objetivo.
6. El jugador recibe una respuesta del alma, cuando corresponda.
7. Se activa la transformación ambiental asociada.
8. Se actualiza el progreso de la misión y se conserva al guardar la partida.

Los encargos pueden ser principales o secundarios. Los principales pueden habilitar la ruta necesaria para continuar. Los secundarios amplían la historia, ofrecen secretos o restauran partes opcionales del mundo.

No todos los encargos deben tener la misma estructura. Se puede variar la forma de encontrar el objetivo, pero el jugador debe recibir pistas suficientes para comprender qué hacer.

### 6.5 Acertijos

Los acertijos pueden incluir:
- Activar mecanismos.
- Encontrar y relacionar símbolos.
- Descubrir secuencias.
- Mover o colocar objetos.
- Encender elementos en un orden.
- Usar plataformas y elementos del escenario para alcanzar un lugar.
- Restaurar mecanismos mediante la interacción con el entorno.

Cada acertijo debe enseñar sus reglas con pistas visuales, sonoras o narrativas. No debe depender de una solución arbitraria que el jugador no tenga forma razonable de deducir.

### 6.6 Plataformas y obstáculos

Los desafíos de plataformas deben aumentar gradualmente. Las distancias y alturas deben ser compatibles con las capacidades reales del personaje. Los saltos obligatorios deben probarse en el juego, no solo estimarse visualmente en el editor.

Los obstáculos pueden incluir precipicios, plataformas móviles si se aprueban para una zona, caminos estrechos, mecanismos temporizados y rutas que se habilitan al restaurar el entorno. No se establece el combate como sistema principal.

### 6.7 Recompensas

Las recompensas principales son:
- Nuevas rutas, atajos y zonas accesibles.
- Cambios visibles en el mundo.
- Historias y recuerdos de las almas animales.
- Secretos y objetos opcionales.
- Progreso hacia el reino celestial.
- Sensación de haber ayudado y restaurado un lugar.

No se requiere un sistema de experiencia, niveles o estadísticas de combate para sostener la identidad del juego.

---

## 7. Checkpoints, fallos y reaparición

Los checkpoints son puntos seguros distribuidos manualmente en las regiones. Su ubicación debe evitar que el jugador pierda demasiado progreso por una caída o un error de recorrido.

### 7.1 Funcionamiento esperado

- El jugador activa un checkpoint al llegar a él o interactuar con él, según la presentación visual elegida.
- El juego registra cuál es el último checkpoint activado.
- Si el protagonista cae al vacío o entra en una situación de fallo, reaparece en el último checkpoint válido.
- La reaparición restaura una posición segura y evita que el jugador quede dentro de una pared, fuera del escenario o sobre una plataforma inestable.
- El checkpoint activado debe conservarse al cerrar y volver a abrir el juego.
- Los checkpoints deben estar ubicados antes o después de desafíos importantes según el ritmo del nivel.

### 7.2 Qué se conserva al reaparecer

La reaparición no debe deshacer injustificadamente el progreso narrativo. Como regla general:
- Se conserva el último checkpoint activado.
- Se conserva el progreso de encargos que ya haya sido confirmado.
- Se conservan las transformaciones ambientales completadas.
- Se conservan los mecanismos o rutas que ya hayan quedado permanentemente activados.
- Los objetos temporales o estados de un acertijo pueden reiniciarse si así lo define el diseño de ese acertijo.

El comportamiento exacto de cada desafío debe estar definido: no todos los mecanismos tienen que persistir si son parte de un reto temporal.

---

## 8. Guardado, carga y continuidad de partida

El juego debe permitir que el jugador salga y continúe más adelante sin perder el progreso importante. El guardado no es un añadido opcional de último momento: forma parte de la experiencia y debe diseñarse junto con misiones, checkpoints y transformaciones.

### 8.1 Guardado automático

Se prevé guardado automático en momentos seguros y significativos, como:
- Al activar un checkpoint.
- Al completar un encargo.
- Al confirmar una transformación ambiental importante.
- Al desbloquear una ruta principal.
- Al entrar en una región o completar un hito narrativo importante.
- Al salir correctamente desde el menú del juego.

No es necesario escribir datos en disco cada frame. El guardado debe producirse en eventos concretos y seguros para evitar escrituras constantes.

### 8.2 Salir del juego y continuar

Cuando el jugador elige **Salir al escritorio** desde el menú:
1. El juego solicita guardar los datos pendientes.
2. Se completa el guardado antes de cerrar, siempre que sea posible.
3. Al iniciar el juego de nuevo, el menú ofrece **Continuar** si existe una partida válida.
4. Al seleccionar Continuar, se carga la región, el checkpoint, el estado del protagonista y el progreso persistente.
5. El jugador aparece en una posición segura y con el mundo en el mismo estado de progreso.

También se debe contemplar el cierre inesperado. Por eso, los eventos importantes deben activar guardados automáticos antes de que el jugador dependa únicamente de pulsar Salir.

### 8.3 Datos que debe conservar la partida

Como mínimo, el sistema de guardado debe contemplar:
- Identificador de la versión del formato de guardado.
- Región o escena actual.
- Último checkpoint activado.
- Posición y orientación segura del jugador, cuando corresponda.
- Progreso de la historia y objetivos principales.
- Estado de cada encargo: no iniciado, activo, completado u otro estado que el diseño requiera.
- Objetos importantes obtenidos o entregados.
- Transformaciones ambientales completadas.
- Mecanismos y rutas que deben permanecer desbloqueados.
- Secretos u objetos opcionales recogidos, si forman parte del progreso persistente.
- Ajustes de juego que deban persistir, si se implementan.

No se deben guardar referencias directas a objetos de escena como si fueran datos permanentes. Los elementos persistentes deben identificarse mediante identificadores estables y reconstruirse al cargar.

### 8.4 Carga y validación

- Si existe una partida válida, se habilita Continuar.
- Si no existe, se inicia una partida nueva.
- Si el archivo está dañado o incompleto, el juego debe informar del problema y evitar bloquear el inicio.
- La carga debe validar que la región, el checkpoint y los identificadores guardados todavía existan.
- El sistema debe evitar duplicar objetos, recompensas o transformaciones al cargar varias veces.
- Debe existir una forma de iniciar una partida nueva sin confundirla con Continuar.

### 8.5 Diseño técnico del guardado

La implementación debe separar los datos guardados de los objetos de escena. Se recomienda un sistema de datos serializables con identificadores estables para misiones, checkpoints y transformaciones. El mecanismo de almacenamiento local se decidirá según la arquitectura del proyecto; puede utilizar archivos locales de datos en el equipo del jugador.

El guardado debe reducir el riesgo de perder el último archivo válido. Se recomienda escribir primero un archivo temporal y reemplazar el archivo principal cuando la escritura termine correctamente, además de validar los datos antes de cargarlos.

La interfaz final de ranuras de guardado, múltiples perfiles o copias manuales no está definida. La primera versión puede utilizar una única partida local con Continuar y Nueva partida, siempre que el diseño final lo apruebe.

---

## 9. Generación procedural

La generación procedural aporta variedad y reduce trabajo manual, pero no controla la estructura crítica de la aventura.

### 9.1 Elementos aptos para generación

- Rocas y variaciones de vegetación.
- Pequeños restos de ruinas.
- Decoración ambiental.
- Islas secundarias u opcionales.
- Secretos dentro de zonas autorizadas.
- Variaciones de detalles del paisaje.

### 9.2 Elementos diseñados manualmente

- Ruta principal.
- Plataformas obligatorias y conexiones críticas.
- Personajes y almas animales.
- Objetivos de misión.
- Acertijos principales.
- Checkpoints.
- Entradas y salidas de región.
- Transformaciones narrativas importantes.
- Puntos de interacción y escenas clave.

### 9.3 Reglas de seguridad

- Utilizar semillas configurables y reproducibles.
- Definir áreas protegidas donde no se puedan colocar objetos.
- Validar distancias entre plataformas y accesibilidad de saltos.
- Evitar objetos superpuestos, flotantes o colocados dentro de la geometría.
- No bloquear rutas, personajes, objetivos, cámaras ni checkpoints.
- Limitar el tamaño y la cantidad de elementos generados.
- Permitir limpiar y regenerar únicamente los objetos que pertenezcan al generador.
- Probar múltiples semillas y conservar las configuraciones que hayan sido validadas.

### 9.4 Generador propio de islas

La primera aproximación será un generador propio en C# para crear geometría de islas flotantes mediante parámetros y semillas, evitando depender de un asset comercial de pago.

La herramienta puede evolucionar para controlar:
- Radio y dimensiones.
- Altura y profundidad inferior.
- Irregularidad del contorno.
- Ruido y variación de la superficie.
- Resolución de la malla.
- Forma superior suficientemente transitable.
- Colisionador apropiado.
- Semilla reproducible.

El generador debe comenzar como prototipo aislado. No se considera terminado hasta probar la malla, colisiones, rendimiento, repetibilidad y posibilidad real de caminar y saltar sobre las islas. Las islas de la ruta principal se diseñarán y revisarán manualmente aunque utilicen geometría generada.

---

## 10. Dirección artística

### 10.1 Estilo visual

Fantasía 3D estilizada, con ruinas antiguas, precipicios, islas suspendidas, niebla, grandes siluetas y puntos de luz que orientan al jugador. El mundo debe sentirse inmenso y misterioso, pero también legible y habitable.

La inspiración puede tomar como referencia la sensación de escala, exploración y atmósfera contemplativa de juegos de fantasía como *Sky*, sin copiar sus escenarios, personajes, criaturas, interfaz, música, modelos ni recursos.

### 10.2 Evolución cromática

**Estado inicial:** tonos fríos, desaturados, sombras, niebla y luces escasas. Debe transmitir soledad y misterio sin impedir la lectura del escenario.

**Estado restaurado:** incorporación gradual de colores, vegetación, flores luminosas, reflejos, dorados y luces cálidas. La recuperación debe ser perceptible y coherente con la importancia de la acción.

El color no debe ser el único indicador de progreso. Se combinará, cuando sea posible, con cambios de forma, iluminación, animación, sonido o apertura física de rutas.

### 10.3 Composición

- Utilizar puntos de interés que guíen la mirada.
- Mantener contraste suficiente entre plataformas y fondo.
- Evitar que la niebla o los efectos oculten peligros.
- Reservar vistas amplias para momentos de descubrimiento.
- Mantener coherencia de escala entre protagonista, arquitectura, islas y objetos.
- No llenar todos los espacios: el vacío también puede reforzar la escala y el tono.

---

## 11. Audio

El audio acompaña el estado emocional y la lectura del mundo.

Elementos previstos:
- Música ambiental por región.
- Viento y ambiente de espacios abiertos.
- Pasos y sonidos de movimiento.
- Sonidos de mecanismos y acertijos.
- Señales de interacción.
- Respuesta sonora al completar encargos.
- Cambios suaves de ambiente o música cuando una zona se restaura.
- Sonido y música específicos para momentos narrativos importantes.

El audio debe ayudar a comunicar acciones y cambios sin saturar. Las fuentes musicales y efectos utilizados deben contar con permisos o licencias adecuados para el proyecto.

---

## 12. Interfaz, menús y accesibilidad

### 12.1 Interfaz durante el juego

La interfaz debe ser discreta y legible. Puede mostrar:
- Indicación de interacción al acercarse a un objeto.
- Objetivo actual o recordatorio breve.
- Subtítulos de diálogos.
- Avisos de checkpoint activado.
- Confirmación de misión completada.
- Avisos de guardado cuando aporten información útil.

No debe llenar la pantalla de marcadores permanentes ni convertir la exploración en una lista de iconos.

### 12.2 Menú principal

Se prevén estas opciones:
- **Continuar:** carga la partida válida más reciente.
- **Nueva partida:** inicia una partida nueva con confirmación si ya existe progreso.
- **Opciones:** ajustes disponibles.
- **Salir:** cierra el juego de forma segura.

Las opciones definitivas de audio, vídeo, controles, idioma y accesibilidad se definirán durante producción.

### 12.3 Menú de pausa

Debe permitir:
- Reanudar.
- Consultar opciones.
- Volver al menú principal, con confirmación y guardado cuando corresponda.
- Salir al escritorio, realizando el guardado pendiente.

Al pausar, el juego debe detener o gestionar correctamente el tiempo de juego, la cámara, los controles y los sonidos. Los diálogos o escenas que no deban interrumpirse tendrán un comportamiento definido.

### 12.4 Accesibilidad y legibilidad

- Subtítulos legibles y con tiempo suficiente.
- Indicaciones que no dependan exclusivamente del color.
- Contraste suficiente para distinguir caminos y plataformas.
- Señales visuales y sonoras para interacciones importantes.
- Controles consistentes.
- Opciones adicionales de accesibilidad por evaluar según alcance y tiempo.

---

## 13. Tecnología y herramientas de producción

### 13.1 Base tecnológica

| Elemento | Tecnología |
|---|---|
| Motor | Unity 6 |
| Renderizado | Universal Render Pipeline (URP) |
| Programación | C# |
| Plataforma | PC Windows |
| Control | Sistema de entrada configurado en el proyecto; debe verificarse antes de implementar controles |
| Control de versiones | Git y GitHub |
| Entorno de código asistido | Visual Studio Code con agente de Claude, según configuración local |

La versión exacta del editor, paquetes y sistema de entrada se verificará en el proyecto. No se debe asumir que una API o paquete es compatible solo por pertenecer a Unity 6.

### 13.2 Paquetes de Unity preparados

Los siguientes paquetes ya están instalados en el proyecto y forman parte de las herramientas disponibles. Su uso debe responder a necesidades concretas del diseño.

| Paquete | Uso previsto en Huellas de luz |
|---|---|
| **Splines** | Crear caminos curvos, senderos, recorridos y distribuir elementos a lo largo de curvas. |
| **Terrain Tools** | Esculpir terrenos, montañas, acantilados y superficies naturales cuando una región lo necesite. |
| **ProBuilder** | Construir prototipos de plataformas, puentes, ruinas, paredes y geometría de prueba dentro de Unity. |
| **Cinemachine** | Configurar cámara de tercera persona, seguimiento suave y encuadres narrativos. |

La presencia de un paquete no obliga a utilizarlo en todos los niveles. Debe evitarse añadir dependencias innecesarias. La compatibilidad exacta y las versiones instaladas se verifican en `Packages/manifest.json` y `Packages/packages-lock.json`.

### 13.3 Herramienta de islas

El proyecto no depende del asset comercial **Procedural Floating Island Generator**. Se prioriza una herramienta propia en C# para generación controlada de islas, con semillas reproducibles y validaciones de jugabilidad. Se pueden evaluar herramientas gratuitas adicionales si aportan una ventaja real y su licencia es adecuada.

### 13.4 Skills disponibles para el trabajo asistido por IA

El entorno de trabajo cuenta con seis Skills preparadas para orientar tareas especializadas:

| Skill | Ámbito de apoyo |
|---|---|
| **Unity 6 + C# Developer** | Scripts, arquitectura sencilla, compatibilidad con Unity 6, Inspector y depuración. |
| **Procedural World Generation** | Generación reproducible, parámetros, límites, zonas protegidas y validación. |
| **Art Director de fantasía 3D** | Coherencia visual, paletas, iluminación, materiales, niebla y atmósfera. |
| **Level Designer** | Diseño de recorridos, plataformas, acertijos, checkpoints, ritmo y legibilidad. |
| **QA y optimización** | Pruebas, errores, colisiones, casos límite, guardado y rendimiento. |
| **Git y gestión del proyecto** | Ramas, cambios controlados, commits, protección de archivos y trazabilidad. |

Estas Skills son guías de trabajo para asistentes de IA; no son paquetes de Unity ni sistemas ejecutables dentro del videojuego. Se utilizan como apoyo según la naturaleza de cada tarea. La documentación de diseño de este GDD prevalece sobre recomendaciones genéricas de una Skill.

---

## 14. Organización conceptual del proyecto

La organización exacta debe respetar la estructura existente del repositorio. Como referencia, el proyecto puede separar:

- `Assets/Scenes`: escenas y regiones.
- `Assets/Scripts/Player`: movimiento y control del protagonista.
- `Assets/Scripts/Camera`: cámara y encuadres.
- `Assets/Scripts/Interaction`: interacción con objetos y personajes.
- `Assets/Scripts/Quests`: encargos y progreso de objetivos.
- `Assets/Scripts/World`: transformaciones, mecanismos y activación de rutas.
- `Assets/Scripts/Checkpoints`: activación y reaparición.
- `Assets/Scripts/Save`: datos, guardado y carga.
- `Assets/Scripts/Procedural`: generación secundaria e islas.
- `Assets/Prefabs`: objetos reutilizables.
- `Assets/Materials`, `Assets/Models`, `Assets/Audio` y `Assets/UI`: recursos visuales, sonoros e interfaz.
- `Assets/ScriptableObjects`: datos configurables, si la arquitectura lo requiere.
- `docs`: GDD y documentación del proyecto.

Esta estructura es orientativa, no una orden de reorganizar el repositorio. Cualquier reorganización debe considerar las referencias serializadas de Unity y el estado de Git.

---

## 15. Progresión y estructura de contenido

La progresión combina avance espacial, narrativo y ambiental.

- El avance espacial se produce al descubrir caminos, superar plataformas y abrir conexiones.
- El avance narrativo se produce al conocer al guardián y las historias de las almas animales.
- El avance ambiental se produce al restaurar zonas y observar sus cambios.
- El avance persistente se conserva mediante misiones, transformaciones, checkpoints y guardado.

Las misiones principales deben habilitar el recorrido hacia el destino. Las misiones secundarias pueden ofrecer historias, secretos o restauraciones opcionales sin bloquear injustamente la historia principal.

### 15.1 Duración

Existe un requisito académico expresado como «por lo menos un día jugando», cuyo significado exacto debe confirmarse: podría referirse a un ciclo de día y noche, a una jornada de juego o a una duración extensa. No se fija una duración total en horas hasta aclararlo con el docente y medir el contenido mediante pruebas. La duración debe surgir de regiones, desafíos, exploración y ritmo reales, no de alargar artificialmente los desplazamientos.

---

## 16. Criterios globales de calidad

El juego debe considerarse funcional cuando, en las partes implementadas:

- El protagonista puede moverse, saltar e interactuar de manera consistente.
- La cámara permite leer el espacio y no interfiere con la jugabilidad.
- Los recorridos obligatorios se pueden completar.
- Los saltos y colisiones han sido probados en ejecución.
- Los encargos presentan objetivos comprensibles y reconocen su cumplimiento.
- Las transformaciones ambientales responden a eventos concretos y se perciben claramente.
- Los checkpoints registran el último punto seguro y permiten reaparecer correctamente.
- El guardado conserva progreso relevante al salir y volver a entrar.
- La carga no duplica recompensas ni reinicia transformaciones completadas.
- La generación procedural no bloquea rutas ni crea situaciones imposibles.
- El juego comunica errores de guardado o carga sin bloquear al jugador.
- El contenido visual y sonoro mantiene una identidad coherente.
- Las pruebas realizadas y las limitaciones conocidas están documentadas.

---

## 17. Riesgos y decisiones de diseño pendientes

| Tema | Estado / decisión pendiente |
|---|---|
| Duración requerida | Confirmar qué significa exactamente «un día jugando» con el docente. |
| Cantidad y tamaño de regiones | Se definirá con prototipos y alcance académico. |
| Historia de cada alma animal | Crear fichas narrativas por personaje y misión. |
| Controles definitivos | Verificar sistema de entrada y decidir asignaciones finales. |
| Sistema de guardado | Definir formato, ubicación local y política de una o varias partidas. |
| Checkpoints | Determinar distribución por región y comportamiento de acertijos temporales. |
| Generador de islas | Prototipar y validar geometría, colisiones, rendimiento y repetibilidad. |
| Dirección artística final | Definir referencias visuales propias, paletas y recursos disponibles. |
| Recursos externos | Comprobar licencias y permisos de modelos, texturas, música y efectos. |
| Rendimiento | Medir en el equipo objetivo y en una build de Windows. |

Las decisiones pendientes no deben confundirse con características ya implementadas o aprobadas. Cuando se tome una decisión, debe reflejarse en este documento o en documentación complementaria.

---

## 18. Glosario

- **Checkpoint:** punto seguro desde el que el jugador reaparece después de un fallo.
- **Guardado automático:** registro de progreso en eventos definidos sin que el jugador tenga que guardar manualmente.
- **Carga:** recuperación de los datos guardados para continuar una partida.
- **Transformación ambiental:** cambio visual o funcional del escenario activado por el progreso.
- **Generación procedural:** creación de contenido a partir de reglas, parámetros y semillas.
- **Semilla:** valor que permite reproducir una misma distribución procedural.
- **Prefab:** objeto reutilizable de Unity.
- **URP:** Universal Render Pipeline, sistema de renderizado de Unity.
- **Spline:** curva que puede utilizarse para definir caminos, recorridos o distribución de elementos.
- **Build:** versión ejecutable del juego.
- **Skill:** conjunto de instrucciones reutilizables que orienta a un asistente de IA en un tipo de tarea.

---

## 19. Referencias de producción

- Unity Manual — Package Manager: https://docs.unity3d.com/Manual/Packages.html
- Unity Manual — Splines: https://docs.unity3d.com/Packages/com.unity.splines@latest
- Unity Manual — Terrain Tools: https://docs.unity3d.com/Packages/com.unity.terrain-tools@latest
- Unity Manual — ProBuilder: https://docs.unity3d.com/Packages/com.unity.probuilder@latest
- Unity Cinemachine Manual: https://docs.unity.cn/Packages/com.unity.cinemachine%403.0/manual/index.html
- Unity — Game Design Document Template: https://connect-prd-cdn.unity.com/20201215/83f3733d-3146-42de-8a69-f461d6662eb1/Game-Design-Document-Template.pdf
- Unity — One-Page Game Design Document: https://unity.com/blog/one-page-game-design-document

Las referencias sirven como documentación técnica y apoyo de diseño. La identidad, historia y mecánicas descritas en este documento pertenecen al diseño de *Huellas de luz*.
