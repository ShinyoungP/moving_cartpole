## **Moving Cartpole**
### **reward 체계 수정**
### **시도 1**
```python
if next_state[0,0]>=0 and next_state[0,0]<0.7 and next_state[0,1]>0:
    reward=next_state[0,0] * next_state[0,1] *(-100)
elif next_state[0,0]>=0 and next_state[0,0]<0.7 and next_state[0,1]<0:
    reward=next_state[0,0] * next_state[0,1]*(-100)
elif next_state[0,0]<0 and next_state[0,0]>-0.7 and next_state[0,1]<0:
    reward=next_state[0,0] * next_state[0,1]*(-100)
elif next_state[0,0]<0 and next_state[0,0]>-0.7 and next_state[0,1]>0:
    reward=next_state[0,0] * next_state[0,1]*(-100)

elif next_state[0,0]>=1.2 and next_state[0,0]<1.8 and next_state[0,1]>0 and next_state[0,2]>0: 
    reward=next_state[0,0] * next_state[0,1]*(5) * next_state[0,2]*(-5) *40
elif next_state[0,0]>=1.2 and next_state[0,0]<1.8 and next_state[0,1]<0 and next_state[0,2]<0: 
    reward=next_state[0,0]*next_state[0,1]*(-100)* next_state[0,2]*(-5)
elif next_state[0,0]<=-1.2 and next_state[0,0]>-1.8 and next_state[0,1]<0 and next_state[0,2]<0: 
    reward=next_state[0,0]* next_state[0,1]*(100)* next_state[0,2]*(5) *2
elif next_state[0,0]<=-1.2 and next_state[0,0]>-1.8 and next_state[0,1]>0 and next_state[0,2]>0:
    reward= (-next_state[0,0])*(next_state[0,1]*(100)* next_state[0,2]*(5))

elif next_state[0,0]>=1.8 and next_state[0,1]>0 and next_state[0,2]>0:
    reward=-1800*next_state[0,0]*(next_state[0,1]*next_state[0,2])
elif next_state[0,0]>=2 and next_state[0,2]<=0:
reward=-1000*next_state[0,2]
elif next_state[0,0]>=1.8 and next_state[0,1]<0 and next_state[0,2]<0:
    reward=100*next_state[0,0]*(next_state[0,1]*next_state[0,2])
elif next_state[0,0]<=-1.8 and next_state[0,1]<0 and next_state[0,2]<0: 
    reward=1800*next_state[0,0]*(next_state[0,1]*next_state[0,2])
elif next_state[0,0]<=-2 and next_state[0,2]>=0:
    reward=1000*next_state[0,2]
elif next_state[0,0]<=-1.8 and next_state[0,1]>0 and next_state[0,2]>0: 
    reward=-100*next_state[0,0]*(next_state[0,1]*next_state[0,2])
```
* 잘한 행동에는 + reward를, 그렇지 못한 행동에는 - reward를 줌. <br>
1. position : 0 ~ 0.7 <br>
오른쪽으로 운동할 떄 : 점점 속도가 줄어들도록 속도가 커짐에 따라 큰 패널티를 부여 <br>
왼쪽으로 운동할 때 : 속도가 커지도록 속도가 커짐에 따라 큰 보상을 부여 <br>
2. position : -0.7 ~ 0.7 <br>
오른쪽으로 운동할 때 : 속도가 커지도록 속도가 커짐에 따라 큰 보상을 부여 <br>
왼쪽으로 운동할 때 : 점점 속도가 줄어들도록 속도가 커짐에 따라 큰 패널티를 부여 <br>
3. position : 1.2 ~ 1.8 <br>
오른쪽으로 운동할 때 : 속도가 +에서 -가 되도록, 각도가 +에서 -가 되도록 속도와 각도가 커짐에 따라 큰 패널티를 부여 <br>
왼쪽으로 운동할 때 : 속도가 -로 커지도록, 각도가 -로 커지도록 속도와 각도가 -로 커짐에 따라 큰 보상을 부여 <br>
4. position : -1.8 ~ -1.2 <br>
오른쪽으로 운동할 떄 : 속도가 +로 커지도록, 각도가 +로 커지도록 속도와 각도가 +로 커짐에 따라 큰 보상을 부여 <br>
왼쪽으로 운동할 때 : 속도가 -에서 +가 되도록, 각도가 -에서 +가 되도록, 속도와 각도가 -로 커짐에 따라 큰 패널티를 부여 <br>
5. position : 1.8 이상 <br>
오른쪽으로 운동할 때 : 속도가 +에서 -가 되도록, 각도가 +에서 -가 되도록 속도와 각도가 커짐에 따라 큰 패널티를 부여
왼쪽으로 운동할 때 : 속도가 -로 더욱 커지도록, 각도가 -로 더욱 커지도록 속도와 각도가 -로 커짐에 따라 큰 보상을 부여 <br>
6. position : -1.8 이하 <br>
오른쪽으로 운동할 때 : 속도가 +로 더욱 커지도록, 각도가 +로 더욱 커지도록 속도와 각도가 +로 커짐에 따라 큰 보상을 부여 <br>
왼쪽으로 운동할 때 : 속도가 -에서 +가 되도록, 각도가 -에서 +가 되도록 속도와 각도가 -로 커짐에 따라 큰 패널티를 부여 <br>
7. position : 2 이상<br>
position에 비례해 큰 패널티 부여 <br>
8. position : -2 이하<br>
position에 비례해 큰 패널티 부여 <br>

### **시도 1 - 결과**
* episode를 충분히 돌리자 cart가 막대를 세우는데에 초점을 맞추어 한 자리에서 균형을 잡고 있었다. reward가 양수가 될수도, 음수가 될수도 있으니 학습이 잘 되지 않는 것 같다. 다음 시도에서는 reward가 무조건 양수만 되도록, 잘한 일에 대해서만 조건을 작성해보자. <br>


### **시도 2**
```python

if next_state[0,0] >= -1.6 and next_state[0,0] < -0.4 and next_state[0,1] > 0 and next_state[0,2] < 0.06 and next_state[0,2] >= 0:
    reward = (-next_state[0,0]) * (next_state[0,1] * 2 + next_state[0,2] * 2)
elif next_state[0,0] >= 0.8 and next_state[0,0] < 1.6 and next_state[0,1] < 0 and next_state[0,2] < 0 and next_state[0,2] > -0.11:
    reward = next_state[0,0] * (next_state[0,1] * (-2) + next_state[0,2] * (-5))
            

elif next_state[0,0] < 1.6 and next_state[0,0] > 0.4 and next_state[0,1] < 0 and next_state[0,2] >= -0.06 and next_state[0,2] < 0:
    reward = next_state[0,0] * (next_state[0,1] * (-2) + next_state[0,2] * (-2))
elif next_state[0,0] <-0.8 and next_state[0,0] >= -1.6 and next_state[0,1] > 0 and next_state[0,2] > 0 and next_state[0,2] < 0.11:
    reward = (-next_state[0,0]) * (next_state[0,1] * (2) + next_state[0,2] * 5)

```
* 잘한 행동에 대해서만 + reward 부여 <br>
1. position : -0.8 ~ -0.4 <br>
오른쪽으로 이동할 때 속도가 커질수록, 각도가 커질수록 보상을 부여 (각도가 너무 커지지 않도록 0.06 rad보다 작을 때만 부여) <br>
2. position : 0.8 ~ 1.6 <br>
왼쪽으로 이동할 때 속도가 -로 커질수록, 각도가 -로 커질수록 보상을 부여 (각도가 너무 -로 커지지 않도록 -0.11 rad보다 클 때만 부여) <br>
3. position : 0.4 ~ 0.8 <br>
왼쪽으로 이동할 때 속도가 -로 커질수록, 각도가 -로 커질수록 보상을 부여 (각도가 너무 -로 커지지 않도록 -0.06 rad보다 클 때만 부여) <br>
4. position : -1.6 ~ -0.8 <br>
오른쪽으로 이동할 때 속도가 커질수록, 각도가 커질수록 보상을 부여 (각도가 너무 커지지 않도록 0.11 rad보다 작을 때만 부여) <br>
0.8 ~ 1.6 과 0.4 ~0.8을 구분한 이유는 0.8 ~ 1.6 구간에서는 각도를 많이 바꾸어도 되기 때문에 각도가 -0.11 rad보다 클 때 보상을 부여했고 0.4 ~ 0.8 구간에서는 각도를 많이 바꾸면 안되기 때문에 각도가 -0.06 rad보다 클 때만 보상을 부여했다.


### **시도 2 - 결과** <br>
계속 막대를 세우는데에 초점을 두는지 cart가 한 자리에서 멈추어 있다. 막대를 세우기만 해도 각 step에서 reward를 1씩 받으니 움직이지 않고 오래 막대의 균형을 맞추기만 해도 움직일 때보다 큰 reward를 받을 수 있다. 따라서, 속도와 각도가 바뀜에 따라 더 큰 reward를 부여해보자. 또, 아직 각속도를 고려하지 않았다. 오른쪽 끝에서 각속도가 -로 커지도록 왼쪽 끝에서는 각속도가 +로 커지도록 보상 체계를 수정해보자. <br>


### **시도 3**
```python
if next_state[0,0]>0 and next_state[0,0]<=0.5 and next_state[0,1]>=0 and next_state[0,2]>=0 :
    reward=next_state[0,0]*10*(next_state[0,1]*200 + next_state[0,2]*500 )
elif next_state[0,0]>0 and next_state[0,0]<=0.5 and next_state[0,1]<0 and next_state[0,2]<0 :
    reward=2*(next_state[0,1]*(-200) + next_state[0,2]*(-500) )
elif next_state[0,0]>=-0.5 and next_state[0,0]<=0 and next_state[0,1]<0 and next_state[0,2]<0 :
    reward=(-next_state[0,0])*10*(next_state[0,1]*(-200) + next_state[0,2]*(-500) )
elif next_state[0,0]>=-0.5 and next_state[0,0]<=0 and next_state[0,1]>=0 and next_state[0,2]>=0 :
    reward=2*(next_state[0,1]*200 + next_state[0,2]*500 )
                
elif next_state[0,0]>0.95 and next_state[0,0]<=1 and next_state[0,3]<0:
    reward=next_state[0,0]*next_state[0,3]*(-1000)
elif next_state[0,0]>=-1 and next_state[0,0]<-0.95 and next_state[0,3]>0:
    reward=(-next_state[0,0])*next_state[0,3]*1000

elif next_state[0,0]<=0.95 and next_state[0,0]>0.5 and next_state[0,2]<0 and next_state[0,1]<0:
    reward=(next_state[0,2]*(-700)+next_state[0,1]*(-500))
elif next_state[0,0]>=-0.95 and next_state[0,0]<-0.5 and next_state[0,2]>0 and next_state[0,1]>0:
    reward=(next_state[0,2]*700+next_state[0,1]*500)

```
* 각속도를 고려하여 보상 체계를 수정한다. 각속도와 관련된 보상을 제외하면 위 시도와 거의 비슷하다. <br>
1. position : 0.95 ~ 1 <br>
오른쪽을 향하는 각도가 왼쪽으로 갈 수 있도록 각소도가 -로 커져야한다. 따라서, 각속도가 -로 커질수록 큰 보상을 준다. <br>
2. position : -1 ~ -0.95 <br>
왼쪽을 향하는 각도가 오른쪽으로 갈 수 있도록 각소도가 +로 커져야한다. 따라서, 각속도가 -+로 커질수록 큰 보상을 준다. <br>


### **시도 3 - 결과**
* 초반에 속도가 줄지 않아 각속도를 바꾸는 행동을 학습하지 못하였다. 각속도를 바꾸기 전에 cart의 속도를 줄여주는 보상이 필요할 듯 하다.



### **시도 4**
```python
if next_state[0,0]>0 and next_state[0,0]<=0.5 and next_state[0,1]<0.8 and next_state[0,1]>=0 and next_state[0,2]>=0 :
    reward=next_state[0,0]*10*(next_state[0,1]*200 + next_state[0,2]*500 )
elif next_state[0,0]>0 and next_state[0,0]<=0.5 and next_state[0,1]<0 and next_state[0,2]<0 :
    reward=2*(next_state[0,1]*(-200) + next_state[0,2]*(-500) )
elif next_state[0,0]>=-0.5 and next_state[0,0]<=0 and next_state[0,1]>-0.8 and next_state[0,1]<0 and next_state[0,2]<0 :
    reward=(-next_state[0,0])*10*(next_state[0,1]*(-200) + next_state[0,2]*(-500) )
elif next_state[0,0]>=-0.5 and next_state[0,0]<=0 and next_state[0,1]>=0 and next_state[0,2]>=0 :
    reward=2*(next_state[0,1]*200 + next_state[0,2]*500 )
                
elif next_state[0,0]>0.95 and next_state[0,0]<=1 and next_state[0,3]<0:
    reward=next_state[0,0]*next_state[0,3]*(-1000)
elif next_state[0,0]>=-1 and next_state[0,0]<-0.95 and next_state[0,3]>0:
    reward=(-next_state[0,0])*next_state[0,3]*1000

elif next_state[0,0]<=0.95 and next_state[0,0]>0.5 and next_state[0,2]<0 and next_state[0,1]<0:
    reward=(next_state[0,2]*(-700)+next_state[0,1]*(-500))
elif next_state[0,0]>=-0.95 and next_state[0,0]<-0.5 and next_state[0,2]>0 and next_state[0,1]>0:
    reward=(next_state[0,2]*700+next_state[0,1]*500)

elif next_state[0,0]>0.5 and next_state[0,0]<=0.95 and next_state[0,1]>=0.8:
    reward=(4-next_state[0,1])*next_state[0,0]
elif next_state[0,0]>=-0.95 and next_state[0,0]<=0.5 and next_state[0,1]<=-0.8:
    reward=(4+next_state[0,1])*(-next_state[0,0])
```
* cart가 각속도를 바꾸기 전에 속도를 줄이는 행동에 대한 보상도 추가한다. <br>
1. position : 0.5 ~ 0.95 <br>
(4-(속도))를 곱해줌으로써 속도가 점점 커지면 작은 reward를 받도록 설계한다. 따라서 agent는 0.95 position까지 속도를 줄여야 한다는 것을 학습할 것이다. <br>
2. position : -0.95 ~ -0.5 <br>
(4+(속도))를 곱해줌으로써 속도가 -로 점점 커지면 작은 reward를 받도록 설계한다.

### **시도 4 - 결과** <br>
이전 시도에 비해서는 살짝의 움직임을 가지지만 여전히 한 구간 내에서만 움직이며 균형을 맞추고 있다. position -0.5 ~ 0.5에서 cart의 속도와 각도에 대해서 reward를 부여하였다. cart는 굳이 다른 구간으로 이동하지 않고 이 구간에서 속도와 각도를 바꿈으로써 충분한 reward를 받고 있는 것 같다. 다음 시도에서는 한 구간에서는 한 방향으로 움직일 때에 대해서 reward를 부여해보자.<br>


### **시도 5** 
```python
if next_state[0,0]<0 and next_state[0,0]>=-0.5 and next_state[0,2]>0 and next_state[0,1]>0:
    reward=next_state[0,1]*200 + next_state[0,2]*500
elif  next_state[0,0]>0 and next_state[0,0]<=0.5 and next_state[0,2]<0 and next_state[0,1]<0:
    reward=next_state[0,1]*(-200) + next_state[0,2]*(-500)

elif next_state[0,0]>0.5 and next_state[0,0]<=0.65 and next_state[0,1]>0 :
    reward=next_state[0,0]*(3-next_state[0,1]) * 300
elif next_state[0,0]>=-0.65 and next_state[0,0]<-0.5 and next_state[0,1]<0:
    reward=(-next_state[0,0])*(3+next_state[0,1]) * 300

elif next_state[0,0]>0.65 and next_state[0,0]<0.7 and next_state[0,3]<0:
    reward=next_state[0,3]*(-5000)
                
elif next_state[0,0]<-0.65 and next_state[0,0]>-0.7 and next_state[0,3]>0:
    reward=next_state[0,3]*5000
```
* 한 구간에서 한 방향으로 움직일 때의 행동에 대해서만 보상을 부여했다. <br>
1. position : 0 ~ 0.5 <br>
왼쪽으로 가는 행동에 대해서만 속도가 -로 커질수록, 각도가 -로 커질수록 큰 reward를 부여했다. <br> <br>
2. position : -0.5 ~ 0 <br>
오른쪽으로 가는 행동에 대해서만 속도가 +로 커질수록, 각도가 +로 커질수록 큰 reward를 부여했다. <br>
3. position : 0.65 ~ 0.7 <br>
각속도가 +에서 -가 되도록 보상을 부여했다. <br>
4. position : -0.7 ~ -0.65 <br>
각속도가 -에서 +가 되도록 보상을 부여했다. <br>
5. position : 0.5 ~ 0.65 <br>
속도가 점점 줄어들도록 보상을 부여했다. <br>
6. position : -0.65 ~ -0.5 <br>
속도가 점점 줄어들도록 보상을 부여했다. <br>

### **시도 5 - 결과** <br>
막대의 균형을 오래 유지하진 못했지만 학습 도중 왔다갔다하면서 막대의 균형을 잡는 모습을 볼 수 있다. <br>

![](https://user-images.githubusercontent.com/122516287/256458884-7f7c6852-a11c-4814-8c1f-f78ad40deca3.gif)

![](https://user-images.githubusercontent.com/122516287/256463737-9603823e-d495-4bde-9597-211319ba621c.gif)
