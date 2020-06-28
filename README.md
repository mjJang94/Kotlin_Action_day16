# 필수적인 함수 Filter와 map

filter와 map은 컬렉션을 사용할 때 기반이 되는 함수로 대부분의 컬렉션 연상을 이 두 함수를 통해 표현할 수 있다.   
아래 코드는 앞전에 나온 person클래스를 filter 함수를 이용하여 컬렉션을 이터레이션하면서 주어진 람다에 각 우너소를 넘겨 람다가 true를 반환하게끔 원소만 모은다.
<code>
<pre>
val people = listOf(Person("Alice", 29), Person("Bob", 31))
println(people.filter {it.age > 30})
Bob, 31
</code>
</pre>
filter 함수는 컬렉션에서 원치 않는 원소를 제거하여 보여주지만 원소를 변환하는 것은 불가능하다. 그래서 map으로 변환시켜야 한다.   
map 함수는 주어진 람다를 컬렉션의 각 원소에 적용한 결과를 모아서 새로운 컬렉션으로 만들어 준다.
<code>
<pre>
val list = listOf(1,2,3,4)
println(list.map{it * it})
[1, 4, 9, 16]
</code>
</pre>
원소 리스트의 개수는 같지만, 각 원소는 주어진 함수에 따라 변형되었다.   
또는 사람의 데이터를 가진 리스트에서 사람의 이름으로만 이루어진 리스트로 만들고 싶으면 map으로 만들 수 있다.
<code>
<pre>
val people = listOf(Person("Alice",29), Person("Bob",31))
println(people.map{it.name})
[Alice, Bob]
</code>
</pre>
멤버 참조를 이용해서 좀 더 합리적으로 코드를 짜보자면 이렇게도 가능하다.
<code>
<pre>
people.filter{it.age>30}.map(Person::name)
[Bob]
</code>
</pre>
이제 이 목록에서 가장 나이가 많은 사람을 추려낸다고 생각하고 코드를 짜보자.
<code>
<pre>
people.filter{it.age == people.maxBy(Person::age)!!.age}
</code>
</pre>
하지만 이렇게 짜면 목록에 있는 사람들만큼 최댓값을 구하는 연산을 한다. 이런 부분을 개선해 최댓값을 한 번만 계산하게 만든 코드는 아래와 같다.
<code>
<pre>
val maxAge = people.maxBy(Person::age)!!.age
people.filter{it.age == maxAge}
</code>
</pre>
(질문해보자..음...? 음...)

필터와 변환 함수를 맵에 적용할 수도 있다.
<code>
<pre>
val numbers = mapOf(0 to "zero", 1 to "one")
println(numbers.mapValues{it.value.toUpperCase()})
</code>
</pre>
