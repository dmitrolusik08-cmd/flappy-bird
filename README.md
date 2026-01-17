from pygame import *
from random import randint




init()
window_size = 1200, 800
window = display.set_mode(window_siz
clock = time.Clock()




player_rect = Rect(150, window_size[




def generate_pipes(count, pipe_width
   pipes = []
   start_x = window_size[0]
   for i in range(count):
       height = randint(min_height, 
       top_pipe = Rect(start_x, 0, p
       bottom_pipe = Rect(start_x, h
       pipes.extend([top_pipe, botto
       start_x += distance
   return pipes




pies = generate_pipes(150)
main_font = font.Font(None, 100)
score = 0
lose = False
y_vel = 2
while True:
   for e in event.get():
       if e.type == QUIT:
           quit()




   window.fill('sky blue')
   draw.rect(window, 'red', player_r
   for pie in pies[:]:
       if not lose:
           pie.x -= 10
       draw.rect(window, 'green', pi
       if pie.x <= -100:
           pies.remove(pie)
           score+=0.5
       if player_rect.colliderect(pi
           lose = True
   if len(pies) < 8:
       pies += generate_pipes(150)




   score_text = main_font.render(f'{
   center_text = window_size[0]//2 -
   window.blit(score_text, (center_t




   display.update()
   clock.tick(60)




   keys = key.get_pressed()
   if keys[K_w] and not lose: player
   if keys[K_s] and not lose: player
   if keys[K_r] and lose:
       lose = False
       score = 0
       pies = generate_pipes(150)
       player_rect.y = window_size[1
       y_vel = 2
   if player_rect.y >= window_size[1
   if lose:
       player_rect.y += y_vel
       y_vel *= 1.1

