+++
title = "Zip-tie Monstrosity :: An Interactive Projected Surface"
date = 2019-08-08T11:06:12-07:00
author = "Audrey Xie"
tags = ["computer vision", "games"]
showFullContent = false
draft = false
+++

Computer vision + music = life-sized rhythm games

<!--more-->

## Background 

There’s quite a long, convoluted backstory to this project. I’ll do my best to shorten it, but if you don’t want to read it, just scroll past this paragraph. Basically, a group of five high schoolers, me included, were tasked with designing a gamified solution to adolescent obesity. One of the first things that came to mind was Dance Dance Revolution (DDR) because it’s not only fun to play, but also forces you to do exercise. Of course we couldn’t directly copy the format of DDR, so that got us thinking. What if we took an existing rhythm game, and just made it larger? Two of us had experience playing a game called *osu!*. In the game there are hit circles, sliders, and spinners which appear on the screen in different locations and at different times. The user is supposed to interact with these items in time with the music. Not much is needed to play this game, you just have to move the cursor around the screen and left-click. In the end, we decided not to make a life-sized *osu!*, but I couldn’t help but feel disappointed at what could have been. So when I had some extra time, I decided to make my dream a reality.

## Planning

The general idea is that there’s a projector vertically mounted overhead that projects the game onto the ground, then there’s a webcam also placed over the projected area that is used to track the player’s location on the field, which will translate into the location of the cursor on the laptop. Lastly, the player will be holding a bluetooth mouse, used only for left-clicking. This means that the player has to actually walk and step on game objects that are projected on the ground.

## Code

The principle behind translating player position into cursor location is simple. Just look for a red blob, find the center of the red blob, set that value as the location of the screen. I guess here’s the code for the color detection algorithm? (btw I'm using OpenCV)

```python
while True:
    _, frame = cap.read()

    # The webcam I'm using inverts everything, I also oriented it the wrong way when attaching it to the ceiling. So I'm compensating for that in code because I'm lazy.
    frame = cv2.flip(frame, -1)

    # Cropping because the projection does not fill up the webcam FOV
    frame = frame[int(r[1]):int(r[1]+r[3]), int(r[0]):int(r[0]+r[2])]

    #HSV works better than thresholding R
    hsv = cv2.cvtColor(frame, cv2.COLOR_BGR2HSV)

    # lower red range
    lower_red = np.array([0, 120, 70])
    upper_red = np.array([10, 255, 255])
    mask1 = cv2.inRange(hsv, lower_red, upper_red)

    # upper red range
    lower_red = np.array([170, 120, 70])
    upper_red = np.array([180, 255, 255])
    mask = mask1 + cv2.inRange(hsv, lower_red, upper_red)

    kernel = np.ones((5, 5), np.uint8)

    # Get only red blobs
    mask = cv2.erode(mask, kernel)

    _, contours, _ = cv2.findContours(mask, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)

    if contours:

        # Only use the largest red blob
        cnt = max(contours, key = lambda x: cv2.contourArea(x))
        cv2.drawContours(frame, [cnt], 0, (0, 0, 0), 5)            
        
        # Calculate centroid of red blob
        M = cv2.moments(cnt)
        
        # Scale the two values based on screen resolution
        center_x = int((M['m10']/M['m00']) * x_mult)
        center_y = int((M['m01']/M['m00']) * y_mult)

        # Set cursor location using centroid of red blob
        pyautogui.moveTo(center_x, center_y)

    cv2.imshow("Frame", frame)
    cv2.imshow("Mask", mask)

    # Use esc to stop program
    key = cv2.waitKey(1)
    if key == 27:
        break

cap.release()
cv2.destroyAllWindows()
```
Since the projection didn’t fill the webcam FOV, I added some code to set ROI.

```python
cap = cv2.VideoCapture(1)
_, frame = cap.read()
 
from_center = False
r = cv2.selectROI(frame, from_center)
 
screen_width = r[2]
screen_height = r[3]
 
x_mult = 3200 / screen_width
y_mult = 1800 / screen_height
```
![ROI selector](/images/interactive-projection/ROI.jpg)

The code can be found [here](https://github.com/audrey-xie/interactive-projected-surface).

## Hardware

So with the code working, it was now time to set up this whole system. The webcam was easily attached to the ceiling using hook and loop tape. The projector was another story. My parents were very against me drilling holes in the ceiling, thus, I had to get creative. Experimentation lead me to create a zip-tie monstrosity that hangs from a clamp fastened to a beam on the ceiling (the clamp was later moved to the skylight). 

![Hook and loop tape](/images/interactive-projection/IMG_3587.jpg)

![Zip-tie pt. 1](/images/interactive-projection/IMG_3591.jpg)

![Zip-tie pt. 2](/images/interactive-projection/IMG_3592.jpg)

Then I just connected everything and hoped that it would work. To my surprise, it did. After some cable management, I got to playing. Sadly, the projected image is really small, which means that the cursor position isn’t very accurate. Also, the latency for the cursor position is pretty bad, which is a death sentence in the world of rhythm games. So my dream of playing life sized *osu!* has to wait until another day.

![Projector setup closeup](/images/interactive-projection/IMG_3635.jpg)

![10/10 cable management](/images/interactive-projection/IMG_3642.jpg)

![Laptop setup](/images/interactive-projection/IMG_3605.jpg)

![Projected surface](/images/interactive-projection/IMG_3650.jpg)

## Final Product

But it can do other functions, such as drawing. Here’s a video.

{{< youtube OWHzJUwTdZI >}}