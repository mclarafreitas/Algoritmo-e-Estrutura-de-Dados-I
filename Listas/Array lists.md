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
Sobre a escolha de capacidade, se for escolhido um valor enorme, podemos desperdiçar memória. Por outro lado, se escolhermos valores menores que desperdicem menos memórias, se em algum momento a lista ficar totalmente preenchida, será necessário a criação de um novo array maior que o anterior que causaria mais processamento.

## Inserção no fim da lista
Arrays instancionados não mudam de tamanho naturalmente. Portanto, sempre que o array estiver totalmente preenchido, uma nova inserção irá requerer a criação de um novo array com maior capacidade, ou uma realocação que aumente a capacidade do array. Isto requer que os elementos previamente inseridos no array original sejam copiador para este novo array.

A seguir é apresentado uma animação que ilustra um ArrayList sendo inicilizado e utilizado além da sua capacidade, forçando a alocação de um novo array. Em seguida, são apresentadas as implementações das funções de duplicar capacidade e inserir elemento no fim.
![image](https://github.com/mclarafreitas/Algoritmo-e-Estrutura-de-Dados-I/assets/62397977/086fe917-effa-4cd2-a744-ea8745f81446)

```
package main

type ArrayList struct {
    vetor     []int
    qtdade    int
    capacidade int
}

func inicializar(capacidade int) *ArrayList {
    lista := &ArrayList{}
    lista.vetor = make([]int, capacidade)
    lista.qtdade = 0
    lista.capacidade = capacidade
    return lista
}

func duplicarCapacidade(lista *ArrayList) {
    novaCapacidade := 2 * lista.capacidade
    novoVetor := make([]int, novaCapacidade)
    copy(novoVetor, lista.vetor)
    lista.vetor = novoVetor
    lista.capacidade = novaCapacidade
}

func inserirElementoNoFim(lista *ArrayList, valor int) {
    if lista.qtdade == lista.capacidade {
        duplicarCapacidade(lista)
    }
    lista.vetor[lista.qtdade] = valor
    lista.qtdade++
}

func main() {
    capacidade := 10
    lista := inicializar(capacidade)

    // Exemplo de uso das funções
    inserirElementoNoFim(lista, 42)
}

```
