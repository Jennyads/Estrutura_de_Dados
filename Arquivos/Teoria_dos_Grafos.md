
<h3>Teoria dos Grafos</h3>

Têm-se duas formas de representar um grafo:

1) Matriz de zeros e uns, onde um é a ligação entre a linha e a coluna
2) Dicionário, onde tem para um vértice, todos os seus vizinhos

Na prática, em geral, usa-se dicionários
Exemplo: no desenho ao lado se tem
```
G = {}
G[a] = [b,c]
G[b] = [b, c]
G[c] = [a]
G[d] = [a]
```

Cavalo 3-por-3 cai na prova, porque ele tem muitas propriedades raras:

<p align="center">
  <img width="500" src="https://github.com/Jennyads/Estrutura_de_Dados/blob/main/Imagens/cavalo_3_por3.jpeg">
</p>

1) Pode ser desenhado sem cruzar as linhas, o nome desse tipo de grafo é planar. 
É importante desenhar sem cruzar as linhas para verificar outras possibilidades!
2) Aqui é possível resolver o problema das damas, se elas forem as letras, casamento possível: A3, B4, C1, D2.
Assim se configura um emparelhamento máximo.
3) É possível resolver o problema dos CAVALEIROS, se as letras e números forem cavaleiros, então pode colocar em torno de uma mesa redonda: A-3-B-4-C-1-D-2-A (volta para A).
Porque é tão importante guardar esse grafo?
Porque ele é um teste para programas que verificam o problema das damas e dos cavaleiros.


Grafos são compostos por vértices e arestas
Existem duas formas de representar:
1) Matriz de zeros e uns, ocupa muito espaço, porém é rápido para verificar se é vizinho
2) Dicionário, onde para cada vértice se associa uma lista de vizinhos

Apesar do desenho não mudar os vértices e arestas, determinadas formas de desenhar permitem ver propriedades especiais.
Por exemplo, desenhar sem cruzar arestas permite ver emparelhos ou circuitos hamiltonianos.

Existem alguns grafos muito importantes. São importantes porque tem algumas propriedades raras, assim pode usar eles como testes para os algoritmos que foram feitos.

Cavalo 3-por-3
Desenhe um tabuleiro 3x3 e coloque o primeiro vértice no canto superior esquerdo, e faça as arestas e os outros vértices, conforme os movimentos de um cavalo do xadrez. 

<p align="center">
  <img width="500" src="https://github.com/Jennyads/Estrutura_de_Dados/blob/main/Imagens/cavalo_3_por3.jpeg">
</p>

Coloca A B C e D nas pontas do quadrado e 1 2 3 e 4 nos vértices do meio. Pega os números e passa para o lado oposto.

Esse novo desenho não cruza nenhuma linha. Assim fica mais fácil resolver o problema das damas e o problema dos casamentos nele.

Casamento é chamado de Emparelhamento na Teoria dos Grafos, e ele é máximo se não sobra ninguém solteiro.

Mesa de cavaleiros é chamado de Circuito Hamiltoniano na Teoria dos Grafos, e ele começa num vértice, passa por todos os outros, sem repetir, e volta para o ínicio.


Cubo Q3
Os vértices são sequências de 3 bits, onde duas sequências são ligadas se existem apenas um bit de diferença.
```
000 001 010 011 100 101 110 111
Por exemplo 000 é ligado com 001 010 e 100
```
Vendo de cima, e aumentando o quadrado de baixo e diminuindo o quadrado de cima, é possível ver que o grafo é PLANAR, ou seja, não cruza a  linha.
Existem 3 casamentos onde todos os vértices se unem, ou todas as horizontais, ou todas as verticais ou todas as diagonais. 


<p align="center">
  <img width="500" src="https://github.com/Jennyads/Estrutura_de_Dados/blob/main/Imagens/cubo_Q3.jpeg">
</p>


Resolve o problema das damas (Emparelhamento máximo)
```
Diagonais: 000-100, 110-010, 001-101, 111-011
Horizontais: 000-010, 100-110, 101-111, 001-011
Verticais: 000-001, 100-101, 110-111, 010-011

Resolve o problema dos cavaleiros (Circuito Hamiltoniano)
000-100-101-001-011-111-110-010-000
Começa no 000, passa por todos os outros vértices, sem repetir e volta para o ínicio.
```


<h5>Revisão</h5>
Grafos são muito usados na prática e é mais fácil entender a abstração por causa do desenho visual. São compostos de vértices e arestas. Apesar do desenho não alterar um grafo, algumas propriedades são mais facilmente visualizadas em determinadas formas de desenhar.
Por exemplo: num grafo planar, sem cruzar linhas, é mais fácil resolver o problema das damas e o problema dos cavaleiros.

Dois exemplos de grafos são muito importantes:
Cavalo 3-por-3 e Cubo Q3.

Eles são: a) planares b) tem um emparelhamento máximo c) tem um circuito hamiltoniano


Existem duas Estrutura de Dados para um grafo: a) Matriz b) Dicionário

Grafo Bipartido

Pode separar em vértices de cima e vértices de baixo, e *todas* as arestas são de cima para baixo.
É uma forma de desenhar diferente, mais fácil de achar os casamentos do problema das damas.
Essa forma de desenhar é mais fácil para ver os casamentos do que o grafo planar.

<p align="center">
  <img width="500" src="https://github.com/Jennyads/Estrutura_de_Dados/blob/main/bipartido.jpeg">
</p>


Grafo bipartido completo tem todos os vértices de cima ligados com os vértices de baixo, são nomeados K n, m onde n são os vértices de cima e m os vértoces de baixo K2, 3 tem dois vértices em cima e 3 vértices embaixo, todos de cima ligados com todos de baixo. K3, 3 tem 3 vértices em cima e 3 embaixo, todos de cima ligados com todos de baixo.

<p align="center">
  <img width="500" src="https://github.com/Jennyads/Estrutura_de_Dados/blob/main/k2_k3.jpeg">
</p>

Fazer o desenho do E1.25 e descubra o casamento onde todas as máquinas estarão funcionando.
Como achar um casamento que maximize as máquinas funcionando?
Qual a primeira máquina que deve ser escolhida em primeiro lugar?
Escolhe a máquina que tem menos operários capazes de operá-la: máquina 1.

<p align="center">
  <img width="500" src="https://github.com/Jennyads/Estrutura_de_Dados/blob/main/maquinas.jpeg">
</p>

Agora se B opera máquina 1, deve tirar B de todas as máquinas que ele opera. 
Agora a máquina 4 é a que tem menos operários, logo será escolhida.
Tira B de todas as listas.
Agora escolhe a máquina 5, que tem apenas F para operá-la. 
Tira 5 das listas.
Agora escolhe 2 que tem apenas A.
E finalmente 3 casa com o operário C.

Como se torna esse algoritmo num programa?
O primeiro é decidir a Estrutura de Dados!
Escolhendo dicionários:
Existem duas possibilidades: ou coloca a máquina como chave, ou o operário como chave.
Nesse modelo, as máquinas devem estar todas funcionando, logo deve escolher a máquina como chave.

```
G = {}
G[1] = ['B']
G[2] = ['A', 'B', 'E', 'F']
G[3] = ['A', 'B', 'C']
G[4] = ['B', 'E']
G[5] = ['B', 'E', 'F']
```

Grafo planar:

Pode ser redesenhado sem cruzar linhas, não muda o grafo, porém fica mais fácil de ver outras propriedaes do grafo.

Fazer E1.81 e E1.82 p25 do ETG julo.pdf
Dica: K4 é um grafo de 4 vértices todos ligados entre si.

<p align="center">
  <img width="500" src="https://github.com/Jennyads/Estrutura_de_Dados/blob/main/Imagens/k4.jpeg">
</p>

Dica 2: k2, 3 é um grafo bipartido, com 2 vértices em cima e 3 embaixo, todos os de cima ligados com todos os debaixo.

<p align="center">
  <img width="500" src="https://github.com/Jennyads/Estrutura_de_Dados/blob/main/k2_k3.jpeg">
</p>

Note que para mostrar que é planar, basta fazer o desenho sem cruzar linhas
Agora para mostrar que não é planar, precisa chegar no impossível, mostrando passo a passo.

Caminho é aberto, uma sequencia de vértices ligados.
Circuito é fechado, volta para a origem.

Árvore é um grafo sem circuitos!

Isomorfismo = pode-se desenhar o grafo de várias formas, como é o mesmo grafo, esses grafos é chamado de isomorfos.
Mostra-se que dois grafos são iguais (isomorfos) colocando o nome dos vértices e mostrando que tem as mesmas arestas
 
Mostre que os 3 desenhos do exercícios E2.7 são o mesmo grafo, colocando os nomes dos vértices:

<p align="center">
  <img width="500" src="https://github.com/Jennyads/Estrutura_de_Dados/blob/main/Imagens/isomorfos.jpeg">
</p>


Revisão:
Grafos planares: grafos sem cruzar linhas
Mostramos que K4 e K2,3 não são planares, para isso chegou-se num desenho onde não dá mais para tirar arestas sem cruzar com as que já tirou antes.

Grafos isomorfos, tem os mesmos vértices e as mesmas arestas, só o desenho que é diferente.
Como se mostra que dois desenhos são isomorfos? Colocando nome nos vértices, de tal forma que as arestas são as mesmas.
Por exemplo, no exercício E2.7 colocou os nomes dos vértices nos 3 desenhos, de tal forma que são as mesmas ligações

Costuma-se desenhar de outras formas, para ver propriedades do grafo mais facilmente.
Em termos de programação os grafos são os mesmos!

Conjuntos Estáveis, p73 do ETG julho 2012.pdf
Conjunto de vértices, onde não tem nenhuma ligação entre um e outros
Aplicação: têm-se substâncias químicas, algumas reagem com outras e explodem, quer-se colocar numa caixa o maior número de substâncias sem perigo de explosão.
Como fazer um programa para resolver esse problema?
1) Precisa modelar uma Estrutura de Dados com as ligações entre as substâncias.
2) Escolha a substância com menos ligações, isto é de grau mínimo, com menos vizinhos.
3) Tem que excluir a substância escolhida e todos os vizinhos dela.
4) Volta ao passo 2 até acabar o grafo.

Maximum Independent Set é o nome em inglês para maior conjunto estável.
```
G = {}
V = [1, 2, 3, 4, 5, 6, 7]
G[1] = [6, 7]
G[2] = [3, 7]
G[3] = [4, 7, 2]
G[4] = [3, 7]
G[5] = [7]
G[6] = [1, 3]
G[7] = [1, 2, 3, 4, 5]
removed = [False]*8
S = []
aux = []
for i in V: aux.append((i, G[i]))
aux.sort(key=lambda a: len(a[1]))
removed[0] = True
while aux:
    v = aux[0]
    if not removed[v[0]]: S.append(v[0])
    for i in v[1]: removed[i] = True
    aux.pop(0)
print(S)
```

Greedy = guloso = escolhe a melhor opção.

Minimum Degree = grau mínimo.

No filme do Batman com Coringa, dizemos que o Coringa é o Alter Ego do Batman.No mundo dos grafos acontece a mesma coisa, é possível resolver o problema de ver todos os que estão ligados entre si, pelo inverso dele, que é o conjunto estável máximo.

Para resolver o problema dos vértices ligados, monte um grafo complementar e use o programa que calcula o maior conjunto estável.

Cobertura de vértices: suponha um museu, onde se quer colocar guardas que consigam ver todos os corredores.

Emparelhamento Máximo é o problema das damas, isto é, conseguir casamentos que maximizem o número de damas casadas.

<p align="center">
  <img width="500" src="https://github.com/Jennyads/Estrutura_de_Dados/blob/main/Imagens/circuitomaximo.jpeg">
</p>

<p align="center">
  <img width="500" src="https://github.com/Jennyads/Estrutura_de_Dados/blob/main/Imagens/circuitomaximo2.jpeg">
</p>


Circuito Hamiltoniano é o problema dos cavaleiros, isto é, conseguir passar por todos os vértices, sem repetir, e voltar para a origem, página 135 do PDF
Faça o circuito hamiltoniano nos dois grafos do E17.3:
<p align="center">
  <img width="500" src="https://github.com/Jennyads/Estrutura_de_Dados/blob/main/Imagens/reiarthur.jpeg">
</p>

