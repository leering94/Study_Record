# Arrays.asList vs ArrayList(Arrays.asList())

## Arrays.asList

- 배열을 **고정 크기의 List객체**로 변환할 수 있다.
- 배열을 목록으로 사용할 수 있도록 하는 래퍼일 분이다. 데이터가 복사되거나 생성되지 않는다.
- **요소 추가 또는 제거가 허용되지 않기 때문에 길이를 수정할 수 없다.**
- 배열 내부의 항목은 수정할 수 있다. List의 항목을 수정하면 원래 배열에도 반영된다.

```java
String[] stringArray = new String[] { "A", "B", "C", "D" };

ArrayList stringList = Arrays.asList(stringArray);
```

> *stringList의 첫 번째 요소를 **수정**하면 어떻게 될까?*
> 

```java
stringList.set(0, "E");
 
assertThat(stringList).containsExactly("E", "B", "C", "D");
assertThat(stringArray).containsExactly("E", "B", "C", "D");
```

> 보*다시피 원래 배열도 수정됐다. 
그럼 stringList에 새 요소를 삽입하면 어떻게 될까?*
> 

```java
stringList.add("F");
```

```java
java.lang.UnsupportedOperationException
	at java.base/java.util.AbstractList.add(AbstractList.java:153)
	at java.base/java.util.AbstractList.add(AbstractList.java:111)
```

> *List에 요소를 **추가/제거** 하면 java.lang.UnsupportedOperationException 이 발생 한다.*
> 

## ArrayList(Arrays.asList())

- Arrays.asList 메서드 와 유사하게 **ArrayList <>(Arrays.asList(array)) 에서 목록 을 생성해야 하는 경우** ArrayList<>(Arrays.asList(array)) 를 사용할 수 있다.
- 그러나 이전과 달리 얘는 배열의 복사본이므로 **새 목록을 수정해도 원래 배열에는 영향을 미치지 않는다.**
- 요소 **추가 및 제거**와 같은 일반 **ArrayList의 모든 기능**이 있다.

```java
String[] stringArray = new String[] { "A", "B", "C", "D" }; 
List stringList = new ArrayList<>(Arrays.asList(stringArray));
```

> *stringList의 첫 번째 요소를 수정해보자!*
> 

```java
stringList.set(0, "E");
 
assertThat(stringList).containsExactly("E", "B", "C", "D");
```

> *원래 Arrray에서는 어떤 일이 발생했을까??*
> 

```java
assertThat(stringArray).containsExactly("A", "B", "C", "D");
```

> *보다시피 원래 배열은 그대로 유지된다.*
>
