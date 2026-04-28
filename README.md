from hub import light_matrix
from hub import port
import motor
import runloop
import time
async def main():
    # write your code here
    await light_matrix.write("Hi!")
    async def forward_fast(angle):
        motor.run_for_degrees(port.F, -angle, 360)
        motor.run_for_degrees(port.E, angle, 360)

    async def forward_slow(angle):
        motor.run_for_degrees(port.F, -angle, 100)
        motor.run_for_degrees(port.E, angle, 100)

    async def back_fast(angle):
        motor.run_for_degrees(port.F, angle, 360)
        motor.run_for_degrees(port.E, -angle, 360)

    async def back_slow(angle):
        motor.run_for_degrees(port.F, angle, 100)
        motor.run_for_degrees(port.E, -angle, 100)

    async def turn_right(angle):
        motor.run_for_degrees(port.E, -angle, 100)
        motor.run_for_degrees(port.F, -angle, 100)

    async def turn_left(angle):
        motor.run_for_degrees(port.E, angle, 100)
        motor.run_for_degrees(port.F, angle, 100)

    async def left_arm(angle):
        await motor.run_for_degrees(port.B, angle, 100)

    async def right_arm(angle):
        await motor.run_for_degrees(port.A, angle, 100)

    async def hit(angle):
        await motor.run_for_degrees(port.A, angle, 1000)
        await motor.run_for_degrees(port.A, -angle, 1000)



# raise arm
    await left_arm(50)
    await right_arm(-190)
    
#go forward to silo
    await forward_fast(650)
    time.sleep(3)

# hit silo
    await hit(167)
    await hit(167)
    await hit(167)

#turn go around the silo 
    await turn_left(200)
    time.sleep(1)
    await forward_fast(200)
    time.sleep(1)
    await turn_right(200)

#go to the rocks
    await forward_fast(300)
    time.sleep(3)
    await turn_right(100)
    time.sleep(1)
    await left_arm(-20)
    time.sleep(1)
    await turn_left(400)



runloop.run(main())
