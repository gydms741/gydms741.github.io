---
title: "Array와 List"
date: 2021-05-20 23:33:28 -0400
categories: Java
---

## Array

- 여러 데이터를 하나의 이름으로 그룹핑해서 관리 하기위한 자료구조. index와 값이 쌍으로 구성
- index는 값에 대한 유일무이한 식별자(마치 주민번호) (리스트에서 인덱스는 몇 번째 데이터인가 정도의 의미를 가짐)
- 논리적 저장 순서와 물리적 저장 순서가 일치 ⇒ index로 해당원소에 접근할 수 있다.(0(1))
- 연속된 메모리의 공간으로 이루어져 있다
- 배열은 정의와 동시에 길이를 지정하며 길이를 바꿀 수 없다.

**장점**
- 인덱스를 통한 검색이 용이함
- 연속적이므로 메모리 관리가 편하다
- 원하는 요소가 몇번째에 있는 지만 알면 아래의 공식에 의해서 빠르게 원하는 값을 찾을 수 있다.
(배열의 인덱스가 n인 요소의 주소 = 배열의 시작주소 + type의 size*n)

**단점**
- 크기가 고정되어 있기 때문에 어떤 엘리먼트가 삭제되면, 삭제된 상태를 빈 공간으로 남겨두어야 한다. ⇒ 메모리 낭비
- 정적이므로 배열의 크기를 컴파일 이전에 정해줘야 한다.
- 컴파일 이후 배열의 크기를 변동 할 수 없다.

## List

- 리스트는 순서가 있는 엘리먼트의 모임으로 배열과는 다르게 빈 엘리먼트는 절대 허용하지 않는다.
- 리스트는 배열이 가지고 있는 인덱스라는 장점을 버리고 대신 빈틈없는 데이터의 적재 라는 장점을 취함
- 리스트에서 인덱스는 몇 번째 데이터인가 정도(순서)의 의미를 가진다.
- 순차성을 보장하지 못하기 때문에 special locality보장이 되지 않아서 cash hit가 어렵다.(데이터 갯수가 확실하게 정해져 있고, 자주 사용된다면 array가 더 효율적이다.)
- 불연속적으로 메모리 공간을 차지

장점
- 포인터를 통하여 다음 데이터의 위치를 가르키고 있어 삽입 삭제의 용이
- 동적이므로 크기가 정해져 있지 않다.
- 메모리의 재사용 편리
- 불연속적이므로 메모리 관리의 편리

단점
- 검색 성능이 좋지 않다.

## ArrayList

일반배열과 ArrayList는 인덱스로 객체를 관리한다는 점에서 동일하지만, **크기를 동적**으로 늘릴 수 있다는 점에서 차이점이 있다. ArrayList는 내부에서 처음 설정한 저장 용량이 있다. 설정한 저장 용량 크기를 넘어서 더 많은 객체가 들어오게 되면, 배열 크기를 **1.5배**로 증가시킴

```java
//DEFAULT_CAPACITY=10
//기본 저장용량 10으로 리스트 생성
List<String> list = new ArrayList<>();

//저장 용량을 100으로 설정해 ArrayList 생성
List<String> list = new ArrayList<>(100);
```

ArrayList에서 특정 인덱스의 객체를 제거하게 되면, 제거한 객체의 인덱스부터 마지막 인덱스까지 모두 앞으로 1칸씩 앞으로 이동한다. 객체를 추가하게 되면 1칸씩 뒤로 이동하게 된다. 인덱스 값을 유지하기 위해서 전체 객체의 위치가 이동한다. 따라서 잦은 원소의 이동, 삭제가 발생할 경우 ArrayList보다 LinkedList를 사용하는 것이 좋다.

## LinkedList

노드 간에 연결을 통해서 리스트로 구현된 객체이다. 다음 노드의 위치 정보만 가지고 있으며 인덱스를 가지고 있지 않기 때문에 탐색시 순차접근만 가능(노드 탐색 시 시간이 많이 소요될 수 있음) 

배열은 모든 데이터가 연속적으로 존재하지만 링크드 리스트는 불연속적으로 존재하는 데이터를 서로 연결한 형태로 구성되어 있다. 

(randomAccess불가능)노드 추가/삭제는 위치정보의 수정만으로 가능하기 때문에 성능이 좋음

```java
public class ArrayListLinkedListTest2 {
	public static void main(String args[]) {
		ArrayList al = new ArrayList(1000000);
		LinkedList ll = new LinkedList();
		add(al);
		add(ll);

		System.out.println("= 접근시간테스트 = ");
		System.out.println("ArrayList :"+ access(al));
		Systme.out.println("LinkedList :"+ access(ll));
	}

	public static void add(List list){
			for(int i=0; i<100000 ; i++) list.add(i+"");
	}

	public static long access(List list){
			long start = System.currentTimeMillis();
			for(int i=0; i<10000;i++) list.get(i);
			long end = System.currentTimeMillis();
			return end - start;
	}

}
```

**결론 1** 순차적으로 추가/삭제하는 경우에는 ArrayList가 LinkedList보다 빠르다.

**결론 2** 중간 데이터를 추가/삭제하는 경우에는 LinkedList가 ArrayList보다 빠르다.
