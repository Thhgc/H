import pygame
import sys

# การตั้งค่าเริ่มต้น
pygame.init()

# ขนาดหน้าจอ
screen_width = 800
screen_height = 600
screen = pygame.display.set_mode((screen_width, screen_height))
pygame.display.set_caption("Simple Game")

# สี
white = (255, 255, 255)
black = (0, 0, 0)

# การตั้งค่าตัวละคร
player_width = 50
player_height = 50
player_x = screen_width // 2
player_y = screen_height // 2
player_speed = 5

# เกมลูป
clock = pygame.time.Clock()

while True:
    # ตรวจสอบเหตุการณ์
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()

    # การควบคุมตัวละคร
    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT]:
        player_x -= player_speed
    if keys[pygame.K_RIGHT]:
        player_x += player_speed
    if keys[pygame.K_UP]:
        player_y -= player_speed
    if keys[pygame.K_DOWN]:
        player_y += player_speed

    # ควบคุมการไม่ให้ตัวละครออกจากหน้าจอ
    player_x = max(0, min(player_x, screen_width - player_width))
    player_y = max(0, min(player_y, screen_height - player_height))

    # ล้างหน้าจอ
    screen.fill(white)

    # วาดตัวละคร
    pygame.draw.rect(screen, black, (player_x, player_y, player_width, player_height))

    # อัพเดทหน้าจอ
    pygame.display.flip()

    # กำหนดอัตราการเรนเดอร์ (FPS)
    clock.tick(60)
