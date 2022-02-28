import rotaryio
import board
import digitalio
import neopixel
import time


#Import both encoders and set the position to default number
encoder_1 = rotaryio.IncrementalEncoder(board.A2, board.A3)
last_position_1 = encoder_1.position
position_1 = 0

encoder_2 = rotaryio.IncrementalEncoder(board.SDA, board.RX)
last_position_2 = encoder_2.position
position_2 = 0

#import pixels LED_1
num_pixels = 8
pixels = neopixel.NeoPixel(board.A1, num_pixels, auto_write=False)

#import pixels LED_2
num_pixels_2 = 10
pixels_2 = neopixel.NeoPixel(board.A4, num_pixels_2, auto_write=False)

#import the button on encoder_2，this will allow the pixel_2 to turn off by using button_2
button_2 = digitalio.DigitalInOut(board.TX)
button_2.direction = digitalio.Direction.INPUT
button_2.pull = digitalio.Pull.UP
button_state_2 = None
button_press_state_2 = False

#read encoder_2 button value
button_2_pre = button_2.value
#using press_count to memorize how many times the button is being pressed.
press_count = 0
OFF = 0x000000

pixels.show()
time.sleep(0.1)
pixels.fill(0)



# variable to select chord type and intervals
crd_type = 0
crd_interval = 0


while True:

    # read the postion of both the encoder
    position_1 = encoder_1.position
    position_2 = encoder_2.position


    #looking for change in both encoder position
    if position_1 != last_position_1:
        print("encoder 1 POS", position_1)
        last_position_1 = position_1

    if position_2 != last_position_2:
        print("encoder 2 POS", position_2 )
        last_position_2 = position_2

    #let the chord type number control by the encoder position.
    crd_type = position_1 % 4
    crd_interval = position_2 % 4



# Encoder_1 controll on crd_type
    if position_1 == 0:
        pixels.fill(0)
    else:
        if position_1 % 8 == 1:
            print("A")
            pixels.fill(0)
            pixels[0] = ((0, 255, 0))
            pixels.show()
        elif position_1 % 8 == 2:
            print("B")
            pixels.fill(0)
            pixels[2] = ((0, 255, 0))
            pixels.show()
        elif position_1 % 8 == 3:
            print("C")
            pixels.fill(0)
            pixels[4] = ((0, 255, 0))
            pixels.show()
        elif position_1 % 8 == 4:
            print("D")
            pixels.fill(0)
            pixels[6] = ((0, 255, 0))
            pixels.show()


# Encoder_2 control on crd_interval
    if position_2 == 0:
            pixels_2.fill(0)
    else:
        if position_2 % 8 == 1:
            print("A2")
            pixels_2.fill(0)
            pixels_2[0] = ((0, 255, 0))
            pixels_2.show()
        elif position_2 % 8 == 2:
            print("B2")
            pixels_2.fill(0)
            pixels_2[2] = ((0, 255, 0))
            pixels_2.show()
        elif position_2 % 8 == 3:
            print("C2")
            pixels_2.fill(0)
            pixels_2[4] = ((0, 255, 0))
            pixels_2.show()
        elif position_2 % 8 == 4:
            print("D2")
            pixels_2.fill(0)
            pixels_2[6] = ((0, 255, 0))
            pixels_2.show()

    #when crd_type is >1, the crd_interval will disappear.
    if crd_type > 1:
        pixels_2.fill(OFF)
        pixels_2.fill(0)
        pixels_2[8] = ((0, 255, 0))
        pixels_2.show()

    #gather input values
    button_2_read = button_2.value
    # print out the current and previous values
    print("Button_2 Read is:", button_2_read)
    print("button_2 Prev is:", button_2_pre, '\n')

    if button_2_read != button_2_pre:
        # the button has changed...
        print("Button_2 Has Changed")
        #remember how many time i have presed the button_2
        press_count +=1
        # turn on the pixels_2 and auto set the position_2 to 0
        if press_count % 2 == 1:
            pixels_2.fill(0)
            position_2 = 0
            pixels_2[0] = ((0, 255, 0))
            pixels_2.show()
            print(press_count, 'is On')
        else:
            #turn off everything on pixels_2
            print(press_count,'is off')
            pixels_2.fill(OFF)
            position_2 =0
