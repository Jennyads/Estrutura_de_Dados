
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
