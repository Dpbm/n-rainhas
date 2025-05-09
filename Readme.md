# Resolvendo o problema de local optima - NRainhas

Durante nossas aulas de Inteligência artificial, estávamos estudando sobre algoritmos de busca, mais precisamente o algoritmo de busca informada `Hill Climbing`. Para aprender sobre esse algoritmo, o implementamos para resolver o problema das `N-Rainhas`. Vimos que este é um algoritmo muito bom para resolver o problema rapidamente, contudo este se mostra como muito propenso a ficar estagnado no ótimo local.

Devido a isso, nosso professor [João Ricardo Favan](https://scholar.google.com.br/citations?user=fm6GR6YAAAAJ) nos deu o desafio de encontrar uma maneira de diminuir as chances do algoritmo empacar no ótimo local, e é por isso que estou aqui.

Neste repositório mostrarei a solução que nós encontramos e também o código que foi usado.


## Pensando no problema

Na implementação atual feita pelo nosso professor:

1. geramos um tabuleiro $nxn$ com as rainhas
2. calculamos o total de ataques
3. verificamos se o total de ataques alcançou o mínimo que queríamos (total de $0$ ataques)\
    3.1. caso tenha alcançado, paramos aqui (global optima encontrado)
4. como não encontramos uma solução ótima, movemos uma rainha aleatoriamente e voltamos para 2.


----

Nesse caso do problema das `NRainhas`, poderíamos pensar em uma representação como esta:

![representação gráfica](./assets/nrainhas-grafico.png)

Pelo grafico, podemos ver que cada configuracao do tabuleiro $x$ gera um numero de ataques $y$, ou seja $f(x)=y$.

Como nosso objetivo nas `NRainhas` é fazer com que nenhuma rainha seja atacada, poderemos ter diversas configurações que são consideradas gloabal optima.

Dessa forma, nosso problema não necessariamente possui um local optima, mas pela natureza da implementação, não é garantido que ele encontre algum dessas soluções globais. Sendo assim, o algoritmo pode muitas vezes enroscar em um ponto da subida da colina e nunca conseguir chegar de fato ao topo.


## Soluções

Aqui iremos propor 3 soluções possíveis para esse caso. 


### Solução 1 - Remover o passo aleatório

Uma vez que a implementação faz com que o próximo passo seja randômico, não temos a certeza de que o espaço de configurações seja devidamente explorado. Sendo assim, mesmo que executado $10000$ de vezes, ainda há uma pequena probabilidade de não encontrar o ponto máximo.

Para resolver isso, podemos movimentar as rainhas de uma forma mais coordenada. Podemos fazer com que cada rainha mova para a esquerda ou direita baseando-se na quantidade de ataques que cada posição gera, escolhendo a posição com menor número de ataques.

Mesmo sendo uma solução interessante para o problema, podemos ter configurações que se não conseguem evoluir. Para isso podemos tomar dois caminhos:

1. verificamos se a configuração é a mesma da anterior. Caso seja, movemos uma rainha aleatoriamente
2. verificamos se a posição do rainha atual é a mesma da anterior. Caso seja, movemos a rainha para a direita $n$ casas.

Dessa forma, podemos fazer com que o algoritmo sempre tenha algo a melhorar, aumentando as chances de encontrar a solução.

