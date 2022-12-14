<h5> Problema: quero saber o vetor de distâncias mínimas da cidade origem 3 até as outras cidades. </h5>


![alt text](https://github.com/Jennyads/Estrutura_de_Dados/blob/main/Imagens/matriz.jpeg)

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
No dicionário, se uma cidade tiver muitos vizinhos, vai ter que andar até o final até descobrir se é vizinho ou não, matriz é imediata a resposta.

Vamos utilizar matriz, já que o número de cidades não é tão grande e é possível otimizar e guardar o conteúdo em um bit, ja que é zero ou um. 

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
Tem-se que guardar as distâncias num local.
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
2) Dicionário, gasta menos memória, porém é pior para testar se alguém é vizinho , porque precisa percorrer uma lista para saber disso. 

Precisa-se de uma Estrutura para guardar as cidades a medida em que são visitadas. Para isso usa-se uma fila, onde o primeiro que entra é o primeiro que sai. 
Entra elemento na fila com f.append(x).
Sai elemento com f.pop(0), isto é, remove o primeiro, passa zero, porque remove o segundo.

Por último, precisa-se garantir que a distância é mínima, para isso coloca-se -1 no vetor de distância, assim sabe-se que é a primeira vez que chega naquela cidade, se já chegou antes, então o caminho anterior é melhor.

Com essas 3 Estruturas de Dados, o código fica apenas com 12 linhas, isto é, fica mais fácil programar se saber usar bem Estruturas de Dados.

Apesar de ser um código de 12 linhas e escrito em Python (que é mais simples), náo é um código trivial, porque tem 3 Estruturas de Dados que são bem difíceis de entender.

Em geral, é maus importante a arquitetura do que a linguagem para escalabilidade do seu sistema. 


<h5> Revisão Filas </h5>

Problema de distâncias mínimas numa rede

Usou-se 3 Estruturas de Dados:
1) Precisou-se representar o desenho. Existem duas possibilidades: matriz ou dicionário. A matriz gasta um pouco mais de espaço, mas para perguntar se é vizinho, é muito mais rápido.
2) Usa-se uma FILA para guardar as cidades onde está chegando, assim, na próxima iteração, pode-se avançar para novas cidades.
3) Tem um vetor de distâncias que começa com -1, sinalizando que é a primeira vez que se chega lá. Assim, garante-se que a distância final é mínima.
O código tem apenas doze linhas. Mas não é por ter poucas linhas que ele é fácil, ele tem 3 estruturas de dados, que são mais difícies de entender do que as linhas de código. 
Na vida real, muitas vezes terá um sistema mais eficaz, se escolher a arquitetura bem. Isto é, modelar bem o banco de dados, escolher bem o tipo de banco de dados. 

