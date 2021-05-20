---
title: "Exception"
date: 2021-05-20 23:33:28 -0400
categories: CS
---

**예외 처리란 Exception 예외가 발생할 것을 대비하여 미리 예측해 이를 소스상에서 제어하고 처리하도록 만드는 것**

**예외** : 프로그램 코드에 의해서 수습될 수 있는 다소 미약한 오류

**에러** : 프로그램 코드에 의해서 수습될 수 없는 심각한 오류

**컴파일 에러 :**  컴파일 시에 발생하는 에러

**런타임 에러** : 실행 시에 발생하는 에러

**논리적 에러** : 실행은 되지만, 의도와 다르게 동작하는 것

- Checked Exception : 컴파일 시간에 검사하는 예외로서, 처리하지 않으면 컴파일 에러가 나므로 반드시 처리해야 한다. 처리 방법에는 try/catch 로 감싸거나, throws로 이를 호출한 메서드에게 예외를 넘겨준다. (이는 자바에만 존재하는 특별한 예외 처리 방식이다.)
- Unchecked Exception : 런타임 시간에 검사하는 예외로서, 컴파일하는데 문제는 없지만 실행 중에 예외가 발생할 수 있다. 주로 프로그래머의 실수, 잘못 작성된 코드, 사용자가 애플리케이션을 잘 못 사용할 때 이를 처리하는 경우에 발생한다.

[Untitled](https://www.notion.so/4f514f458bca49e6890aa2a4d2e81200)

## 예외처리 코드 및 실행순서(Try-Catch-Finally)

Try블록 : 실제 코드가 들어가는 곳으로써 예외 Exception이 발생할 가능성이 있는 코드

Catch블록 : Try 블록에서 Exception이 발생하면 코드 실행 순서가 Catch쪽으로 오게 된 후 처리

Finally블록 : Try블록에서의 Exception과 발생 유무와 상관 없이 무조건 수행되는 코드

Exception발생!

Try블록 수행 ⇒ Catch블록 수행 ⇒ Finally블록 수행(생략가능)

Exception미발생!

Try블록 수행 ⇒ Finally 블록 수행(생략가능)

```java
package jp02.part02;

/*
==> java ExceptionTest 10 20 0 실행시 3번째 인자값이 0이면 실행시 문제발생
==> 출력결과(실행시 에러)읽고 출력결과 확인
*/
public class ExceptionTest04{
	
	private int sum;
	private int avg;

	public ExceptionTest04(){
	}

	public void sum(int x,int y){
		System.out.println("1.==>sum시작");
		sum = x+y;
		System.out.println("1.==>합 :"+sum);
		System.out.println("1.==>sum끝");
	}

	public void avg(int z)throws ArithmeticException{
		System.out.println("2.==>avg시작");
		avg=sum/z;//z=0인경우 불능
		System.out.println("2.평균 : "+avg);
		System.out.println("2.==> avg끝");
			
	}

	public static void main(String[] args){
		
		int i = Integer.parseInt(args[0]);
		int j = Integer.parseInt(args[1]);
		int k = Integer.parseInt(args[2]);

		ExceptionTest04 et= new ExceptionTest04();
		et.sum(i,j);

		try{
			et.avg(k);
		}catch(ArithmeticException e){
			System.out.println("1.>>============================");
			System.out.println("et.avg(k)에서 Exception이 발생한 모양");
			System.out.println("2.>>============================");
			System.out.println(e);
			System.out.println("3.>>============================");
			System.out.println();
			System.out.println("4.>>============================");
		}

		System.out.println("main Method End...");
	}

}
```
