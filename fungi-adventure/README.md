# Diseño de Juego (GDD): Fungi Adventure

## 1. Ficha Técnica y Visión General

| Parámetro | Definición |
| :--- | :--- |
| **Género** | Plataformas 2D de acción y aventura |
| **Alcance** | 1 nivel completo continuo (*Vertical Slice* / Demo jugable) |
| **Duración estimada** | 7 a 9 minutos (~19 pantallas en total) |
| **Motor de juego** | Godot Engine 4.x (2D, GDScript) |
| **Plataforma** | PC (Teclado + Mouse / soporte opcional para mando) |
| **Resolución base** | 1920x1080 px (Relación de aspecto 16:9) |
| **Referencia principal** | *Super Mario Bros.* (estructura de plataformas, claridad visual y ritmo de obstáculos) |
| **Referencias secundarias** | *Gris* (narrativa visual y color por estaciones), *Hollow Knight* / *Ori and the Blind Forest* (agilidad y bioluminiscencia), *Super Meat Boy* (respuesta rápida), *Fireboy & Watergirl* / *Geometry Dash* (lectura de obstáculos), *Plants vs. Zombies* (tono accesible y expresivo) |

### Pilares de Diseño

1. **Narrativa ambiental sin texto:** No existe minimapa ni indicador de porcentaje; el progreso se comunica a través del color del cielo, la iluminación, la música y las partículas (Verano, Otoño, Invierno y Primavera).
2. **Contraste de escala:** Todo transcurre en un mundo microscópico del bosque, culminando en un enfrentamiento contra unas "personas" de las que solo se alcanzan a ver sus manos gigantes.
3. **Plataformeo clásico y ágil:** Inspirado en *Super Mario Bros.* en su lectura clara de peligros, potenciado con doble salto, dash rompedor y disparo de esporas.

---

## 2. Historia y Arco Narrativo

### Sinopsis General

En un mundo microscópico oculto entre la vegetación del bosque, **Hongo** y **Honguina** viven felices bajo la luz cálida del verano. Sin embargo, una repentina ráfaga de viento arrastra a Honguina lejos de su hogar. Decidido a reencontrarse con ella, Hongo emprende una travesía horizontal a través del paso de las cuatro estaciones, sorteando peligros naturales, enemigos del bosque y la oscuridad del invierno hasta derrotar a las misteriosas manos que la mantienen cautiva y devolver la primavera a su mundo.

### Progresión Narrativa por Estaciones

| Estación | Rol Narrativo | Atmósfera y Paleta | Evento Clave |
| :--- | :--- | :--- | :--- |
| **1. Verano** | Prólogo y Tutorial | Pleno día en un claro luminoso. Tonos celestes vibrantes, verdes frescos y rayos de sol cálidos. | Hongo y Honguina comparten un momento de calma mientras se introducen las mecánicas básicas. Un vendaval irrumpe y arrastra a Honguina hacia lo profundo del bosque. |
| **2. Otoño** | Desarrollo (Tramo 1) | Bosque al atardecer envuelto en naranjas, amarillos dorados y rojos intensos, con hojas cayendo y viento constante. | Hongo avanza entre la hojarasca, rompe ramas secas con su dash y se defiende de avispas y escarabajos con esporas mientras recolecta gotas de agua. |
| **3. Invierno** | Clímax y Boss | Noche cerrada y nevada. Oscuridad morada y azul profundo en contraste con nieve blanca/celeste y flora bioluminiscente (cian, violeta, amarillo y verde). | Tras superar luciérnagas y escarabajos en el tramo más frío, Hongo llega a un claro helado donde dos manos monumentales emergen para aplastarlo o capturarlo. Al derrotarlas, se retiran hacia la oscuridad. |
| **4. Primavera** | Epílogo y Reencuentro | Mañana luminosa y serena en tonos pastel (rosas, lilas, amarillos y celestes suaves) con pétalos flotantes. | La nieve se disipa y el bosque florece sin peligros. Hongo recorre los últimos metros hasta reencontrarse con Honguina para vivir felices para siempre. |

---

## 3. Core Loop (Bucle Principal)

1. **Explorar y avanzar** horizontalmente interpretando el entorno, la iluminación y los peligros.
2. **Plataformear** combinando salto simple, doble salto y dash para sortear espinas, huecos en el piso y ráfagas de viento.
3. **Interactuar y combatir:** Romper ramas secas que bloquean el camino mediante el Dash y defenderse de insectos enemigos con esporas o embestidas.
4. **Gestionar vitalidad:** Recolectar gotas de agua en el camino principal o en rutas altas opcionales para mantener los 5 puntos de vida.
5. **Progresar:** Alcanzar checkpoints invisibles, atravesar el cambio de estación y superar el enfrentamiento final contra Las Manos.

---

## 4. Mecánicas de Juego y Controles

### Mapeo de Controles (PC y Mando)

| Acción | Teclado y Mouse | Mando (Sugerido) | Comportamiento |
| :--- | :--- | :--- | :--- |
| **Mover a la izquierda** | `A` | Stick Izq. / D-Pad Izq. | Desplazamiento horizontal hacia la izquierda. |
| **Mover a la derecha** | `D` | Stick Izq. / D-Pad Der. | Desplazamiento horizontal hacia la derecha. |
| **Salto simple** | `Espacio` (1 tap) | Botón `A` / `X` | Salto estándar con altura controlable. |
| **Doble salto** | `Espacio` (2 taps) | Botón `A` / `X` en el aire | Segundo impulso aéreo para superar espinas o huecos amplios. |
| **Dash rompedor** | `Shift` (mantener apretado) | `RT` / `R2` o `B` / `O` | Impulso rápido hacia adelante que rompe ramas secas y daña enemigos al embestir. |
| **Lanzar esporas** | `Click Izquierdo` (Mouse) | `X` / `Cuadrado` | Proyectil de ataque a distancia. |
| **Pausa** | `Esc` | `Start` / `Options` | Detiene la partida y despliega el menú de pausa. |

### Reglas de Salud, Combate y Reaparición

* **Sistema de vida:** Hongo posee **5 puntos de vida** máximos. Cada golpe recibido de enemigos, espinas o del jefe descuenta **1 punto de vida** y activa un breve tiempo de invulnerabilidad (*i-frames* de ~1 segundo con parpadeo visual).
* **Gotas de agua (Ítem curativo):** Recolectar una gota de agua restaura **+1 punto de vida** (hasta un máximo de 5).
* **Caída en huecos:** Al caer en un precipicio, el personaje pierde vida y vuelve a la plataforma segura anterior (o activa el retorno directo al checkpoint, según la dificultad final elegida).
* **Muerte y Checkpoints:** Cuando la vida llega a 0, se realiza una transición rápida y Hongo reaparece en el **último checkpoint alcanzado con la vida completa (5/5)**.
* **Restricciones de habilidades:**
  * **Esporas:** Munición infinita con tiempo de reutilización (*cooldown*) breve (ej. `0.35 s`) y alcance medio.
  * **Dash:** Al mantener `Shift`, Hongo realiza la embestida durante una ventana acotada (ej. `0.25 s` a `0.4 s`) con *cooldown* corto (ej. `0.8 s`) o recarga al tocar el suelo.

---

## 5. Entidades: Enemigos, Obstáculos y Jefe Final

### Enemigos Regulares

| Enemigo | Estación | Comportamiento (IA) | Resolución |
| :--- | :--- | :--- | :--- |
| **Escarabajo** | Otoño e Invierno | Patrulla horizontalmente sobre plataformas y gira al detectar paredes o bordes. | 2 impactos de esporas o 1 embestida con Dash. |
| **Avispa** | Otoño | Vuela siguiendo un recorrido aéreo corto u ondulatorio, obstaculizando saltos. | 1 a 2 impactos de esporas o Dash aéreo. |
| **Luciérnaga Bioluminiscente** | Invierno | Emite brillo propio en la oscuridad. Al detectar a Hongo dentro de su rango, lo persigue lentamente. | 1 impacto de esporas. |

### Obstáculos del Entorno

* **Espinas:** Peligro fijo sobre el terreno; requieren salto preciso o doble salto.
* **Huecos en el piso:** Abismos de dificultad progresiva (salto simple, doble salto, salto + dash).
* **Ramas secas:** Bloquean pasillos o rutas opcionales; únicamente se destruyen usando el **Dash**.
* **Ráfagas de viento (Invierno):** Empujan al jugador en contra de su avance durante los tramos aéreos.

### Jefe Final: "Las Manos" (Personas)

* **Concepto:** Debido a la escala diminuta de Hongo, de las personas únicamente se ven sus dos manos monumentales ingresando desde la oscuridad en una arena fija de `1920x1080 px`.
* **Ventana de daño:** Las manos son invulnerables en el aire. Hongo puede atacarlas con esporas o Dash cuando **se clavan o apoyan en el suelo** tras un golpe (ventana de 2 a 3 segundos).
* **Feedback visual de daño:** A medida que baja la vida del jefe, aparecen **manchas de esporas bioluminiscentes** sobre las manos.
* **Fases del combate:**
  * **Fase 1 (100% a 51% de vida):** Ataques alternados de una sola mano (aplastamiento vertical telegrafiado por sombra en el suelo y barrido horizontal que se evade saltando).
  * **Fase 2 (50% a 0% de vida):** Al reducirse a la mitad de su vida, surgen manchas de esporas brillantes y los ataques pasan a ser sincronizados y más veloces con ambas manos. Al ser derrotadas, se retiran hacia la oscuridad y despejan el camino hacia la Primavera.

---

## 6. Diseño de Nivel y Duración por Pantallas

| Tramo | Extensión | Duración aprox. | Función de Diseño |
| :--- | :--- | :--- | :--- |
| **1. Verano (Tutorial Narrativo)** | 2.5 pantallas | ~45 seg | Honguina sigue a Hongo mientras el jugador aprende movimiento, salto, doble salto, Dash rompedor (1 rama) y esporas (1 enemigo). Cierra con la ráfaga de viento que se lleva a Honguina. |
| **2. Otoño (Desarrollo y Ritmo)** | 6.5 pantallas | 2 a 2.5 min | Exploración horizontal con rutas altas opcionales de hongos repisa (con gotas de agua escondidas), ramas secas para romper con Dash y encuentros escalonados con avispas y escarabajos. |
| **Transición Otoño a Invierno** | 0.5 pantalla | ~10 seg | Puente o claro sin enemigos donde la luz global cambia de ámbar a azul nocturno y comienza a caer la primera nieve. |
| **3. Invierno (Oscuridad y Tensión)** | 7 pantallas | 2.5 a 3 min | **Checkpoint invisible #1** al ingresar. Tramos de plataformeo técnico combinando ráfagas de viento en contra, pozos grandes, luciérnagas perseguidoras y escarabajos en plataformas estrechas. |
| **4. Arena del Boss (Las Manos)** | 1 pantalla fija (`1920x1080`) | 1.5 a 2 min | **Checkpoint invisible #2** justo antes de entrar al claro cerrado. Combate en 2 fases contra las dos manos monumentales. |
| **5. Primavera (Epílogo)** | 1.5 pantallas | 25 a 35 seg | Recorrido breve y emocional sin peligros: el escenario florece en tonos pastel entre pétalos flotantes hasta el reencuentro con Honguina en el claro iluminado y el cierre con créditos. |

---

## 7. Interfaz de Usuario (UI/UX) y Flujo de Pantallas

### Flujo de Pantallas (*Game Flow*)

1. **Menú Principal:** Fondo animado del bosque, título del juego y opciones: *Jugar*, *Controles* y *Salir*.
2. **Gameplay:** Nivel continuo con acceso al **Menú de Pausa** (*Reanudar*, *Controles*, *Reiniciar desde Checkpoint*, *Menú Principal*).
3. **Reaparición:** Fundido rápido tras perder todas las vidas y retorno inmediato al último checkpoint.
4. **Cierre y Créditos:** Secuencia de reencuentro en Primavera seguida de los créditos del grupo.

### HUD Mínimo

* **Indicador de vida:** 5 íconos en la esquina superior izquierda que representan la vitalidad actual de Hongo.
* **Sin minimapa, puntaje ni contador de porcentaje**, reforzando la lectura puramente ambiental del progreso.

---

## 8. Dirección de Arte y Lista de Assets

### Estilo Visual y Resolución

* **Resolución de todo el juego:** `1920x1080 px` (16:9).
* **Definición estética (pendiente de unificación):** El equipo está evaluando entre **Pixel Art** e **Ilustración 2D**. Se recomienda elegir una sola dirección antes de la producción final:
  * **Ilustración 2D:** Ideal para aprovechar `1920x1080` de forma nativa con fondos en *parallax*, trazos orgánicos, iluminación suave y gran detalle en las manos del jefe.
  * **Pixel Art:** Requiere definir una resolución interna menor (ej. `480x270` o `640x360`) con escalado entero a `1920x1080` para mantener consistencia en el tamaño del píxel en todos los sprites.

### Lista de Assets Mínimos para la Demo

| Categoría | Assets necesarios |
| :--- | :--- |
| **Hongo (Protagonista)** | Animaciones: *Idle*, Caminar, Salto (ascenso/caída), Doble salto, Dash, Lanzar esporas, Recibir daño, Muerte. |
| **Honguina** | Animaciones: *Idle*, Caminar/seguir, Arrastrada por el viento, Reencuentro. |
| **Enemigos y Boss** | Escarabajo (caminar/daño), Avispa (volar/daño), Luciérnaga (volar con brillo/daño), Las Manos (reposo, caída vertical, barrido, clavada/vulnerable y capas de manchas de esporas). |
| **Entorno y Props** | *Tilesets* de terreno adaptados a las 4 estaciones, hongos repisa, espinas, ramas secas (entera y destruida), gotas de agua, flora bioluminiscente. |
| **Fondos (Parallax)** | 3 capas (cielo, plano lejano, vegetación intermedia) con variantes de color/iluminación para Verano, Otoño, Invierno y Primavera. |

---

## 9. Diseño Sonoro (Música y SFX)

La banda sonora acompaña de forma dinámica el cambio de estaciones (con transiciones suaves entre cada tramo).

| Tipo | Elemento | Estado actual | Descripción |
| :--- | :--- | :--- | :--- |
| **Música** | Temas por estación / nivel | Definido | Verano (cálida y alegre), Otoño (rítmica y melancólica), Invierno (tensa y atmosférica), Boss (intensa), Primavera (emotiva y serena). |
| **Ambiente** | Sonido ambiental por estación | **Pendiente** | Brisa y aves (Verano), viento y hojas (Otoño), viento helado nocturno (Invierno), brisa suave (Primavera). |
| **SFX** | Ataque de esporas | Contemplado | Disparo orgánico corto. |
| **SFX** | Pérdida de vida / Daño | Contemplado | Sonido de alerta e impacto. |
| **SFX** | Impacto de la mano en tierra | Contemplado | Golpe grave para transmitir peso y escala gigante. |
| **SFX** | Caminata / Pisadas | **Pendiente** | Pasos suaves (pasto, hojarasca, nieve). |
| **SFX** | Salto, doble salto y Dash | **Pendiente** | Impulso aéreo, ráfaga de Dash y crujido al romper ramas. |
| **SFX** | Recolectar gota de agua | **Pendiente** | Sonido cristalino de curación. |

---

## 10. Especificaciones Técnicas (Godot Engine 4.x)

### Arquitectura de Nodos Recomendada

* **Jugador (`Hongo.tscn`):** `CharacterBody2D` con `CollisionShape2D`, `AnimatedSprite2D` (o `Sprite2D` + `AnimationPlayer`), nodos `Timer` para *cooldowns* (esporas, dash, invulnerabilidad) y `Marker2D` como origen de los proyectiles.
* **Terreno:** `TileMapLayer` con capas de colisión para suelo sólido, plataformas *one-way* (hongos repisa) y áreas de espinas.
* **Objetos e Interactivos:** Escenas basadas en `Area2D` (`Espora.tscn`, `GotaAgua.tscn`, `Checkpoint.tscn`, `RamaRompible.tscn`).
* **Cámara (`Camera2D`):** Seguimiento horizontal con suavizado (*position smoothing*) y transición a cámara fija (`1920x1080`) al activar el `Area2D` de la arena del Boss.
* **Atmósfera y Estaciones:**
  * `CanvasModulate` animado con `Tween` para transicionar el color global entre estaciones.
  * `PointLight2D` en Hongo, luciérnagas, flora invernal y manchas de esporas del jefe durante Invierno.
  * `GPUParticles2D` para polen/luz (Verano), hojas (Otoño), nieve y viento (Invierno) y pétalos (Primavera).

### Variables Clave de Ajuste (*Game Feel* en GDScript)

| Variable (`@export`) | Valor inicial sugerido | Función |
| :--- | :--- | :--- |
| `speed` | `320.0` px/s | Velocidad horizontal base de Hongo. |
| `jump_velocity` | `-520.0` px/s | Impulso vertical del salto simple y doble salto. |
| `dash_speed` | `780.0` px/s | Velocidad durante la embestida del Dash. |
| `dash_duration` | `0.25` s | Duración máxima del Dash. |
| `max_health` | `5` | Cantidad máxima de puntos de vida. |
| `spore_cooldown` | `0.35` s | Tiempo mínimo entre lanzamientos de esporas. |