---
title: 언리얼 엔진 인터페이스 BlueprintNativeEvent 호출 문제
date: 2025-01-23 12:00:00
categories: [Problem, UnrealEngine]
tags: [Problem, UnrealEngine, Interface, BlueprintNativeEvent]
published: true
---

## 문제

```c++
#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "UObject/Interface.h"
#include "TestCode.generated.h"

UINTERFACE(MinimalAPI, Blueprintable)
class UTestInterface : public UInterface
{
	GENERATED_BODY()
};

class ITestInterface
{
	GENERATED_BODY()

public:
	UFUNCTION(BlueprintNativeEvent)
	void Test(int A, const FString& B);

};

UCLASS()
class TESTPROJECT_API ATestActor : public AActor, public ITestInterface
{
	GENERATED_BODY()

protected:
	virtual void BeginPlay() override;

public:	
	virtual void Test_Implementation(int A, const FString& B) override;

};
```

```c++
void ATestActor::BeginPlay()
{
	Super::BeginPlay();
	
    // 문제가 발생하는 코드
	Test(123, "Hello");
}

void ATestActor::Test_Implementation(int A, const FString& B)
{

}
```

위 예시와 같이 인터페이스에서 UFUNCTION의 BlueprintNativeEvent 키워드를 
사용한 함수를  
직접적으로 사용할 경우 다음과 같은 에러가 발생합니다.  

> Assertion failed: 0 && "Do not directly call Event functions in Interfaces. Call Execute_Test instead." [File:C:\Important\Project\Unreal Project\TestProject\Intermediate\Build\Win64\UnrealEditor\Inc\TestProject\UHT\TestCode.gen.cpp] [Line: 30] 

## 원인

언리얼 엔진에서는 인터페이스의 함수를 직접 호출할 수 없도록 하였기 때문에 에러가 발생합니다. 

## 해결법 

아래와 같은 방법으로  `인터페이스 클래스::Execute_함수 이름(인터페이스 객체, 매개 변수1, 매개 변수2)`  
와 같은 방법을  사용하여 BlueprintNativeEvent 키워드를 사용한 함수를 호출해야 합니다.

```c++
void ATestActor::BeginPlay()
{
	Super::BeginPlay();
	
	ITestInterface::Execute_Test(this, 123, "Hello");
}

void ATestActor::Test_Implementation(int A, const FString& B)
{

}
```