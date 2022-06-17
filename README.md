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
#### 교차연산
* 교차 연산은 두해의 특징부분을 결합해 하나의 새로운 해를 만들어내는 연산
* 먼저 문제의 표현 방법이 결정 되어야한다.
#### 돌연변이 연산 
* 부모해의 없는 속성을 자식해에 도입하는 역할을 한다.
* 교차 연산이 수행된 후에 돌연변이 연산을 수행한다. 돌연변이 연산은 아주 작은 확률로 후보해의 일부분을 임의로 변형시키는 것이다. 
