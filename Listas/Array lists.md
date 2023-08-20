## Array Lists
Array Lists são as listas implementadas com arrays. As arrays lists não podem ser modificadas, se você quiser colocar um novo número deverá criar um novo array.

Arrays em ED para implementação de listas tem algumas consequências positivas e negativas. Estas são pelo fato das operações serem executas de forma rápida e outras lentas.

## Operações em Array Lists
Primeiramente, vamos criar uma função para inicializar nosso Array em GoLang. A capacidade do array pode ser especficada no momento de sua criação.

```
package main

import (
	"fmt"
)

type List interface {
	Add(value int)
  AddPos(value int, pos int)
  Update(value int, pos int)
	RemoveLast()
  Remove(pos int)
  Get(pos int) int
	Size() int
}

type ArrayList struct {
	values []int
	inserted  int
}

/**
 * Duplica o vetor.
 */
func (list *ArrayList) doubleArray(){
  curSize := len(list.values)
  doubledValues := make([]int, 2*curSize)
	
  for i := 0; i < curSize; i++ {
    doubledValues[i] = list.values[i]
  }
  list.values = doubledValues  
}

/**
 * Adiciona sempre da esquerda para a direita,
 * após o último elemento inserido anteriormente.
 *
 * Melhor caso: Ômega(1)
 *   Just: não precisa duplicar vetor, nem varrer o vetor
 *         do início para encontrar o endereço a ser Add
 * Pior caso: O(n)
 *   Just: duplicar o vetor requer copiar os elementos
 *         para o novo vetor, causando um custo computa-
 *         cional proporcional ao tamanho do vetor (n)
 */
func (list *ArrayList) Add(val int) {
  //verificar se array está lotado
  if list.inserted >= len(list.values) {
    list.doubleArray();  
  }
	list.values[list.inserted] = val
  list.inserted++
}

/**
 * Adiciona elemento na posição especificada, deslocando
 * os elementos à direita dessa posição.
 *
 * Melhor caso: Ômega(1)
 *   Just: não precisa duplicar vetor, nem varrer o vetor
 *         do início para encontrar o endereço a ser Add
 * Pior caso: O(n)
 *   Just: 1) duplicar o vetor requer copiar os elementos
 *         para o novo vetor, causando um custo computa-
 *         cional proporcional ao tamanho do vetor (n)
 *         2) adicionar no início requer deslocar os n
 *            elementos do vetor para a direita
 */
func (list *ArrayList) AddPos(val int, pos int) {
  //pos eh um valor válido?
  if pos >= 0 && pos <= list.inserted{
    //verificar se array está lotado
    if list.inserted >= len(list.values) {
      list.doubleArray();  
    }

    // começar do início para o fim, para aproveitar
    // a cache pode de fato melhorar o desempenho?
    for i:=list.inserted; i > pos; i-- {
      list.values[i] = list.values[i-1]
    }
    list.values[pos] = val;
    list.inserted++
  }
}

func (list *ArrayList) Size() int {
	return list.inserted
}

func main() {
	fmt.Println("Hello, World!")
}
```
