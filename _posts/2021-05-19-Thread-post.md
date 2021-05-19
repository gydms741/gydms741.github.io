---
title: "Thread"
date: 2021-05-19 12:40:28 -0400
categories: CS
---

## 1. 프로세스와 쓰레드

Thread

프로그램 : 파일이 저장 장치에 저장되어 있지만 메모리에는 올라가 있지 않은 정적인 상태를 말한다.

프로세스 : '실행중인 프로그램' 프로그램을 실행하면 OS로부터 실행에 필요한 자원(메모리)을 할당받아 프로세스가 된다.

멀티태스킹과 멀티쓰레딩

현재 우리가 사용하고 있는 윈도우나 유닉스를 포함한 대부분의 OS는 멀티태스킹을 지원하기 때문에 여러 개의 프로세스가 동시에 실행될 수 있다.

 이와 마찬가지로 멀티쓰레딩은 하나의 프로세스 내에서 여러 쓰레드가 동시에 작업을 수행하는 것이다. 

**멀티쓰레드의 장점**
- CPU의 사용률을 향상시킨다.
- 자원을 보다 효율적으로 사용할 수 있다.
- 사용자에 대한 응답성이 향상된다.
- 작업이 분리되어 코드가 간결해진다.

## 2. 쓰레드의 구현과 실행

1.Thread클래스를 상속

```java
class MyThread extends Thread{
	public void run() {/* 작업내용 */} // Thread클래스의 run()을 오버라이딩
}
```

2. Runnable인터페이스를 구현

```java
class MyThread implements Runnable{
	public void run() {/* 작업내용 */} // Runnable인터페이스의 run()을 구현
}
```

```java
package jp04.part01;

public class AfterThreadRunnable implements Runnable{
	
	private String name;
	
	public AfterThreadRunnable() {
	}
	public AfterThreadRunnable(String name) {
		this.name = name;
	}
	
	public void run() {
		for (int i = 1; i < 100; i++) {
			System.out.println(name+":"+i);
			
			// sleep() ==> API확인
			 try{
				Thread.sleep(100);
				}catch(InterruptedException e){
				System.out.println(e);
				}
			 
		}
	}

	public static void main(String[] args) {

		System.out.println("여기는 main start...");
		Runnable bt1 = new AfterThreadRunnable("1번째");
		AfterThreadRunnable bt2 = new AfterThreadRunnable("2번째");
		
		Thread t1 = new Thread(bt1);
		Thread t2 = new Thread(bt2);
		
		t1.start();
		t2.start();
		System.out.println("여기는 main end....");

	}

}
```
