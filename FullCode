# Implementation of classic arcade game Pong

import simplegui
import random

# initialize globals - pos and vel encode vertical info for paddles
WIDTH = 600
HEIGHT = 400       
BALL_RADIUS = 20
PAD_WIDTH = 8
PAD_HEIGHT = 80
HALF_PAD_WIDTH = PAD_WIDTH / 2
HALF_PAD_HEIGHT = PAD_HEIGHT / 2
LEFT = False
RIGHT = True
ball_pos = [300,200]
ball_vel = [3,-3]
paddle1_pos = 240
paddle2_pos = 240
paddle1_vel = 0
paddle2_vel = 0
score1 = 0
score2 = 0
# initialize ball_pos and ball_vel for new bal in middle of table
# if direction is RIGHT, the ball's velocity is upper right, else upper left
def spawn_ball(direction):
    global ball_pos, ball_vel # these are vectors stored as lists
    #canvas.draw_circle(ball_pos, 20, 1, 'white',"white")
    ball_pos = [300,200]
    if direction == RIGHT:
        ball_vel = [random.randrange(2,5),-random.randrange(1,3)]
    elif direction == LEFT:
          ball_vel = [-random.randrange(2,5),-random.randrange(1,3)]
    
    

# define event handlers
def new_game():
    global paddle1_pos, paddle2_pos, paddle1_vel, paddle2_vel , score1,score2 # these are numbers
    global score1, score2  # these are ints
    score1 = 0
    score2 =0 
    spawn_ball(RIGHT)   

def draw(canvas):
    global score1, score2, paddle1_pos, paddle2_pos, ball_pos, ball_vel, paddle1_vel,paddle2_vel,score1,score2
 
        
    # draw mid line and gutters
    canvas.draw_line([WIDTH / 2, 0],[WIDTH / 2, HEIGHT], 1, "White")
    canvas.draw_line([PAD_WIDTH, 0],[PAD_WIDTH, HEIGHT], 1, "White")
    canvas.draw_line([WIDTH - PAD_WIDTH, 0],[WIDTH - PAD_WIDTH, HEIGHT], 1, "White")
        
    # update ball
    if ball_pos[1] <= 20 :
        ball_vel[1] = -1*ball_vel[1]
    if ball_pos[1] >= HEIGHT-20 :
        ball_vel[1] = -1*ball_vel[1]
    if ball_pos[0] <= 20+PAD_WIDTH:
        if ball_pos[1] <= paddle1_pos and ball_pos[1] >= paddle1_pos - 80:    
            ball_vel[0] = -1*ball_vel[0]
            ball_vel[0] = 1.1*ball_vel[0]
            ball_vel[1] = 1.1*ball_vel[1]
        else :
            spawn_ball(RIGHT)
            score2 += 1
    if ball_pos[0] >= WIDTH - PAD_WIDTH - 20:
        if  ball_pos[1] <= paddle2_pos and ball_pos[1] >= paddle2_pos - 80:
            ball_vel[0] = -1*ball_vel[0]
            ball_vel[0] = 1.1*ball_vel[0]
            ball_vel[1] = 1.1*ball_vel[1]
        else : 
            spawn_ball(LEFT)
            score1+=1
    ball_pos[0] += ball_vel[0]
    ball_pos[1] += ball_vel[1]
    
    
    # draw ball
    canvas.draw_circle(ball_pos, 20, 1, 'white',"white")
    
    
    # update paddle's vertical position, keep paddle on the screen
    paddle1_pos += paddle1_vel
    paddle2_pos += paddle2_vel    
    if paddle1_pos >= 400:
        paddle1_pos = 400
    elif paddle1_pos <= 80:
        paddle1_pos = 80
    if paddle2_pos >= 400:
        paddle2_pos = 400
    elif paddle2_pos <= 80:
        paddle2_pos = 80        
        

    # draw paddles
    canvas.draw_line((0,paddle1_pos-80 ), (0, paddle1_pos), 16, 'white')
    canvas.draw_line((600, paddle2_pos-80), (600, paddle2_pos), 16, 'white')
    
    # determine whether paddle and ball collide    
    
    # draw scores
    canvas.draw_text(str(score1), (250, 70), 60, 'white')
    canvas.draw_text(str(score2), (320, 70), 60, 'white')
        
def keydown(key):
    global paddle1_vel, paddle2_vel
    if key==simplegui.KEY_MAP["up"]:
        paddle2_vel = -2.5
    if key==simplegui.KEY_MAP["down"]:
        paddle2_vel = 2.5
    if key==simplegui.KEY_MAP["w"]:
        paddle1_vel = -2.5
    if key==simplegui.KEY_MAP["s"]:
        paddle1_vel = 2.5
def keyup(key):
    global paddle1_vel, paddle2_vel
    if key==simplegui.KEY_MAP["up"]:
        paddle2_vel = 0
    if key==simplegui.KEY_MAP["down"]:
        paddle2_vel = 0
    if key==simplegui.KEY_MAP["w"]:
        paddle1_vel = 0
    if key==simplegui.KEY_MAP["s"]:
        paddle1_vel = 0   


# create frame
frame = simplegui.create_frame("Pong", WIDTH, HEIGHT)
frame.set_draw_handler(draw)
#frame.set_draw_handler(spawn_ball)
frame.set_keydown_handler(keydown)
frame.set_keyup_handler(keyup)
button1 = frame.add_button('Restart', new_game)

# start frame
new_game()
frame.start()
