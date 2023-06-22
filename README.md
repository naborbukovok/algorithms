Подготовка к устному зачету по курсу «Алгоритмы и структуры данных», первая часть.

## Список билетов
### 1. Статический массив. Динамический массив, среднее время добавления элемента.
**Массив** - набор однотипных элементов, доступ к которым осуществляется по индексу. В памяти массив представляется непрерывным куском. 

Массив, который не изменяет свой размер, называется **статическим**. Для статического массива размер задается при его инициализации.

**Динамический** массив - такой массив, который может изменять свой размер в зависимости от количества элементов в нём. Есть несколько способов добавить элемент в динамический массив.

**1) В конец:** Если в массиве есть место для добавления нового элемента (физическое), то добавление по индексу ```n``` происходит за константное время ```O(1)```. В худшем случае, если в массиве больше нет места, создается новый массив в несколько раз большей длины, в который копируются все элементы и далее по индексу ```n``` добавляется новый. Для худшего случая получаем сложность ```O(n)```, так как копируем каждый из ```n``` элементов. Однако, так как при отсутствии места длина массива увеличивается не на 1, а в несколько раз, среднее время добавления элемента в конец массива будет ```O(1)```.

**2) В начало:** Если место есть, то каждый из элементов, начиная с конца, смещается на 1 вправо, а затем в начало добавляется новый элемент. Если места нет, создается новый массив в несколько раз большей длины, в котрый копируются все значения исходного массива со сдвигом вправо на 1, а затем в начало добавляется новый элемент. В обоих случаях сложность линейная - ```O(n)```. То есть среднее время добавления элемента в начало массива - так же ```O(n)```.

**3) В произвольное место:** Алгоритм и сложность аналогичны добавлению в начало (за исключением того, что в данном случае сдвигаются не все элементы).

### 2. Односвязный список, двусвязный список. Псевдокод добавления и удаления.
**Односвязный список** - структура данных, состоящая из элементов (узлов), содержащих помимо собственных данных указатель на следующий элемент в списке.

**Двусвязный список** - структура данных, состоящая из элементов (узлов), содержащих помимо собственных данных указатели на предыдущий и следующий элемент в списке. Благодаря этоик становится проще удалять и переставлять элементы.

**Вставка в односвязном списке:**
1. Создаем новый узел
2. Находим в списке место для вставки (можно отсчиать от head)
3. Новому узлу назначаем ссылку на следующий, а текущему на новый

В общем случае сложность вставки в односвязном списке ```O(n)```, для добавления в начало или в конец ```O(1)```.

**Удаление в односвязном списке:**
1. Ищем в списке узел, который находится перед удаляемым
2. Назначаем этому узлу ссылку, которую хранил удаляемый (то есть следующий)

При удалении важно обратить внимание на крайние случаи: элемента нет в списке, элемент один, элемент находится в начале или в конце списка. Сложность удаления - ```O(n)``` (в худшем случае переберем все элементы и не найдем тот, что нужно удалить).

**Вставка и удаление в двусвязном списке** идейно похожи, добавляется только переназначение указателя на предыдущий узел. Сложность та же.

Двусвязный список, в отличие от односвязного, позволяет вручную итерироваться по списку в обе стороны. На основе связных списков строятся другие, более сложные, структуры данных.

### 3. АТД Стек. Реализация стека на основе динамического массива, на основе списка.
**Стек** - структура данных, представляющая из себя набор элементов, в которой добавление новых элементов и удаление существующих производится с одного конца, называемого вершиной стека. Притом первым из стека удаляется элемент, который был помещен туда последним (last-in, first-out - LIFO). Операции стека:
1. ```isEmpty``` - проверка стека на наличие в нем элементов;
2. ```push``` - операция вставки нового элемента;
3. ```pop``` - операция удаления элемента.

**Реализация стека на основе динамического массива:**
```
 1.  class Stack {
 2.      private ArrayList stack;
 3.  
 4.      boolean isEmpty() {
 5.          return (stack.size() == 0);
 6.      }
 7.  
 8.      void push(int element) {
 9.          stack.add(element);
10.      }
11.
12.      void pop() {
13.          if (!isEmpty()) {
14.              stack.remove(stack.size() - 1);
15.          }
16.      }
17.  }
```
**Реализация стека на основе списка:**

Стек можно реализовать на односвязном списке. Идея следующая: вершиной стека будет первый узел списка (```head```). ```isEmpty``` будет работать так: если в ```head``` хранится ```null```, стек пуст. При вызове ```push``` будем добавлять новые элементы перед ```head``` (в начало списка). При вызове ```pop``` будем удалять узел, который в текущий момент является ```head```.

### 4. АТД Очередь и Дек. Реализация на основе списка, оценка времени сложности.

**Очередь** - это структура данных, представляющая из себя набор элементов, в которой добавление новых элементов и удаление существующих производится с разных концов. Первым из очереди удаляется элемент, который был помещен туда первым (first-in, first-out - FIFO). У очереди имеется ```head``` и ```tail```. Когда элемент ставится в очередь, он занимает место в её хвосте. Из очереди всегда выводится элемент, который находится в ее голове. Очередь поддерживает следующие операции:
1. ```isEmpty``` - проверка наличия элементов;
2. ```push``` - операция вставки нового элемента;
3. ```pop``` - операция удаления элемента;
4. ```size``` - операция получения количества элементов в очереди.

**Дек** - структура данных, представляющая из себя список элементов, в которой добавление новых элементов и удаление существующих производится с обоих концов. Эта структура поддерживает как FIFO, так и LIFO, поэтому на ней можно реализовать как стек, так и очередь. Дек можно воспринимать как двустороннюю очередь. Он имеет следующие операции:
1. ```isEmpty``` - проверка наличия элементов;
2. ```pushBack``` - операция вставки нового элемента в конец;
3. ```popBack``` - операция удаления конечного элемента;
4. ```pushFront``` - операция вставки нового элемента в начало;
5. ```popFront``` - операция удаления начального элемента;

В реализации на основе списка ```isEmpty``` проверяет, совпадают ли ```head``` и ```tail```. Для очереди необходимо реализовать стандартные добавление/удаление элемента в конце списка, для дека - в начале и в конце списка. Для получения количества элементов их предется перебрать.

Сложность добавления и удаления - ```O(1)```, получения количества элементов - ```O(n)```.

### 5. Бинарный поиск. Задача поиска элемента в отсортированном массиве - постановка задачи, оценка сложности алгоритма.
**Бинарный поиск** - алгоритм поиска объекта по заданному признаку в множестве объектов, упорядоченных по тому же самому признаку.

**Задача:** Дан упорядоченный массив, состоящий только из целочисленных элементов. Требуется найти позицию, на которой находится заданный элемент.

Идея заключается в том, что на каждом шаге множество объектов делится на две части и далее рассматривается только та часть, где находится искомый объект. На каждом шаге необходимо брать элемент в середине оставшегося массива и сравнивать его с искомым элементом. Если искомое больше середины, то середина становится левой границей. В противном случае - правой. Повторять нужно до тех пор, пока элемент не найден и разница между левой и правой границами больше 1.

```
 1.  int binSearch(int[] a, int key):    // ищем key
 2.      int l = -1                      // l - левая граница
 3.      int r = len(a)                  // r - правая граница   
 4.      while l < r - 1
 5.          m = (l + r) / 2             // m - середина области поиска
 6.          if a[m] < key
 7.              l = m
 8.          else 
 9.              r = m
10.      return r
```

Используя приведенный выше алгоритм, мы найдем самое левое вхождение искомого элемента. Это левосторонний бинарный поиск. Чтобы найти самое правое вхождение, нужно заменить условие в 6 строке на ```a[m] <= key``` и возвращать ```l```. Это правосторонний бинарный поиск.

Худший случай - если искомый элемент окажется первым или последним. Каждую итерацию мы делим массив пополам, Это значит, что сложность алгоритма будет зависеть от того, сколько раз мы можем поделить массив на двое - то есть в какую степень нужно возвести 2, чтобы получить длину рассматриваемого массива. Получаем сложность ```O(log n)```.

### 6. Поддержка минимума в стеке и очереди.

**Поддержка минимума** в стеке и очереди - это задача по нахождению минимального элемента в структуре данных.

**Для стека:**

Модифицируем стек так, чтобы получить возможность нахождения минимума за ```O(1)```, сохранив такой же асимптотику добавления и удаления элементов стека. Для этого будем хранить в стеке не сами элементы, а пары: элемент и минимум в стеке, начиная с этого элемента и ниже. Таким образом, нахождение минимума во всём стеке будет заключаться во взятии дополнительного значения из вершины стека. Добавляя новый элемент в стек, будем задавать ему дополнительное значение, равное меньшему из значения нового элемента и дополнительного значения старой вершины. Удаление элемента из стека ничем не отличается от удаления из обычного стека, поскольку удаляемый элемент никак не мог повлиять на дополнительные значения для оставшихся элементов.

**Для очереди:**

Поддержка минимума в очереди сводится к поддержке минимума в стеке. Представим очередь в виде пары двух стеков с поддержкой минимума (для простоты обозначим их как ```stack1``` и ```stack2```). Добавлять новые элементы будем только в ```stack1```, а  удалять - только из ```stack2```. Если при попытке удалить элемент из ```stack2``` он окажется пустым, перенесём все элементы из ```stack1``` в ```stack2```. Заметим, что нужный порядок элементов при перенесении из стека в стек никак не нарушится, но дополнительные значения элементов при переносе из ```stack1``` в ```stack2``` нужно переписать. Таким образом, чтобы найти минимум очереди, нужно взять меньшее из минимумов ```stack1``` и ```stack2```. Асимптотика добавления и удаления элементов очереди не изменилась, но при этом добавилась возможность находить минимум очереди за ```O(1)```.

### :rotating_light: 7. Двоичная куча. Описание, построение, добавление элемента, извлечение минимума.

### 8. Квадратичные сортировки (пузырьком, вставками, выбором), сортировка с помощью двоичной кучи. Описание алгоритмов, оценка времени работы и дополнительной памяти.

**Сортировка пузырьком** заключается в повторении проходов по массиву и сравнении пар соседних элементов. Элементы меняются местами, если они находятся в неправильном порядке. Сложность - ```O(n^2)```.
```
 1.  public static void bubbleSort(int[] sortArr){
 2.      for (int i = 0; i < sortArr.length - 1; i++) {
 3.          for(int j = 0; j < sortArr.length - i - 1; j++) {
 4.              if(sortArr[j + 1] < sortArr[j]) {
 5.                  int swap = sortArr[j];
 6.                  sortArr[j] = sortArr[j + 1];
 7.                  sortArr[j + 1] = swap;
 8.              }
 9.          }
10.      }
11.  }
```

**Сортировка вставками** заключается делении на отсортированную и неотсортированную часть, с последующим проходом по неотсортированной части и вставке каждого элемента на нужное место в отсортированной. Сложность - ```O(n^2)```.
```
 1.  public static void insertionSort(int[] sortArr) {
 2.      int j;
 3.      for (int i = 1; i < sortArr.length; i++) {              // сортировку начинаем со второго элемента
 4.          int swap = sortArr[i];                              // сохраняем ссылку на индекс предыдущего элемента
 5.          for (j = i; j > 0 && swap < sortArr[j - 1]; j--) {
 6.              sortArr[j] = sortArr[j - 1];                    // перемещаем вперед все, что больше элемента для вставки
 7.          }
 8.          sortArr[j] = swap;
 9.      }
10.  }
```

**Сортировка выбором** заключается делении на отсортированную и неотсортированную часть, с последующим повторяющимся поиском минимума в неотстортированной части и постановкой его в конец отсортированной. Сложность - ```O(n^2)```.
```
 1.  public static void selectionSort(int[] sortArr) {
 2.      for (int i = 0; i < sortArr.length; i++) {
 3.          int pos = i;
 4.          int min = sortArr[i];
 5.          for (int j = i + 1; j < sortArr.length; j++) {  // цикл выбора наименьшего элемента
 6.              if (sortArr[j] < min) {
 7.                  pos = j;                                // pos - индекс наименьшего элемента
 8.                  min = sortArr[j];
 9.              }
10.          }
11.          sortArr[pos] = sortArr[i];
12.          sortArr[i] = min;                               // меняем местами наименьший с sortArr[i]
13.      }
14.  }
```

### 9. Сортировка слиянием. Описание алгоритма, оценка времени работы.

**Сортировка слиянием** разбивает список на две части, каждую из них она разбивает ещё на две и так далее, пока не останутся единичные элементы. Массив из одного элемента считается упорядоченным. Соседние элементы сравниваются и соединяются вместе. Так происходит до тех пор, пока все элементы не будут отсортированы. Сортировка осуществляется путём сравнения наименьших элементов каждого подмассива. Первые элементы каждого подмассива сравниваются первыми. Наименьший элемент перемещается в результирующий массив. Счётчики результирующего массива и подмассива, откуда был взят элемент, увеличиваются на один.
```
 1.  public static int[] mergeSort(int[] sortArr) {
 2.      int[] buffer1 = Arrays.copyOf(sortArr, sortArr.length);
 3.      int[] buffer2 = new int[sortArr.length];
 4.      int[] result = mergeSortInner(buffer1, buffer2, 0, sortArr.length);
 5.      return result;
 6.  }
```
```
 1.  public static int[] mergeSortInner(int[] buffer1, int[] buffer2, int startIndex, int endIndex) {
 2.      if (startIndex >= endIndex - 1) {
 3.          return buffer1;
 4.      }
 5.  
 6.      //уже отсортирован
 7.      int middle = startIndex + (endIndex - startIndex) / 2;
 8.      int[] sorted1 = mergeSortInner(buffer1, buffer2, startIndex, middle);
 9.      int[] sorted2 = mergeSortInner(buffer1, buffer2, middle, endIndex);
10.  
11.      //слияние
12.      int index1 = startIndex;
13.      int index2 = middle;
14.      int destIndex = startIndex;
15.      int[] result = sorted1 == buffer1 ? buffer2 : buffer1;
16.      while (index1 < middle && index2 < endIndex) {
17.          result[destIndex++] = sorted1[index1] < sorted2[index2] ? sorted1[index1++] : sorted2[index2++];
18.      }
19.      while (index1 < middle) {
20.          result[destIndex++] = sorted1[index1++];
21.      }
22.      while (index2 < endIndex) {
23.          result[destIndex++] = sorted2[index2++];
24.      }
25.      return result;
26.  }
```

Пусть ```T(n)``` - время сортировки массива длины ```n```. Тогда для сортировки слиянием справедливо: ```T(n) = 2T(n/2) + O(n)```, где ```O(n)``` - время, необходимое на то, чтобы слить два массива длины n. Распишем: ```T(n) = 2T(n/2) + O(n) = 4T(n/4) + 2O(n) = ... = T(1) + log(n)O(n) = O(n log n)```. Сложность сортировки слиянием - ```O(n log n)```.

### :rotating_light: 10. Быстрая сортировка. Описание алгоритма, оценка времени работы в лучшем, среднем и худшем случае.

### :rotating_light: 11. Поиск k-ой порядковой статистики на основе быстрой сортировки. Оценка времени работы и лучшем, среднем и худшем случае.

### 12. Граф. Хранение графа в памяти: список смежности, матрица смежности (плюсы и минусы). Оценка времени поиска всех соседей, добавление ребра. Оценка расходуемой памяти.

**Граф** - это абстрактный математический объект, состоящий из набора вершин и ребер, которые соединяют эти вершины. Хранение графа в памяти можно осуществлять двумя способами: списком смежности и матрицей смежности. **Список смежности** представляет собой набор списков, каждый из которых содержит вершины, смежные с данной вершиной. **Матрица смежности** представляет собой квадратную матрицу, в которой на пересечении строки и столбца стоят 1, если между соответствующими вершинами есть ребро, и 0 в противном случае.

**При использовании списка смежности** удобно перебирать ребра, выходящие из вершины ```i``` (это просто список ```W[i]```), но сложно проверять наличие ребра между вершинами ```i``` и ```j``` – для этого необходимо проверить, содержится ли число ```j``` в списке ```W[i]```. Но если заменить списки на множества, то и эта проверка существования ребра между двумя вершинами также будет выполняться за ```O(1)```.

- Поиск всех соседей: O(число ребер из вершины)
- Поиск ребра: O(число ребер из вершины)
- Память: ```O(N + сумма степеней всех вершин) = O(N + 2 * число ребер) = O(N + число ребер)```

**При использовании матрицы смежности** удобно проверять соединены ли две вершины ребром - это просмотр одного элемента матрицы ```A[i][j]```, но сложнее перебирать все ребра, исходящие из данной вершины (для этого необходимо перебрать все оставшиеся вершины и проверить, соединены ли они ребром). Также матрица смежности требует ```O(N^2)``` памяти и может оказаться неэффективным способом хранения дерева или разреженных графов.

- Поиск всех соседей: ```O(N)```
- Поиск ребра: ```O(1)```
- Память: ```O(N^2)```

Список смежности - более компактный способ представления графа, он требует меньше памяти и особенно удобен для "разреженных" графов, у которых немного ребер. В то же время матрица - более наглядная и удобная структура, позволяющая быстро определить, есть ли связь между двумя вершинами. Для "плотных" графов с большим количеством ребер матрица обычно выгоднее, чем список.

### 13. Виды графов. Деревья. Связность. Циклы. Полные графы. Ориентированность.

**Связный граф** - это граф, в котором существует путь между любой парой вершин.

**Цикл** - путь в графе, который начинается и заканчивается в одной и той же вершине.

**Дерево** - связный граф без циклов.

**Полный граф** - граф, в котором каждая вершина соединена с каждой другой вершиной.

Графы бывают ориентированными и неориентированными. **Ориентированный граф** - граф, в котором каждое ребро имеет направление. **Неориентированный граф** - граф, в котором ребра не имеют направления.

### 14. Обход графа в ширину. Описание алгоритма, примеры задач, временная сложность.

**Обход графа в ширину** (BFS, Breadth First Search) - это алгоритм обхода графа, который начинается с выбора стартовой вершины, от которой запускается процесс поиска всех вершин, достижимых из нее за наименьшее количество шагов. Для этого вершины посещаются в порядке, определяемом расстоянием от стартовой вершины, начиная с той, что находится на расстоянии 1, затем на расстоянии 2, и так далее. 

**Алгоритм:**
1. Поместить узел, с которого начинается поиск, в изначально пустую очередь.
2. Извлечь из начала очереди узел ```u``` и пометить его как развёрнутый.
3. - Если узел ```u``` является целевым узлом, то завершить поиск с результатом «успех».
   - В противном случае, в конец очереди добавить всех преемников узла ```u```, которые ещё не развёрнуты и не находятся в очереди.
4. Если очередь пуста, то все узлы связного графа были просмотрены, следовательно, целевой узел недостижим из начального; завершить поиск с результатом «неудача».
5. Вернуться к п. 2.

**Временная сложность** алгоритма  ```O(N + M)```, где ```N``` - количество вершин в графе, ```M``` - количество ребер.

**Применение:**
1. Поиск кратчайшего пути в невзвешенном графе.
2. Поиск компонент связности в графе за ```O(N + M)```
3. Нахождения решения какой-либо задачи (игры) с наименьшим числом ходов, если каждое состояние системы можно представить вершиной графа, а переходы из одного состояния в другое — рёбрами графа.
4. Нахождение кратчайшего цикла в ориентированном невзвешенном графе: производим поиск в ширину из каждой вершины; как только в процессе обхода мы пытаемся пойти из текущей вершины по какому-то ребру в уже посещённую вершину, то это означает, что мы нашли кратчайший цикл, и останавливаем обход в ширину; среди всех таких найденных циклов (по одному от каждого запуска обхода) выбираем кратчайший.
5. Нахождение всех рёбер или вершин, лежащих на каком-либо кратчайшем пути между заданной парой вершин ```(a, b)```. Для этого надо запустить 2 поиска в ширину: из a, и из b. Обозначим через ```d_a[]``` массив кратчайших расстояний, полученный в результате первого обхода, а через ```d_b[]``` — в результате второго обхода. Для ребра ```(u, v)``` критерий того что он на пути - ```d_a[u] + 1 + d_b[v] = d_a[b]```. Для вершины ```v```  получаем критерий ```d_a[v] + d_b[v] = d_a[b]```.


### 15. Обход графа в глубину. Описание алгоритма, примеры задач, временная сложность. Свойство дерева обхода.

**Обход графа в глубину** (DFS, Depth First Search) - это алгоритм обхода графа, который начинается с выбора стартовой вершины, от которой запускается процесс поиска всех вершин, достижимых из нее путем посещения соседних вершин и их дальнейшего обхода соседних от соседних вершин. Согласно этому алгоритму обход вершин графа осуществляется так. Начиная с некоторой вершины, мы идем по ребрам графа, пока не попадем в вершину, у которой нет исходящих ребер, ведущих в непосещенные вершины. Тогда мы возвращаемся назад вдоль пройденного пути, пока не обнаружим вершину, у которой есть исходящие ребра, ведущие в непосещенные вершины, и из нее идем по одному из таких ребер. Процесс кончается, когда мы возвращаемся в начальную вершину, а все соседние вершины уже оказались посещенными.

**Алгоритм реализовывается рекурсивно:**
1. Выбираем стартовую вершину
2. Запускаем процедуру поиск в глубину от этой вершины:
- Помечаем вершину ```u``` как пройденную
- Для каждой не пройденной и смежной с ```u``` вершиной (назовем ее ```v```) запускаем поиск в глубину от этой вершины
3. Повторяем шаги 1 и 2, пока все вершины не окажутся пройденными

**Временная сложность** алгоритма  ```O(N + M)```, где ```N``` - количество вершин в графе, ```M``` - количество ребер.

**Применение:**
Поиск в глубину применим в ситуациях, когда граф неизвестен целиком и нужно его исследовать.
1. Подсчет числа компонент связности в неориентированном графе. Чтобы найти все компоненты связности, будем обходить все вершины графа и проверять, была ли очередная вершина посещена ранее. Если не была – то это означает, что найдена новая компонента связности, для выделения всей компоненты связности необходимо запустить DFS от этой вершины.
2. Проверка на двудольность. Граф называется двудольным, если его вершины можно разбить на два множества так, что концы каждого ребра принадлежат разным множествам. Иными словами, можно покрасить вершины графа в два цвета так, что концы каждого ребра покрашены в разный цвет. Для решения этой задачи нужно не просто отмечать посещенные вершины, а отмечать их одним из двух "цветов". Алгоритм DFS для каждого ребра будет проверять цвет конечной вершины этого ребра. Если вершина не была посещена, то она красится в цвет, неравный цвету текущей вершины. Если же вершина была посещена, то ребро либо пропускается, если его концы – разноцветные, а если его концы одного цвета, то мы понимаем что граф не является двудольным.
3. Топологическая сортировка. Пусть дан ориентированный граф не содержащий циклов. Тогда вершины этого графа можно упорядочить так, что все ребра будут идти от вершин с меньшим номером к вершинам с большим номером. Для топологической сортировки графа достаточно запустить алгоритм DFS, при выходе из вершины добавляя вершину в конец списка с ответом. После окончания алгоритма список с ответом развернуть в противоположном порядке.

**Свойство дерева обхода** заключается в том, что каждая вершина дерева посещается только один раз.

### :rotating_light: 16. Поиск цикла в графе (ориентированном и неориентированном) при помощи обхода в глубину. Описание алгоритма, оценка по времени и памяти.

**Поиск цикла в графе** (ориентированном и неориентированном) при помощи обхода в глубину - это алгоритм, который использует обход в глубину для обнаружения цикла в графе. При посещении каждой вершины алгоритм помечает ее как посещенную, а затем проходит по всем ее непосещенным соседним вершинам. Если находится непосещенная вершина, то алгоритм рекурсивно вызывается для нее, иначе проверяется, находится ли текущая вершина в стеке. Если текущая вершина уже есть в стеке, то это означает наличие цикла в графе. Оценка времени работы алгоритма - ```O(n + m)```, где ```n``` - количество вершин в графе, ```m``` - количество ребер.

### :rotating_light: 17. Поиск мостов в графе. Определение моста. Алгоритм нахождения мостов.

**Мостом** называется ребро, при удалении которого граф распадается на две компоненты связности. Алгоритм поиска в глубину позволяет найти все мосты в связном графе за один DFS.

### :rotating_light: 18. Поиск точек сочленения в графе. Определение точки сочленения. Алгоритм нахождения точек сочленения.
