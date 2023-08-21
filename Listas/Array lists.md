## Array Lists
Array Lists são as listas implementadas com arrays. As arrays lists não podem ser modificadas, se você quiser colocar um novo número deverá criar um novo array.

Arrays em ED para implementação de listas tem algumas consequências positivas e negativas. Estas são pelo fato das operações serem executas de forma rápida e outras lentas.

## Operações em Array Lists
Primeiramente, vamos criar uma função para inicializar nosso Array em GoLang. A capacidade do array pode ser especficada no momento de sua criação.

```
package main

import "fmt"

type ArrayList struct {
    vetor      []int
    qtdade     int
    capacidade int // capacidade atual do vetor
}

func inicializar(capacidade int) *ArrayList {
    // precisamos alocar memória para a estrutura
    lista := &ArrayList{
        vetor:      make([]int, capacidade),
        qtdade:     0,
        capacidade: capacidade,
    }
    return lista
}

func main() {
    capacidade := 10
    lista := inicializar(capacidade)
    fmt.Println(lista)
}

```
