<h3> Busca de Palavras </h3>
Mudando de matéria:
Vamos buscar as ocorrências da palavra "algoritmo" dentro da frase "os algoritmos de ordenação".
```
os algoritmos de ordenação
   algoritmo
```

O jeito tradicional é sequencial, pode ser da direita para a esquerda, ou pode ser da esquerda para a direita. Para efeito de comparação, vamos fazer a comparação de trás para frente, isto é, direita para a esquerda, primeira letra da palavra é "o", depois "m".
```
Os algoritmos de ordenação
algoritmo
```
Como melhoras o algoritmo sequencial?
Olhando os dados! Qual dado? A palavra que está sendo procurada: "algoritmo"
No algoritmo sequencial dá pulos de 1 em 1, sempre não bate, será que pode dar pulos maiores do que 1, usando a palavra?

```
os algoritmos de ordenação
                      algortimo
*Aqui foi dado 3 pulos apenas para descobrir a mesma ocorrência da palavra. Precisa fazer um pré-processamento da palavra e montar uma tabela "pulos".
```

1) Se a tabela faz parte da palavra, pode pular  o deslocamento dela, para encaixar a próxima letra da frase, com a letra na posição certa na palavra.
2) Se a letra não faz parte, pode pular todo o tamanho da palavra.

Note que a maior parte das vezes, a próxima letra não faz parte da palavra, permitindo pulos gigantes a maior parte das vezes. Também, quando a próxima letra
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
