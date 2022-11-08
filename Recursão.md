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
		devolve valor que se sabe
	senão:
		faz alguma conta que diminui os argumentos
		devolve valor composto que monta o resultado que se quer
```

No fatorial recursivo não tem while e não tem for.
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

Funções recursivas são poderosas porque "concentram" mais programação em menos linhas. Será que são sempre eficientes?
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
Observação: nem toda função recursiva é eficiente, depende de como é implementada!

Fibonacci: #essa forma não é eficiente porque repete!!!!
```
def fib(n):
    if n <= 2: return 1
    return fib(n-1) + fib(n-2)
print(fib(10))
```

Usando dicionário para armazenar os valores:

```
dic = {}
def fib(n):
    if n<=2: return 1
    if n not in dic: dic[n] = fib(n-1) + fib(n-2)
    return dic[n]
print(fib(100))
```

Obs.: Embora armazenar dados exija mais espaço, evita repetição.


Usando dicionário, guarda-se as respostas já calculadas. Assim não se repete mais e o programa fica muito mais rápido.
Porém usando o dicionário o código fica mais feio. 

Dicionário = estrutura chave-valor.

O jeito de deixar de repetir sem mudar o código é usar bibliotecas.

Com isso, usa a memória do sistema operacional (cache) para guardar os retornos já calculados. Assim, usa-se um decorador do Python,
chamado lru_cache, lru = less results utilized.
O decorador faz um envelope da função Fibonacci e dá super poderes sem mudar o código:

```
from functools import lru_cache
@lru_cache(maxsize=None)
def fib(n):
    print(n)
    if n<=2: return 1
    return fib(n-1) + fib(n-2)
print(fib(100))
```

<h3> Estrutura de Dados = Algoritmos II </h3>

Programar melhor com DADOS
Para saber que um programa é melhor preciso saber medir a eficiência.
Atenção: não se esqueça que programa eficiente tem menos passos e também ocupa menos memória.
Em geral acaba compensando gastar um pouco mais de espaço para ter maior velocidade.
Exemplo: índice de banco de dados, cabeça de lista ligada, matriz para o problema de rede.

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
Quando coloca o decorador @lru_cache que faz um envelope da função fibonacci, onde o Sistema Operacional sabe que deve guardar todas as chamadas e antes de fazer uma nova chamada, verifica se ela se encontra na memória. 


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
