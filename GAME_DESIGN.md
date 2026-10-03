# GAME_DESIGN.md — Cacao Quest: del vivero al licor de cacao

> Documento de diseño del videojuego · Versión 0.1 (diseño previo a la implementación)
> Programa de Ingeniería Agroindustrial · Uso previsto: feria estudiantil

---

## 1. Nombre y descripción del videojuego

**Nombre provisional:** *Cacao Quest: del vivero al licor de cacao*

**Género:** plataformas 2D de desplazamiento lateral con estaciones educativas.

**Descripción breve:**
El jugador controla a un joven aprendiz de la cadena del cacao que recorre una finca y una pequeña planta de transformación. El escenario avanza de izquierda a derecha y está dividido en ocho estaciones, desde el vivero hasta la obtención del licor de cacao. En cada estación el avatar realiza una actividad corta (recolectar, clasificar, ordenar, esquivar o ajustar un parámetro), responde una pregunta educativa y obtiene una insignia.

El juego busca que un visitante de feria comprenda, en pocos minutos, que el chocolate empieza en el campo y que su calidad depende de decisiones técnicas tomadas en cada etapa: justamente el campo de trabajo de la Ingeniería Agroindustrial.

**Duración objetivo:**
- Versión completa (8 estaciones): de 6 a 8 minutos.
- Versión mínima viable (1 estación): de 2 a 3 minutos.

**Tono visual:** colorido, amable y limpio, con ilustraciones planas tipo *flat* o *pixel art* sencillo de creación propia, inspirado en el paisaje cacaotero colombiano (árboles de sombra, cacaotales, marquesinas de secado).

---

## 2. Público objetivo

| Segmento | Descripción | Implicaciones de diseño |
|---|---|---|
| **Principal** | Estudiantes de educación media (aprox. 14 a 18 años) que visitan la feria y exploran opciones de carrera. | Controles inmediatos, textos breves, partidas cortas, recompensas visibles. |
| **Secundario** | Estudiantes universitarios de primeros semestres, docentes y familias acompañantes. | Contenido técnico correcto, sin infantilizar. |
| **Contexto de uso** | Computador de stand, a veces proyectado en pantalla grande, con fila de visitantes y ruido ambiente. | Partidas que no superen 8 minutos, reinicio rápido, juego comprensible sin sonido. |

**Supuestos:**
- La mayoría de jugadores conoce juegos de plataformas, pero no todos.
- Ningún jugador tiene conocimientos previos sobre el cacao.
- Un monitor del programa puede acompañar al jugador, aunque el juego debe entenderse sin explicación.

---

## 3. Objetivo educativo

### Objetivo general
Que el visitante identifique las etapas principales de la cadena productiva del cacao, desde la selección de plántulas hasta la obtención del licor de cacao, y reconozca el papel de la Ingeniería Agroindustrial en la calidad del producto.

### Objetivos específicos
Al terminar la partida, el jugador podrá:

1. **Ordenar** las ocho etapas de la cadena: vivero → siembra → manejo → cosecha → beneficio (apertura y extracción) → fermentación → secado → transformación.
2. **Reconocer** criterios básicos de calidad en el campo: plántulas sanas y vigorosas, y mazorcas maduras frente a verdes o enfermas.
3. **Explicar** con sus palabras por qué la fermentación y el secado son decisivos para el sabor y la conservación del grano.
4. **Diferenciar** el licor de cacao (pasta obtenida al moler los granos tostados) de una bebida alcohólica, un error frecuente en el público general.
5. **Asociar** al menos dos de estas etapas con actividades profesionales de un ingeniero agroindustrial (control de procesos, calidad, poscosecha, transformación).

### Principios pedagógicos
- **Aprender haciendo:** cada concepto se vive primero en una actividad y luego se refuerza con una pregunta.
- **Retroalimentación inmediata:** toda respuesta explica por qué es correcta o incorrecta.
- **Microcontenido:** como máximo dos frases de texto por pantalla informativa.
- **Error sin castigo fuerte:** equivocarse resta pocos puntos y siempre se muestra la respuesta correcta.

> **Validación de contenidos:** los datos técnicos de este documento (tiempos, temperaturas, humedades, distancias) son valores de referencia aproximados que dependen de la variedad, la región y las prácticas de cada finca. Deben ser revisados por docentes del programa antes de publicar el juego. En pantalla se presentarán con expresiones como «aproximadamente» o «en muchas fincas».

---

## 4. Historia del juego

**Protagonista:** *Kakaw* (nombre provisional y editable), aprendiz de agroindustria. Su apariencia será neutra y personalizable en versiones futuras.

**Mentora:** *Doña Teo*, productora de cacao con experiencia, que aparece al inicio de cada estación con un consejo breve. Su nombre alude a *Theobroma cacao*.

**Premisa:**
> La cooperativa del pueblo quiere elaborar su propio chocolate de origen, pero el último lote no salió bien: los granos estaban mal fermentados y húmedos. Doña Teo le propone a Kakaw recorrer todo el proceso, del vivero a la planta, para aprender a hacerlo bien. Al final del camino, si Kakaw logra un lote de calidad, la cooperativa obtendrá su primer **licor de cacao** listo para convertirse en chocolate.

**Estructura narrativa:**
1. **Introducción** (pantalla de historia, máximo 3 viñetas): el problema del lote fallido.
2. **Recorrido:** ocho estaciones; cada una termina con un diálogo breve de Doña Teo.
3. **Cierre:** Kakaw entrega el licor de cacao en la planta, la cooperativa celebra y se muestran las insignias obtenidas y un mensaje del programa de Ingeniería Agroindustrial.

---

## 5. Mecánica principal

### Bucle de juego
```
Avanzar por el escenario → Llegar a la estación → Leer el consejo de la mentora
→ Ejecutar la actividad corta → Responder la pregunta educativa
→ Recibir la insignia y los puntos → Continuar a la siguiente estación
```

### Mecánicas base (todas las escenas de recorrido)
- **Movimiento lateral:** caminar a izquierda y derecha con aceleración suave.
- **Salto:** salto simple con altura fija; se permite un pequeño margen para saltar justo después de dejar una plataforma (*coyote time*, unos 0,1 s) para que el juego resulte amable con jugadores novatos.
- **Colisiones:** suelo, plataformas (troncos, cajones, terrazas) y obstáculos suaves (charcos, ramas). No hay enemigos violentos: los obstáculos solo hacen retroceder al avatar o le restan unos pocos puntos.
- **Recolección:** objetos que se recogen al tocarlos (mazorcas, semillas, gotas de agua, hojas sanas), cada uno con su propio valor de puntos.
- **Zona de estación:** al entrar en ella se detiene el desplazamiento de la cámara y se activa el reto de la estación.

### Mecánica de la pregunta educativa
- Pregunta de opción múltiple con 3 opciones, cuyo orden se mezcla en cada partida.
- Se responde con el ratón o con las teclas 1, 2 y 3.
- Sin límite de tiempo: en una feria la presión de tiempo genera ansiedad y filas lentas.
- **Acierto:** puntos completos, explicación breve y animación de la insignia.
- **Error:** se muestra la respuesta correcta con la explicación, el jugador obtiene una parte de los puntos y la insignia queda en versión «bronce».

### Dificultad
Baja y constante. El objetivo es que más del 90 % de los visitantes complete el recorrido. El desafío está en hacerlo mejor (más puntos y más insignias de oro), no en sobrevivir.

---

## 6. Controles

| Acción | Teclado (principal) | Alternativa | Ratón |
|---|---|---|---|
| Moverse a la izquierda | `←` | `A` | — |
| Moverse a la derecha | `→` | `D` | — |
| Saltar | `Espacio` | `↑` o `W` | — |
| Interactuar o usar herramienta | `E` | `Enter` | Clic sobre el objeto (según la actividad) |
| Elegir una respuesta | `1`, `2`, `3` | Flechas + `Enter` | Clic en la opción |
| Pausa | `P` | `Esc` | Botón de pausa |
| Silenciar o activar el sonido | `M` | — | Botón de sonido |

**Reglas de control:**
- Los controles aparecen en pantalla durante los primeros segundos de la primera escena y en el menú de pausa.
- Ninguna acción requiere pulsaciones rápidas ni combinaciones de teclas.
- Todas las pantallas de menú se pueden recorrer solo con teclado.
- **Futuro:** controles táctiles en pantalla y soporte de gamepad.

---

## 7. Descripción de cada estación

Cada estación sigue el mismo esquema: **zona de recorrido → consejo de la mentora → actividad → pregunta → insignia.** Duración objetivo: de 40 a 60 segundos por estación.

### Estación 1 · Selección de plántulas (Vivero)
- **Ambiente:** vivero con polisombra, bolsas con plántulas en hileras.
- **Concepto clave:** una buena plantación empieza con material vegetal sano, vigoroso y de origen conocido. Muchas fincas usan plantas injertadas con clones seleccionados por productividad y tolerancia a enfermedades.
- **Actividad (clasificar):** pasan plántulas por una mesa; el jugador acepta (`E`) las sanas (tallo recto, hojas verdes y completas) y deja pasar las defectuosas (hojas amarillas o manchadas, tallo torcido o con raíz expuesta). Cada plántula muestra un ícono además del color para no depender solo de él.
- **Pregunta ejemplo:** *¿Qué característica indica una plántula apta para sembrar?*
  - ✅ Tallo vigoroso y hojas sanas, sin manchas.
  - ❌ Que sea la plántula más alta del vivero, aunque tenga hojas amarillas.
  - ❌ Que tenga muchas hojas secas en la base.
- **Dato para la retroalimentación:** «La sanidad de la plántula reduce pérdidas futuras; una planta enferma puede contagiar al cultivo».

### Estación 2 · Siembra
- **Ambiente:** lote preparado con hoyos marcados y árboles de sombra temporal (plátano).
- **Concepto clave:** la siembra respeta distancias entre plantas y se acompaña de sombra temporal y permanente, porque el cacao joven no tolera bien el sol directo.
- **Actividad (ubicar):** el avatar transporta plántulas y las deposita en los hoyos marcados mientras evita charcos. La planta crece en una breve animación al ser sembrada.
- **Pregunta ejemplo:** *¿Por qué se siembra plátano junto al cacao joven?*
  - ✅ Para dar sombra temporal mientras el cacao se establece.
  - ❌ Porque el plátano hace que el cacao produzca chocolate más dulce.
  - ❌ Para que el cacao no necesite agua.
- **Dato:** «En muchas fincas se usan distancias de alrededor de 3 × 3 metros, según la variedad y el sistema agroforestal».

### Estación 3 · Manejo del cultivo
- **Ambiente:** cacaotal adulto con árboles de sombra permanente.
- **Concepto clave:** el cultivo requiere poda, fertilización según el análisis de suelo, regulación de sombra y control sanitario; por ejemplo, retirar con frecuencia las mazorcas afectadas por moniliasis.
- **Actividad (sanidad):** el avatar recorre plataformas entre árboles y retira (`E`) las mazorcas enfermas, que muestran manchas y un ícono de alerta, sin tocar las sanas. Recoge gotas de agua y hojas sanas como bonificación.
- **Pregunta ejemplo:** *¿Qué hacer con las mazorcas enfermas que se encuentran en el árbol?*
  - ✅ Retirarlas y manejarlas para evitar que la enfermedad se disperse.
  - ❌ Dejarlas en el árbol hasta la cosecha.
  - ❌ Abrirlas y mezclar sus granos con los sanos.
- **Dato:** «Las podas sanitarias y la remoción frecuente de frutos enfermos son prácticas clave del manejo integrado».

### Estación 4 · Cosecha *(estación de la versión mínima viable)*
- **Ambiente:** cacaotal con mazorcas en los troncos (el cacao es cauliflor: da flores y frutos directamente en el tronco y las ramas gruesas).
- **Concepto clave:** se cosechan solo las mazorcas maduras, reconocibles por el cambio de color (por ejemplo, de verde a amarillo o de rojo a anaranjado, según la variedad) y por el sonido característico al golpearlas suavemente. El corte se hace con una herramienta adecuada, sin dañar el cojín floral del que salen nuevas flores.
- **Actividad (recolectar):** el avatar salta entre plataformas y recolecta mazorcas al tocarlas.
  - **Mazorca madura:** suma puntos; tiene un contorno brillante y un ícono de estrella.
  - **Mazorca verde (inmadura):** resta pocos puntos; tiene un ícono de hoja.
  - **Mazorca enferma:** resta puntos; tiene manchas y un ícono de alerta.
  - **Meta:** recolectar al menos **8 mazorcas maduras** para llenar la canasta y activar la pregunta.
- **Pregunta de la versión mínima viable:** *¿Cuál mazorca se debe cosechar?*
  - ✅ La mazorca madura, que cambió de color según su variedad.
  - ❌ La mazorca verde más grande, porque tiene más granos.
  - ❌ Cualquier mazorca, siempre que esté a la altura de la mano.
- **Retroalimentación correcta:** «Las mazorcas maduras tienen granos bien desarrollados y la cantidad adecuada de mucílago para fermentar bien. Cosechar verde baja la calidad».
- **Retroalimentación incorrecta:** «Las mazorcas verdes tienen granos inmaduros que fermentan mal. Se cosechan las maduras, sin dañar el cojín floral del tronco».

### Estación 5 · Apertura de mazorcas y extracción de granos
- **Ambiente:** zona de beneficio en la finca con canastas y baldes limpios.
- **Concepto clave:** las mazorcas se abren pocos días después de la cosecha, con cuidado de no dañar los granos. Se extraen los granos con su mucílago (pulpa blanca), se retira la placenta (vena central) y se separan los granos dañados o germinados.
- **Actividad (separar):** dentro de la mazorca abierta aparecen granos sanos, placenta y granos dañados; el jugador lleva cada elemento a su recipiente: «Fermentar», «Descartar» o «Compost».
- **Pregunta ejemplo:** *¿Qué se envía a fermentar?*
  - ✅ Los granos sanos con su mucílago.
  - ❌ Los granos junto con la cáscara de la mazorca.
  - ❌ Solo la placenta.
- **Dato:** «La cáscara de la mazorca puede aprovecharse como abono o subproducto: otra oportunidad de la agroindustria».

### Estación 6 · Fermentación
- **Ambiente:** cajones de madera escalonados, cubiertos con hojas de plátano o costales.
- **Concepto clave:** durante varios días (con frecuencia entre 5 y 7, según el material y el clima) la masa se fermenta y se voltea periódicamente para airearla y homogeneizarla. La temperatura sube de forma natural (puede superar los 40 °C), el mucílago escurre y en el grano se forman los precursores del sabor y el aroma a chocolate.
- **Actividad (control de proceso):** una línea de tiempo muestra los «días» de fermentación. El jugador debe voltear la masa (`E`) cuando el indicador de temperatura y aireación llegue a la zona marcada; no sirve hacerlo demasiado pronto ni dejar pasar demasiado tiempo. El indicador combina color, número y posición para no depender solo del color.
- **Pregunta ejemplo:** *¿Para qué se voltea la masa durante la fermentación?*
  - ✅ Para airearla y lograr una fermentación uniforme.
  - ❌ Para enfriarla y detener la fermentación desde el primer día.
  - ❌ Para separar el chocolate del grano.
- **Dato:** «Un grano bien fermentado tiene interior color marrón; uno sin fermentar es violeta y muy astringente».

### Estación 7 · Secado
- **Ambiente:** marquesina o secador solar con bandejas de madera y un cielo con nubes que van y vienen.
- **Concepto clave:** el grano fermentado se seca, generalmente al sol durante varios días, hasta una humedad cercana al 7 %. Así se conserva, se evitan los hongos y se completa el desarrollo del sabor. Debe protegerse de la lluvia, el humo, el suelo y los animales.
- **Actividad (cuidar):** el jugador remueve los granos de las bandejas (`E`) y cubre o descubre la marquesina cuando se acerca una nube de lluvia. Una barra muestra la humedad descendiendo hasta la meta.
- **Pregunta ejemplo:** *¿Por qué es importante secar bien el grano?*
  - ✅ Para conservarlo y evitar el crecimiento de hongos.
  - ❌ Para que el grano vuelva a germinar.
  - ❌ Para que pierda todo su sabor.
- **Dato:** «Secar el grano sobre la tierra o cerca del humo puede contaminarlo con olores indeseados».

### Estación 8 · Transformación hasta obtener licor de cacao
- **Ambiente:** pequeña planta de transformación con tostador, descascarilladora y molino.
- **Concepto clave:** en planta se clasifican y limpian los granos, se **tuestan** (desarrollo final del aroma), se **descascarillan** (separando la cascarilla de los *nibs*) y se **muelen**. Al moler, la grasa del cacao (manteca) se funde y se obtiene una pasta fluida: el **licor de cacao**, que **no contiene alcohol**.
- **Actividad (secuencia):** cuatro máquinas aparecen desordenadas y el jugador las activa en el orden correcto: clasificación → tostado → descascarillado → molienda. Si se equivoca, la máquina muestra un aviso y el producto no avanza. Al final cae el licor de cacao en un molde.
- **Pregunta ejemplo:** *¿Qué es el licor de cacao?*
  - ✅ La pasta que se obtiene al moler los granos de cacao tostados y descascarillados.
  - ❌ Una bebida alcohólica hecha con cacao.
  - ❌ El jugo de la pulpa fresca de la mazorca.
- **Dato:** «Del licor de cacao se obtienen la manteca y el cacao en polvo, y es la base del chocolate».

### Resumen de estaciones

| # | Estación | Tipo de actividad | Insignia |
|---|---|---|---|
| 1 | Selección de plántulas | Clasificar | Guardián del Vivero |
| 2 | Siembra | Ubicar y transportar | Sembrador Experto |
| 3 | Manejo del cultivo | Sanidad en plataformas | Protector del Cacaotal |
| 4 | Cosecha | Recolectar saltando | Cosechador de Oro |
| 5 | Apertura y extracción | Separar | Maestro del Beneficio |
| 6 | Fermentación | Control de tiempo | Alquimista de la Fermentación |
| 7 | Secado | Cuidar y reaccionar | Señor del Sol (o Señora del Sol) |
| 8 | Transformación | Ordenar una secuencia | Ingeniero del Licor |

---

## 8. Recompensas e insignias

### Insignias por estación
- Cada estación otorga **una insignia** con un diseño ilustrado propio (ver la tabla anterior).
- **Tres niveles por insignia,** según el desempeño en la estación:
  - 🥇 **Oro:** actividad superada con alto puntaje y pregunta respondida correctamente.
  - 🥈 **Plata:** pregunta correcta con puntaje medio en la actividad, o actividad excelente con la pregunta incorrecta.
  - 🥉 **Bronce:** estación completada.
- Toda insignia muestra nombre y nivel en texto, además del color del metal (accesibilidad).

### Insignia final
- **«Cadena Completa del Cacao»:** se obtiene al terminar las 8 estaciones.
- **«Agroindustrial en Potencia»:** se obtiene con 6 o más insignias de oro.

### Otras recompensas
- **Datos curiosos desbloqueables:** cada insignia desbloquea una tarjeta de dato curioso (por ejemplo: *«El cacao es originario de la región amazónica»*, *«Colombia es reconocida internacionalmente por su cacao fino de sabor y aroma»*). Estos datos deben ser validados por el programa.
- **Certificado digital de la feria** (pantalla final): resumen con nombre o alias opcional, puntaje, insignias y un mensaje del programa, preparado para fotografiarlo con el celular. No se recopilan datos personales.

---

## 9. Sistema de puntuación

### Principios
- La puntuación premia **decisiones correctas y aprendizaje** más que velocidad o habilidad.
- Ninguna penalización puede dejar el puntaje de una estación por debajo de 0.
- El tiempo da solo una bonificación pequeña y opcional.

### Distribución por estación (máximo 1.000 puntos por estación)

| Componente | Puntos máximos | Detalle |
|---|---|---|
| Actividad | 500 | Según aciertos de la actividad. |
| Pregunta educativa | 400 | 400 si acierta; 100 si falla (se premia haber leído la explicación). |
| Recolectables del recorrido | 100 | Semillas, gotas y hojas sanas del tramo previo. |
| Bonificación de tiempo | Hasta +50 | Si completa la estación en menos del tiempo de referencia. No cuenta para las insignias. |

**Puntaje máximo del juego completo:** 8.000 puntos, más las bonificaciones de tiempo.

### Detalle de la estación de cosecha (versión mínima viable)

| Evento | Puntos |
|---|---|
| Mazorca madura recolectada | +50 (meta: 8 mazorcas = 400) |
| Mazorca madura adicional (más allá de la meta, máximo 2) | +50 |
| Mazorca verde recolectada | −20 |
| Mazorca enferma recolectada | −40 |
| Pregunta correcta | +400 |
| Pregunta incorrecta | +100 (con explicación) |
| Bonificación de tiempo (menos de 90 s) | +50 |

**Umbrales de la insignia de cosecha:** oro con 800 puntos o más y la pregunta correcta; plata entre 500 y 799; bronce por debajo de 500.

### Rangos finales (juego completo)

| Puntos | Rango |
|---|---|
| 0 – 3.999 | Aprendiz del Cacao |
| 4.000 – 5.999 | Técnico Cacaotero |
| 6.000 – 7.199 | Especialista en Poscosecha |
| 7.200 o más | Ingeniero(a) Agroindustrial en Potencia |

### Tabla de puntajes
- **Versión mínima viable:** solo se muestra el puntaje de la partida actual.
- **Futuro:** tabla local de mejores puntajes del día en el navegador del stand (`localStorage`), con alias opcional y botón para borrarla.

---

## 10. Condiciones para completar el juego

### Juego completo
- **Victoria:** completar las 8 estaciones en orden y llegar a la planta de transformación con el licor de cacao.
- **No existe derrota definitiva:** el jugador no «muere». Si cae a un vacío o se queda atascado, reaparece en el último punto de control, al inicio del tramo de la estación, con una pequeña penalización de 10 puntos.
- **Estaciones obligatorias:** no se pueden saltar porque cada una aporta el material necesario para la siguiente (plántulas → árboles → mazorcas → granos, etc.).

### Versión mínima viable
1. Recorrer el tramo de cosecha.
2. Recolectar al menos 8 mazorcas maduras.
3. Responder la pregunta educativa (correcta o incorrectamente).
4. Recibir la insignia «Cosechador de Oro» en el nivel correspondiente.
5. Ver la pantalla final con puntaje e insignia.

### Salvaguardas para la feria
- Si el jugador no alcanza la meta de mazorcas porque las recolectó mal, aparecen nuevas mazorcas maduras al final del tramo para que siempre pueda terminar.
- **Futuro (recomendado):** tras 60 segundos sin actividad, el juego muestra «¿Sigues ahí?» y, si nadie responde, vuelve al menú para el siguiente visitante.

---

## 11. Pantallas y escenas necesarias

Nombres sugeridos de escenas Phaser (una clase por escena):

| Escena | Propósito | Versión mínima viable |
|---|---|---|
| `BootScene` | Configuración inicial y carga mínima (logotipo y barra de carga). | ✅ |
| `PreloadScene` | Carga de sprites, fondos, sonidos y textos, con barra de progreso. | ✅ |
| `MenuScene` | Título, botón «Jugar», «Cómo jugar», sonido sí/no y créditos breves. | ✅ |
| `HowToPlayScene` | Controles e indicaciones (puede ser una superposición del menú). | ✅ (simple) |
| `StoryScene` | Viñetas de introducción con Doña Teo. | ❌ (futuro) |
| `StationMapScene` | Mapa del recorrido con las 8 estaciones y el progreso. | ❌ (futuro) |
| `LevelScene` | Escena de recorrido lateral reutilizable, configurada por datos de cada estación. | ✅ (solo cosecha) |
| `QuestionScene` | Superposición modal con la pregunta, las opciones y la retroalimentación. | ✅ |
| `BadgeScene` | Animación de obtención de la insignia. | ✅ (simple) |
| `PauseScene` | Menú de pausa: continuar, reiniciar, controles, sonido, salir al menú. | ✅ (básico) |
| `HUDScene` | Interfaz superpuesta: puntaje, mazorcas recolectadas/meta, estación, botones. | ✅ |
| `EndScene` | Resultados: puntaje, insignias, mensaje del programa, «Jugar de nuevo». | ✅ |
| `CreditsScene` | Créditos del programa, del equipo y de los recursos con licencia. | ❌ (en el menú, como texto) |

**Arquitectura de datos recomendada:** las estaciones, preguntas, textos y umbrales se definen en archivos de datos JSON (por ejemplo `stations.json` y `questions.json`) y no dentro del código. Así los docentes pueden corregir contenidos sin tocar la lógica y agregar estaciones reutilizando `LevelScene` con otra configuración.

---

## 12. Recursos gráficos necesarios

Todos los recursos deben ser **de creación propia** o tener **licencias libres compatibles** (por ejemplo CC0 o CC BY, citando la fuente en los créditos). No se usarán personajes, sprites, fuentes ni sonidos de videojuegos comerciales.

### Estilo y especificaciones
- **Resolución base del juego:** 1280 × 720 px, escalada al tamaño de la ventana manteniendo la proporción 16:9.
- **Estilo:** ilustración plana (*flat*) o *pixel art* de 32 × 32 px por tile, sin mezclar ambos estilos.
- **Paleta:** verdes del cacaotal, ocres y marrones del grano, amarillos y anaranjados de la mazorca madura, azul del cielo; alto contraste entre el personaje y el fondo.
- **Formato:** PNG con transparencia; los personajes y objetos animados en *spritesheets* o atlas de texturas.

### Inventario (✅ = necesario para la versión mínima viable)

| Categoría | Recurso | Detalle | MVP |
|---|---|---|---|
| Personaje | Kakaw | Animaciones: reposo (2 cuadros), caminar (4–6), saltar (1–2), recoger (2), celebrar (2–3). | ✅ |
| Personaje | Doña Teo | Retrato para diálogos y pose de saludo. | ❌ |
| Fondos | Cacaotal (cosecha) | 3 capas de *parallax*: cielo, árboles lejanos y árboles cercanos. | ✅ |
| Fondos | Vivero, lote de siembra, zona de beneficio, fermentadores, marquesina, planta | Una ambientación por estación. | ❌ |
| Escenario | Tiles de suelo y plataformas | Tierra, raíces, troncos y ramas transitables. | ✅ |
| Objetos | Mazorcas | Madura (con estrella y contorno brillante), verde (ícono de hoja), enferma (manchas e ícono de alerta). | ✅ |
| Objetos | Canasta | Indicador visual de progreso de la cosecha. | ✅ |
| Objetos | Plántulas, granos, placenta, cajones, bandejas, máquinas | Para las estaciones futuras. | ❌ |
| Interfaz | Botones, paneles y marco de la pregunta | Estilo coherente con bordes redondeados. | ✅ |
| Interfaz | Íconos | Sonido, pausa, puntaje, mazorca, flechas y teclas. | ✅ |
| Insignias | Cosechador de Oro | Versiones oro, plata y bronce con nombre y nivel en texto. | ✅ |
| Insignias | Las 7 restantes y las 2 finales | Mismo marco con ilustración propia. | ❌ |
| Branding | Logotipo del juego y del programa | Con autorización institucional. | ✅ (logotipo del juego) |
| Efectos | Partículas | Destellos al recoger, confeti al obtener la insignia (moderado y sin parpadeos). | ✅ (básico) |

### Tipografía
- Una fuente legible de licencia libre, alojada localmente en el repositorio (por ejemplo, una sans serif redondeada).
- Tamaño mínimo de 24 px a la resolución base para el texto de juego; 32 px o más para preguntas.

---

## 13. Recursos de sonido necesarios

Todos los sonidos deben ser propios, generados (por ejemplo con herramientas de síntesis retro) o con licencias libres compatibles.

| Tipo | Recurso | Duración aprox. | MVP |
|---|---|---|---|
| Música | Tema del menú (ritmo alegre e instrumentación latinoamericana suave) | Bucle de 30–60 s | ✅ (opcional) |
| Música | Tema del recorrido en el cacaotal | Bucle de 45–90 s | ✅ (opcional) |
| Efectos | Salto | < 0,3 s | ✅ |
| Efectos | Recoger mazorca madura (positivo) | < 0,5 s | ✅ |
| Efectos | Recoger mazorca verde o enferma (neutro y suave, no estridente) | < 0,5 s | ✅ |
| Efectos | Respuesta correcta | < 1 s | ✅ |
| Efectos | Respuesta incorrecta (suave) | < 1 s | ✅ |
| Efectos | Insignia obtenida (fanfarria corta) | 1–2 s | ✅ |
| Efectos | Clic de botón | < 0,2 s | ✅ |
| Ambiente | Pájaros y viento en el cacaotal | Bucle | ❌ |
| Efectos | Máquinas, volteo de cajón, lluvia | Variable | ❌ |

**Especificaciones:**
- Formatos OGG y MP3 (Phaser elige el compatible con cada navegador).
- Volumen moderado por defecto, con música y efectos en canales separados.
- El audio solo comienza después de la primera interacción del usuario, como exigen los navegadores.
- **En feria:** todo el juego debe entenderse sin sonido, porque el stand será ruidoso o estará silenciado.

---

## 14. Requisitos de accesibilidad

| Área | Requisito |
|---|---|
| **No depender del color** | Las mazorcas maduras, verdes y enfermas se distinguen también por forma o ícono (estrella, hoja, alerta) y por un contorno. Esto es crítico porque el concepto educativo de madurez se basa en el color. Los indicadores de temperatura y humedad usan número y posición además del color. |
| **Legibilidad** | Textos de al menos 24 px a la resolución base, alto contraste (relación mínima de 4,5:1) y fondo sólido detrás de todo texto sobre escenario. |
| **Control por teclado** | Todo el juego, incluidos los menús y las preguntas, se puede jugar solo con teclado, con foco visible en el elemento seleccionado. |
| **Sin presión de tiempo** | Las preguntas no tienen límite de tiempo y el cronómetro solo otorga bonificación. |
| **Pausa** | Disponible en todo momento (`P` o `Esc`). |
| **Sonido** | Botón de silencio visible; toda información sonora tiene un equivalente visual. |
| **Movimiento y destellos** | Sin parpadeos rápidos (menos de 3 destellos por segundo) y opción de reducir el movimiento (sin *parallax* ni vibración de cámara). |
| **Lenguaje** | Español claro, frases cortas, sin tecnicismos sin explicar; términos técnicos en negrita con una definición breve. |
| **Tolerancia a errores** | Sin muerte del personaje y reaparición inmediata en un punto de control cercano. |
| **Alternativa textual** | El documento HTML que contiene el juego incluye un título, una descripción y las instrucciones de controles en texto fuera del canvas. |

---

## 15. Requisitos para funcionar en GitHub Pages

1. **Sitio 100 % estático:** HTML, CSS, JavaScript, imágenes, audio y JSON. Sin backend, base de datos, inicio de sesión ni APIs con claves.
2. **`index.html` en la raíz** del repositorio, o en `/docs` si se configura así en *Settings → Pages*.
3. **Rutas relativas** en todas las referencias, por ejemplo `assets/img/mazorca.png`, nunca `/assets/...` ni rutas locales. GitHub Pages publica bajo `usuario.github.io/nombre-repo/`, por lo que una ruta absoluta desde la raíz del dominio se rompería.
4. **Mayúsculas y minúsculas exactas** en nombres de archivos: GitHub Pages distingue `Mazorca.png` de `mazorca.png`. Se recomienda usar solo minúsculas y guiones.
5. **Phaser alojado localmente** (copia de `phaser.min.js` versión 3.x estable dentro del repositorio) en lugar de un CDN. Así el juego funciona aunque la red de la feria sea inestable, siempre que el sitio ya esté cargado o se ejecute desde una copia local.
6. **Sin paso de compilación obligatorio** en la versión mínima viable: JavaScript nativo con módulos ES (`type="module"`) o *scripts* clásicos. Si en el futuro se usa un empaquetador, se publica la carpeta resultante.
7. **Prueba local con un servidor estático simple,** porque los navegadores bloquean la carga de recursos de Phaser desde `file://`. Debe documentarse en el README.
8. **Peso total recomendado** inferior a 15 MB para la versión completa y a 5 MB para la mínima viable: imágenes optimizadas, atlas de texturas y audio comprimido.
9. **Almacenamiento:** solo `localStorage` para preferencias (sonido, movimiento reducido) y, en el futuro, puntajes del día, con manejo de errores si no está disponible.
10. **Compatibilidad:** versiones recientes de Chrome, Edge y Firefox en computador (prioridad del stand); Safari como objetivo secundario.
11. **Plan B de feria:** el README explicará cómo ejecutar el juego en el computador del stand sin internet, con la copia local del repositorio y un servidor estático.

**Estructura de carpetas sugerida:**
```
cacao-quest/
├── index.html
├── README.md
├── GAME_DESIGN.md
├── LICENSE
├── css/
├── js/
│   ├── lib/          (phaser.min.js)
│   ├── scenes/
│   └── data/         (stations.json, questions.json)
└── assets/
    ├── img/
    ├── audio/
    └── fonts/
```

---

## 16. Alcance de la primera versión mínima viable

**Objetivo de la versión mínima viable:** validar en la feria que la mecánica de plataformas con pregunta educativa es comprensible, divertida y cabe en 2 a 3 minutos por visitante.

**Incluye únicamente:**

| # | Funcionalidad | Criterio de aceptación |
|---|---|---|
| 1 | **Menú inicial** | Título del juego, botón «Jugar» y controles visibles; se opera con teclado y ratón. |
| 2 | **Movimiento lateral** | El avatar camina a izquierda y derecha con flechas o A/D, con animación de caminar y reposo. |
| 3 | **Salto** | Salto con `Espacio`, `↑` o `W`; altura suficiente para alcanzar las plataformas del nivel. |
| 4 | **Colisiones** | El avatar se apoya en el suelo y las plataformas y no atraviesa paredes ni sale del nivel. Al caer al vacío reaparece en el punto de control. |
| 5 | **Recolección de mazorcas** | Mazorcas maduras, verdes y enfermas distinguibles por color e ícono; al tocarlas desaparecen con un efecto y modifican el puntaje. |
| 6 | **Una estación de cosecha** | Tramo lateral con plataformas y mazorcas; al llegar a la meta de 8 mazorcas maduras y a la zona de la estación, se activa la pregunta. |
| 7 | **Puntuación** | HUD con puntaje y contador de mazorcas («5/8»), actualizado en tiempo real según la tabla de la sección 9. |
| 8 | **Una pregunta educativa** | Pregunta de cosecha con 3 opciones mezcladas, retroalimentación y explicación; se responde con ratón o teclas 1–3. |
| 9 | **Una insignia** | «Cosechador de Oro» en nivel oro, plata o bronce según el puntaje, con animación breve. |
| 10 | **Pantalla final** | Puntaje total, insignia obtenida, mensaje del programa de Ingeniería Agroindustrial y botón «Jugar de nuevo» que reinicia por completo el estado. |

**Requisitos transversales mínimos de la versión mínima viable:** botón de silencio, pausa básica, textos legibles, mazorcas distinguibles sin depender del color, funcionamiento en GitHub Pages y ausencia de errores en la consola.

**Fuera del alcance de la versión mínima viable:** las estaciones 1, 2, 3, 5, 6, 7 y 8, la historia, el mapa de estaciones, Doña Teo, la tabla de puntajes, el certificado y los controles táctiles.

---

## 17. Funcionalidades para versiones futuras

### Versión 1.1 · Preparación para la feria
- Reinicio automático por inactividad (*modo quiosco*).
- Tabla local de mejores puntajes del día con alias opcional y botón de borrado.
- Opción de movimiento reducido.
- Pantalla de créditos.

### Versión 2.0 · Recorrido completo
- Estaciones 1, 2, 3, 5, 6, 7 y 8 con sus actividades.
- Historia introductoria con Doña Teo y diálogos por estación.
- Mapa de estaciones con progreso.
- Las 8 insignias, las 2 insignias finales y los datos curiosos desbloqueables.
- Puntos de control entre estaciones.

### Versión 2.1 · Experiencia ampliada
- Certificado digital de la feria descargable o para fotografiar, sin datos personales.
- Banco de preguntas ampliado con selección aleatoria (2–3 variantes por estación).
- Modo docente: configuración de qué estaciones jugar y modo «solo preguntas» para usar en clase.
- Personalización básica del avatar.

### Versión 3.0 · Alcance extendido
- Controles táctiles para tabletas y teléfonos.
- Soporte de gamepad.
- Versión en inglés.
- Etapa opcional de **chocolatería** (mezcla, refinado, conchado y templado) y de **subproductos** (cascarilla, mucílago, cáscara de mazorca) para mostrar la economía circular.
- Panel de estadísticas anónimas de la feria guardadas localmente (por ejemplo, la pregunta más fallada), exportable a CSV para el programa.

---

*Fin del documento. Próxima etapa: definición técnica (arquitectura de escenas, estructura de datos JSON y prototipo de la versión mínima viable en Phaser 3).*
