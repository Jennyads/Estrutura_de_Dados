<h3> Ponteiros </h3>

Vetores em C usam dados contíguos, um dado do ladinho do outro.
Vantagem é movimentar rápido grandes massas de dados.
Desvantagem é inserir ou remover, pois tem que mover todos os elementos da direita. 
Como resolve essa ineficiência?
Usando ponteiros, assim há dados que não são contíguos e para inserir ou remover basta mudar ponteiros. 
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
Regras: assista Binky pointer fun!
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


Porque há um elemento sem nada no início?
Por dois motivos:
Chama-se de cabeça esse elemento. 

1) Não precisa testar lista vazia toda hora no insere (eficiência), porque sempre tenho a cabeça, nunca está vazio.
2) Não precisa usar ponteiros para ponteiros (clareza). Se não tiver cabeça precisa alterar lst que aponta para o início, só que lst é um ponteiro e se passar o endereço de um ponteiro, isso vira no insere ponteiro para ponteiro. 


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

* & aponta para ponteiro que já é ponteiro;
* int * p = é usado na declaração para dizer que é ponteiro e no acesso para indiretamente mudar o enreço;
* & passa a posição na memória de uma variável (acessar de longe o k);
* (*p). conteudo = p -> conteudo (flecinha serve para trocar (*p));

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

Exemplos de resolução de exercícios onde esses detalhes todos em C são importantes:
```
1) Lista Ligada Vetor para Lista.c (exercício 9)
   Percorre o vetor ao contrário, porque insire no início da lista

2) Lista Ligada Concatena.c (exercício 10)
   Anda-se até o final da primeira lista,
   Aponta-se o final para o inicío da segunda, 
   Devolve-se para a memória a cabeça da segunda 
   (cabeça é o que se declara com o malloc(função)) 

3) Lista Ligada Libera.c (exercício 18)
   Antes de devolver para a memória é necessário salvar o seguinte, senão não se sabe mais para onde deve ir. 

4) Inversão e Josephus não cai na prova (exercício 19 e 20).
````

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
<h5> Vetores em C </h5>

Tem dados contíguos, isto é, um do lado do outro. Isto tem vantagens para grandes movimentações de dados. Porém, para inserir e remover elementos, principalmente no início, é muito ineficiente. Para resolver isso, usa-se Caça ao Tesouro, isto é, pistas que ligam um lugar a outro. No C, pistas são ponteiros.

Em C usa ponteiro para: 
1) Passagem de variáveis numa função por referência. Se tem variáveis locais, que se deseja mudar na função, precisa-se passar o endereço delas.
2) Vetores de aloação dinâmica. Pode-se definir o tamanho do vetor em tempo de execução, isto é, quando o programa já está rodando. Em linguagens estáticas, precisa definir na declaração do vetor, o seu tamanho. 

Regras para o uso de ponteiros:
1) Ponteiro e coisa apontada são diferentes.
2) Não tem sentido usar um ponteiro que não inicializa.

A Caça ao Tesouro é feita assim:

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
1) Evita assim perguntar toda hora se a lista é vazia. 
2) Não usa ponteiros para ponteiros.

C é uma linguagem criada para construir o Linux
Logo C é bem baixo nível, isto é, é necessário ter mais cuidado com detalhes que linguagens de alto nível, como JAVA/Pytjon.

Exemplos:
1) Ao inserir tem que fazer isso no ínicio, porque se inserir no final, tem que andar até o final. Logo, para ter uma lista 1 2 3, precisa inserir 3 2 1, ao contrário.
2) Quando se busca o mínimo numa lista, é necessário devolver um ponteiro.
3) Ao devolver todos os elementos de uma lista para a memória, precisa guardar o seguinte *antes* de dar free na célula, pois se der free se perde o seguinte. 
4) Para implementar a inversão de uma lista, precisa-se de 3 ponteiros auxiliares, um para a posição atual, outro para a anterior, e outra para a seguinte.
	Quando se está em uma posição, precisa-se saber o anterior, porque não tem campo de anterior, só seguinte. Na hora em que atualizar o ponteiro atual, para apontar para o anterior, se perde o seguinte!
	Por isso, salva o seguinte, antes de atualizar o atual. Então são 3 ponteiros: atual, anterior e seguinte. 


Revisão geral:

- Ponteiros e Listas Ligadas(Encadeadas):


 Vetores em C tem dados contíguos (um do ladinho do outro). C é uma linguagem de baixo nível (feita para construção de um sistema operacional - Linux). Em C é muito rápido mover grandes áreas de dados, porém para inserir ou remover num vetor, em C, é muito ineficiente, principalmente no início do vetor, porque precisa mover todo mundo para direita ou esquerda, para inserção, remoção. Em C resolve esse problema numa estrutura de dados, chamada lista ligada (caça ao tesouro). Na caça ao tesouro, os locais estão em posições diferentes, o que une um local ao outro são as pistas. 
As pistas em C são chamadas de ponteiros.

Ponteiros em C são usados em muitas coisas: 
1) Passagem de parâmetros por referência, em muitas vezes, precisa alterar uma variável local, em outro escopo, só é possível fazer isso passando o endereço da variável local. 
2) Faz alocação dinâmica de vetor, para definir o tamanho do vetor em tempo de execução.


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
