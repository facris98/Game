# Game
-----------------------------------------
import pygame
import random
import sys

# Inicializar pygame
pygame.init()

# Configuración de la pantalla
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Esquivar los Enemigos")

# Colores
WHITE = (255, 255, 255)
RED = (255, 0, 0)
GREEN = (0, 255, 0)

# Jugador
player_size = 50
player_x = WIDTH // 2 - player_size // 2
player_y = HEIGHT - 2 * player_size
player_speed = 5

# Enemigos
enemy_size = 40
enemy_speed = 2
enemies = []

# Puntuación
score = 0

# Fuente de texto
font = pygame.font.Font(None, 36)

def draw_player(x, y):
    pygame.draw.rect(screen, RED, (x, y, player_size, player_size))

def draw_enemy(x, y):
    pygame.draw.rect(screen, GREEN, (x, y, enemy_size, enemy_size))

def show_score():
    text = font.render(f"Puntuación: {score}", True, RED)
    screen.blit(text, (10, 10))

def game_over():
    text = font.render("¡Juego Terminado!", True, RED)
    screen.blit(text, (WIDTH // 2 - 120, HEIGHT // 2 - 18))
    pygame.display.update()
    pygame.time.delay(2000)

# Game Loop
running = True
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT] and player_x > 0:
        player_x -= player_speed
    if keys[pygame.K_RIGHT] and player_x < WIDTH - player_size:
        player_x += player_speed

    # Generar enemigos
    if len(enemies) < 5:
        enemy_x = random.randint(0, WIDTH - enemy_size)
        enemy_y = 0
        enemies.append([enemy_x, enemy_y])

    # Mover y dibujar enemigos
    for enemy in enemies:
        enemy[1] += enemy_speed
        draw_enemy(enemy[0], enemy[1])

    # Colisión con los enemigos
    for enemy in enemies:
        if (
            player_x < enemy[0] + enemy_size
            and player_x + player_size > enemy[0]
            and player_y < enemy[1] + enemy_size
            and player_y + player_size > enemy[1]
        ):
            game_over()
            running = False

    # Eliminar enemigos que salieron de la pantalla
    enemies = [enemy for enemy in enemies if enemy[1] < HEIGHT]

    # Actualizar la puntuación
    score += 1

    # Dibujar el jugador y la puntuación
    screen.fill(WHITE)
    draw_player(player_x, player_y)
    show_score()
    pygame.display.update()

# Salir del juego
pygame.quit()
sys.exit()
-------------------------------------------------------



# Juego de Esquivar los Enemigos

Este es un juego simple de "Esquivar los Enemigos" desarrollado en Python utilizando la biblioteca Pygame. El objetivo del juego es controlar un personaje y esquivar los enemigos que caen desde la parte superior de la pantalla.

![Captura de pantalla del juego](screenshot.png)

## Controles

- Usa las teclas de flecha izquierda (`←`) y derecha (`→`) para mover al personaje y esquivar los enemigos.

## Características

- **Personaje Jugable:** Controla un cuadrado rojo para evitar a los enemigos que caen.

- **Enemigos:** Enemigos verdes caen desde la parte superior de la pantalla y debes evitar que colisionen con tu personaje.

- **Puntuación:** Tu puntuación aumenta cada vez que evitas que un enemigo colisione con tu personaje.

## Requisitos

- Python 3.x
- Pygame (puedes instalarlo con `pip install pygame`)

## Cómo Ejecutar el Juego

1. Clona o descarga este repositorio a tu máquina.

2. Abre una terminal y navega al directorio donde se encuentra el archivo `main.py`.

-----------------



3. Ejecuta el juego usando el siguiente comando:

   ```bash
   python main.py

