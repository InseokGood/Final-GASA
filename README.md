## 유전알고리즘
* 생물학적 진화에 바탕을 둔 통계적 탐색 알고리즘 집합이다.
* 유전알고리즘은 자연선택과 유전학에서 영감을 얻은 선택, 교차, 돌연변이 연산을 사용한다.
#### 알고리즘 구조
1. 초기 염색체의 집합 생성

2. 초기 염색체들에 대한 적합도 계산

3. 현재 염색체들로부터 자손들을 생성

4. 생성된 자손들의 적합도 계산

5. 종료 조건 판별

6-1. 종료 조건이 거짓인 경우, (3.)으로 이동하여 반복

6-2. 종료 조건이 참인 경우, 알고리즘을 종료

#### 선택연산
* 선택 연산은 현재 세대의 후보해 중에서 우수한 후보해를 선택하는 연산이다.  현재 세대의 n개의 후보해가 있으면 , 이들 중 우수한 후보해는 중복되어 선택될수 있고 적합도가 낮은  후보해들은  선택되지 않을수도 있다. 이렇게 선택된 후보해의 수는 n개로 유지된다. 이러한 선택은 '적자 생존' 개념을 모방한것이다.

![image](https://user-images.githubusercontent.com/101339244/174268201-34c37860-c03e-46cd-ae11-26f6262b16f2.png)

#### 교차연산
* 교차 연산은 두해의 특징부분을 결합해 하나의 새로운 해를 만들어내는 연산
* 먼저 문제의 표현 방법이 결정 되어야한다.


![image](https://user-images.githubusercontent.com/101339244/174264462-d59488da-8d3c-4ec0-b25a-902b678af046.png)


#### 돌연변이 연산 
* 부모해의 없는 속성을 자식해에 도입하는 역할을 한다.
* 교차 연산이 수행된 후에 돌연변이 연산을 수행한다. 돌연변이 연산은 아주 작은 확률로 후보해의 일부분을 임의로 변형시키는 것이다. 


![image](https://user-images.githubusercontent.com/101339244/174264565-01983f07-a924-4951-95ec-60a6c359c42f.png)


### 유전알고리즘 설계 
* 유전 알고리즘을 설계할 때, 최적해의 정확한 값이나 패턴을 알지 못하기 때문에 목표 적합도를 추정해야한다.   이 과정에서 절대로 나올 수 없는 목표 적합도를 설정하게 되는 경우가 있는데, 이러한 경우에는 알고리즘이 끝나지 않는다. 그래서 매우 복잡한 문제를 풀어야 할 때는 목표 적합도뿐만 아니라, 최대 반복 횟수도 같이 설정해주는 것이 일반적이다.
##### TSP 적용
*   세일즈맨은 A 도시에서 출발하여 4개의 도시(B, C, D, E)를 방문해야하고, 현재 도시에서 다른 도시로 이동하는데 소모되는 비용은 아래의 표와 같다.


![image](https://user-images.githubusercontent.com/101339244/174276339-ace148a7-2e8c-4c7f-a70a-36a429344696.png)


* 표에서 비용은 이동거리, 톨게이트 비용 등 도시를 이동할 때 소모되는 자원을 추상화하여 모두 더한 값이라고 정의한다.  알고리즘을 설계할 때, 가장 먼저 정해야 하는 것은 한 세대 당 개체 수(염색체의 수)와 목표 적합도 또는 최대 반복 횟수이다.
* 도시의 수가 적고, 예시를 보이는 문제이기 때문에 한 세대 당 개체 수는 아주 작게 5로 설정하고, 목표 적합도는 1900으로 한다. 또한 하나의 염색체가 갖는 유전자의 수는 5개이며, 시작 도시는 A로 고정되었기 때문에 첫번째 유전자의 값은 항상 A이다.

1) 초기 세대 생성  일반적으로 초기 세대는 유전자의 값을 임의로 할당하면서 염색체를 생성한다. 즉, 초기 세대는 일정한 규칙 없이 임의로 생성된다. 임의로 생성된 초기 세대는 아래와 같다.

![image](https://user-images.githubusercontent.com/101339244/174276616-18441383-4644-47ff-a59e-a4422ba398e3.png)

2) 초기 세대 적합도 평가
* 이 예제에서는 한 염색체가 나타내는 순서대로 도시를 방문했을 경우 소모되는 비용의 합을 S라고 했을 때, 해당 염색체의 적합도는 3000 - S라고 정의한다. 이제 초기에 생성된 각각의 염색체에 대한 적합도를 계산하면 된다.   첫번째 염색체인 [A B D C E]의 적합도를 계산하면 위의 표에서 A에서 B로 이동할 때 소모되는 비용은 170이고, B에서 D로 이동할 때 소모되는 비용은 150이다. D에서 C로 이동할 때는 600, C에서 E로 이동할 때는 420이므로 [A B D C E]의 순서로 도시를 방문하는 경우에는 총 1340의 비용이 소모된다. 앞에서 정의한 적합도 함수를 통해 해당 염색체의 적합도를 계산하면 3000에서 1340을 뺀 값인 1660이 나온다. 다른 4개의 염색체에 대해서도 같은 과정으로 적합도를 계산하면 아래와 같다.

Fit([A B D C E]) = 1660  ,
Fit([A D E C B]) = 1520  ,
Fit([A D C E B]) = 1350  ,
Fit([A C D E B]) = 1520  ,
Fit([A E C B D]) = 1680  

3) 초기 세대 교배 및 돌연변이  
* 이 단계에서는 두 개의 염색체를 선택하여 교차연산을 통해 다음 세대의 유전체를 생성한다.교차연산은 3번째와 4번째 유전자 사이에서 두 염색체의 유전자를 교차하도록 정의한다.
* 예를 들어, [A B D C E]와 [A E C B D]가 선택되었다면 교차연산에 의해 생성된 염색체는 [A B D E C]이다. 
* 여기에서 첫번째 염색체의 1부터 3번째 유전자가 A B D이기 때문에 두번째 염색체의 4~5번째 유전자인 B D와 중복된다. 
* 이러한 경우에는 두번째 염색체의 유전자 순서를 유지하면서 중복되지 않은 값으로 4~5번째를 채워야 하기 때문에 [A B D C E]와 [A E C B D]가 교차되어 [A B D E C]가 생성된 것이다.  다음으로 고려해야 하는 것은 유전 알고리즘에서 가장 중요한 것은 염색체의 다양성을 유지하는 것이다. 따라서 유전 알고리즘에서는 적합도가 가장 좋은 염색체를 선택해서 교배를 하는 것이 아니라,적합도가 가장 좋은 염색체가 선택될 확률을 가장 높게 설정하고 확률적으로 염색체를 선택하는몬테카를로 방법(Monte Carlo method)을 이용한다.  따라서 이 예제에서는 초기 세대의 적합도를 모두 더한 값이 7730이므로 첫번째 염색체([A B D C E])가 선택될 확률은 1660을 7730으로 나누고 100을 곱한 값인 21.47%가 된다. 
*  추가적으로 유전 알고리즘의 성능을 향상시키는 방법으로 엘리트주의(elitism)이 있다. 엘리트주의는 이전 세대에서 적합도가 가장 좋은 염색체를 다음 세대에 그대로 보존하는 것으로 몇 개를 보존할지는 알고리즘의 설계에 따라 다르다. 이 예제에서는 적합도가 가장 높은 상위 2개의 염색체를 보존하도록 한다.그러므로 초기 세대에서 적합도가 가장 높은 [A B D C E]와 [A E C B D]를 다음 세대까지 그대로 보존하도록 한다. 따라서 교배연산에서는 총 3개의 다음 세대 염색체를 생성하면 된다. 임의로 선택된 세 쌍의 염색체쌍은 아래와 같다고 가정한다.


![image](https://user-images.githubusercontent.com/101339244/174278944-6360498c-286b-4f01-a29a-8a87cbb31936.png)

* 이항연산자 ( + )를 교배연산이라 정의하고, 각각에 교배연산을 적용하여 생성한 다음 세대 염색체는 아래와 같다.

![image](https://user-images.githubusercontent.com/101339244/174278999-3122870e-beeb-4560-982f-ac7e9ac9da4f.png)

* 마지막으로 교배연산을 통해 생성된 염색체에서 2~5번째 유전자는 각각 5%의 확률로 돌연변이를 일으켜 알파벳 순서상 그 다음 도시로 변경된다고 알고리즘을 설계한다. 
* 예를 들어 돌연변이가 발생하면 C는 D로, E는 B로 변경된다.
* [A D C E B]의 5번째 유전자에서 돌연변이가 발생했다고 가정하면, 염색체는 [A D B E C]로 변경된다.그러므로 초기 세대 다음인 첫 번째 세대는 아래와 같은 염색체로 구성된다.

![image](https://user-images.githubusercontent.com/101339244/174279113-f5abee24-2525-491f-8a56-4228d018cf81.png)

4) 다음 세대 적합도 평가  다음으로 초기 세대로부터 생성된 첫 번째 세대의 적합도를 평가한다.
 Fit([A B D C E]) = 1660  , Fit([A E C B D]) = 1680 , Fit([A B D C E]) = 1660 , Fit([A E C D B]) = 1430 , Fit([A D B E C]) = 1800
 
 5) 목표 적합도 검사  현재 세대의 염색체 중에서 가장 높은 적합도는 1800이므로 목표 적합도인 1900 이상의 적합도를 갖는 염색체가 존재하지 않는다. 그러므로 알고리즘을 계속 진행한다.
 
 6) 교배 및 돌연변이  현재 세대의 염색체를 이용하여 교배 및 돌연변이를 수행한다. 이 과정에서 수행하는 교배 및 돌연변이 연산은 과정 3의 연산과 같다. 새롭게 생성된 염색체들을 유지하면서 과정 4로 이동한다.
#### 위에  유전알고리즘 설계 같은 경우 이해를 하나도 하지 못한 나에게 이해를 할수 있도록 해준 자료이다.
유전 알고리즘 설계 출처자료: https://storycode.tistory.com/169




