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
### Outra forma de aumentar a capacidade
O professor passou um exemplo com a linguagem C na qual provê ferramentar paga gereciamento rigosos de memória RAM. A forma mais trivial de aumentar o tamanho de um array é alocando um novo array com maior capacidade e copiando os elementos do array antigo para o novo array, como mostrado acima. Agora vamos usar a função realloc, que é capaz de aumentar o tamanho do bloco de memória alocado, movendo-o para outra posição na memória quando for necessário. Porém, em GoLang não temos essa função então perguntei ao ChatGPT o que seria equivalente a isso e obtive essa resposta:
```
package main

import "unsafe"

type arraylist struct {
    vetor      *int
    capacidade int
}

func duplicarCapacidade(lista *arraylist) {
    novaCapacidade := 2 * lista.capacidade
    novoVetor := make([]int, novaCapacidade)
    copy(novoVetor, lista.vetor)

    lista.vetor = (*int)(unsafe.Pointer(&novoVetor[0]))
    lista.capacidade = novaCapacidade
}

func main() {
    // Exemplo de uso
    minhaLista := arraylist{
        vetor:      make([]int, 5),
        capacidade: 5,
    }

    duplicarCapacidade(&minhaLista)
}
Observe que, em Go, não há uma função realloc equivalente como em C/C++. Portanto, a abordagem usada aqui é criar um novo slice com a capacidade duplicada e copiar os elementos do slice antigo para o novo slice. A conversão do ponteiro do novo slice para *int é feita usando o pacote unsafe.

Lembre-se de que em Go, a manipulação direta de ponteiros e o uso do pacote unsafe devem ser evitados sempre que possível, pois a linguagem prioriza a segurança e a robustez. O exemplo fornecido é apenas uma demonstração de como algo semelhante ao realloc poderia ser alcançado em Go, mas em muitos casos, existem abordagens mais seguras e Go-friendly para alcançar o mesmo resultado.
```
## Obtenção
Os arrays naturalmente nos dão a opção de obter um elemento em uma posição específica usando o índice. O único cuidado que devemos ter é verificar se aquele índice é válido.

Note também que apesar da lista ter uma capacidade específica, ela pode ter uma quantidade de elementos menor do que esta capacidade. Na ilustriação a seguir, a capacidade usada como exemplo é 10. Então, precisamor ter uma variável para controlar quantos elementos já foram inseridos na lista, de forma a usar este valor para saber se existe algum elemento em uma poisição específica.

A seguir são apresentadas uma animação que ilustra uma Arraylist sendo inicializada, além da obtenção do elemnto no índice 2 do Array List e a implementação da função obter elemento.
![image](https://github.com/mclarafreitas/Algoritmo-e-Estrutura-de-Dados-I/assets/62397977/856e0151-7998-4a3b-9568-e0bf50cb3993)

```
package main

type arraylist struct {
    vetor  []int
    qtdade int
}

func obterElementoEmPosicao(lista *arraylist, posicao int) int {
    if posicao >= 0 && posicao < lista.qtdade {
        return lista.vetor[posicao]
    }
    // Se a posição estiver fora dos limites válidos, você pode retornar um valor padrão ou lidar com o erro de alguma outra forma.
    return -1 // Por exemplo, retornando -1 para indicar um erro.
}

func main() {
    // Exemplo de uso
    minhaLista := arraylist{
        vetor:  []int{10, 20, 30, 40, 50},
        qtdade: 5,
    }

    elemento := obterElementoEmPosicao(&minhaLista, 2)
    if elemento != -1 {
        println("Elemento na posição 2:", elemento)
    } else {
        println("Posição inválida.")
    }
}

```
## Inserção em local específico da lista

