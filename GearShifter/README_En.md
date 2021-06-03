# Gear Shifter
Adjustable gear shifter with EGP Hud, and custom settings.  
Refer to "ShifterPattern.txt" for example patterns.

## Settings
KeyLeft #KeyLeft                                      **#Left**  
KeyRight = "Pad_6"                                    **#Right**  
KeyUp = "Pad_8"                                       **#Up**  
KeyDown = "Pad_5"                                     **#Down**  
KeyShifterToggle1 = ""                                **#Ranger (for trucks, leave empty if you don't want to use it)**  
KeyShifterToggle2 = ""                                **#Splitter (for trucks, leave empty if you don't want to use it)**  
KeyClutch = "LShift"                                  **#Clutch (leave empty if you don't want to use it)**  
Delay = 0.2                                           **#Shifting delay (seconds)**  
InputPriority = "Col"                                 **#Processing priority (put "Row" or "Col")**  

#Engine
Powerband = vec2(800,3000)                            **#Powerband of engine (min, max)**  

#Egp
Offset = vec2(0,0)                                    **#Hud offset**  
Scale = 30                                            **#Gear shifter size (pixel)**  
Thickness = 1                                         **#Gear shifter thickness (multiply, based on Scale)**  
Color = vec(150)                                      **#Gear shifter color**  
KnobSize = 50                                         **#Gear knob size (pixel)**  
KnobColor = vec(200)                                  **#Gear knob color**  
KnobTextSize = 1                                      **#Gear knob text size (multiply, based on KnobSize)**  
KnobTextColor = vec(0)                                **#Gear knob text color**  
ShifterToggle1Color = array(vec(55,0,0),vec(255,0,0)) **#Ranger color (off, on)**  
ShifterToggle2Color = array(vec(0,0,55),vec(0,0,255)) **#Splitter color (off, on)**  

#Gears
                                                      **#Gear C list for output (leave empty if you don't want to use it)**  
Gear["D",array] = array(1,2,3,4,5)                    **#Gear D lsit for output**  
Gear["R",array] = array(-1)                           **#Gear R list for output**  

Pattern["Row1",array] = array(0,-1,1,0)               **#Row lines for Pattern (Ypos, Xmin, Xmax, MidPoint; leave empty if you don't want to use it)**  

Pattern["Col1",array] = array(-1,-1,1)                **#Column lines for Pattern (Xpos, Ymin, Ymax, MidPoint; leave empty if you don't want to use it)**  
Pattern["Col2",array] = array(0,-1,1)
Pattern["Col3",array] = array(1,-1,1)

Pattern["Gear_0,0",array] = array("N")                **#Gear lists for output**  
Pattern["Gear_-1,-1",array] = array("D1")
Pattern["Gear_-1,1",array] = array("D2")
Pattern["Gear_0,-1",array] = array("D3")
Pattern["Gear_0,1",array] = array("D4")
Pattern["Gear_1,-1",array] = array("D5")
Pattern["Gear_1,1",array] = array("R")

## how to make custom shifter pattern
### 1. Draw pattern what you want to make.
If you don't want to make any problems, I highly recommend to draw shifter pattern on grid or paper, etc.  
In this example, I will use this pattern for explain.  
![Example Pattern](/GearShifter/image/PatternEx01.png)
### 2. Check your pattern before starting.
If you draw your pattern, then check it.  
The pattern must not have any empty space, invalid route, and overlap section.  
Also check if the ForceDirection is correct.
### 3. Give cordinates to each points.
After that, give cordinates to each points and corners.  
![Example Pattern](/GearShifter/image/PatternEx02.png "Example pattern for explain.")  
In this example, I set Gear N to [-1,0].  
### 4. Set up ForceDirection to each lines.
`ForceDirection` is new system in this E2 which makes gear move to specific location by it self.  
You need to set up it's mid point to use ForceDirection.  
![Example Pattern](/GearShifter/image/PatternEx03.png "Example pattern for explain.")
### 5. Set up gears to points you want.
And then, you need to put gears in right position you want.  
Gears must not overlapped with each other without ranger or splitter.  
![Example Pattern](/GearShifter/image/PatternEx04.png "Example pattern for explain.")
### 6. Fill up Pattern and Gear array.
Finally, fill up two arrays in correct format.  

format)  
Gear["{Gear Type}",array] = array({Gear}) **#Gear Type must be one between C, D, and R. / You don't have to write C gear if you don't use unlike D and R.**  
Pattern["Row{n}",array] = array(Ypos, Xmin, Xmax, ForceDirection MidPos) **Leave {ForceDirection MidPos} empty if you don't want to use it.**  
Pattern["Col{n}",array] = array(Xpos, Ymin, Ymax, ForceDirection MidPos) **Leave {ForceDirection MidPos} empty if you don't want to use it.**  
Pattern["Gear_{Pos}",array] = array({Gear Text}) **The amount of {Gear Text} must be in range between 1 to 4. / You must use KeyShifterToggle1 at over 2, KeyShifterToggle2 at over 3.**  

ex)  
Gear["D",array] = array(1,2,3,4,5)  
Gear["R",array] = array(-1)  

Pattern["Row1",array] = array(-2,-1,1,-1)  
Pattern["Row2",array] = array(-1,0,1,0)  
Pattern["Row3",array] = array(0,-1,0,-1)  
Pattern["Row4",array] = array(1,-1,0)  
Pattern["Row5",array] = array(2,0,1,0)  

Pattern["Col1",array] = array(1,-2,-1)  
Pattern["Col2",array] = array(0,-1,0)  
Pattern["Col3",array] = array(-1,0,1)  
Pattern["Col4",array] = array(0,1,2)  
Pattern["Col5",array] = array(1,2,3)  

Pattern["Gear_-1,-2",array] = array("P")  
Pattern["Gear_0,-1",array] = array("R")  
Pattern["Gear_-1,0",array] = array("N")  
Pattern["Gear_-1,1",array] = array("D")  
Pattern["Gear_0,1",array] = array("D3")  
Pattern["Gear_0,2",array] = array("D2")  
Pattern["Gear_1,3",array] = array("D1")  

## Errors
There are 5 different error in this E2. Refer to following explanations if you have an error.
1. NullPointException : Missing value
2. SuchElementException : Cannot find specific ID
3. ArgumentMismatchException : Missing or too many arguments in array
4. IOException : Invalid input or output
5. OutOfRangeException : value out of range
