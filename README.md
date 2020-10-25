# refactoring

From my mygame code : https://github.com/KOngTNP/mygame

def on_draw(self) method In the screen.py file

https://github.com/KOngTNP/mygame/blob/master/Final%20project/screen.py

consider this code:
```
def on_draw(self): 
  arcade.start_render()
  arcade.draw_texture_rectangle(SCREEN_WIDTH//2,SCREEN_HEIGHT//2,SCREEN_WIDTH,SCREEN_HEIGHT,self.background)
  self.world.spot.draw()
  if self.world.state != self.world.STATE_FROZEN:
      arcade.draw_text(f"Time: {self.world.start_time:.0f}",23,450,arcade.color.RED,30)

  if self.world.state == self.world.STATE_FROZEN:

      arcade.draw_text(f"CAR PARKING GAME",210,440,arcade.color.RED,30)
      arcade.draw_text(f"Press any key to start",180,30,arcade.color.BLACK,15)
      
      
  for i in self.car_list:
      i.draw()
  if self.world.state == self.world.STATE_DEAD:
      self.background = arcade.load_texture("Wallpaper2END.jpg")
      if self.world.start_time < 15:
          ModelSprite('star_score3.png',model = self.world.win).draw()
          arcade.draw_text(f"You get 3 star!!!!!",300,250,arcade.color.BLUE,25)

      elif self.world.start_time < 20:
          ModelSprite('star_score2.png',model = self.world.win).draw()
          arcade.draw_text(f"You get 2 star!!!!!",300,250,arcade.color.BLUE,25)

      elif self.world.start_time >20:
          ModelSprite('star_score1.png',model = self.world.win).draw()
          arcade.draw_text(f"You get 1 star!!!!!",300,250,arcade.color.BLUE,25)


      arcade.draw_text(f"Thank you for playing",240,200,arcade.color.BLUE,30)
      arcade.draw_text("Press any key to restart.", 235, 150, arcade.color.BLACK, 30)
      self.world.die()
```
Refactoring Signs:
  - the name of variable is to confuse
  - have many if and elif in the function that should be more easier to manage.


Refactoring rename method:
  - change variable i to car

Refactoring: Extract method.

```
def on_draw(self): 
    arcade.start_render()
    arcade.draw_texture_rectangle(SCREEN_WIDTH//2,SCREEN_HEIGHT//2,SCREEN_WIDTH,SCREEN_HEIGHT,self.background)
    self.world.spot.draw()
  
    state = self.world.state
    forzen = self.world.STATE_FROZEN
    dead = self.world.STATE_DEAD
    if state == forzen:
        arcade.draw_text(f"CAR PARKING GAME",210,440,arcade.color.RED,30)
        arcade.draw_text(f"Press any key to start",180,30,arcade.color.BLACK,15)
    else:
        arcade.draw_text(f"Time: {self.world.start_time:.0f}",23,450,arcade.color.RED,30)
        
        
    for car in self.car_list:
        car.draw()
    if state == dead:
        self.background = arcade.load_texture("Wallpaper2END.jpg")
        time = self.world.start_time
        score = ["star_score3.png","You get 3 star!!!!!"] if time < 15 else ["star_score2.png","You get 2 star!!!!!"] if time < 20 else ["star_score1.png","You get 1 star!!!!!"]
        ModelSprite(score[0],model = self.world.win).draw()
        arcade.draw_text(f"{score[1]}",300,250,arcade.color.BLUE,25)
        
        
      arcade.draw_text(f"Thank you for playing",240,200,arcade.color.BLUE,30)
      arcade.draw_text("Press any key to restart.", 235, 150, arcade.color.BLACK, 30)
      self.world.die()
```
        
