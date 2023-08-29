# Linked Lists
Linked Lists são listas implementadas com nós e cada nó possui um espaço de memória para armazenar o elemento e outro espaço de memória para armazenar o ponteiro (endereço de memória) para o nó seguinte.

## Operações com LinkedLists
Listas ligadas são compostas por nós. Cada nó tem um valor e um ponteiro para o próximo nó. A primeira coisa que precisamos fazer é criar a estrutura que representa o nó.
```
struct no{
    int val;
    struct no *prox;
};
```
Ao contrário de ArrayLists, em que é preciso inicializar um array, linkedlists podem iniciar com o primeiro nó nulo, pois sempre que for adicionado um novo nó utilizaremos a função malloc para alocarmos espaço na RAM para o novo nó. No entanto, precisamos pelo menos inicializar as variáveis que representará a nossa lista:
```
struct no{
    int val;
    struct no *prox;
};
```



## Referências:
https://github.com/eduardolfalcao/edi/blob/master/conteudos/ArrayLists.md

ATENÇÃO: Este é apenas um material para meu estudo próprio e todos os créditos são destinados ao professor Eduardo Falcão com o link para o trabalho original acima.
