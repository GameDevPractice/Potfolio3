## Potfolio3(리듬게임)
### 목표
![image](https://github.com/user-attachments/assets/b4b471f2-f924-4610-adf4-8df484812cee)<br/>
DJ Max와 같은 리듬 게임을 목표

### 구상도
![image](https://github.com/user-attachments/assets/b75a89be-f164-4a83-883b-c54f9d78b54a)

![image](https://github.com/user-attachments/assets/b78224e6-9edd-45a6-ab93-5ec60f421285)<br/>

### Actor들
#### Node
![image](https://github.com/user-attachments/assets/0c7b62e1-fd46-4742-bd51-63bf35fabdd4)<br/>
SpawnActor에서 떨어질 Node

#### Button
![image](https://github.com/user-attachments/assets/bab2663d-6e5e-4df0-bad9-cf32e65208b8)<br/>
- 키를 눌러 활성화 되는 버튼들, 활성화된 버튼은 Node와 접촉 시 반응을 합니다.<br/>
= 활성화 시 표시를 위해 Point Light를 사용하였습니다. 키를 때면 비 활성화가 되며 PointLight가 꺼집니다. 또한 Box충돌체들이 활성화 됩니다.<br/>

###### Button On
![image](https://github.com/user-attachments/assets/e1ec3c9c-fd90-40bb-82bb-592f3b391e1b)<br/>
- 지속적으로 누를 경우를 생각하여 Bool 변수 Input을 만들어 사용하였습니다.<br/>
- 후술할 제작 모드를 판별하기 위해 Bool 변수 Make를 만들어 사용하였습니다.<br/>
  
###### Button Off
![image](https://github.com/user-attachments/assets/30cda2ee-23aa-47a9-9097-15778588fa40)<br/>

###### Begin Overlap
![image](https://github.com/user-attachments/assets/29117d82-8877-46ae-b1cb-00aad46d1f29)<br/>
- 접촉된 충돌체에 따라 점수가 다르며, 성공한 횟수만큼 콤보 횟수가 늘어납니다. 이는 GameMode에서 관리합니다.<br/>

#### FinalCollision 
![image](https://github.com/user-attachments/assets/a272d953-84a5-4b1d-b10e-5a85a7efc41f)<br/>
- 버튼에서 놓친 Node들을 제거하는 Actor이고, Node와 접촉하게 되면 쌓아올리던 콤보가 사라집니다.<br/>

#### Spawn Node
- Node를 생성하는 Actor 입니다.<br/>
- DataTable를 통해 Node를 생성할 시간, 노래, 스폰할 위치를 저장하고 이를 이용해 스폰합니다.<br/>

![image](https://github.com/user-attachments/assets/6efb4522-d099-47ac-9880-0e5b415fcd0b) <br/>
- DataTable의 정보들을 저장합니다.<br/>
<br/>

![image](https://github.com/user-attachments/assets/64eadb0d-9672-4208-b7ce-dcb7ebf792de)<br/>
- 저장된 정보에서 저장된 노래가 없음 게임이 종료가되고, 노래의 재생이 끝이 나도 종료가 됩니다.<br/>
- 노래가 있다면, SetTimer를 사용하여 저장된 Node들을 스폰합니다.<br/>

### GameMode
- 점수와 콤보에 관련된 함수들을 관리합니다.<br>
- 게임이 종료 시 UI인 Finish를 생성합니다.<br/>

### LevelBluePrint
![image](https://github.com/user-attachments/assets/f93f3c5b-b5ed-4462-afe7-20c4c7236ad6)<br/>
- 게임을 진행하는 맵의 Blueprint이며, 버튼을 비 . 활성화 시킬 수 있는 Blueprint 입니다.<br/>
- 시작 시 점수와 콤보를 표시해 줄 UI를 생성한다.<br/>

###### Buttons
![image](https://github.com/user-attachments/assets/433b37de-33de-4b20-840c-008273ea2f37)<br/>
![image](https://github.com/user-attachments/assets/9fe0ecac-7604-4b3a-b809-6f1a9fc66f9e)<br/>
- Custom Event를 통해 해당 버튼을 활성화 혹은 비활성화 시키게 합니다.<br/>
- 여기에 Time이란 변수는 월드에서 흐르는 시간을 의미하고 BtnTime은 버튼을 누른 시간을 말합니다.<br/>
- 이 두 변수를 사용하여 제작 모드일 시 Node를 생성 해야 할 시기를 정할 수 있습니다.<br/>

###### Tick
![image](https://github.com/user-attachments/assets/2e7c0802-0007-4d5d-aea8-7d4332760cb0)<br/>
- 월드의 시간을 저장하고 Bool 변수 Play를 통해 후술할 UI(WB_Main)에서 정한 노래를 재생하게 합니다.<br/>

### HUD
#### WB_MainScroll
![image](https://github.com/user-attachments/assets/95b1d555-c7d0-41d8-b832-e09d77d55b1f)
- 메인 화면에 들어갈 Scroll Box 이며, 버튼을 누를 시 맞는 노래가 재생이 되고 배경이 바뀝니다.<br/>

###### Construct
![image](https://github.com/user-attachments/assets/2772fcca-bb30-493a-b076-f78d7220ee6e)<br/>
- 위젯 생성 시 받는 변수로 Title(Text),Data(DataTable),Index(Index),Image(Texture 2D)가 있으며,<br/>
Title을 곡 제목을, Data는 노래가 저장되어 있는 DataTable을 사용하여 재생할 노래에, Image는 배경을, Index는 버튼에 맞는 번호로 들어가게 됩니다.<br/>

###### Pressed(Button)
![image](https://github.com/user-attachments/assets/442a65c0-a16b-4f91-a25e-6b3c9351cc42)<br/>
![image](https://github.com/user-attachments/assets/ed078c98-c3d6-4d39-95d8-a36e1e5e8ac5)<br/>

- 버튼에 맞는 노래가 재생되고 있지 않다면, 생성 시 저장된 노래를 재생하게 합니다.
- 연속으로 누를 가능성이 있어 DoOnce를 통해 1번만 하게끔 강제합니다.
- 노래가 재생되고 있다면, 노래를 중지 시키며, DoOnce의 Reset 기능을 사용합니다.
- 이때 저장된 노래는 AudioComponent를 사용하여 재생됩니다.
- MainWidget의 Index와 배경을 변경합니다.

###### Tick
![image](https://github.com/user-attachments/assets/34ff9f5e-68db-43ad-a124-ac36942acb27)<br/>

- 각각 다른 버튼을 누를 경우 노래가 중복으로 재생이 되어 MainWIdget의 Index와 해당 버튼의 Index을 값을 상시 검사를 하여 막았습니다.

#### WB_MainWidget
###### 위젯
![image](https://github.com/user-attachments/assets/f0b3d9c6-b2f0-4bf9-bb3b-e108ca14a2ca)<br/>
###### 게임 시작
![image](https://github.com/user-attachments/assets/fe0495f6-9bf0-41d4-a4ee-ee7d4d2b6915)<br/>
- 메인 화면이며, Play버튼을 누르면 게임이 시작되게 만들었습니다.

###### Construct
![image](https://github.com/user-attachments/assets/a7534f94-9fda-40b5-b494-bbd44143e69c)<br/>
- 여기에 있는 변수 Data는 위에서 설명한 데이터테이블이 아닌 데이터테이블을 담은 데이터테이블 변수입니다.
- 이 변수를 WB_MainScroll을 생성할 때 전달하여 각자 맞는 노래와 배경, 제목을 지정할 수 있습니다.
- 제작모드와 플레이모드를 지정 할 수 있게 월드에 있는 버튼들을 가져와 저장합니다.

###### OnPressed(PlayBtn)
![image](https://github.com/user-attachments/assets/779866f5-afb9-476a-8ab4-13f910fdd498)<br/>
- 게임이 시작되는 버튼입니다.
- 게임에 집중할 수 있게 세팅을 합니다.

###### OnPressed(MakeBtn)
![image](https://github.com/user-attachments/assets/ab2f0e39-b54f-41e4-82d3-1eada7cd64c6)<br/>
- 제작모드가 되는 버튼입니다.

#### WB_Score
![image](https://github.com/user-attachments/assets/bfb057a8-b31a-49c5-9024-765e222c9e3d)<br/>
- 플레이 도중 쌓은 점수를 볼 수 있게 해주는 위젯입니다.

###### Construct
![image](https://github.com/user-attachments/assets/f22d6c8e-96d3-4d07-909e-3047dfc70022)<br/>
- 게임플레이를 저장합니다.

###### Tick
![image](https://github.com/user-attachments/assets/f1545003-fd6f-4460-94cc-e65a5b13dc84)<br/>
- Tick을 통해 점수와 콤보를 표시하도록 했습니다.
- 콤보가 5이상일 시 에만 표시되도록 했습니다.

#### WB_Finsish
![image](https://github.com/user-attachments/assets/71c49ae1-e72f-4040-bade-4d00c581fc84)<br/>
- 게임이 끝날 경우 나오는 위젯입니다.
  
###### Construct
![image](https://github.com/user-attachments/assets/03df280f-3432-4292-b88b-717d59c4fb0a)<br/>
- 최종 점수를 표시하고 엔딩 곡이 나오도록 하였습니다.

###### Buttons
![image](https://github.com/user-attachments/assets/efe83634-8db9-4f33-971f-02722d2c2700)<br/>
- 각 버튼에 맞는 기능들을 하게 하였습니다.

