<h3> Busca Binária </h3>

```
def dec2bin(n):
    p = []
    while n != 0:
        p.append(n%2)
        n =n//2
    while len(p) > 0:
        print(p.pop(), end = '')

dec2bin(18)

```

Se o número for sorteado entre 1 e 100 qual é o seu primeir chute?

50

Se chutar sempre metade da metade, em quantos passos se acerta o número?
 

```

from random import randint
sorteado = randint(1,1000)
while True:
    x = int(input('chute: '))
    if x == sorteado:
        print('Ganhou: ')
        break
    elif x > sorteado:
        print ('Alto')
    else:
        print('Baixo')
#acerte dez chutes
```

Esse algoritmo é muito rápido, quanto maior, mais vale a pena usar.
Para 1 milhão, gasta-se apenas 30 passos.

```
cont = 0
def busca_binaria(x, v):
  global cont
  e = -1
  d = len(v)
  while e < d-1: 
    m = (e + d) // 2
    cont = cont + 1
    if v[m] < x:
      e = m
    else:
      d = m
  return d


v = list(range(1000000))
from random import randint
print (busca_binaria(randint(1, 1000000), v))
print (cont)

```

Por isso, busca binária é como a invenção da roda, reaproveita-se a ideia de dividir o mundo em dois em vários outros contextos.
O oposto também é rápido, dobra-se o número de resultados bons a cada passo.


Suponha que precise desenhar, numa folha de papel 128 retângulos.
Existem duas formas básicas:
1) Mede-se a largura e comprimento, divida a folha em 128 retângulos, desenhando-se um por um.
2) Pode-se dobrar a folha no meio, e depois dobrar novamente no meio e assim pr diante em 7 passos tem-se 128 retângulos.

Se tem uma lista telefonica (páginas amarelas) e se deseja descobrir um telefone, abre-se no meio para ir mais rápido. Essa é a mesma ideia de busca binária!

Viu-se busca binária num vetor ordenado, porém na vida real não encontra-se vetores ordenados, então é necessário ordenar o vetor antes de usar busca binária.
Para ordenar existem vários algoritmos. Os que funcionam rápido usam IDEIA da busca binária, de dividir o mundo em dois.

<h5> Revisão Busca Binária </h5> 

* Dividir o mundo em dois, então a cada passo tenho metade das buscas;
* Vetor ordenado;
* Busca binária é muito rápido;

Custa log(n,2) passos onde n é o tamanho do vetor.

Nota que quanto maior é o n, mais vale a pena usar busca binária!

```
n = 1k          log(n,2) = 10
n = 1M          log(n,2) = 20
n = 1Tri        log(n,2) = 30
n = 1Qua        log(n,2) = 40
```

Enquanto é aumentado o n exponencialmente, o número de passos aumenta linearmente.
Busca binária é como a invenção da roda, usa-se a ideia em outros contextos:

1) Se procura um nome na Lista Telefônica (páginas amarelas), abre-se a lista no meio.
2) Se quer desenhar 128 retângulos numa folha, é mais fácil ir dobrando a folha sucessivamente ao meio.
3) Para fazer o índice do banco de dados.


Porém para usar busca binária é preciso ter um vetor ordenado, será que custa muito ordenar um vetor? Porque se demorar não vale a pena uscar busca binária.

<p> 5 algoritmos de ordenação: </p>
<p> - 2 ruins: seleção e inserção </p>
<p> - 3 bons: mergesort, quicksort e heapsort </p>

* Inserção (algoritmo do baralho)

Quando se recebe as cartas de um baralho, percorre-se da esquerda para a direita e enfia cada carta no lado esquedo na posição ordenada.

```
2 3 1 5 4 0 7 6
1 2 3                       1 empurra 23 
1 2 3 5                     5 está ok
1 2 3 4 5                   4 empurra 5
0 1 2 3 4 5                 0 empurra 12345
0 1 2 3 4 5 7               7 está ok
0 1 2 3 4 5 6 7             6 empurra 7
```

Exemplo:

```
4 3 6 0 1 2 5 7

3 4                     3 empurra 4
3 4 6                   6 está ok
0 3 4 6                 0 empurra 346
0 1 3 4 6               1 empurra 346
0 1 2 3 4 6             2 empurra 346
0 1 2 3 4 5 6           5 empurra 6
0 1 2 3 4 5 6 7         7 está ok
```

Quantos passos custa inserção?
Percorrer todos da esquerda para direita custa n passos.
Para cada elemento, o pior caso é onde é necessário empurar todo mundo para a direita, isto é, números muito pequenos.
Então no pior caso custa n * n passos n ** 2. Note que o pior caso não ocorre sempre, então na média , inserção será melhor que n ** 2, principalmente quando se têm números grandes. Inserção, portanto, não serve para esse caso!

* Inserção.py

Se tiver que esperar mais de 20 segundos para ordenar apenas 20k elementos, não vale a pena usar busca binária. 

```
def inserção(v):
  for j in range(1, len(v)):
    x = v[j]
    i = j - 1
    while i >= 0 and x < v[i]:
      v[i+1] = v[i]
      i = i - 1
    v[i + 1] = x
  return v
from time import time
from random import shuffle
v = list(range(20000))
shuffle(v)
t1 = time()
inserção(v)
t2 = time()
print (t2-t1)
##from random import sample
##v = sample(range(10), 10)
##print (v)
##v = inserção(v)
##print (v)
```

- Outra ideia é a seleção:
 Percorre da esquerda para direita e para cada elementos, verifica o menor que está adiante.
 Então, troca-se a posição atual com o menor que se encontrou pela frente.
 Seleção, porque seleciona e troca.
 
 ```
 4 3 6 0 1 2 5 7
 0 3 6 4 1 2 5 7             troca 0 4
 0 1 6 4 3 2 5 7             troca 1 3
 0 1 2 4 3 6 5 7             troca 2 6 
 0 1 2 3 4 6 5 7             troca 3 4 
 
 Note que sempre precisa ir até o final para ter certeza que achou o menor, como ser humano é possível ver tudo de uma vez, o programa não, por isso sempre anda até o fim.
 
 0 1 2 3 4 6 5 7             troca 4 4 
 0 1 2 3 4 5 6 7             troca 5 6 
 0 1 2 3 4 5 6 7             troca 6 6 
 ```
 
 Quanto custa seleção?
 
 ```
 Precisa percorrer todos: custa n passos.
 Para cada, precisa verificar o menor: custa n passos.
 Logo, no total custa n*n = n ** 2 passos
 Será que pode melhorar isso: Sim
 Para calcular o menor, tem-se uma função min do Python que é otimizada.
 ```
 
 * Seleção.py
 
 Para 20k demorou mais de 5 segundos, ainda é muito ruim, mesmo usando uma função embutida do python.
 
 ```
 def seleção(v):
  r = []
  while v:
    m = min(v) 
    r.append(m)
    v.remove(m)
  return r

from time import time
from random import shuffle
v = list(range(20000))
shuffle(v)
t1 = time()
seleção(v)
t2 = time()
print (t2-t1)
``` 

Repare que seleção, se não usar função embutida, é pior que inserção, porque inserção tem casos ruins e casos bons, no caso da seleção *sempre* precisa ir até o fim para descobrir o menor.
Na média, inserção é melhor que seleção. O único caso em que são ambos no pior caso, é quando se tem um vetor em ordem decrescente. Esse caso é muito raro, então, na média, inserção é melhor que seleção.
Nesse caso só é pior, porque está utilizando uma função do python, min que é otimizada para pegar os menores.

Melhorando isso com a ideia de dividir o mundo em dois com Mergesort:

```
4 3 6 0         1 2 5 7        2 quadruplas
4 3    6 0    1 2    57        4 duplas
4  3  6  0  1  2  5  7         8 unidades
34    06    12    57           4 duplas ordenadas
0346              1257         2 quadruplas ordenadas
01234567                       Tudo ordenado

```

* Mergesort.py

```
def mergesort(v):
    if len(v) <= 1: return v
    else:
        m = len(v) // 2
        e = mergesort(v[:m])
        d = mergesort(v[m:])
        return merge(e, d)

def merge(e, d):
    r = []
    i, j = 0, 0
    while i < len(e) and j < len(d):
        if e[i] <= d[j]:
            r.append(e[i])
            i += 1
        else:
            r.append(d[j])
            j += 1
    r += e[i:]
    r += d[j:]
    return r

from time import time
from random import shuffle
v = list(range(20000))
shuffle(v)
t1 = time()
v = mergesort(v)
t2 = time()
print (t2-t1)

```
Agora sim, demorou apenas 0,1 segundos!

- Melhorando mais ainda:

Quicksort usa sempre um pivô (voluntário).
Divide-se em duas partes, menores que o pivô e maiores que o pivô.
Assim, tem-se o pivô na posição correta e definitiva. Repete-se o processo para cada metade.
Assim, vai dobrando a cada passo o número de pessoas na posição correta (dividindo em duas partes sempre, dobra o número de elementos ordenados no passo seguinte).

```
1 0 2 6 3 4 7 5
0 1 2 6 3 4 7 5 //lado esquerdo resolvido porque o 0 só tem tamanho 1
    2 6 3 4 7 5 //com pivo 2 não tem lado esquerdo e todos do direito são maiores
      3 4 5 6 7 // 3 4 5 são maiores que 6, então ele já fica na posição definitiva e 7 acaba
      3 4 5 //3 é pivo
        4 5 //tamanho um, para
```
Observação: pior caso é o vetor ordenado, pois não é possível dividir o mundo em dois. Porém é muito raro! Na média, como divide em 2, tem log(n,2) * passos. Para vetores pequenos não se consegue ver a vantagem, o ideal é pensar no acumulado 1 + 2 + 4 + 8... de elementos na posição ordenada.


* Quicksort.py

```
##from memory_profiler import profile
##@profile
def quicksort(v):
  if len(v) <= 1: return v    
  pivô = v[0]
  iguais  = [x for x in v if x == pivô]
  menores = [x for x in v if x <  pivô]
  maiores = [x for x in v if x >  pivô]
  return quicksort(menores) + iguais + quicksort(maiores)

from time import time
from random import shuffle
v = list(range(20000))
shuffle(v)
t1 = time()
quicksort(v)
t2 = time()
print (t2-t1)
##from random import sample
##v = sample(range(10), 10)
##print (v)
##v = quicksort(v)
##print (v)


```
Já está ótimo em 0.5

- Dá para melhorar mais ainda?
Sim, com heapsort que usa a ideia de Busca Binaria noa índices do vetor.
Segue dois passos: 
```
1)colocar todos numa estrutura chamada heap, onde o índice k tem conteúdo maior ou igual que seus dois "filhos" 2*k e 2*k+1. No final, o primeiro será o maior de todos, não garantindo a ordenação do resto. 
2)Troca o primeiro com o último, assim entra um elemento "fraco" na primeira posição, assim ele é "sacudido" até ele descer à sua posição correta. 

Note que colocar todo mundo na estrutura de heap, ou fazer o processo de "sacode" é rápido, log(n,2) passos. 

Teste de mesa:
1 2 3 4 5 6 7 8  //índices para não se bagunçar e saber identificar que, é pai e filho.
                 Não começa com índice 0 para dar certo a conta do 2*k e 2*k+1
1 0 2 6 3 4 7 5  //1 e 0 está e heap
2 0 1            //2(pai) maior que seus dois filhos ( 0 1)
2 6 1 0          //6 vai no índice dividido por 2 que é o 0
6 2 1 0          //6 sobe mais uma posição pq o pai do pai é o 2 que é fraco
6 3 1 0 2        //3 entra no lugar do 2 que é o pai dele
6 3 4 0 2 1      //4 entra no lugardo 1 que é o pai dele 
6 3 7 0 2 1 4    //7 troca com 4 que é pai dele
7 3 6 0 2 1 4
7 3 6 5 2 1 4 0  //5 troca com 0 que é seu pai
7 5 6 3 2 1 4 0 //troca com o pai do pai
Aqui chegou na estrutura de heap, gastando log(n,2) * n passos
```
Pode usar a ideia de dividir o mundo em dois andando pelos índices do vetor.
Assim, vai dobrando o índice a cada passo para andar para a direita e vai dividindo o índice pela metade a cada passo para andar no final para o começo. 
Essa estrutura é chamada heap.

* heapsort.py 

Usa estrutura do python!
Observação: não em partes independentes, então não dá para fazer em parelelo!
```
from heapq import heappush, heappop
def heapsort(v):
  h = []
  for x in v: heappush(h, x)
  return [heappop(h) for i in range(len(h))]

from time import time
from random import shuffle
v = list(range(20000))
shuffle(v)
t1 = time()
heapsort(v)
t2 = time()
print (t2-t1)
##from random import sample
##v = sample(range(10), 10)
##print (v)
##v = heapsort(v)
##print (v)

```

* Sort interno.py

É uma mistura de mergersort com outros esteróides de otimização.
TIMSORT é o nome do algoritmo. O sort interno da linguagem java é o mesmo TIMSORT que foi inventado no python.

```
from time import time
from random import shuffle
v = list(range(20000))
shuffle(v)
t1 = time()
v.sort()
t2 = time()
print (t2-t1)

```

Mergesort dobra a cada passo, porém quicksort não apenas dobra, mas acumula.
1 + 2 + 4 + 16 + 32 + ...

<h3> Árvore Binária </h3>

![alt text](https://github.com/Jennyads/Estrutura_de_Dados/blob/main/Imagens/arvorebinaria.png)

É binária porque em cada nó tem no máximo dois filhos para baixo, cada um dos nós tem dois filhos para baixo.

Árvore binária de busca balanceada:


Filhos da esquerda são menores ou igual e filho da direita são maiores ou igual.
Se procurar qualquer elemento a partir da raiz, vai gastar log(n,2) passos.
Se baixar todos os nós na vertical dá o vetor ordenado 0 1 2 3 4 5 6 7 8 9, mesma ordem que vetor ordenado!
É muito rápido a busca em vetor ordenado, pois divide em 2 e descarta a outra metade. 
Em termos de busca é igual vetor ordenado e árvore binária de busca!

Vantagens: Inserir ou remover em vetor ordenado é muito ruim, principalmente em c (vetores contíguos que empurra todo mundo para a direita, ou para remover puxar todo mundo para esquerda).
Em termos de inserção e remoção é muito mais rápido em árvore binária, pois utiliza ponteiros.
Usa-se em índices de banco de dados.
No pior caso, se tiver árvore desbalanceada!

<h4> Revisão </h4>
Algoritmos de Ordenação

É bom ver várias formas de fazer um mesmo código.

5 formas diferentes!
```
2 ruins: inserção e seleção custam n*n ou n ** 2 passos, inserção no pior caso é n * n, porém tem casos bons (números grandes não mexem os anteriores), então na média inserção é melhor que seleção, seleção é sempre ruim, só tem caso pior. Melhora-se usando min, função embutida no python, que usa uma estrutura de dados auxiliar para guardar o menor, sem ter que passar por todos os elementos. 
3 boas: mergesort (divide o vetor em dois), quicksort (divide os elementos em maiores ou menores que um pivô), heapsort (anda muito rápido em passos que vão dobrando no índice).
Mergesort: divide o vetor em dois até ficar do tamanho 1, então junta-se (merge) os vetores até voltar ao original, juntando-se tem duas fileiras de crianças em ordem, pode-se ir escolhendo a menor entre as duas da ponta de cada fileira. Gasta-se n passos nesse "juntando" porque todo mundo tem que ser comparado e gasta também um espaço igual ao vetor original. Lição: não basta ter um número de passos pequenos, precisa-se gastar pouca memória também, mergesort gasta bastante memória.
Desvantagens: mergesort, apesar de rápido, gasta mais espaço.
Vantagens: as partes do vetor divididas são independentes e pode ser resolvido de forma assíncrona. 

Quicksort: divide em maiores ou menores que um pivô e repete sucessivamente até todos estarem na posição final. O interessante do quicksort é que o número de pessoas na posição final cresce muito mais rápido que mergesort. 
Quicksort é acumulativo, não só dobra, mas acumula os anteriores.

Total: 1 + 2 + 4 + 8 + 16 + 32 + 64 + 128 + 256 + 512 + 1024

Análise detalhada: Qual é o pior caso? Vetor já ordernado, sempre não vai ninguém para um dos lados, o que resulta que não dobra o número a cada passo, e pior, vai demorar n passos até todo mundo ficar na posição.
Então no total vai gastar n * n, tão ruim quanto inserção e seleção na prática nunca encontra um vetor ordenado. Então na média quicksort é muito bom!
```
