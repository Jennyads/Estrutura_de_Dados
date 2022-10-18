<h3> Recursão </h3>

Recursão = função que chama a si própria no código.

```
Fatorial
fat(0) ou fat(1) = 1     0! ou 1! = 1
n! = n*(n-1)!
4! = 4.3! = 4x3x2! = 4x3x2x1! = 4x3x2x1 = 24
```
```
def fat(n):
    if n == 0 or n==1: return 1
    else:
        return n*fat(n-1)

print(fat(4))
```

A maior parte das funções recursivas são da seguinte forma:

```
def f(argumentos):
	se caso simples:
		devolve valor que sei
	senão:
		faz alguma conta que diminui os argumentos
		devolve valor composto que monta o resultado que quero
```

Repare que no fatorial recursivo não tem while e não tem for.
Então como ele faz a repetição?
Ele faz a repetição no *return*

```
fat(4):
	if 4 == 0 or 4 == 1:
	else:
		return 4 * fat(3)
fat(3):
	if 3 == 0 or 3 == 1:
	else:
		return 3 * fat(2)
fat(2):
	if 2 == 0 or 2 == 1:
	else:
		return 2 * fat(1)
fat(1):
	if 1 == 0 or 1 == 1: return 1
```

* Exemplo - Potência:

```
def pot(x,n):
    if n == 0: return 1
    return x * pot(x, n-1)

print(pot(2,3))
```

* Exemplo - Fatiamento:

```
def inv(s):
    if len(s) == 0: return ""
    return inv(s[1:]) + s[0]
print(inv("abacate"))
```

* Exemplo - mdc:

```
def mdc(a,b):
    if a % b == 0: return b
    return mdc(b, a%b)
print(mdc(21,15))
print(mdc(15,21))
```

* Exemplo soma dos dígitos de um inteiro n

```
def sd(n): 
    #sd(123) = 6 = 1 + 2 + 3
    if n <= 9: return n
    return sd(123 // 10) + n % 10
print(sd(123))
```

* Exemplo - Fibonacci:

```
def fib(n):
    if n <= 2: return 1
    return fib(n-1) + fib(n-2)
print(fib(10))
```

Funções recursivas são poderosas porque "concentram" mais programação em menos linhas. Será que são sempre eicientes?
Não! Depende de como é programado.

Para números muito grandes:

```
from functools import lru_cache

@lru_cache(maxsize=None)
def fib(n):
    if n <= 2: return 1
    return fib(n-1) + fib(n-2)
print(fib(100))
```

<h3> Ponteiros </h3>

Vetores em C usam dados contíguos, um dado do ladinho do outro.
Vantagem é movimentar rápido grandes massas de dados.
Desvantagem é inserir ou remover, pois tenho que mover todos os elementos da direita. 
Como resolve essa ineficiência?
Usando ponteiros, assim eu tenho dados que não são contíguos e para inserir ou remover basta mudar ponteiros. 
Isso lembra Caça ao Tesouro.
Como implementar isso?


```
struct {
   int conteudo;
   struct cel * seg; //seguinte
}
type struct cel celula;
```

Existem duas formas de se passar argumentos para uma função em C.
1) Passagem por valor, somente uma cópia das variáveis.
2) Passagem por referência, isto é ponteiros para as variáveis de origem. 


Python também faz tudo por referência, mas ao alto nível C foi desenhada para construir um Sistema Operacional (Linux) por isso é tão "baixo" nível. 
Portanto, é mais difícil programar em C (como dançar num salão bem encerado, com várias facas na mão). Os perigos maiores são devido aos ponteiros.
Regras: assista Binky pointer fun
1) Ponteiro e coisa apontada são *diferentes*
2) Não tem sentido ponteiro que não aponta para nada.

* Lista ligada com cabeça com alocação dinâmica.c

É melhor inserir elementos novos no final ou no começo da lista??
No começo, porque se inserir no final tenho que andar até o final, isto é ineficiente. Pode-se imaginar um milhão de elementos, se tiver que andar até o final vai gastar muito tempo.

Quando se programa em Python ou Java não é necessário olhar todos esses detalhes, porque são linguagens de alto nível.

 - O que significam as flechas?
São o conteúdo de um ponteiro que é struct.

```
struct cel {
    int conteudo;
    struct cel seg;
}
typedef struct cel celula;
celula * nova;
nova = malloc(sizeoff(celula));
nova -> conteudo = y;  // jeito diferente de representar
(*nova).conteudo = y; // mesma coisa
````

nova -> seg = p->seg;   // igual
(*nova).seg= (*p).seg; //igual


Porque eu tenho um elemento sem nada no início?
Por dois motivos:
Chama-se de cabeça esse elemento. 

1) Não preciso testar lista vazia toda hora no insere (eficiência), porque sempre tenho a cabeça, nunca está vazio.
2) Não preciso usar ponteiros para conteiros (clareza). Se não tiver cabeça preciso alterar lst que aponta para o início, só que lst é um ponteiro e se eu passar o endereço de um ponteiro, isso vira no insere ponteiro para ponteiro. 


<h5> Ponteiros são muito usados em C </h5>

1) Passagem de variável por referência;
2) Vetor de alocação dinâmico.

Regras:
1) Ponteiro e coisa apontada são diferentes:
```
int *p; 
p = malloc(sizeuf(int));
//são coisas diferentes 
```
2) Não tem sentido ponteiro não inicializado.

Com ponteiros se implementa "Caça ao Tesouro", isto é, Listas Ligadas ou Listas Encadeadas. Detalhes de implementação:
<br/>
A) Insere no começo, porque andar até o fim é ineficiente, logo, se quer 1 2 3, precisa inserir ao contrário 3 2 1.
<br/>
B) Uso cabeça de lista, porque assim se tem duas vantagens:
<br/>
	B1) Não precisa testar lista vazia;
   <br/>
	B2) Não usa ponteiros para ponteiros. 

* & aponta para ponteiro que já é ponteiro 
* int * p = é usado na declaração para dizer que é ponteiro e no acesso para indiretamente mudar o enreço 
* & passa a posição na memória de uma variável (acessar de longe o k)
* (*p). conteudo = p -> conteudo (flecinha serve para trocar (*p))

```
int * p;
int k;
p = & k;
*p = 42;
```

Apesar de C conseguir otimizar código no baixo nível, hoje se têm soluções boas no alto nível:
1) Concorrência em Go, NodeJS
2) iteradores com yield em Python 

```
for k in range (10000000000000000000000000000):
	if k == 42:
		print('achei')
		break
```

3) Algoritmos probabilísticos 

Vamos ver exemplos de resolução de exercícios onde esses detalhes todos em C são importantes:

1) Lista Ligada Vetor para Lista.c (exercício 9)
   Percorro o vetor ao contrário, porque insiro no início da lista

2) Lista Ligada Concatena.c (exercício 10)
   Ando até o final da primeira lista,
   Aponto o final para o inicío da segunda, 
   Devolvo para a memória a cabeça da segunda 
(cabeça é o que declaro com o malloc(função)) 

3) Lista Ligada Libera.c (exercício 18)
   Antes de devolver para a memória preciso salvar o seguinte, senão não sei mais para onde devo ir. 

4) Inversão e Josephus não cai na prova (exercício 19 e 20).

```
Python Referencia 
a = [1, 2 ,3]
b = a
a[0]= 42
id(a) será o mesmo que id(b)


para ser diferente tenho que criar um novo objeto, cópia de a 
b = list(a)

a = [1,2,3]
b = lista(a)
a[0]= 42
a será [42,2,3]
b será [1,2,3]
além disso, id(a) será diferente que id(b)
```


<h5> Problema: quero saber o vetor de distâncias mínimas da cidade origem 3 até as outras cidades. </h5>

Em primeiro lugar precisa-se de uma estrutura de dados para representar o desenho. 
Existem duas possibilidades:

```
1) Matriz de 0's e 1's onde a linha representa a origem e a coluna o destino, e o valor 1 significa tem caminho entre origem e destino.
2) Dicionários, onde a chave é a origem e tenho uma lista de destinos: 
dic[3] = [2,4]
dic [2] = [4]
```

As duas possibilidades tem vantagens e desvantagens. 
Matriz ocupa muito mais espaço, além de ter muitas posições com zero, isto é, inúteis, porém é muito mais rápido perguntar se uma cidade é vizinha da outra.
No dicionário, se uma cidade tiver muitos vizinhos, vou ter que andar até o final até descobrir se é vizinho ou não, matriz é imediata a resposta.

Vamos utilizar matriz, já que o número de cidades não é tão grande e posso até otimizar e guardar o conteúdo em um bit, ja que é zero ou um. 

Para andar pelas cidades precisa-se guardar as seguintes, para a partir delas ir para frente.

Utiliza-se uma estrutura de dados chamada FILA, primeiro que entra, primeiro que sai.
FIFO - First in, First out

Qual a estrutura lógica do programa?

<h3> Filas </h5>

```
fila = origem 
enquanto a fila não estiver vazia 
   retira o primeiro
   verifica se o primeiro tem vizinho
   para cada vizinho calcula a distância
coloca o vizinho na fila
```

Como se garante que a distância é mínima?
Tem-se que guardar as distâmncias num local.
Sugestão: a distância é sempre positiva, inicia-se com -1 para dizer que nunca passou por lá. 

Distâncias em um Rede.py

```
A = [[0, 1, 0, 0, 0, 0], 
     [0, 0, 1, 0, 0, 0],
     [0, 0, 0, 0, 1, 0],
     [0, 0, 1, 0, 1, 0],
     [1, 0, 0, 0, 0, 0],
     [0, 1, 0, 0, 0, 0]]

def Distancias(n, origem):
  d = [-1] * n
  d[origem] = 0
  f = []
  f.append(origem)
  while len(f) > 0:
    x = f.pop(0) #remove o primeiro da fila
    for y in range(n):  #percorre colunas
      if A[x][y] == 1 and d[y] == -1:
      #tem vizinho e é a primeira vez
        d[y] = d[x] + 1
        f.append(y)
  return d

print (Distancias(len(A), 3))
```
Existem problemas muito difícies que se consegue resolver usando estrutura de dados.
1) Define-se uma matriz para representar o desenho, apesar de gastar mais espaço, como se tem poucas cidades, vale a pena, porque é muito mais rápido consultar se é vizinho.
2) Definiu-se uma FILA para guardar as cidades em que vai chegando, assim pode-se ir avançando até onde puder ir. 
3) Com um vetor começando com -1 sinaliza-se que nunca esteve lá, assim é garantido que a distância é mínima. 


<h5> Revisão de Filas </h5>

Viu-se que o problema de Distâncias Mínimas Rede 
A Figura ajuda a entender o problema, porém o computador não consegue processar a figura.
Existem duas possibilidades de Estruturas de Dados para a figura.
1) Matriz, vantagem que testa rápido se é vizinho, gasta um pouco mais de memória, mas o número de cidades não é grande.
2) Dicionário, gasta menos memória, porém é pior para testar se alguém é vizinho , porque preciso percorrer uma lista para saber disso. 

Precisa-se de uma Estrutura para guardar as cidades a medida em que são visitadas. Para isso usa-se uma fila, onde o primeiro que entra é o primeiro que sai. 
Entra elemento na fila com f.append(x).
Sai elemento com f.pop(0), isto é, remove o primeiro, passa zero, porque remove o segundo.

Por último, precisa-se garantir que a distância é mínima, para isso colaca-se -1 no vetor de distância, assim sabe-se que é a primeira vez que chega naquela cidade, se já chegou antes, então o caminho anterior é melhor.

Com essas 3 Estruturas de Dados, o código fica apenas com 12 linhas, isto é, fica mais fácil programar se sabe usar bem Estruturas de Dados.

Apesar de ser um código de 12 linhas e escrito em Python (que é mais simples), náo é um código trivial, porque tem 3 Estruturas de Dados que são bem difíceis de entender.

Em geral, é maus importante a arquitetura do que a linguagem para escalabilidade do seu sistema. 

<h3> Pilha </h3>

O último a ser colocado é o primeiro a ser tratado, como uma pilha de dados. 
{()}  [()]
A expressão é bem formada? 
Usa-se pilha para saber disso.
([{)]} náo é bem formado.

Qual é a lógica?
Tudo o que é abre, significa menino, e coloca-se na pilha.
Tudo o que é fecha, é menina, e ela só pode ver o último que entrou, isto é, no topo da pilha. 
Se o topo for compatível, então deu match, porém se for diferente deu ruim. 
Por último se sobrou menino sozinho na pilha também deu ruim.


<h3> Estrutura de Dados = Algoritmos II </h3>

Programar melhor com DADOS
Para saber que um programa é melhor preciso saber medir a eficiência.
Atenção: não se esqueça que programa eficiente tem menos passos e também ocupa menos memória.
Em geral acaba compensando gastar um pouco mais de espaço para ter maior velocidade.
Exemplo: índice de banco de dados, cabeça de lista ligda, matriz para o problema de rede.

Programas recursivos: funções que se chama a si próprias.

```
def fat(n):
  if n <= 1: return 1 #caso mais simples, sei a resposta
  return n * fat(n-1) #diminuindo o argumento da função
```

Está se fazendo repetições sem while e sem for. Como? no return, isto é usando DADOS.
Nem sempre código recursivo é eficiente. 

```
def fib(n):
  if n<=2: return 1
  return fib(n-1) + fib(n-2)
```

Não é eficiente, porque repete coisa já feita. 
Como melhorar? Usando DADOS!
Duas formas?
1) Usando um dicionário para guardar os valores passados.
2) Usando lru_cache, isto é, a memória do Sistema Operacional para guardar os cálculos já feitos from functools import lru_cache

```
@lru_cache(maxsize = None)
if n<=2: return 1
  return fib(n-1) + fib(n-2)
```
O código acima não repete chamada, pois se estiver na memória já pega. 
Quando coloca o decorador @lru_cache, faz-se um envelope da função fibonacci, onde o Sistema Operacional sabe que deve guardar todas as chamadas e antes de fazer uma nova chamada, verifica se ela se encontra na memória. 

<h5> Vetores em C </h5>

Tem dados contíguos, isto é, um do lado do outro. Isto tem vantagens para grandes movimentações de dados. Porém, para inserir e remover elementos, principalmente no início, é muito ineficiente. Para resolver isso, usa-se Caça ao Tesouro, isto é, pistas que ligam um lugar a outro. No C, pistas são ponteiros.

Em C usa ponteiro para: 
1) Passagem de variáveis numa função por referência. Se tem variáveis locais, que se deseja mudar na função, precisa-se passar o endereço delas.
2) Vetores de aloação dinâmica. Pode-se definir o tamanho do vetor em tempo de execução, isto é, quando o programa já está rodando. Em linguagens estáticas, precisa-se definir na declaração do vetor, o seu tamanho. 

Regras para o uso de ponteiros:
1) Ponteiro e coisa apontada são diferentes.
2) Não tem sentido usar um ponteiro que não inicializa.

A Caça ao Tesuouro é feita assim:

```
struct cel {
  int conteudo;
  struct cel * seg; //ponteiro para o seguinte
}

typedef struct cel celula; //celula = struct cel
celula x;
x.conteudo = 42;
celula *p;
(*p). conteudo = 42; //é a mesma coisa
p -> conteudo = 42; //Em C isto é o mesmo que (*p).conteudo

```

Na lista ligada ou Lista encadeada usa CABEÇA:
1) Evito assim perguntar toda hora se a lista é vazia. 
2) Não uso ponteiros para ponteiros

C é uma linguagem criada para construir o Linux
Logo C é bem baixo nível, isto é, precisa-se ter mais cuidado com detalhes que linguagens de alto nível, como JAVA/Pytjon.

Exemplos:
1) Ao inserir tem-se que fazer isso no ínicio, porque se inserir no final, tem-se que andar até o final. Logo, para ter uma lista 1 2 3, precisa inserir 3 2 1, ao contrário.
2) Quando se busca o mínimo numa lista, precisa-se devolver um ponteiro.
3) Ao devolver todos os elementos de uma lista para a memória, precisa guardar o seguinte *antes* de dar free na célula, pois se der free se perde o seguinte. 
4) Para implementar a inversão de uma lista, precisa-se de 3 ponteiros auxiliares, um para a posição atual, outro para a anterior, e outra para a seguinte.
	Quando se está em uma posição, precisa-se saber o anterior, porque não tem campo de anterior, só seguinte. Na hora em que atualizar o ponteiro atual, para apontar para o anterior, se perde o seguinte!
	Por isso, salva o seguinte, antes de atualizar o atual. Então são 3 ponteiros: atual, anterior e seguinte. 

<h5> Revisão Filas </h5>

Problema de distâncias mínimas numa rede

Usou-se 3 Estruturas de Dados:
1) Precisou-se representar o desenho. Existem duas possibilidades: matriz ou dicionário. A matriz gasta um pouco mais de espaço, mas para perguntar se é vizinho, é muito mais rápido.
2) Usa-se uma FILA para guardar as cidades onde está chegando, assim, na próxima iteração, pode-se avançar para novas cidades.
3) Tem um vetor de distâncias que começa com -1, sinalizando que é a primeira vez que se chega lá. Assim, garante-se que a distância final é mínima.
O código tem apenas doze linhas. Mas não é por ter poucas linhas que ele é fácil, ele tem 3 estruturas de dados, que são mais difícies de entender do que as linhas de código. 
Na vida real, muitas vezes terá um sistema mais eficaz, se escolher a arquitetura bem. Isto é, modelar bem o banco de dados, escolher bem o tipo de banco de dados. 


<h5> Revisão Pilhas </h5>

((){()})

```
Abre parenteses menino fofo
Abre chaves menino pontudo
Fecha parenteses menina fofa
Fecha chaves menina pontuda

Todo menino vai para a pilha.
Quando aparece menina vê o último na pilha, se for compátivel match
Se no final de tudo sobrou menino, também deu ruim
```


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
O oposto também é rápido, se dobra o número de resultados bons a cada passo.


Suponha que precise desenhar, numa folha de papel 128 retângulos.
Existem duas formas básicas:
1) Mede-se largura e comprimento, divida a folha em 128 retângulos, desenhando-se um por um.
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

- Outra ideia:

 Percorrer da esquerda para direita e para cada elementos, verificar o menor que está adiante.
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
 
 Precisa percorrer todos: custa n passos.
 Para cada, precisa verificar o menor: custa n passos.
 Logo, no total custa n*n = n ** 2 passos
 Será que pode melhorar isso: Sim
 Para calcular o menor, tem-se uma função min do Python que é otimizada.
 
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
Na média, inserção é melhor que seleção. O únicp caso em que são ambos no pior caso, é quando se tem um vetor em ordem decrescente. Esse caso é muito raro, então, na média, inserção é melhor que seleção.
Nesse caso só é pior, porque está utilizando uma função do python, min que é otimizada para pegar os menores.

Melhorando isso com a ideia de dividir o mundo em dois:

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

- Melhorar mais ainda:

Quicksort usa sempre um pivô (voluntário).
Divide-se em duas partes, menores que o pivô e maiores que o pivô.
Assim, tem-se o pivô na posição correta. Repete-se o processo para cada metade.
Assim, vai dobrando a cada passo o número de pessoas na posição correta.

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

Pode usar a ideia de dividir o mundo eem dois andando pelos índices do vetor.
Assim, vai dobrando o índice a cada passo para andar para a direita e vai dividindo o índice pela metade a cada passo para andar no final para o começo. 
Essa estrutura é chamada heap.

* heapsort.py 

Usa estrutura do python!

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


<h4> Revisão </h4>
Algoritmos de Ordenação

É bom ver várias formas de fazer um mesmo código.

5 formas diferentes!

2 ruins: inserção e seleção custam n*n ou n ** 2 passos, inserção no pior caso é n * n, porém tem casos bons (números grandes não mexem os anteriores), então na média inserção é melhor que seleção, seleção é sempre ruim, só tem caso pior. Melhora-se usando min, função embutida no python, que usa uma estrutura de dados auxiliar para guardar o menor, sem ter que passar por todos os elementos. 
3 boas: mergesort (divide o vetor em dois), quicksort (divide os elementos em maiores ou menores que um pivô), heapsort (anda muito rápido em passos que vão dobrando no índice).
Mergesort: divide o vetor em dois até ficar do tamanho 1, então junta-se (merge) os vetores até voltar ao original juntant0 = se tem duas fileiras de crianças em ordem, pode-se ir escolhendo a menor entre as duas da ponta de cada fileira. Gasta-se n passos nesse "juntando" porque todo mundo tem que ser comparado e gasta também um espaço igual ao vetor original. Licão: não basta ter um número de passos pequenos, precisa-se gastar pouca memória também, mergesort gasta bastante memória.
Desvantagens: mergesort, apesar de rápido, gasta mais espaço.
Vantagens: as partes do vetor divididas são independentes e pode ser resolvido de forma assíncrona. 

Quicksort: divide em maiores ou menores que um pivô e repete sucessivamente até todos estarem na posição final. O interessante do quicksort é que o número de pessoas na posição final cresce muito mais rápido que mergesort. Quicksort é acumulativo, não só dobra. mas acumula os anteriores.

Total: 1 + 2 + 4 + 8 + 16 + 32 + 64 + 128 + 256 + 512 + 1024

Análise detalhada: Qual é o pir caso? Vetor já ordernado, sempre não vai ninguém para um dos lados, o que resulta que não dobra o número a cada passo, e pior, vai demorar n passos até todo mundo ficar na posição.
Então no total vai gastar n * n, tão ruim quanto inserção e seleção na prática nunca encontra um vetor ordenado. Então na média quicksort é muito bom!

Revisão Geral:

* Funções recursivas (são aquelas que chamam a si próprias). 
Faz repetições sem for e sem while, usando o retorno do dado para fazer a composição final do que quer:
```
def função_recursiva(argumentos):
   if caso mais simples: 
  	retorno valor que sei de antemão
   retorno uma composição diminuindo algum dos argumentos
```
```
def fib(n): 
  if n == 1: return 1
  return n * fat(n-1)
  
def fib (n):
  if n == 1 or n == 2: return 1
  return fib(n-1) + fib(n-2)
```

Fibonacci recursivo acima não é eficiente, porque repete contas já feitas. 
Como resolve essa ineficiência? (repetir cálculos já feitos).
Usando estruturas de dados para guardar os cálculos e não repetir mais.


#Forma1: usando dicionários para guardar o que já fez

```
dic = {}
def fib(n): 
  if n == 1 or n == 2: return 1
  if n not in dic: dic[n] = fib(n-1) + fib(n-2)
  return dic[n]
```

#Forma2: usando o cache do Sistema Operacional

```
from functools import lru_cache
def fib(n):
  if n == 1 or n == 2: return 1
  return fib(n-1) + fib(n-2)
 ```
 
 Nesse exemplo, usa a memória do sistema operacional para guardar os cálculos já feitos.
 O decorador @lru_cache faz um envelope da função, dando super poderes para a função debaixo.
 
 
 
 Ponteirs e Listas Ligadas(Encadeadas)
 Vetores em C tem dados contíguos (um do ladinho do outro). C é uma linguagem de baixo nível (feita para construção de um sistema operacional - Linux). Em C é muito rápido mover grandes áreas de dados, porém para inserir ou remover num vetor, em C, é muito ineficiente, principalmente no início do vetor, porque precisa mover todo mundo para direita ou esquerda, para inserção, remoção. Em C resolve esse problema numa estrutura de dados, chamada lista ligada (caça ao tesouro). Na caça ao tesouro, os locais estão em posições diferentes, o que une um local ao outro são as pistas. 
As pistas em C são chamadas de ponteiros.

Ponteiros em C são usados em muitas coisas: 
1) Passagem de parâmetros por referência, em muitas vezes, preciso alterar uma variável local, em outro escopo, só consegue fazer isso passando o endereço da variável local. 
2) 2) Faz alocação dinâmica de vetor, para definir o tamanho do vetor em tempo de execução.


Ponteiros tem regras de uso:
1) Ponteiro e coisa apontada são diferentes.
2) Não tem sentido usar ponteiro que não foi inicializado.

Agora pode resolver o problema dos vetores, usando a estrutura abaixo: 
```
struct cel {
  int conteudo;
  struct cel *seg;  // pista para o seguinte
}
```

Listas encadeada tem muitos detalhes: 
1) Insere no começo, porque é ineficiente andar até o fim para inserir, por isso se quero uma lista 1 2 3 precisa inserir 3 2 1.
2) Usa cabeça de lista, para duas coisas: // cabeça é um elemento sem conteúdo
   2.1) Não precisa mais testar lista vazia no insere.
   2.2.) Não usa ponteiros para ponteiros, lst é o ínicio da lista, se começa sem cabeça, lst começa com NULL e vai precisar alterar dentro de insere, ora, lst deverá ser passado por endereço, mas o endereço de uma coisa que já ponteiro, virá ponteiro para ponteiro, o que é muiyo difícil de entender e dar manutenção. 
 
<h3> Algoritmos de Força Bruta, Backtracking ou Enumeração </h3>

São Algoritmos que tentam todas as entradas possíveis.
Ex.: Tem-se uma mochila, e um cadeado que foi esquecida a senha, força bruta é tentar todas as combinações 000, 001, 002, ... 999

Algoritmos de Força Bruta são ruins no tempo, porém, muito usados quando não tem mais nenhuma outra solução. 

Porque se estuda algoritmos lentos? Porque muitas vezes não tem outra solução. E além disso tem muita diferença entre cada um dos algoritmos lentos. 

Existem duas famílias:
1) Gerar todos os subconjuntos, custa 2 ** n
2) Gerar todas as permutações, custa n!

São muito diferentes:

2 ** n é lento, porém muito mais lento

```
from math import factorial
n = 1000
2 ** n
len(str(2**n))
len(str(factorial(n)))
```

Exemplos de problemas:
Na corte do Rei Arthur têm 250 damas e 250 cavaleiros. O Rei Arthur passa dois problemas para o Mago Merlim:
1) Casar todos as damas, respeitando suas preferências de cavaleiros.
2) Colocar todos os cavaleiros em torno de uma mesa, chamada de Távola Redonda, sem que briguem. Então os dois vizinhos tem que ser amigos.

Os dois problemas são muito difícies, concretamente, hoje se prova que vamos gastar todo o tempo do universo para resolver, o número de possibilidades é maior que o número de prótons existentes. 

Qual a estratégia de Merlim? Vamos tentar convercer o Rei que não vale a pena tentar resolver os dois problemas. 

1) Se tiver um subconjunto de damas, que tem preferidos em número menor, então é fácil mostrar para  o Rei que não é possível. É preciso de apenas um programa que gere todos os subconjuntos.
2) Será que tem uma forma fácil de convercer o rei sobre o problema dos cavaleiros?
Não é fácil mostrar um exemplo, no caso dos cavaleiros precisa testar todas as 250! permutações para mostrar que não foi possível.

O problema das damas é muito diferente do dos cavaleiros, tem-se uma "obstrução" fácil de achar e mostrar para o Rei. 

Artur Merlim Games é o nome dos dois problemas para estudar complexidade dos algoritmos. 

Algoritmos para gerar todos os subconjuntos e todas as permutações: 
1) Todos os subconjuntos.
```
n = 2
1
12
2

Aumentar de 1 em 1 até chegar a n. Sempre tentar aumentar, se chegar no n, então jogue fora o último e aumente de 1 o anterior. 

n = 3
1
12
123
13
2
23
3

n = 4
1
12
123
1234
124
13
134
14
2
23
234
24
3
34
4
```

2) Todas as permutaçoes:
Fixa o primeiro e repete as permutações com n -1 elementos do nível anterior
```
n = 2
12
21


n = 3
123
132
213
231
312
321


n = 4
1234
1243
1324
1342
1423
1432
2134
2143
2314
2341
2413
2431
3124
3142
3214
3241
3412
3421
4123
4132
4213
4231
4312
4321
```

* Código Merlin.py
```
def enumerações(items):
    n = len(items)
    s = [0]*(n+1)
    k = 0
    while True:
        if s[k] < n:
            s[k+1] = s[k] + 1
            k += 1
        else:
            s[k-1] += 1
            k -= 1
        if k == 0:
            break
        else:
            lista = []
            for j in range(1, k+1):
                lista.append(items[s[j]-1])
            yield lista

def combinações(items, n):
    if n==0: yield []
    else:
        for i in range(len(items)):
            for cc in combinações(items[:i]+items[i+1:],n-1):
                yield [items[i]]+cc

def permutações(items):
    return combinações(items, len(items))
print ('Enumerações')
for p in enumerações(['Jessica', 'Fernanda', 'Pamela', 'Renata']):
    print (p)
x = input('Digite algo...')
print ('Permutações')
for p in permutações(['Adriano','Bruno', 'Diogo', 'Eclis', 'Gabriel', 'Leandro', 'Walber']):
    print (p)
```

* Código EP2.py
```
from Merlin import *

f = open('casamento no.txt')
damas = []
queridos = {}
for linha in f:
  linha = linha.strip().split()
  queridos[linha[0]] = linha[1:]
  damas.append(linha[0])
print (queridos)

for s in enumerações(damas):
  lista = []
  for d in s:
    lista.extend(queridos[d])
  if len(s) > len(set(lista)):
    print ('Não é possível casar todas')
    s = ' e '.join(s)
    lista = ' '.join(set(lista))
    print (f'{s} gostam de {lista}')
    break
else:
  print ('Possível casar todas')
print ()

f = open('cavaleiros no.txt')
amigos = {}
cavaleiros = []
for linha in f:
  linha = linha.strip().split()
  amigos[linha[0]] = linha[1:]
  cavaleiros.append(linha[0])
print (amigos)

for p in permutações(cavaleiros):
  for k in range(len(p)):
    if p[k] not in amigos[p[(k+1)%len(p)]]:
      break
  else:
    print ('Conseguimos uma mesa')
    print (' '.join(p))
    break
else:
  print ('Não é possível mesa')
```

Subconjuntos são 2 ** n elementos fatorial são n! elementos subconjuntos <<< fatorial.

Viu-se 2 problemas do Rei Arthur:
1) Casar 150 damas, respeitando as preferências.
2) Colocar 150 cavalerios em torno de uma mesa redonda, respeitando também as preferências de vizinhos.

O Mago Merlim consegue mostrar para o rei que o problema das damas é impossível de resolver, basta mostrar um subconjunto de damas, com queridos em menor número. Porém, para mostrar que o problema dos cavaleiros é muito difícil, não terá mais jeito que tentar todos, isto é, vai morrer fazendo isso.

<h3> Busca de Palavras </h3>
Mudando de matéria:
Vamos buscar as ocorrências da palavra "algoritmo" dentro da frase "os algoritmos de ordenação".
```
os algoritmos de ordenação
   algoritmo
```

O jeito tradicional é sequencial, pode ser da direita para a esquerda, ou pode ser da esquerda para a direita. Para efeito de comparação, vamos fazer a comparação de trás para frente, isto é, direita para a esquerda, primeira letra da palavra é "o", depois "m".

Os algoritmos de ordenação
algoritmo
Como melhoras o algoritmo sequencial?
Olhando os dados! Qual dado? A palavra que está sendo procurada: "algoritmo"
No algoritmo sequencial dá pulos de 1 em 1, sempre não bate, será que pode dar pulos maiores do que 1, usando a palavra?

```
os algoritmos de ordenação
                      algortimo
aqui foi dado 3 pulos apenas para descobrira mesma ocorrência da palavra. Precisa fazer um pré-processamento da palavra e montar uma tabela "pulos".
```

1) Se a tabela faz parte da palavra, pode pular  o deslocamento dela, para encaixar a próxima letra da frase, com a letra na posição certa na palavra.
2) Se a letra não faz parte, pode pular todo o tamanho da palavra.

Note que a maior parte das vezes, a próxima letra não faz parte da palvra, permitindo pulos gigantes a maior parte das vezes. Também, quando a próxima letra
faz parte, sempre dará pulos maiores que 1, com exceção da última letra da palavra. 

Será que custa muito processar a palavra e criar esta tabela . Em geral a palavra é muito menor que o texto onde está procurando.

Outros contextos onde usa esta ideia:
Busca de vírus na memória toda u HD.
Busca de anomalias genéticas no sequencimento total de DNA da pessoa.

* Algoritmo de Boyer Moore
```
algoritmo
987154321
se a letra não faz parte é 9 também

os algoritmos de ordenação
   algoritimos

```
Por que transforma para tupla? 
Tupla é imutável, então para acessar é muito mais rápido que lista. Depois de montar a tabela, não muda mais, então pode transformar em imutável para ser mais rápido.

```
lista = [1, 2, 3]
tupla = (1, 2, 3)

Acessar:
lista[0]
tupla[0]

Mudar: 
lista[0] = 42
tupla[0] = 42 -> type error -> tupa não muda
```

* Código Boyermoore.py

```
def boyermoore(p, t): 
    m = len(p)
    n = len(t)
    if m > n: return -1 
    pulo = [m for k in range(256)] 
    for k in range(m - 1): pulo[ord(p[k])] = m-k-1
    pulo = tuple(pulo) #imutável é mais rápido
    print (pulo)
    k = m - 1
    while k < n:
        j = m - 1
        i = k
        while j >= 0 and t[i] == p[j]: 
            j -= 1
            i -= 1
        if j == -1: return i + 1
        k += pulo[ord(t[k])] #dou "pulos" > 1
    return -1

texto = 'os algoritmos de ordenação'
palavra = 'algoritmo'
print (boyermoore(palavra, texto))
```
