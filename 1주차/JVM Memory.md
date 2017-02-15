## JVM Memory
### JVM 구조
#### 메모리 : 프로그램을 실행하기 위한 데이터 및 명령어를 저장하는 공간
- 왜 메모리 구조를 공부해야하나 ?
 - 같은 기능의 프로그램이더라도 메모리 관리에 따라 성능 좌우
 - 메모리 관리가 되지 않는 경우 속도저하 현상 / 튕김 현상이 나타날 수 있음
 - 한정된 메모리를 효율적으로 사용하여 최고의 성능을 내기 위함


#### 자바 프로그램의 실행구조
- 프로그램이 실행되기 위해서는 OS가 제어하고 있는 시스템 리소스의 일부인 메모리를 제어할 수 있어야 한다.
- C는 OS에 종속되어 실행되게 되어있다.
- JAVA는 JVM만 있으면 실행 가능한데, JVM이 OS에게 메모리 사용권한을 할당받고 JVM이 JAVA 프로그램을 호출하여 실행한다.
- JAVA는 OS에 직접 제어받는 방식보단 느리다.


![jvm_exe](/images/jvm_exe.png)

#### JVM이란?
- Java Virtual Machine
- JAVA  - OS 사이의 중계자
- JAVA가 OS에 구애받지 않고 재사용 가능하게 해줌.
- 메모리 관리 기능 (Garbage Collection)

#### JAVA 프로그램 실행 과정과 JVM 메모리 구조
- JAVA 프로그램이 실행 -> JVM은 OS로부터 필요한 메모리 할당 -> JVM은 이 메모리를 용도에 따라 여러 영역으로 나누어 관리

```
- Java Compiler : JAVA 코드를 Byte Code로 변환
- Class Loader : Class 파일을 메모리(Runtime Data Area)에 적재하는 기능
- Execution Engine : Byte Code를 실행 가능하게 해석해주는 기능
- Runtime Data Area : 프로그램 수행을 위해 OS 에서 할당받은 공간
```
#### Runtime Data Area
1. Class Area
 - Method Area, Code Area, Static Area로 불리어짐
 - Field Info : 멤버변수 이름, 데이터 타입, 접근 제어자 정보
 - Method Info : 메서드의 이름, 리턴타입, 매개변수, 접근 제어자 정보
 - Type Info : Type 속성이 Class인지 Interface인지 여부
 - 상수 풀(Constant Pool) : Type에서 사용된 상수를 저장하는 곳, 문자 상수, 타입, 필드, Method의 symbolic reference
 - Class variable : Static 변수
 - Class 사용 이전에 메모리 할당 : final class

2. Stack Area
 - Last In First Out(LIFO)
 - 메서드 호출 시마다 각각 스택 프레임 생성
 - 메서드 안에서 사용되는 값들 저장하고, 메서드 수행이 끝나면 프레임별로 삭제

3. Heap Area
 - new 연산자로 생성된 객체와 배열 저장
 - 클래스 영역에 로드된 클래스만 생성 가능
 - Garbage Collector를 통해 메모리 반환
 - Permanet Generation : 생성된 객체들의 정보의 주소값이 저장된 공간
    - New Area : 객체들이 최초로 생성되는 공간
    - Eden : 객체들이 최초로 생성되는 공간
    - Survivor : Eden에서 참조되는 객체들이 저장되는 공간
    - Old Area : New Area에서 일정시간 이상 참조되고 있는 객체들이 저장되는 공간

4. Native method stack Area
 - 자바 외의 다른 언어에서 제공되는 메서드들이 저장

5. PC Register
 - Thread가 생성될 때마다 생성
 - 현재 실행되는 부분의 명령과 주소 저장

6. Garbage Collection
 - 참조되지 않은 객체들 탐색 후 삭제
 - Heap 메모리 재사용
 - __Minor GC__
    1. New 영역에서 일어나는 GC
    2. Eden 영역에 객체가 가득 차게 되면 첫번째 GC 발생
    3. Survivor1 영역에 값 복사
    4. Survivor1 영역을 제외한 나머지 영역의 객체들 삭제
    5. Eden 영역과 Survivor1 영역의 메모리가 기준치 이상일 경우, Eden 영역에 생성성된 객체와 Survivor1 영역에 있는 객체 중 참고되고 있는 객체가 있는지 검사
    6. 참조되고 있는 객체 Survivor2에 복사
    7. Survivor2 제외하고 객체 삭제
    8. 일정 시간 이상 참조되는 객체 Old로 이동
    9. 반복

 - __Major GC__
    1. Old영역에 있는 모든 객체 검사
    2. 참조되지 않은 객체들 한번에 삭제
    3. Minor GC에 비해 시간이 오래걸리고, 실행 중 프로세스가 정지

출처 : http://huelet.tistory.com/entry/JVM-%EB%A9%94%EB%AA%A8%EB%A6%AC%EA%B5%AC%EC%A1%B0
