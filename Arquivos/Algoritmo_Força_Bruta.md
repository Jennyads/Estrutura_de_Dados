<h3> Algoritmos de Força Bruta, Backtracking ou Enumeração </h3>

São Algoritmos que tentam todas as entradas possíveis.
Ex.: Tem-se uma mochila, e um cadeado que foi esquecida a senha, força bruta é tentar todas as combinações 000, 001, 002, ... 999

Algoritmos de Força Bruta são ruins no tempo, porém, muito usados quando não tem mais nenhuma outra solução. 

Porque se estuda algoritmos lentos? Porque muitas vezes não tem outra solução. E além disso tem muita diferença entre cada um dos algoritmos lentos. 

Existem duas famílias:
1) Gerar todos os subconjuntos, custa 2 ** n-1
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

Os dois problemas são muito difícies, concretamente, hoje se prova que iria ser gasto todo o tempo do universo para resolver, o número de possibilidades é maior que o número de prótons existentes. 

Qual a estratégia de Merlim? Tentar convercer o Rei que não vale a pena tentar resolver os dois problemas. 

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
