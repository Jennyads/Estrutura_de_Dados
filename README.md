
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

FILAS

Problema de distâncias mínimas numa rede

Usou-se 3 Estruturas de Dados:
1) Precisou-se representar o desenho. Existem duas possibilidades: matriz ou dicionário. A matriz gasta um pouco mais de espaço, mas para perguntar se é vizinho, é muito mais rápido.
2) Usa-se uma FILA para guardar as cidades onde está chegando, assim, na próxima iteração, pode-se avançar para novas cidades.
3) Tem um vetor de distâncias que começa com -1, sinalizando que é a primeira vez que se chega lá. Assim, garante-se que a distância final é mínima.
O código tem apenas doze linhas. Mas não é por ter poucas linhas que ele é fácil, ele tem 3 estruturas de dados, que são mais difícies de entender do que as linhas de código. 
Na vida real, muitas vezes terá um sistema mais eficaz, se escolher a arquitetura bem. Isto é, modelar bem o banco de dados, escolher bem o tipo de banco de dados. 

Pilhas 

((){()})

Abre parenteses menino fofo
Abre chaves menino pontudo
Fecha parenteses menina fofa
Fecha chaves menina pontuda

Todo menino vai para a pilha.
Quando aparece menina vê o último na pilha, se for compátivel match
Se no final de tudo sobrou menino, também deu ruim


<h5> Busca Binária </h5>


def dec2bin(n):
    p = []
    while n != 0:
        p.append(n%2)
        n =n//2
    while len(p) > 0:
        print(p.pop(), end = '')

dec2bin(18)



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


Suponha que precise desenhar, numa folha de papel 128 retângulos
Existem duas formas básicas:
1) Mede-se largura e comprimento, divida a folha em 128 retângulos, desenhando-se um por um.
2) Pode-se dobrar a folha no meio, e depois dobrar novamente no meio e assim pr diante em 7 passos tem-se 128 retângulos.

Se tem uma lista telefonica (áginas amarelas) e se deseja descobrir um telefone, abre-se no meio para ir mais rápido. Essa é a mesma ideia de busca binária!

Viu-se busca binária num vetor ordenado, porém na vida real não encontra-se vetores ordenados, então é necessário ordenar o vetor antes de usar busca binária.
Para ordenar existem vários algoritmos. Os que funcionam rápido usam IDEIA da busca binária, de dividir o mundo em dois.

5 algoritmos de ordenação: 
2 ruins: selação e inserção
3 bons: mergesort, quicksort e heapsort










