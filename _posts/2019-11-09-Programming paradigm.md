---
layout: post
title: Programming Paradigm
categories : [ML,DL]
use_math: true
---
Prgramming Paradigm
================
by 알고리즘 문제 해결 전략

1. 단순한 문제로 만들고 최적화 시켜 나간다.

Type of Problems 
------------
- 원하는 답이 존재하는가?
- 여러 답 중 최적의 답 찾기(최적화 문제)


Brute Force
----------------   
완전 탐색 exhaustive search 라고도 한다. 가장 단순한 방법. 모든 경우의 수를 직접 컴퓨터로 돌려보고 그 결과를 찾는 방법이다.
무식해보이지만 컴퓨터는 반복연산에 강점이 있어 별다른 제약이 없는 경우 이 방법으로 대부분의 문제를 풀 수 있다.
실제 상업용 프로그램이나 대회에서는 메모리, 연산량, 연산시간 등에서 제한이 있는 경우가 많지만
제한이 미미한 경우 그냥 사용하기도 한다.
장점은 쉽고 단순하다는 것. 제약조건을 잘 따져본 후 가능하다면 brute force 방법을 쓴다면 많은 노력을 아낄 수 있다.
재귀호출으로 쉽게 구현할 수 있는 경우가 많다.

Divide & Conquer
---------------
분할정복. 주어진 문제를 둘 이상의 부분문제로 분해한 후 각 부분문제를 재귀호출로 계산한다. 각 부분문제의 답이 나오면 이를 이용하여
전체 문제의 답을 계산한다. 재귀 호출과 유사하나 하나의 재귀함수를 찾는 대신 여러 부분문제(거의 절반 정도의)로 분해한다는 점이 다르다.

조건 
1. 문제를 부분문제로 나눌 수 있는 자연스러운 방법이 있다.
2. 부분문제의 답들로 전체문제의 답을 계산하는 효율적인 방법이 있다.

주의점
잘못 분할할 경우 전체 과정에서 여러번 중복계산되는 부분 문제들이 나올 수 있다. 이는 전체 성능을 저하시킨다.
이 경우 Dynamic programming을 사용한다.

Dynamic Programming
---------------
중복계산되는 부분문제는 분할정복을 할 때 부분문제를 계산할 때 나타나는 중복되어 계산되는 부분문제이다. 중복계산되는 부분문제는 분할의 횟수가 늘어날수록 지수적으로 증가한다. 
대표적인 문제로 이항계수 계산이 있다.
DP는 분할정복과 비슷한 패러다임이지만 중복계산되는 부분문제(Overlapping subproblems)를 메모리에 저장해서 중복계산에 드는계산자원을 줄이는 방법이다.
(계산량이 줄어드는 대신 메모리 사용량이 늘어난다) 
이렇게 값을 저장해뒀다 재사용하는 방법을 memoization이라고 부른다. memoization은 입력에만 출력이 결정되는 referential transparent function에만 적용할 수 있다. 
입력 외의 요소가 결과에 영향을 주는 함수는 사용할 수 없다.
DP는 최적화 문제를 풀기위해 제안되었다. 최적화문제에서 유용하게 쓸 수 있다.(다른 문제들에서도 일부 유용하게 쓸 수 있음)

최적 부분 구조(optimal substructure)
현재 부분 문제가 어떤 경로로 호출되었던간에 남은 부분 문제들을 항상 최적으로 풀어도 되는 구조.
각 부분문제의 최적해를 얻었을 때 전체 문제의 최적해를 얻을 수 있을 경우 성립.
ex) 서울부터 대전을 지나 부산까지 가는 최적 경로 = 서울-대전의 최적경로 + 대전-부산의 최적 경로

최적화 문제의 DP 설계
1. 가장 간단한 해법인, 모든 답을 만들고 그 중 전체 점수가 가장 높은 최적해를 반환하는 부분문제 기반 exhaustive search 알고리즘을 설계
2. 전체 점수만 반환하는게 아니라 앞으로 남은 선택들의 점수를 반환하도록 부분문제 정의를 변경
3. 재귀 호출 입력에 이전 선택과 관련된 정보가 있다면 가능한 제거(독립적으로 만들기). 최적부분구조라면 완전 제거 가능.
    목적은 가능한한 중복되는 부분문제를 많이 만드는 것으로 중복된 문제가 많을수록 memoization을 효율적으로 할 수 있음.
4. 입력이 배열이나 문자열일 경우 가능하다면 memoization을 효율적으로 할 수 있도록 구조 변환(stl map등의 연관배열로 할 수 있으나 매우 느림)
5. memoization을 적용하여 1의 문제를 최적화.

경우의 수 계산하기 DP 설계
1. 모든 답을 직접 만들고 세어보는 exhaustive search 알고리즘 설계.
    a)모든 경우는 이 선택지들에 포함되어야 함
    b)어떤 경우도 두개 이상의 선택지에 포함되지 않음
2. 이전 조각에서 결정한 요소들에 대한 입력올 가능한 제거. 재귀 함수가 앞으로 남아있는 조각들을 고르는 경우의 수만 반환하도록 
3. memoization을 적용하여 최적화.

Greedy Method
---------------
위의 방법들과 마찬가지로 원하는 답을 재귀호출처럼 여러 조각으로 쪼갠 후 각 단계의 답을 이용해 전체 답을 구한다는 아이디어를 가진다.
exhaustive search나 DP와 다를 것이 없어보인다.. 하지만 모든 선택지를 전부 고려한 후 그 중 가장 좋은것을 고르는 두 방법과 달리
greedy method는 매 단계마다 해당 단계에서 가장 좋은 방법을 선택하는 알고리즘들을 말한다.

즉 현재 선택이 앞으로 남은 장기적인 선택들에 끼칠 영향을 고려하지 않는다. 
당연히 최적의 해를 찾을 가능성은 낮다. 
하지만 
1. greedy method를 사용해도 최적의 해를 찾을 수 있는 문제
2. 최적의 해를 찾기 너무 어려워 근사해를 찾는것만으로 의미가 있는 문제
에서 유용하게 사용할 수 있다. (인공신경망 학습의 gradient descent 방법이 greedy method에 속한다)

1에 해당하는 문제는 DP로도 풀 수 있으나 greedy method는 메모리나 계산시간에서 이점을 가진다.
2에 해당하는 문제는 조합탐색이나 메타휴리스틱 알고리즘들로 더 좋은 답을 구할 수 있다.

greedy method로 문제를 풀 수 있는것은 두가지 속성을 증명하면 된다.
greedy choice property. 이 속성이 성립할경우 매 순간의 greedy 선택은 최적해로 가는 선택이다.
optimal substructure 부문문제의 최적해에서 전체 문제의 최적해를 구할 수 있음을 보인다.

greedy method 설계
1. 문제의 답을 만드는 과정을 여러 부분문제로 나눈다.
2. 각 부분문제가 어떤 우선순위로 답을 내는지 결정한다. (직접 문제를 손으로 풀어보면 좋다)
3. 2가 결정되면, greedy method의 두 속성을 증명해본다.
    a) greedy choice property 각 단계에서 우리가 선택한 답을 포함하는 최적해가 존재하는가?
    우리의 답과 다른 최적해가 존재한다고 가정하고 이것을 조작하여 우리가 선택한 답을 포함하는 최적해로 바꿀수있는지 확인
    b) optimal substructure. 각 단계에서 최적의 선택만 했을 때 전체 최적해를 구할 수 있는지 증명
    
사용하기 좋은 문제 : 스케쥴링 문제 


Combinatorial Search
------------
그 동안의 방법들은 분할 방법이 없거나, 중복되는 부분문제가 없는 경우 적용할 수 없다.
이 경우 다시 exhaustive search로 돌아와야 한다. 
exhaustive search는 답을 내는 과정을 여러 선택으로 나누고 재귀호출로 각각의 선택지를 채워나가는 방법을 사용한다.
이때 부분답과 완성된 답의 집합을 search space라고 부른다. 
exhaustive search는 모든 답을 다 만들어보면서 문제를 해결한다. 따라서 수행시간은 search space의 크기에 비례한다.
하지만 대부분의 문제에서 search space의 크기는 문제 규모에 따라 기하급수적으로 증가한다.

유한한 크기의 탐색공간을 뒤지면서 답을 찾아내는 알고리즘들을 combinatorial search라고 한다(exhaustive search 포함)
이를 최적화하는 방법들은 기본적으로 최적해가 될 가능성이 없는 답들이 탐색되는것을 방지하여
seach space에서 탐색할 답의 수를 줄이는 것을 목표로 한다.
조합탐색은 문제 자체에 대한 식견, 속도와 정확도 사이의 trade off, 다양한 입력 형태 사이의 trade off를 모두 고려해야하며
어려운 문제에 속한다. 이렇다 할 정답이 없기에 모든 주제를 다룰 수는 없고 가장 유명한 접근법들, 처음으로 시도해보기 좋은
기법들에 대해 논의한다.

논의할 combinatorial search의 최적화 기법을 크게 두 가지로 분류한다.
pruning : 탐색 과정에서 최적해로 연결될 가능성이 없는 부분들을 가지치기한다. 
예를들어 현재 상태에서 나머지 답을 완성해도 현 시점에서 가지고 있는 최적해보다 나쁘다면 탐색을 중지할 수 있다.
greedy search : greedy method를 이용해 적당히 좋은 답을 먼저 찾아내어 pruning과 함께 사용할 경우 탐색의 효율을 높일 수 있다.

heuristic : 경험적으로 어림짐작 하는 것. 특정한 조건을 찾아내어 탐색종료 조건으로 활용할 수 있지만 말 그대로 경험적이기에 답이 있다기보단 문제를 보고 유추해야함.

정수 계획법 <- 참고만

Decision Problem
----------
Optimization problem을 decision problem(yes or no 형태의 답만 나오는 문제) 형태로 바꾼 후 이분법을 이용해 해결하는 방법.
특정문제에서 decision problem이 optimization problem보다 훨씬 풀기 쉬운 경우 유용.(반대는 불가능)


Numerical Analysis
------------



Partial Sum
------------
0부터 현재 주소까지의 값을 더한 값을 저장해두고(memoization) 이를 이용해 a~b까지의 합을 쉽게 구할 수 있다.
2차원 배열에도 사용할 수 있고 2차원 배열값이 이미지일 경우 integral image라고 함.

Queue, Stack, Dequeue
------------
online algorithm : 전체입력이 한번에 주어지지 않고 일부만 계속해서 주어질 때 계산을 할 수 있는 알고리즘. 입력의 크기가 굉장히 클 때 유용.

Strings
------------
KMP algorithm : 문자열 검색문제를 위한 간단한 알고리즘
    부분 일치 테이블 (needle[:n]까지의 접미사이면서 접두사가 될 수 있는 최대 문자열의 길이를 반환)
suffix array : 문자열 처리를 위한 자료구조
<-- 다시보기

Tree
-----------
트리는 계층관계를 갖는 객체를 표현하기 위해 쓰이지만, 실제로는 계층관계와 상관없이 같은 연산을 더 빠르게 할 수 있는
경우에 유용하게 사용할 수 있다.
-일반적인 트리
    트리의 용도 
    1)계층관계를 갖는 객체 표현 : 눈에 보이는 계층관계가 아니더라도 따져보았을 때 계층 형태를 띄는 문제도 있다.
    2)탐색형 자료구조
    트리의 성질
    재귀적 속성 - 트레에서 한 노드와 그 자손들은 또 하나의 트리이다.(sub tree) 따라서 재귀 호출로 구현한다.
    트리의 순회
    트리는 구조가 일정하지 않아 모든 자료를 순회하는 것이 어렵다. 이를 쉽게 하기 위해 재귀적인 속성을 이용한다.
    크게 3가지 방법이 있으며 preorder traverse(root-left-right), inorder traverse(left-root-right), postorder traverse(left-right-root)이다.
    
  
-트리에서 가장 긴 path 찾기 
    hint : 가장 긴 path의 양 끝 노드는 항상 leaf or root 노드이다.
       
-이진 검색 트리(탐색형 자료형). 
    이진트리(자식이 두개)이며 자료가 크기 순서로 정렬되어있어 추가,삭제,존재 여부 등의 연산을 배열보다 훨씬 빠르게 수행가능.
    크기 순서로 정렬된 배열과 차이점은 선형 자료구조가 아니기에 삽입이 수월하다는 것이다.
    삭제는 삭제하려는 노드의 두 자식을 각각 루트로 하는 두 서브트리를 합친(merge) 후 해당 트리의 루트를 삭제하려는 노드와 바꾼다.

-skewed tree
    예를 들어 root가 1이고 1~100까지 주어지는 이진 탐색 트리는 사실상 연결리스트가 되어 이진탐색트리로 사용하는 의미가 없다.
    이런 경우에도 제대로 기능할 수 있도록 balance를 잡아주는 변종들도 있으며 대표적으로 red black tree가 있다.

-트립(이진 검색 트리의 변종)
    트리에서 x보다 작은 원소의 수 찾기, k번째 원소 찾기 연산 등은 표준 라이브러리들에서 지원하지 않는 경우가 많다.
    이런 경우 이진 검색트리를 직접 구현해야하는데 단순한 이진 검색 트리는 skewed 문제로부터 자유롭지 않다.
    교과서적인 balanced tree인 AVL 트리나 red black 트리는 구현이 매우 까다로우며 어렵다.
    따라서 구현이 간단한 balanced tree인 treap이 유용하게 쓰일 수 있다.
    트리에 노드를 추가 할 때 임의의 priority를 부여한 후, 부모의 priority가 항상 자식의 priority보다
    크거나 같다는 조건을 조건을 추가한다. 즉 treap은 이진탐색트리의 조건과 함께 heap의 조건을 동시에 만족하도록 구성된다.(tree + heap이라서 treap이다.)
    쉽게 이해하려면 입력 순서대로 트리에 추가하는것이 아니라 우선순위를 먼저 매긴 후 우선순위로 정렬하여 높은것부터 트리에 추가한것이라고 이해하면 된다.
    (아주 낮은 확률로 skewed가 등장할 수도 있다.)
    treap의 삽입연산은 재귀호출을 통해 하면 되지만 새로운 노드의 priority가 root보다 높을 경우 새로운 root가 되어야 하기 때문에 조금 복잡해진다.
        기존 root의 key값이 새로운 노드보다 클 경우와 작을 경우로 나뉘는데, 방법은 비슷하다.
        만약 작다면, 기존 tree에서 root의 오른쪽 자손을 root로 하는 sub tree를 떼어낸다.
        그리고 이 sub tree를 추가된 노드의 key값과 비교하여 큰 것과 작은 것 두 sub tree로 분리한다.
        값이 작은 sub tree를 기존 root의 오른쪽 자손으로 연결하고, 값이 큰 sub tree는 추가된 노드의 오른쪽 자손으로 연결한다.
        그리고 기존 root를 추가된 노드의 왼쪽 자손으로 연결한다. 
    노드 삭제는 이진 탐색트리와 유사하다.
    treap을 직접만들어야하는 경우는 표준 라이브러리 구현에서 제공하지 않는 기능들(k번째 원소 찾기, x보다 작은 원소의 개수 세기 등)이 필요할 때 뿐이다.
    따라서 treap을 만들 때 각 노드 클래스는 서브트리의 크기 size등을 추가하여 만들게 된다. 
    
-우선순위 큐
    일반적인 큐와 비슷하지만 priority가 높은 자료가 먼저 pop되는 큐.
    수행할 작업이 여럿 있는데 시간은 제한되어 있을 때 우선순위가 높은 것부터 수행하는 경우에 사용하며 현실에서 종종 필요한 구조이다.
    balanced binary search tree로도 가능하지만 해야할 작업에 비해서 너무 복잡하다.
    우선순위 큐는 이러한 작업을 더 단순하게 수행할 수 있으며 대표적인 것이 heap tree이다.
    
-힙 
    heap은 최대,최소값을 root로 하도록 유지하는 조건이 걸린 트리로 최대 최소값을 찾는데 특화되어있다.
    우선순위 큐는 heap을 이용하면 아주 쉽게 구현할 수 있는데 heap의 최대값 조건을 priorty로 하여 구현하면 된다.
    heap은 이진트리와 달리 부모 노드가 자식 노드보다 큰 값을 가지기만 하면 되고 좌우의 대소관계는 신경쓰지 않는다.
    대신 skewed 될 경우 트리의 장점을 잃는다는 것은 똑같기 때문에 두가지 모양 규칙을 부여하여 만든다.
        1) 마지막 레벨을 제외한 모든 레벨에 노드가 꽉 차있어야 함
        2) 마지막 레벨에 노드가 있을 경우에는 항상 가장 왼쪽부터 순서대로 채워나가야 함.
    힙의 이런 조건들 덕분에 힙을 구현할 때 동적 배열로 트리를 표현할 수 있게 된다.(index를 이용해 부모자식관계등을 쉽게 찾을 수 있음)
    동적배열을 사용한 heap을 구현하였을 때 어떻게 새 원소를 꺼낼 수 있을까?
    특히 root를 제거할 경우 heap의 조건을 만족시키는 새로운 heap tree를 만드는 것은 까다롭다.
    이 경우 제거된 root node 자리에 맨 마지막 노드를 보내서 우선 모양 규칙을 만족시키고 대소규칙을 따르도록 자식노드들과
    자리를 바꾸어가는 재귀호출을 사용한다.
    
-heap sort
    배열을 정렬할때 자료를 heap으로 만들고 root부터 pop하면 정렬된 순서대로 출력되기 때문에 heap sort가 된다.
    pop되면 heap의 배열에 한자리가 비는데 여기에 pop된 자료를 넣으면 메모리 낭비도 없으며 최악의 경우에도 O(NlogN)만 사용한다.
    
-구간 트리
    segment tree는 저장된 자료를 구간별로 전처리하여 구간에 대한 질의에 빠르게 대답할 수 있게 만든 자료구조이다.
    흔히 일차원 배열에서 특정 구간에 대한 질문을 빠르게 대답하는데 쓸 수 있다.
    대표적인 예시로 특정 배열이 주어질 때 배열의 부분 구간의 최소치를 구하는 문제가 있다.
    이런 문제는 배열을 binary tree에 넣고(각 절반의 범위) 각 노드마다 해당하는 구간의 최소치를 넣어둔다.
    그리고 특정 구간이 주어졌을 때 주어진 구간은 노드로 표현된 범위의 합집합으로 표현할 수 있게 되는데 포함되는 노드에 저장된
    최소치들을 비교하여 가장 작은 값을 출력하면 된다. 이를 구간 최소 트리(range minimum query RMQ)라고 한다.
    꽉 찬 이진트리는 heap처럼 배열에 저장하여 메모리를 절약할 수 있다.
    구간트리는 약간의 값이 바뀔 때는 처음부터 새로 만들지 않고도 업데이트가 가능하다.
    구간별로 최소값이 아니라 값의 출현 빈도 등 다른 질의일 경우 이를 풀 수 있도록 필요한 추가정보들도 반환할 수 있도록 해야한다.
    최소 공통 조상 문제(lowest common ancestor) 예를들면, 촌수 찾기 문제.
    최소 공통 노드는 두 노드가 주어질 때 두 노드를 모두 자손으로 가지는 노드 중 가장 아래 있는 노드이다.
    
    
-펜윅 트리
    segment tree 중 구간 합을 구하기 쉽도록 만든 트리로, binary indexed tree라고도 한다.
    개념이 조금 복잡하지만 구현은 상대적으로 간단하다.
    <- 다시보기 
    
-유니온 파인드 자료구조(집합을 트리로 표현)
    공통원소가 없는 disjoint set을 표현할 때 쓰는 자료구조.
    disjointed set은 한 원소가 여러 집합에 속할 수 없다.
    이런 set을 표현하기 위해 3가지 연산이 필요한데, 초기화, 합치기(union), 찾기(find)중 union과 find를 이용해 union-find 자료구조라고 부른다.
    union은 초기화된 상태에서 공통된 집합에 속한 원소를 집합으로 묶는 연산이며
    find연산은 묶인 집합들에 대해 원소가 주어졌을 때 해당 원소가 속한 집합을 반환한다.
    union-find 자료구조를 트리로 표현하기 위해 각 집합을 트리로 표현한다. 그리고 루트 노드는 자기 자신을 루트로 가지도록 구현한다.
    (부모에서 자식으로 갈 일은 없기 때문에 해당 포인터를 구현할 필요는 없다.)
    루트는 대표 노드라고 부르며, 그냥 임의의 원소를 루트로 둔다고 생각하자.
    특정 원소를 다른 집합으로 합칠 경우 특정 원소의 루트를 찾아 그 루트를 합치고자 하는 다른 트리의 루트에 자식으로 한다.
    skewed 문제를 막기 위해 두 트리를 합칠 때 단순하게 높이가 낮은 트리를 높이가 높은 트리의 자식으로 두도록 구현한다.(union by rank 최적화)
    특정 노드의 root를 찾는 연산이 중복되기 때문에 parent 변수를 만들고 root를 찾았을 때 이를 갱신한다(path compression 최적화)
    disjoint set으로 풀 수 있는 문제는 대부분 그래프나 다른 자료구조로도 풀 수 있으나
    구현이 매우 간단하며 동작 속도가 아주 빨라 다른 알고리즘에 섞어 쓸 수 있다.
    ex ) 그래프 연결설 확인 문제, 가장 큰 집합 추적하기 문제
    
-트라이(문자열을 표현하는 트리)
    문자열을 다루는 알고리즘은 정수나 실수같은 다른 자료형 다루는 것과 다르다.
    문자열변수의 비교는 최악의 경우 문자열의 길이에 비례하는 시간이 걸린다.
    그래서 정수나 실수에서 잘 동작하는 탐색 자료구조들도 문자열을 키로 사용할 시 너무 느릴 수 있다.
    이런 문제를 완화하기 위해 문자열 특화 자료 구조가 있으며 대표적으로 트라이(trie)가 있다.
    트라이는 문자열의 집합을 표현하는 트리 자료구조로 문자열 집합 내에서 원하는 원소를 찾는 탐색 작업을 O(M)만에 할 수 있다.
    트라이는 접두사들에 대응되는 노드들이 서로 연결된 트리이다.
    한 접두사 맨 뒤에 글자를 더해 다른 접두사를 얻을 수 있을 때, 두 노드는 부모 자식 관계로 연결된다.
    edge에 덧붙인 글자가 대응된다는 사실이 특이하다.
    트라이의 루트는 항상 길이가 0인 문자열에 대응된다. 노드의 깊이가 깊어질수록 대응되는 문자열의 길이는 1씩 늘어난다.
    완성된 글자는 종료 노드로, Be, Bet, tea가 있을 때 be는 bet의 부모이지만 종료노드이다. 따라서 항상 leaf노드가 종료 노드가 아님에 주의하자.
    트라이는 루트부터 시작해서 특정 노드까지 내려가는 경로에서 만나는 글자를 모두 모으면 해당 노드에 해당하는 접두사를 얻을 수 있다.
    따라서 각 노드에 대응되는 문자열을 저장할 필요가 없다. 
    트라이의 한 노드는 자손 노드들을 가리키는 포인터목록과 노드가 종료노드인지 아닌지를 표현하는 boolean 변수로 이루어진다.
    포인터는 동적배열로 구현하지 않고 입력에 등장할 수 있는 가능한 모든 글자들에 대응되는 고정길이 배열로 구현한다.(메모리 낭비는 있지만 다음 노드를 찾을 때 
    탐색이 필요하지 않다. 없다면 null)
    트라이는 간단하고 탐색속도가 다른 어떤 자료구조보다 빠르다(검색엔진, 문자열 처리 프로그램에서 유용)
    트라이의 문제점은 필요로 하는 공간이 너무 크다는 것이다. 이를 최적화하는 방법들도 있지만 복잡하고 작성하는데 오래 걸려 대회등에서는 문자열의 개수가 적을 경우에만 사용한다.
    
    트라이는 집합에 포함된 문자열을 찾을 때 유용하지만, 트라이를 이용해 다중 문자열 검색도 수행할 수 있다. 접두사가 같은 노드에 대응된다는 점을 이용하여 탐색공간을 줄일 수 있다.
    KMP알고리즘(실패함수를 사용하는 방법)과 트라이를 이용하여 실패함수 f(s)를 s의 접미사이면서 트라이에 포함된 가장 긴 문자열까지가는 포인터 로 재정의할 수 있다.
    이 알고리즘을 아호-코라식 문자열 검색 알고리즘이라고 한다.
    아호 코라식 알고리즘을 위해 각 노드마다 추가적인 정보 두가지를 포함해야한다.
    1) failure link : 이 노드에서 다음 글자 대응이 실패했을 때 그 다음으로 가서 검색을 재개해야 할 노드의 포인터
    2) 출력 문자열 목록 
    <- 다시보기
    
그래프
    그래프는 객체들의 상호관계를 표현하기 위해 고안된 자료구조로, 계층구조에 특화된 트리에 비해 더 다양한 문제들을 표현할 수 있다.
    
그래프 기초
    선형자료구조 - > 계층구조를 위한 트리 -> 상호관계를 위한 그래프
    그래프는 정점과 간선으로 구성된다. 
    기본 구조는 간단하지만 정점이나 간선에 추가적인 속성을 부여하거나, 형태의 제약을 두기도 한다.
    대표적으로 directed graph가 있으며 방향이라는 속성을 추가하여 특정 간선이 한쪽 방향으로만 동작하게 한 것이다.
    weighted graph는 각 간선에 가중치가 주어지는 그래프이다.
    multigraph는 두 정점 사이에 두 개 이상의 간선이 있을 수 있는 그래프를 말한다.<-> simple graph
    bipartite graph는 각 정점들이 겹치지 않는 두개의 그룹으로 나뉘고, 각 그룹 간에만 간선이 존재할 수 있는 그래프이다.
    DAG(directed acyclic graph) 자기자신으로 돌아오는 사이클이 없는 방향성 그래프.
    
그래프의 경로
    path. 경로란 끝과 끝에 해당하는 정점들이 주어질 때 서로 연결된 간선들을 순서대로 나열한 것이다. 
    simple path: 경로 중 한 정점을 최대 한번씩만 지나는 경로. 그냥 path라고 해도 보통 simple path를 의미하는 경우가 많다.
    cycle : 경로 중 시작한 정점으로 끝나는 경로를 cycle이라고 한다.
    
implicit graph 
    그래프 형태가 아니더라도 그래프를 통해 표현하면 쉽게 표현할 수 있는 구조.
    ex 할일 목록. 
        의존관계에 있는 객체들을 한번에 하나씩 어떤 순서대로 해나갈지 결정하는 문제 : 위상정렬로 푼다.
    15-퍼즐. 
        4x4 칸 위에서 타일들을 움직여 원래 순서대로 정렬하는 퍼즐. 4x4 상태 하나를 정점으로, 
        하나의 위치를 변경하는 것을 간선으로 하여 정답과 현재 상태 사이의 최단경로를 구하는 문제로 치환.
    게임판 덮기. 
        NxN 게임판 위에 1x2 사이즈의 블록으로 모두 덮는 문제. 이분 그래프로 풀 수 있다.
    회의실 배정. 
        N개의 팀이 회의를 하려 하는데 회의실이 하나 뿐일 경우, 한번에 한팀만 사용할 수 있다. 각 팀이 회의실을 사용하고자 하는 시간을 2개씩 적어 냈다. 
        각 팀의 시간 중 한개씩을 선택하여 모든 팀이 회의할 수 있도록 할 수 있을까? 만족성 문제(satisfiability problem. SAT). 
        두 선택지를 내기 때문에 2-SAT라고 한다. 이를 그래프의 강 결합성 문제로 풀 수 있다.
    
그래프의 표현
    트리처럼 표현할 수 있지만, 그래프는 보통 정적인 용도로 사용된다.
    정적이라는 것은 새로운 정점이나 간선을 추가하거나 삭제하는 경우가 자주 일어나지 않는다는 뜻이다.
    이미 주어진 그래프 안에서 경로에 대한 연산을 하는 경우가 훨씬 많다.
    따라서 대부분 그래프는 구조를 변경하기 좀 어렵더라도 간단하고 메모리를 적게 차지하는 방법으로 표현한다.
    이 방법은 각 정점에 0~N의 번호를 메기고, 배열에 각 정점의 정보를 저장하는 것이다.
    각 간선은 반대쪽 끝 정점 객체의 포인터를 저장하는 대신 반대쪽 정점의 번호(배열 index)를 저장하는 식으로 구현한다.
    이런 표현 방식은 간선의 정보를 어떤 식으로 저장하느냐에 따라 두가지로 나뉜다.
    메모리나 시간 사용 특성이 많이 달라 프로그램 성능에 큰 영향을 끼치니 주의깊게 선택해야 한다.
        1)인접리스트의 표현
    adjacency list는 그래프의 각 정점마다 해당 정점에서 나가는 간선의 목록들을 저장하여 그래프를 표현한다.
    각 정점마다 하나의 연결리스트를 가지는 방식으로 구현된다.(이 리스트에 실제로 추가 삭제를 할 일은 많이 없으니 벡터 리스트 대신 동적배열을 사용해도 된다.)
    adjacency list는 해당하는 정점과 연결되어있는 정점들의 번호를 저장하고 있다. 
    추가적인 정보(weight라던지..)도 함께 저장해야한다면 구조체나 dictionary등으로 저장할 수 있다.
        2)인접 행렬의 표현
    인접리스트 표현의 단점은 두 정점이 주어질 때 두 정점이 연결되어있는지 여부를 확인하려 할 때, 연결리스트를 일일이 뒤져야한다는 것이다.
    이 연산의 속도를 줄이기위해 고안된 그래프 표현 방식이 adjacency matrix라고 한다. 
    이름에서 유추할 수 있듯, adjacency matrix는 VxV 크기의 행렬을 이용하여 그래프의 간선정보를 저장한다.
    가장 간단한 형태는 불리언 배열이지만 weight등이 있다면 weight값을 이용하여 저장하거나 할 수 있다. 간선이 없는 경우 0,-1, 아주 크거나 작은 값등을 사용할 수 있다.
        두 표현의 비교
    두 표현 방식은 서로 장단점이 반대이다. 따라서 알고리즘의 종류나 그래프의 종류에 따라 적절히 선택해야 한다.
    인접행렬의 장점은 두 정점이 주어졌을 때, 그 사이에 간선이 있는지를 한번의 배열 접근만으로 확인할 수 있다는 것이다.
    인접행렬의 단점은 실제 간선의 개수와 관계없이 항상 $V^{2}$크기의 공간을 사용한다는 문제점이 있다.
    인접 리스트의 장점은 V+E의 공간만을 사용한다는 것이며, 간선의 수가 적은 sparse graph를 다루면서 메모리가 한정적일 경우 유용하다.
    인접 리스트의 단점은 두 정점이 연결되어있는지 여부를 확인할 때 연결리스트를 순회해야한다는 것이다.
    
암시적 그래프의 표현
    그래프개념을 이용해 푸는 문제라고 해도 항상 그래프를 직접 메모리에 표현할 필요는 없다.
    입력이 그래프의 형태를 띄지 않는다면 그래프 구조로 표현하지 않고도 알고리즘들을 적용할 수 있다.
    미로에서 최단경로 찾기 문제의 경우가 대표적인데, 모든 열린 칸을 정점으로, 인접된 칸들을 서로 간선연결한 후 너비 우선 탐색을 통해 쉽게 풀 수 있으나,
    입력을 일일이 그래프로 표현하는 것이 번거롭다.
    이 경우 그냥 빈 칸의 위치 좌표로 표현하고 간선을 탐색하는 대신 좌표의 상하좌우를 탐색할 경우 그래프로 표현하지 않아도 너비 우선 탐색을 이용할 수 있다.
    암시적 그래프 표현이 유용한 또 다른 예는 그래프의 크기는 아주 큰데 실제로는 그 중의 일부만 사용하는 경우이다.
    예를 들어 15-퍼즐의 경우, 가능한 상태의 경우의 수는 16!로 약 20조개인데, 현재 상태와 정답 상태의 사이를 연결하는 최단경로는 이 중 극히 일부만 방문하기 마련이다.
    따라서 암시적 그래프 표현으로 그래프 전체를 메모리에 올리지 않고도 문제를 풀 수 있다.
    암시적 그래프의 표현의 단점은 그래프를 사용하는 알고리즘과 변환 과정이 결합되어 코드가 더 복잡해지기마련이다. 
    따라서 그래프에 대해 복잡한 연산이나 알고리즘을 적용할 계획이라면 조금 번거롭더라도 입력을 미리 그래프 표현으로 바꿔두는 것이 코드를 간결하게 만들어준다.
    
        
그래프의 탐색
    트리의 순회와 같이 그패으의 모든 정점을 특정한 순서에 따라 방문하는 알고리즘들을 그래프 탐색(search)라고 한다.
    트리의 순회는 트리에 있는 모든 정점들을 확인할 때가 아니라면 큰 의미가 없었으나 그래프는 트리보다 구조가 훨씬 복잡하여 탐색과정에서 얻을 수 있는 정보들이 아주 중요하다.
    탐색은 흔히 그래프 전체의 구조를 파악하기 위해 사용된다.
    탐색 과정에서 어떤 간선들을 사용하였는지, 또 어떤 순서대로 정점들이 방문되어있는지를 통해 그래프의 구조를 알 수 있다.
    탐색 알고리즘 중 가장 널리 사용되는 두가지는 깊이 우선 탐색(Depth first search)와 너비 우선 탐색(Breadth first search)이 있다.
     
깊이 우선 탐색 DFS
    DFS는 그래프의 모든 정점을 발견하는 가장 단순하고 고정적인 방법이다. 현재 정점과 인접한 간선들을 하나씩 검색하다가 아직 방문하지 않은 정점으로 향하는 간선을 찾으면 무조건 그 간선을 따라간다.
    이 과정에서 더이상 갈 곳이 없는 정점에 도달하면 마지막에 따라왔던 간선을 따라 뒤로 돌아오는 방법으로 동작한다.
    뒤로 돌아오는 것은 재귀함수를 이용하면 쉽게 구현할 수 있다. 재귀함수는 호출이 끝나면 원래 진행되던 순서로 돌아가기 때문이다.
    DFS는 연결된 모든 정점을 방문하지만 그래프가 연결되지 않고 두개 이상으로 분리되어 표현된 경우에는 모든 정점을 방문할 수 없다. 따라서 모든 정점을 순회하면서 방문되지 않은 경우 dfs를 수행하는 함수를 추가해준다.
    dfs의 시간복잡도는 인접 리스트를 썼을 경우 O(V+E), 인접 행렬을 썼을 경우 O($V^{2}$)이다.
    깊이 우선 탐색을 이용하면 두 정점 사이를 잇는 경로가 있는지 쉽게 확인할 수 있다. 어떤 정점 u에 대해 dfs(u)를 호출하고 visited[]변수를 만들어 u로부터 각 정점에 갈 수 있는지를 쉽게 찾을 수 있다.
    분리된 그래프의 경우, 전체 그래프에서 서로 연결되지 않고 자기들끼리 연결되어있는 서브 그래프를 컴포넌트라고 하는데, 그래프 내에서 컴포넌트가 몇개 있는지 파악하는 것이 기초적인 그래프 문제 중 하나이다.
    이 경우도 dfs를 이용하여 풀 수 있며, dfsall 함수가 dfs를 몇번 호출했는지를 세면 쉽게 확인할 수 있다.

위상 정렬
    위상정렬 문제는 dfs로 풀 수 있는 유명한 문제 중 하나로, 의존성이 있는 작업들이 주어질 때 이를 어떤 순서로 수행해야하는지 계산하는 문제이다.
    대표적으로 레시피 문제가 있는데, 레시피중 일부 작업은 사전에 다른 작업을 수행해두어야만 수행될 수 있다.(돼지고기 굽기 작업A는 돼지고기 자르기B 이후에 올 수 있다. 이 경우 작업 A가 작업 B에 의존한다고 한다.)
    각 작업을 정점으로, 의존성을 방향성 간선으로 표현한 방향성 그래프를 의존성 그래프라고 한다.
    의존성 그래프의 가장 큰 특징은 사이클이 없다는 것으로, DAG가 된다. 
    의존성 그래프의 모든 정점을 일렬로 늘어놓고 왼쪽부터 하나씩 수행한다고 가정할 때, 모든 의존성이 정상적으로 만족되려면 모든 간선이 왼쪽에서 오른쪽으로 향해야만 한다.
    이렇게 DAG 정점들을 배열하는 문제를 위상정렬 문제라고 한다.
    위상정렬을 가장 간단하게 구현하는 방법은 들어오는 간선들이 하나도 없는 작업들을 하나씩 찾아서 정렬 결과의 뒤에 붙이고, 그래프에서 이 정점을 지우는 것을 반복하는 것이다.
    하지만 dfs를 이용하면 이를 더 간단하게 풀 수 있다. 의존성 그래프에 dfsall()을 수행하고 dfs가 종료할때마다 현재 정점의 번호를 기록하는것이다.
    dfsall()이 종료한 후 기록된 순서를 뒤집으면 위상정렬 결과를 얻을 수 있다.
    
오일러 경로
    그래프의 모든 간선을 정확히 한번씩 지나서 시작점으로 돌아오는 경로 찾기(오일러 서킷!)
    그래프 이론에서 첫번째로 연구된 문제로 유명. 한붓 그리기 문제.
    유향, 무향 그래프에서 모두 풀 수 있으나 무향 그래프를 가정한다.
    오일러 서킷이 있는지 확인하기 위해 우선 간선들이 두개 이상의 컴포넌트에 분배되어있는지 확인한다.(간선없는 정점으로 이루어진 컴포넌트가 존재하는 경우에는 오일러 서킷은 있을 수 있다.)
    한 그래프에서 가장 많은 간선을 지나는 경로를 알고 있다고 가정하고 경로의 시작점이 u, 끝점이 v라고 할 때 v에 인접한 모든 간선은 이미 지나간 이후여야 한다.(그렇지 않다면 그 간선을 통해 경로가 연장될것)
    u와 v가 다를 경우와 같은 경우로 나누어서 생각해보자.
    1)u!=v인 경우
        항상 v는 홀수개의 간선과 인접해 있어야 한다. v를 지나가기 위해 v로 들어가는 데 하나, 나가는데 하나의 간선이 필요하고 v로 들어가서 나올수 없다는 말은 간선의 수가 홀수라는 뜻
    2)u=v인 경우
        v에 인접한 간선의 개수는 항상 짝수이다. u에서 나가는 것으로 시작하였으니 들어온 후 나갈 수 없다면 사용한 간선의 수는 항상 짝수여야 한다.
    즉, 각 정점에 인접한 간선의 수가 오일러 서킷의 존재 가능성과 밀접한 연관이 있음을 알 수 있다. 
    한 정점에 인접한 간선의 수를 degree라고 부른다. degree가 짝수인 정점을 짝수점, 홀수인 정점을 홀수점이라고 하자.
    오일러 서킷의 존재 가능성에 직접적으로 영향을 미치는 점은 홀수점이다. 오일러 서킷을 위해서는 모든 정점에 들어가는 횟수와 나오는 횟수가 같아야 하는데 홀수점은 이게 불가능하기 때문이다.
    따라서 그래프의 모든 정점이 짝수점이어야만 오일러 서킷이 존재할 수 있다.
    홀수점이 하나라도 있다면 오일러 서킷은 존재할 수 없는데, 반대로 만약 모든 정점이 짝수점이라면 오일러서킷은 항상 존재할까?
    모든 정점이 짝수점이면서 간선들이 하나의 컴포넌트에 포함된 그래프가 주어질 경우 항상 오일러 서킷을 찾아낼 수 있다.
        오일러 서킷 찾기 알고리즘
        모든 정점이 짝수점이고 모든 간선이 하나의 컴포넌트에 속한 그래프가 주어진다고 가정해보자.
        u에서 시작하여 인접한 간선을 찾고, 더이상 따라갈 간선이 없을 때 중지한다. 그래프의 모든 정점은 짝수개의 간선을 가지기 때문에 항상 시작점에서 끝나게 된다.
        이렇게 찾은 circuit을 저장하고 아직 방문하지 않은 간선이 있으면 거기서부터 circuit을 마저 찾는다. 모든 간선을 지났으면 찾은 circuit들을 모두 합친다.
        재귀호출을 이용하면 이를 dfs로 풀 수 있다.
        
        오일러 트레일 Eulerian trail
        오일러 서킷처럼 모든 간선을 정확히 한번씩 지나지만 시작점과 끝점이 다른 경로를 오일러 트레일이라고 부른다.(한 점을 두 번 이상 지날 수 있기 때문에 path가 아니라 trail이다.)
        a와 b 사이의 오일러 트레일을 찾고 싶다면, a와 b사이를 연결하는 임의의 간선 (b,a)를 임의로 추가한 후 오일러 서킷을 찾는다. 그리고 (b,a)를 끊으면 원하는 오일러 트레일을 얻을 수 있다.
        따라서 오일러 트레일의 존재 조건은 오일러 서킷과 크게 다르지 않다. a,b는 홀수점이고, 나머지 모든 정점이 짝수점이며 모든 간선이 하나의 컴포넌트에 속하면 된다.
        
        해밀토니안 경로(Hamiltonian path)
        그래프의 모든 정점을 정확히 한번 지나는 경로. 큰 그래프에 대해 해밀토니안 경로를 빠르게 찾는 방법은 아직 없다.
        이 문제를 찾을 수 있는 유일한 방법은 조합 탐색으로 모든 정점의 배열을 하나 하나 시도하며 이들이 경로가 되는지 모두 확인하는 것이다.
        최악의 경우 n!의 경우의 수를 시도해봐야 하기에 한계가 있다.
        문제를 오일러 서킷,혹은 트레일로 바꾸어 풀면 풀 수 있는 경우가 있다.
        
        방향 그래프의 오일러 서킷
        방향 그래프에서 오일러 서킷을 찾는 알고리즘은 무향 그래프와 크게 다르지 않으나 오일러서킷의 존재 조건은 다르다.
        방향 그래프의 오일러 서킷 존재 조건은 각 정점에 들어오는 간선의 수와 나가는 간선의 수가 같아야만 한다.
        오일러 트레일의 존재 조건은 시작점에서는 나가는 간선이 들어오는 간선보다 한개 많고,
        종점에서는 들어오는 간선이 나가는 간선보다 하나 많으며 나머지 모든 정점에서 나가는 간선과 들어오는 간선의 수가 같으면 된다.
        
        오일러 서킷? 트레일? 
        어떤 문제는 주어진 입력에 따라 서킷이나 트레일 둘 중 하나를 찾으면 된다. 이 경우 각 정점의 degree를 확인하여 서킷을 조건을 만족하는지,
        트레일의 조건을 만족하는지 확인한 후 문제를 푼다.

DFS 스패닝 트리
    DFS를 수행해나가면서 탐색할 때 따라가는 간선들을 모으면 트리 형태를 띄게 된다. 이런 트리를 DFS 스패닝 트리 라고 부른다.
    DFS 스패닝 트리를 만들면 그래프 내의 모든 간선을 다음과 같이 4가지로 분류할 수 있다.
        1) Tree edge
        dfs 스패닝 트리에 포함된 간선.
        2) forward edge
        스패닝 트리의 선조에서 자손으로 연결되나 dfs 탐색 과정에서 탐색하지 않아 스패팅 트리를 구성하는 간선에 포함되지 않은 간선
        3) back edge
        스패닝 트리의 자손에서 선조로 연결되나 dfs 탐색과정에서..이하생략
        4) cross edge
        1,2,3 분류에 해당하지 않는 다른 모든 간선. 선조-자손 관계가 아닌 정점들 사이에 존재하는 간선들
    (dfs를 어떻게 수행하느냐에 따라 다른 간선들이 선택될 수 있음)
    무향 그래프일 경우 : cross edge가 없음. forward edge와 back edge의 구분이 없음.
    이러한 간선의 분류는 그 자체로 중요하다기보다는 유용한 도구로 쓰인다. 
    ex) 방향 그래프의 dfs 스패닝 트리에서 back edge가 존재할 경우 해당 방향 그래프에서 사이클이 존재한다.
    
절단점 찾기 알고리즘
    어떤 무향 그래프에서 절단점이랑 이 점과 점에 인접한 간선들을 모두 지웠을 때 해당 정점이 포함되어있던 컴포넌트가 두개 이상으로 분리되는 정점을 말한다.
    절단점은 현실에서 중요한 의미를 갖는다(철도망에서 절단점인 특정 역을 폐쇄하였을 때 전체 철도망이 마비될것)
    완전 탐색을 하면 모든 정점을 지워보고 컴포넌트의 개수를 세봐야 하지만, dfs를 한번 수행하는 것으로도 절단점 찾기 알고리즘을 수행할 수 있다.
    무향 그래프에서는 cross edge가 없음으로 어떤 정점 u와 연결된 모든 정점들은 자손 아니면 선조이다.
    u의 자손을 루트로 가지는 서브트리들을 순회하다가 u의 선조로 연결되는 간선을 찾을 경우 체크해두고, 모든 서브트리들이 u의 선조와 연결되지 않았다면
    u는 절단점이다. dfs 탐색 과정에서 u의 선조는 u보다 먼저 방문됨으로, 방문되는 순서를 이용하여 이를 확인할 수 있다.
    절단점찾기와 비슷한 다리 찾기 문제도 있다. 어떤 간선을 삭제했을 때 이 간선을 포함하던 컴포넌트가 두 개 이상으로 쪼개질 때 다리라고 부른다.
    절단점찾기와 비슷하게 풀 수 있다. 다리는 항상 tree edge이기 때문에 tree edge들에 대해서만 검사하면 된다.

강결합 컴포넌트 분리
    무향 그래프에서 절단점을 포함하지 않는 서브 그래프를 이중결합 컴포넌트라고 부른다.(임의의 한 정점을 그래프에서 지우더라도 정점간 연결관계가 유지됨)
    이중 결합 컴포너트의 개념과 유사하게 방향 그래프에서 존재하는 개념이 강결합 컴포넌트,SCC 이다.
    방향 그래프에서 두 정점 u,v에 대해 양방향으로 가는 경로가 모두 있을 경우 두 정점은 같은 scc에 속해있다고 말한다.
    방향그래프에서 각 scc사이를 연결하는 간선들을 모으면 scc들을 일종의 정점으로 하는 DAG를 구성할 수 있다.
    그래프의 정점들을 scc별로 묶어 이를 정점으로 하는 새로운 그래프를 만드는 과정을 그래프 압축이라고 한다.
    주어진 그래프를 scc로 분할하는 간단한 방법은 모든 정점에서 한 번씩 dfs를 수행하는 것이다.
    타잔의 알고리즘은 한번의 dfs로 장 정점을 scc별로 분리할 수 있으며 dfs를 이용해 풀 수 있는 그래프 문제의 좋은 예시이다.
    
dominating set 찾기
    강 정점이 자기 자신과 모든 인접한 정점들을 지배한다고 할 때, 그래프의 모든 정점을 지배하는 정점의 부분집합을 그래프의 dominating set이라고 한다.
    이는 NP문제이지만 그래프에 사이클이 존재하지 않는 경우, 노드 간 상하관계가 없을 뿐 트리와 유사한 구조를 가지게 된다.
    이런 그래프들을 루트없는 트리라고 부르며 그래프에서는 어려운 문제가 트리에서는 쉽게 풀리는 경우가 많아 그래프를 트리로 볼 수 있는지 판정하는 것이 중요하다.
    V-1개의 간선이 있고, 사이클이 없으며 두 정점 사이를 연결하는 단순경로가 정확히 하나라면 루트없는 트리라고 할 수 있다.
    루트없는 트리구조임이 확실하다면, 이에 대해 dfs를 수행하면 결과적으로 얻은 dfs 스패닝 트리는 원래 그래프의 구조를 그대로 가진 트리라고 볼 수 있다.
    이 트리의 잎 노드들부터 시작하여 루트로 올라가며 지배여부를 체크하면 dominating set을 얻을 수 있다.
   
SAT 문제
    false/true 의 결정을 여러번 해야하는 문제를 boolean satisfiability problem, SAT문제라 부른다.
    SAT문제는 boolean 변수 형태로 구성된 식이 주어질 때 이 식을 참으로 하는 해(true/false 조합)가 있는지 찾는 것이다. 
    SAT문제는 아주 강력하고 일반적인 문제로, 아주 많은 문제들을 SAT문제로 바꿔서 풀 수 있다. 하지만 SAT문제를 빠르게 푸는 방법이 아직 없다.
    하지만 2-SAT문제(논리곱 정규형으로 표현했을 때 각 절에 최대 2개의 변수만이 존재하는 경우)는 다항시간안에 풀 수 있다.
    논리식에 포함된 변수들의 값에 대한 요구조건을 표현한 그래프를 implication graph라고 한다.
    <--다시보기
    
너비 우선 탐색 BFS
    너비 우선 탐색은 시작점에서 가까운 정점부터 순서대로 방문하는 직관적인 탐색 알고리즘이다.
    가까운 것의 기준은 시작점부터 해당 정점까지 도달하는데 걸리는 최단 경로이다.
    너비 우선 탐색은 우선 인접 정점들을 모두 기록한 후 별도의 위치에 저장한다. 그리고 인접한 정점을 모두 검사하면 저장된 목록에서 다음 정점을 꺼내 방문한다.
    따라서 너비 우선 탐색의 방문 순서는 저장된 정점 목록에서 어떤 정점을 먼저 꺼내는지에 의해 결정된다. 가장 흔하게 큐가 사용된다.
    dfs에서 그랬던것처럼 bfs에서도 bfs 스패닝 트리를 만들 수 있다.
    dfs는 그래프의 구조와 관련된 다양한 문제를 푸는데 사용될 수 있었지만, bfs는 대개 단 하나의 용도로 사용된다.
    그것은 그래프에서의 최단 경로 문제를 푸는 것이다.
    최단 경로 문제란 두 정점을 연결하는 경로 중 가장 길이가 짧은 경로를 찾는 문제로 그래프 이론의 고전적인 문제 중 하나이다.
    가중치가 없는 간단한 그래프를 다루고 있음으로 경로의 길이를 경로에 포함된 간선의 개수라고 정의한다.
    bfs 스패닝 트리에서 각 정점에서 루트인 시작점으로 가는 경로가 실제 그래프상에서 최단경로임을 확인할 수 있다.
    bfs에서 인접한 간선들을 저장할 때 간선들이 가진 값이 있을 경우 이 값을 고려하는것으로 몇몇 문제들을 풀 수있다.
    
최단 경로 전략
    bfs는 유용한 방법이지만 문제에 따라 다른 탐색 알고리즘들이 더 강력한 경우도 있다.
        양방향 탐색 
        15퍼즐을 푼다고 생각해보자. 상태의 저장은 연관배열에 넣게된다. 한 상태는 4개의 다른 상태와 연결되며, 다음 상태에서 자기 자신으로 돌아오는 경우를 제외한다고 해도
        2~3배로 경우의 수가 늘어난다. 만약 현재 상태와 정답 상태 사이의 거리가 짧다면 큰 문제가 안되겠지만 최악의 경우라면 너무 많은 공간을 탐색하게 된다.
        이 경우 현재 상태에서 정답 상태로 bfs를 수행하면서 반대로 정답 상태에서 현재 상태로 bfs를 수행하는 것으로 탐색공간을 크게 줄일 수 있다.
        이를 양방향 탐색이라고 하며 탐색 중 가운데에서 만나면 종료한다.
        같은 큐를 이용하되 역방향 탐색은 -값으로 저장하면 탐색 중 인접상태를 검사했을 때 현재 부호와 다른 값이 있다면 가운데에서 만났음을 확인할 수 있다.
        0은 사용할 수 없기에 처음 시작 거리가 0이 아니라 1,-1이며, 따라서 수행 결과에서 1을 빼주어야한다.
        Iteratively Deppening Search IDS
        너무 규모가 큰 탐색 문제를 풀 때는 깊이 우선 탐색을 기반으로 한 방법을 사용해야 하낟.
        dfs는 큐가 너무 많은 메모리를 차지하지 않는다. 하지만 dfs는 지금까지 찾은 경로가 최단 경로인지 확신할 수 없으며, 각 정점을 방문했는지 확인하지 않는다.
        따라서 같은 상태를 두번 방문하거나 사이클에 빠지는 문제가 생길 수 있다.
        IDS는 이런 문재를 해결하기 위해 고안되었다. IDS는 특정 깊이를 제한한 l을 결정한 후 이 제한보다 짧은 경로가 존재하는지 dfs로 확인한다.
        답을 찾으면 성공이고, 찾지 못하면 l을 늘려서 다시 시도한다. 
        이 과정에서 찾은 현 시점의 최단경로를 전역변수로 저장해두면 이후 탐색과정에서도 탐색을 조기종료(저장된 값보다 커질 시 )할 수 있어 유용하다.(pruning)
        예전에 봤던 조합 탐색과 관련이 있다. 따라서 조합탐색의 기법들을 IDS에서도 사용할 수 있다.

적절한 탐색 방법 선택하기 
    1) 상태공간에서 최단 경로를 찾는 경우, bfs를 우선적으로 고려한다. 깊이 한계가 정해져있지 않거나, 메모리 사용량의 제한을 고려해본다.
    2) 탐색의 최대 깊이가 정해져있고 너비 우선 탐색을 하기에 메모리와 시간이 부족하면 양방향 탐색을 고려한다. 역방향 탐색이 쉬워야 한다.
    3) 두 방법 모두 메모리를 너무 많이 쓰거나 느린 경우, IDS를 사용한다.
    
상태 객체의 구현
    탐색알고리즘과는 상관 없으나, 상태를 표현하는 자료구조의 선택은 알고리즘의 효율성에 큰 영향을 미친다.
    상태객체를 구현할 때는 상태에 대한 여러 연산을 효율적으로 구현해야한다.
    두 상태가 같은지를 확인하거나 현재 상태에 인접한 상태들을 모두 계산하는 연산 등은 탐색과정에서 반복적으로 수행되므로 이들을 가능한 한 효율적으로 구현해야한다.
    두번째로 유의할 점은 가능한 한 적은 메모리를 사용해야 한다는 것이다.
                
가중치가 있는 그래프의 정점 사이 최단경로 문제
    가중치가 없는 그래프의 최단경로 문제(두 정점 사이를 연결하는 path에 속한 간선의 갯수가 최소인 path를 찾는것)는 bfs로 풀 수 있었다.
    이제는 가중치가 있는 그래프에서의 최단경로 문제를 다뤄본다.
    이 알고리즘들은 실제 최단 경로를 구성하는 정점의 목록을 구해주지 않으며, 최단경로의 길이를 찾아 줄 뿐이다.
    실제 경로를 계산하려면 추가적으로 탐색과적에서 별도의 정보를 저장하고 이를 이용해 실제 경로를 찾아내는 코드를 작성해야 한다.
    최단경로 문제는 다양한 그래프의 종류와 특성에 따라 최적화된 많은 최단경로 알고리즘이 존재한다. 이 중에서도 대표적인 알고리즘들에 대해 다룬다.
        음수 간선
        최단 경로 문제에서 가장 먼저 유의해야 할 점은 그래프에 음수 가중치를 가지는 간선이 있는지 확인하는것이다.
        음수간선을 지나면 전체 경로의 길이가 짧아진다. 이는 그래프를 다른 형태의 그래프로 바꿔서 푸는 과정에서 자주 등장한다.
        음수간선이 있는 경우 가중치 합이 음수인 음수 사이클이 존재할 가능성이 있다. 음수 사이클이 존재할 경우 경로가 음의 무한대로 발산할 수 있어 최단경로가 정의되지 않는다.
        
        단일 시작점 알고리즘
        단일 시작점 알고리즘들은하나의 시작점에서 다른 모든 정점까지 가는 최단 거리를 구해준다.
        
        모든 쌍 알고리즘
        모든 정점의 쌍에 대하여 최단거리를 계산한다. ex)플로이드 최단경로 알고리즘
        
        방향 그래프와 무방향 그래프
        방향 그래프에 대해 동작하는 것을 가정한다. 따라서 무방향 그래프일 경우 양방향 간선 하나를 각 방향의 간선 2개로 쪼개어 방향그래프로 만든다. 
        하지만 음수간선에 대해서는 이렇게 문제를 바꾸면 음수사이클이 발생하기 때문에 음수간선이 있는 무방향 그래프에 대한 최단경로 문제는 제대로 풀수 없다.
        
다익스트라 최단 경로 알고리즘
    다익스트라 알고리즘은 아주 유명한 단일 시작점 최단경로 찾기 알고리즘이다. bfs와 크게 다르지 않다.
    weight가 있는 그래프에서 bfs처럼 거리가 가까운 순으로 탐색하기 위해 시작점으로부터의 거리와 정점의 set을 우선순위 큐에 저장하여 거리 순서대로 pop되도록 한다.
    경로를 찾는 도중 특정 정점까지의 최단 경로가 갱신될 수 있다. 이 경우 그냥 우선순위 큐에 새로운 거리와 정점의 set을 우선순위 큐에 넣고 나중에 기존의 set이 pop되면
    이를 무시한다. 이를 위해 별도의 dist 리스트를 가지고 특정 정점까지의 현재시점까지의 최단거리를 저장해두는 방법을 쓴다.
    다익스트라 방법은 최단경로의 길이만 반환하며, 실제 경로를 찾기 위해서는 스패닝 트리를 만들어두고 종점부터 시작점까지 거슬러 올라가며 경로를 찾는 알고리즘을 추가한다.
    다익스트라 알고리즘은 음수간선이 포함된 그래프에서 최단경로를 찾을 수 없다.
    <-철인 n종 다시보기

벨만-포드 최단 경로 알고리즘 
    다익스트라 알고리즘은 음수간선이 있는 그래프의 경우 그 정당성이 보장되지 않는다.
    벨만 포드 최단경로 알고리즘은 음수 간선이 있는 그래프에서도 최단 경로를 찾을 수 있으며 음수 사이클의 존재로 최단거리를 정의할 수 없을 경우 이것도 알려준다.
    벨만 포드 알고리즘은 시작점에서 각 정점까지 가는 최단 거리 상한을 적당히 예측한 후, 예측값과 실제 최단거리 사이의 오차를 반복적으로 줄여나가는 방식으로 동작한다.
    bfs를 기반으로 한번에 하나의 정점의 최단거리를 확장해나가는 다익스트라 방법과 아주 다르다.
    벨만 포드 알고리즘은 수행 과정에서 각 정점까지의 최단거리의 상한을 담은 uppper[] 배열을 유지하며, 이 값은 알고리즘이 진행되면서 점점 줄어들고 알고리즘이 종료하면
    실제 최단거리를 담게 된다.
        벨만 포드의 동작 과정 
        알고리즘 초기에는 알고있는것이 없으며, 시작 정점 s 까지의 거리가 0이라는것만 안다.
        upper[s]를 0으로 하고 나머지는 아주 큰 수로 초기화한다.
        이를 최단 거리에 가깝게 초기화하기 위해  u부터 v까지의 최단거리 dist에 대해 다음 조건이 항상 참임을 이용한다.
        dist[v] <= dist[u] + w(u,v)  
        (w(u,v)는 u에서 v까지 가는데 걸리는 weight(거리를 의미))
        따라서 
        upper[u] + w(u,v) < upper[v] 일 때
        upper[v]의 길이는 최대 upper[u] + w(u,v)이며,
        따라서 upper[v] = upper[u] + w(u,v)로 갱신할 수 있다.
        이를 모든 간선에 대하여 전파하며 반복적으로 실행할 수 있으며, 이를 통해 실제 원하는 최단거리에 가까워진다.
        사이클이 없을 시 최단경로는 한 정점을 두번 반복하지 않음으로, 이 반복은 정점의 개수 V에 대해 가질수있는 간선의 최대치인 abs(V) -1 번 반복된다.
        이 방법은 다익스트라의 bfs기반 방법과 다르게 음수 간선이 존재할때도 최단거리를 찾을 수 있다.
        하지만 음수 사이클이 존재한다면 역시 최단경로를 찾을 수 없고 의미없는 값을 출력하는데, 벨만 포드 알고리즘은 변형을 통해 음수 사이클이 존재한다는 사실을 반환할 수 있다.
        이 변형은 abs(V)-1번이 아니라 abs(V)번 반복하는 것이다.
        벨만 포드는 abs(V)-1번에 최단경로를 찾을 수 있기 때문에 abs(V)번째 반복에서는 어떠한 갱신도 일어나지 않는것이 정상이다. 따라서 이 반복에서 upper갱신이 일어날 경우
        음수 사이클이 존재한다는 것을 알 수 있다.
        최단 거리 말고 실제 최단 경로를 얻기 위해서는 벨만 포드 알고리즘 중 특정 정점을 마지막으로 갱신시킨 간선들을 모아 스패닝트리를 만들고 각 정점에서부터 
        시작점까지 거슬러올라가는 경로를 찾아 반환한다.(다익스트라 방법과 비슷한 방법으로 찾음.)
        벨만 포드 방법은 처음 큰 값으로 upper를 초기화하기 때문에 특정 정점에 대한 upper값이 초기값일 경우 해당 정점으로 가는 경로가 존재하지 않는다는 것을 알 수도 있다.
        하지만 음수 간선이 있을 경우 해당하지 않으니 주의해야 한다.<--다시보기

플로이드의 모든 쌍 최단 거리 알고리즘
    <-코드와 함께 다시 보기.. 구현은 쉬운데 개념이 헷갈린다.
    다익스트라, 벨만 포드 알고리즘은 특정한 시작점에서 모든 정점에 대한 최단경로를 찾는 알고리즘이다.
    하지만 몇몇 경우에는 그래프 내의 임의의 두 점 사이의 최단 경로를 반복적으로 구해야하는 경우도 있다.
    이를 위한 가장 간단한 해결책은 모든 정점에 대해 정점을 시작점으로 하여 다익스트라나 벨만 포드 알고리즘을 돌려 저장해두는 것이다.
    하지만 이보다 더 간단한 방법이 있으며, 플로이드 알고리즘이라고 한다. 
    플로이드 알고리즘은 다익스트라나 벨만 포드 알고리즘과는 다른 방식으로 동작한다.
    플로이드 알고리즘은 그래프의 모든 정점 쌍의 최단거리를 저장하는 2차원 배열을 만들고 여기에 각 정점 쌍의 최단경로들을 저장한다.
        정점의 경유점
        두 정점 u,v를 잇는 경로가 있다고 했을 때, 이 경로는 다른 정점을 거칠 수 있다.
        양 끝점을 제외하고 경로가 지나는 정점들을 경유점이라고 한다.
        가능한 모든 정점 S 일때 어느 정점을 x라 하자.
        u부터 v까지 가는 최단 경로가 x를 지난다면 u부터 x까지의 최단 경로와 x부터 v까지의 최단 경로로 분해할 수 있다.(이 경우 x는 경유점에서 제외된다)
        x를 지나지 않는다면, u부터 v까지 가는 경로에서 x를 제외할 수 있다.            
        이를 점화식으로 만들 수 있고, 0~k부터 k까지의 정점들을 이용하여 점화식을 만들 수 있다
        <- 다시 보기
        점화식을 만들 경우 이를 동적 계획법을 이용하여 풀 수 있다. 
        두 정점 사이의 간선이 없는 경우 아주 큰 값을 넣어 경로가 존재하지 않는 경우를 따로 처리하지 않아도 된다.
        이 방법은 대량의 메모리를 사용하기 때문에 슬라이딩 윈도우 기법으로 메모리를 최적화 할 수 있다.
        
        
최소 스패닝 트리 문제
    어떤 무향 그래프의 스패닝 트리는 원래 그래프의 정점 전부와 간선의 부분집합으로 구성된 부분 그래프이다.
    스패닝 트리에 포함된 간선들은 정점들을 트리 형태로 전부 연결해야 한다.
    트리 형태 = 사이클을 이루지 않음.
    한 그래프의 스패닝 트리는 유일하지 않다.
    가중치 그래프의 스패닝 트리 중 가중치의 합이 가장 작은 트리를 찾는 문제를 최소 스패닝 트리 문제라고 한다.
        크루스칼 알고리즘
        가중치가 큰 간선과 작은 간선이 있다면 최소 스패닝 트리에 포함될 가능성이 높은 간선은 후자일것이다.
        크루스칼 알고리즘은 그래프의 모든 간선을 가중치의 오름차순으로 정렬한 후 스패닝 트리에 하나씩 추가해간다.
        사이클이 생기면 안되기 때문에 사이클이 생기는 간선은 고려에서 제외해야 한다.
        이 부분이 크루스칼 알고리즘에서 핵심적인 부분이다.
        단순하게 생각하면 각 간선을 추가할때마다 만들어둔 트리에 대해 dfs를 수행하여 알 수 있다. $O(E^{2})$가 걸림으로 더 빠른 방법이 필요하다.
        어떤 간선을 추가해 그래프에서 사이클이 생기려면 양 끝 점이 같은 컴포넌트에 속해있어야 한다.
        두 정점이 주어질 때 이들이 같은 컴포넌트에 속하는지, 그렇지 않다면 두 컴포넌트를 합치는 연산을 빠르게 지원하는 자료구조가 있다면
        이 부분을 쉽게 해결할 수 있다.
        이를 위해 상호 배타적 집합 자료구조를 사용한다. 
        한 집합이 그래프의 한 컴포넌트를 표현하도록 한다. 따라서 그래프에 새 간선을 추가해 사이클이 생기는지 확인하려면
        두 정점이 이미 같은 집합에 속해 있는지 확인하면 되고, 간선을 트리에 추가할 경우 이들이 포함된 두 집합을 합치면 된다.
        프림 알고리즘
        또 다른 스패닝 트리 알고리즘으로 프림 알고리즘이 있다.
        크루스칼 알고리즘은 간선을 중심으로 산발적으로 만들어직 작은 트리들을 연결해 스패닝트리를 만들지만
        프림 알고리즘은 하나의 시작점으로 구성된 트리에 간선을 하나씩 추가하며 스패닝 트리를 만든다.
        프림 알고리즘은 모든 간선이 아니라 현재 구성된 트리에 인접한 간선들을 대상으로 검사한다는 점을 제외하면 크루스칼 알고리즘과 같다.
        스패닝 트리의 특성상 프림알고리즘을 구현할 때 아직 속하지 않은 각 정점에 대해 트리와 이 정점을 연결하는 가장 짧은 간선에 대한 정보를 저장하고
        각 정점을 순회하며 다음에 추가할 정점을 찾을 수 있다. 이를 위해 트리와 정점을 연결하는 간선의 최소 가중치를 저장하는 배열을 유지한다.
        거의 모든 정점들 사이에 간선이 있는 밀집 그래프에서 프림 알고리즘이 크루스칼보다 더 빠르게 동작할 수 있다.
        다익스트라 알고리즘처럼 우선순위 큐를 이용하여 마지막 간선의 가중치를 우선순위로 하여 저장하면 O(ElogV)에 프림알고리즘을 구현할 수  있따.
        
    
간선의 용량을 고려한 그래프의 최대 유량 문제

    
    
    
    
     