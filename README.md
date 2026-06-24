# Reto Videojuego - Gráfica y Multimedia 2

========================================================================
ENLACE DIRECTO A LOS ARCHIVOS DEL JUEGO (GOOGLE DRIVE):
https://drive.google.com/drive/folders/1Zc2TA-vZGHS4y0IbOcU5Vew4Mbw4DnNA?usp=sharing
========================================================================

Este repositorio contiene el desarrollo del proyecto para la materia de Gráfica y Multimedia 2 (Unifranz). El proyecto cumple al 100% con los requerimientos estipulados en el documento de evaluación del reto (Reto (1).docx).

---

## Descripción del Juego y Temática

El juego está ambientado en la ciudad de El Alto, Bolivia. La trama nos sitúa en medio de bloqueos en ciertos puntos estratégicos de la ciudad. Como jugador, el objetivo principal es movilizarse a través de las calles alteñas para encontrar alimento y suministros para sobrevivir, mientras se despejan los puntos bloqueados neutralizando a tres tipos de enemigos específicos:

1. **Bloqueadores tirapiedras:** Enemigos que atacan a distancia lanzando proyectiles de piedra.
2. **Bloqueadores cuerpo a cuerpo:** Enemigos hostiles que persiguen al jugador para atacarlo directamente con golpes a corta distancia.
3. **Bloqueadores que lanzan dinamita:** Enemigos de alto peligro que arrojan explosivos con daño de área.

---

## Cumplimiento del Reto (100% Conforme a Reto (1).docx)

Este proyecto ha sido estructurado y desarrollado cumpliendo estrictamente cada una de las directrices y etapas del reto académico:

* **Etapa 1: Fundamentos y Locomoción (100% Completado)**
  * Configuración del entorno del jugador en la ciudad de El Alto.
  * Correcto etiquetado y separación de capas (Layers y Tags) para colisiones y sensores de IA.
  * Movimiento fluido y rotación orientada a la cámara mediante Character Controller.
  * Configuración de Cinemachine FreeLook Camera para un seguimiento preciso que gestiona las colisiones con el entorno.

* **Etapa 2: Sistema de Combate y Animación (100% Completado)**
  * Integración del Animator Controller con Blend Trees para transiciones suaves entre caminar, correr y saltar.
  * Sistema de combate con armas de fuego Raycast (Physics.Raycast) para detectar impactos y generar efectos visuales (VFX) en el punto de colisión.
  * Gestión completa de munición, recargas y recolección de armas del suelo.

* **Etapa 3: IA Básica e Interacción (100% Completado)**
  * Sistema de navegación basado en NavMesh de Unity para que los enemigos sigan e intercepten al jugador.
  * Uso de una arquitectura desacoplada para aplicar daño a los objetivos (jugador y enemigos).

* **Etapa 4: Game Loop y UI (100% Completado)**
  * Interfaz de usuario que incluye barra de salud vinculada a eventos, contador de puntos/alimentos recolectados y pantalla de Game Over.
  * Menú principal y condiciones de victoria al limpiar las zonas bloqueadas y recolectar el alimento necesario.

---

## Jerarquía y Descripción de Scripts

A continuación se detalla la estructura y propósito de los scripts utilizados en el proyecto:

### 1. Control del Jugador y Locomoción
* **CharacterLocomotion.cs:** Controla el movimiento en tres ejes, el salto y la física del jugador utilizando el Character Controller de Unity.
* **CharacterAiming.cs:** Alinea el torso y la mirada del personaje con la mira central de la cámara para apuntar con precisión.
* **MouseLook.cs:** Gestiona la rotación de la cámara basándose en el movimiento del ratón.
* **CharacterFootStepSoundManager.cs:** Genera efectos de audio (SFX) para las pisadas según el movimiento y la superficie.

### 2. Sistema de Combate y Armamento
* **RaycastWeapon.cs:** Script principal del arma. Implementa `Physics.Raycast` para calcular trayectorias de disparo, detecta impactos en colisionadores, aplica daño y genera efectos visuales (VFX de chispa/sangre) y sonido.
* **ActiveWeapon.cs:** Administra el equipamiento de armas del jugador, permitiendo el cambio entre pistola, rifle y francotirador.
* **ReloadWeapon.cs:** Controla los tiempos y animaciones de recarga del arma actual actualizando la reserva de munición.
* **WeaponPickup.cs:** Permite al jugador y a los enemigos recoger nuevas armas y munición al pasar sobre ellas.
* **Grenade.cs / ThrowGrenade.cs:** Lógica para lanzar y detonar proyectiles explosivos (utilizado por el jugador y adaptado para los enemigos dinamiteros).

### 3. Inteligencia Artificial (Enemigos FSM y NavMesh)
* **AiAgent.cs / AgentController.cs:** Componente central del enemigo. Inicializa los sistemas de navegación, sensores y la máquina de estados.
* **AiStateMachine.cs / State.cs:** Estructura de programación orientada a objetos (POO) que maneja los cambios de estado de forma limpia y desacoplada.
* **AiVisionSensor.cs / AiSensoryMemory.cs:** Sensor cónico de visión que detecta al jugador basándose en su distancia y ángulo de visión directa, gestionando la pérdida de rastro.
* **Estados de la IA (states/):**
  * **AiPatrolState.cs / PatrolState.cs:** Movimiento cíclico por puntos de patrulla en las barricadas.
  * **AlertState.cs:** El oponente busca la fuente de un sonido sospechoso.
  * **InvestigationState.cs:** El enemigo se mueve a investigar la última posición conocida del jugador.
  * **AiChaseTargetState.cs / ChaseTargetState.cs:** Persecución activa del jugador utilizando NavMesh.
  * **AiAttackTargetState.cs / AttackState.cs:** El enemigo se posiciona para atacar usando su respectiva arma o habilidad (piedras, cuerpo a cuerpo o dinamita).

### 4. Interfaz de Usuario y Game Loop
* **PlayerHealthSlider.cs / HealthSliderControl.cs:** Actualizan la barra de vida del jugador mediante eventos, evitando que el script de salud tenga que comunicarse directamente con la UI.
* **WeaponWidget.cs:** Informa visualmente sobre la munición disponible en el cargador y en reserva.
* **Minimap.cs:** Genera la visualización del minimapa en tiempo real en la pantalla.

### 5. Salud y Destrucción
* **Health.cs / Destructible.cs:** Lleva el control de la salud del personaje o elemento destructible, desencadenando la muerte y efectos asociados.
* **HitBox.cs:** Colisionadores específicos distribuidos en el modelo que reenvían el daño recibido al componente de salud principal, permitiendo multiplicadores de daño.
* **Ragdol.cs:** Activa la física de muñeco de trapo (ragdoll) en los personajes al morir.

---

## Instrucciones de Control

* **Movimiento:** Teclas W, A, S, D
* **Saltar:** Barra Espaciadora
* **Apuntar:** Clic Derecho (sostenido)
* **Disparar:** Clic Izquierdo
* **Recargar:** Tecla R
* **Cambio de Arma:** Teclas numéricas 1, 2, 3 o Rueda del Ratón
* **Lanzar Dinamita/Granada:** Tecla G
