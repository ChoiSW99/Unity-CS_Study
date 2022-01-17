# Unity-CS_Study

##### GameObject  
게임을 실행하면 나오는 게임을 구성하는 요소  
	예) 플레이어, 장애물, 게임 배경 등  
##### 하이에라키뷰(Hierarchy)  
	새로 만든 GameObject를 Cube라는 목록으로 표시
##### 씬뷰(Scene)  
	새로 만든 Cube라는 게임오브젝트의 배치상태와 모양 표시
	플레이시 게임오브젝트를 비추게함 shift+F
##### 게임오브젝트의 조작
 Q  
	신뷰에 마우스를 누르고 드래그하면 화면이 이동  
 W  
	GameObject의 위치를 조절  
 E  
	GameObject를 회전  
 R  
	GameObject의 크기 조절  
##### 시점 조절
	Alt키를 누르고 신뷰를 드래그
	마우스 우클릭 + wasd
       줌인/줌아웃
	마우스 휠 드래그
##### 복제(복붙)
	ctrl c, ctrl v == ctrl d
##### Inspector
	Transform 컴포넌트
		화살표로 조절 가능
##### 컴포넌트 : 게임오브젝트의 성질을 정해줌

##### -rigidbody : 물리법칙 (중력 등), Use Gravity 언체크하면 무중력
	     AddForce(Vector3);
##### -physics material : collider의 material에 적용됨, 동적/정적 마찰력과 탄성력 값, 충돌하는 두 오브젝트의 마찰이 합쳐지는 방식(friction combine)이 있음.
##### -collider : 충돌체, 물리엔진의 동작 기준이 됨. 
	void OnCollisionEnter(Collision collision) : 실제 충돌 시
		collision.gameObject가 자신과 부딪힌 게임오브젝트임
	void OnTriggetEnter(Collider collider) : 물체가 특정 영역을 지나갔을 때 발생하는 트리거, 물체 사라지게할 때 사용 
	물체가 충돌이 아니라 지나갔는지만(접촉) 감지하려면 Is Trigger를 체크 
		
##### - script(c#) : 개발자가 정의한 컴포넌트, 클래스명과 스크립트명이 꼭 같아야함.
	component 가져오기 : Rigidbody rb = GetComponent<Rigidbody>();
	gameobject 가져오기 : GameObject ball = GameObject.Find(“Ball”);
	(태그)
	GameObject g = GameObject.FindGameObjectWithTag(“태그명”);
   			 GameObject.FindGameObjectWithTags(“태그명”); //배열로 가져옴

	Vector3.Distance(position1, position2); //두 벡터간의 거리
	Vector3.MoveTowards(current위치, target위치, 속도); //현위치에서 target위치로 속도만큼씩 직선으로 감
	transform.Rotate(new Vector3(0,0,1)); //(0,0,1)방향으로 회전함

	GameManager 오브젝트, 스크립트 : 게임관리에 관한 메소드들을 모아서 관리, public
           GameObject.Find(“GameManager”).SendMessage(“게임매니저의 메소드명”);
	   호출할 메소드가 public이면 다른 스크립트에서 스크립트_컴포넌트.메소드로 호출가능함.
	public으로 변수 정의하면 Inspector에 나타남. 초기값은 Inspector의 값을 따라감.
Application.LoadLevel(“씬이름”); //씬 시작
Instantiate(원본오브젝트(prefab), 생성될위치, 돌리기)// 게임오브젝트 생성
Destroy(오브젝트) // 게임오브젝트 제거
Time.deltaTime // 전 프레임과의 시간
Prefab //원본, 나중에 꺼내 씬에 복제품으로 넣을 수 있음.

class : 설계도 
component : 객체

상속 
class A : B
부모클래스의 메소드 호출 base.메소드명();
이 때 부모클래스의 메소드는 private가 아니라 protected로 바꿔줘야 함.
	

사용자의 입력 받기 (Edit – Project Setting – Input - InputManager)
	Input.GetAxis(“Horizontal”); //화살표좌우 or AD(-1 ~ +1)
	Input.GetAxis(“Vertical”); //화살표상하 or WS(-1 ~ +1)

	Input.GetKeyDown(KeyCode.Space); //스페이스 누를 때 한번
	Input.GetKeyUp(KeyCode.Space); //스페이스 뗄 때 한번
	Input.GetKey(KeyCode.Space); //스페이스 누를때 계속

	Input.touchCount //어딘가 눌릴 때

	Input.GetMouseButton(0) //마우스 왼쪽 키 누를 때 
	Input.GetMouseButton(1) //마우스 오른쪽 키 누를 때 
	Input.mousePosition //마우스 위치
	if(Input.mousePosition  < Screen.Width/2) //마우스 클릭한 부분이 게임화면의 좌측

오일러각(EulerAngles)은 짐벌락현상이 발생할 수 있음. 이를 방지하려면 사원수(Quaternion을 사용)

부모/자식 오브젝트 : 예시) stage가 회전할 때 그 위의 장애물도 같이 회전되어야 함.
	스크립트에서 transform.position은 글로벌, transform.localPosition 로컬위치이므로 localPosition으로 작성해야 stage에 장애물이 붙은채로 동작함.
