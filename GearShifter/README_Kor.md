# Gear Shifter
EGP Hud와 커스텀 설정이 있는 수정 가능한 기어 변속기입니다.  
예제 패턴은 "ShifterPattern"를 참고해주세요.

## Settings
KeyLeft #KeyLeft                                      **#왼쪽**  
KeyRight = "Pad_6"                                    **#오른쪽**  
KeyUp = "Pad_8"                                       **#윗쪽**  
KeyDown = "Pad_5"                                     **#아랫쪽**  
KeyShifterToggle1 = ""                                **#레인저 (화물 트럭용, 사용하지 않을 시 비워두세요)**  
KeyShifterToggle2 = ""                                **#스플리터 (화물 트럭용, 사용하지 않을 시 비워두세요)**  
KeyClutch = "LShift"                                  **#클러치 (사용하지 않을 시 비워두세요)**  
Delay = 0.2                                           **#변속 딜레이 (초 단위)**  
InputPriority = "Col"                                 **#처리 우선순위 ("Row" 혹은 "Col"를 기재하세요)**  

#Engine  
Powerband = vec2(800,3000)                            **#엔진의 파워밴드 (최솟값, 최댓값)**  

#Egp  
Offset = vec2(0,0)                                    **#Hud 위치 조절**  
Scale = 30                                            **#기어 변속기 크기 (픽셀 단위)**  
Thickness = 1                                         **#기어 변속기 두께 (배수, Scale 기반)**  
Color = vec(150)                                      **#기어 변속기 색상**  
KnobSize = 50                                         **#기어 노브 크기 (픽셀)**  
KnobColor = vec(200)                                  **#기어 노브 색상**  
KnobTextSize = 1                                      **#기어 노브 문자 크기 (배수, KnobSize 기반)**  
KnobTextColor = vec(0)                                **#기어 노브 문자 색상**  
ShifterToggle1Color = array(vec(55,0,0),vec(255,0,0)) **#레인저 색상 (꺼짐, 켜짐)**  
ShifterToggle2Color = array(vec(0,0,55),vec(0,0,255)) **#스플리터 색상 (꺼짐, 켜짐)**  

#Gears  
                                                      **#출력을 위한 C단 목록 (사용하지 않을 시 비워두세요)**  
Gear["D",array] = array(1,2,3,4,5)                    **#출력을 위한 D단 목록**  
Gear["R",array] = array(-1)                           **#출력을 위한 R단 목록**  

Pattern["Row1",array] = array(0,-1,1,0)               **#패턴의 가로축 (Y좌표, X최솟값, X최댓값, 중심점; 사용하지 않을 시 비워두세요)**  

Pattern["Col1",array] = array(-1,-1,1)                **#패턴의 세로축 (X좌표, Y최솟값, Y최댓값, 중심점; 사용하지 않을 시 비워두세요)**  
Pattern["Col2",array] = array(0,-1,1)  
Pattern["Col3",array] = array(1,-1,1)  

Pattern["Gear_0,0",array] = array("N")                **#출력을 위한 기어 배열**  
Pattern["Gear_-1,-1",array] = array("D1")  
Pattern["Gear_-1,1",array] = array("D2")  
Pattern["Gear_0,-1",array] = array("D3")  
Pattern["Gear_0,1",array] = array("D4")  
Pattern["Gear_1,-1",array] = array("D5")  
Pattern["Gear_1,1",array] = array("R")  

## 커스텀 변속기 패턴 만드는 법
### 1. 만들고 싶은 변속기의 패턴을 그리세요.
만약 당신이 어떠한 문제도 만들고 싶지 않다면, 변속기 패턴을 격자나 종이등에 그려볼 것을 강력히 추천드립니다.  
이 예시에서는, 설명을 위해 다음 구조를 사용하겠습니다.  
![Example Pattern](/GearShifter/image/PatternEx01.png "설명을 위한 예시 패턴")
### 2. 시작하기 전 구조를 한번 확인하세요.
패턴을 모두 그렸다면, 한번 확인해보세요.  
변속기 구조에는 어떠한 빈 공간과 부적절한 경로, 그리고 겹치는 부분도 있어서는 안됩니다.  
ForceDirection이 올바르게 되어있는지도 확인하세요.  
### 3. 각 지점에 좌표를 지정하세요.
확인한 후, 각 지점과 꼭짓점에 좌표를 지정하세요.  
![Example Pattern](/GearShifter/image/PatternEx02.png "설명을 위한 예시 패턴")  
이 예시에서는, N단을 [-1,0]으로 지정했습니다.  
### 4. ForceDirection을 각 축에 지정하세요.
`ForceDirection` 은 이 E2에 있는 새로운 시스템으로, 기어가 스스로 지정된 위치로 움직이게 해주는 기능입니다.  
ForceDirection을 올바르게 사용하기 위해서는 그것의 중심점을 설정해주어야 합니다.  
![Example Pattern](/GearShifter/image/PatternEx03.png "설명을 위한 예시 패턴")
### 5. 원하는 지점에 기어를 설정하세요.
이후, 올바른 위치에 원하는 기어를 설정해야 합니다.  
기어들은 레인저나 스플리터 없이는 절대 겹쳐서는 안됩니다.  
![Example Pattern](/GearShifter/image/PatternEx04.png "설명을 위한 예시 패턴")
### 6. Pattern과 Gear 배열을 채워넣으세요.
마지막으로, 두 배열을 올바른 양식에 따라 작성하세요.  

양식)  
Gear["{기어 종류}",array] = array({기어}) **#기어 종류는 반드시 C, D, R 중에서 하나가 되어야 합니다. / D단이나 R단과 달리 C단은 사용하지 않을 시 작성하지 않아도 됩니다.**  
Pattern["Row{번호}",array] = array(Y좌표, X최솟값, X최댓값, ForceDirection 중심점) **ForceDirection을 사용하지 않을 시 {ForceDirection 중심점}를 비워두세요.**  
Pattern["Col{번호}",array] = array(X좌표, Y최솟값, Y최댓값, ForceDirection 중심점) **ForceDirection을 사용하지 않을 시 {ForceDirection 중심점}를 비워두세요.**  
Pattern["Gear_{좌표}",array] = array({기어 이름}) **{기어 이름}의 갯수는 1개에서 4개 사이어야 합니다. / 기어 갯수가 2개 이상일 시 ShifterToggle1을, 3개 이상일 시 ShifterToggle2를 사용해야 합니다.**  

예시)  
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

## 에러들
이 E2에는 5개의 다른 에러가 있습니다. 에러가 발생할 경우 다음 설명을 참고해주세요.  
1. NullPointException : 값이 없음
2. SuchElementException : 지정 ID를 찾을 수 없음
3. ArgumentMismatchException : 함수에 인수가 부족함
4. IOException : 입력 혹은 출력값이 적합하지 않음
5. OutOfRangeException : 값이 지정된 범위를 벗어남
