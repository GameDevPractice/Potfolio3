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

##### Button On
![image](https://github.com/user-attachments/assets/e1ec3c9c-fd90-40bb-82bb-592f3b391e1b)<br/>
- 지속적으로 누를 경우를 생각하여 Bool 변수 Input을 만들어 사용하였습니다.<br/>
- 후술할 제작 모드를 판별하기 위해 Bool 변수 Make를 만들어 사용하였습니다.<br/>

##### Button Off
![image](https://github.com/user-attachments/assets/30cda2ee-23aa-47a9-9097-15778588fa40)<br/>

##### Begin Overlap
![image](https://github.com/user-attachments/assets/29117d82-8877-46ae-b1cb-00aad46d1f29)<br/>
- 접촉된 충돌체에 따라 점수가 다르며, 성공한 횟수만큼 콤보 횟수가 늘어납니다. 이는 GameMode에서 관리합니다.<br/>
