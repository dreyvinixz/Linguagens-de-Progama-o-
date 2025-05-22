# Linguagens-de-Progamação

## Respostas — Linguagens de Programação

### 1. Métodos gerais de implementação de uma linguagem de programação

1. **Compilação**: Tradução completa do código-fonte para código de máquina antes da execução.
2. **Interpretação**: Tradução e execução linha a linha ou instrução a instrução, sem gerar código intermediário.
3. **Implementação Híbrida**: Combinação de compilação e interpretação, geralmente gerando um código intermediário (bytecode).

---

### 2. Compilação mais rápida: Compilador ou Interpretador?

Um **interpretador puro** permite uma **compilação mais rápida**, pois não há processo completo de tradução antes da execução. Entretanto, o desempenho em tempo de execução tende a ser mais lento.

---

### 3. Gargalo de von Neumann

O **gargalo de von Neumann** refere-se à limitação no fluxo de dados entre a CPU e a memória principal, causada pelo uso do mesmo barramento de comunicação.

**Importância**: Limita a velocidade de processamento e influencia diretamente a eficiência dos programas e o design de sistemas computacionais.

---

### 4. Primeira linguagem aprendida — tipo de implementação

Depende da trajetória pessoal. Exemplo: Python — **interpretador puro**; Java — **implementação híbrida**.

---

## PARTE 1 — Linguagens de Programação: Nomes, Vinculações e Escopo

### 1. Diferença entre palavras-chave e palavras reservadas

* **Palavras-chave**: Identificadores com função sintática específica, não podem ser redefinidos. Ex.: `if`, `else`, `while`.
* **Palavras reservadas**: Identificadores reservados, podendo não ter uso atual, mas não podem ser utilizados como nomes de variáveis. Ex.: `goto` em Java.

---

### 2. Atributos fundamentais de uma variável

1. **Nome**
2. **Endereço**
3. **Valor**
4. **Tipo**
5. **Tempo de vida**
6. **Escopo**

---

### 3. Binding

**Binding** é a associação entre uma propriedade e um identificador.

* **Estático**: Feito em tempo de compilação. Ex.: `int x = 5;` em C.
* **Dinâmico**: Feito em tempo de execução. Ex.: `x = 5; x = "texto"` em Python.

---

### 4. Escopo Estático vs. Dinâmico

* **Estático**: Determinado em tempo de compilação, baseado na estrutura do código.
* **Dinâmico**: Determinado em tempo de execução, com base na cadeia de chamadas de funções.

**Mais utilizado**: Escopo **estático** — proporciona maior previsibilidade e facilidade de manutenção.

---

### 5. Exemplo de escopo em C

```c
int globalVar = 10;

void exemplo() {
    static int staticVar = 0;
    int localVar = 5;
}
```

* `globalVar`: escopo global.
* `staticVar`: escopo local persistente.
* `localVar`: escopo local temporário.

---

### 6. Tempo de vida de uma variável

* **Locais**: Existência limitada ao bloco ou função.
* **Globais e Estáticas**: Existência durante toda a execução.
* **Dinâmicas**: Controladas manualmente, via alocação/desalocação.

---

### 7. Tipos de variáveis

* **Estáticas**: Alocadas antes da execução e persistem até o fim.
* **Dinâmicas de pilha**: Alocadas automaticamente durante chamadas de função.
* **Dinâmicas de monte**: Alocadas e desalocadas explicitamente pelo programador.

---

### 8. Constantes nomeadas

São identificadores com valores imutáveis após definição.

**Em C#**:

* `const`: valor conhecido em tempo de compilação.
* `readonly`: valor definido em tempo de execução, mas imutável posteriormente.

Exemplo:

```csharp
const double PI = 3.1415;
readonly int ano;
```

---

## PARTE 2 — Ponteiros e Alocação de Memória

### 1. O que são ponteiros? Por que precisam ser inicializados antes de usados?

**Ponteiros** são variáveis que armazenam o endereço de memória de outra variável. Precisam ser inicializados antes de serem utilizados para evitar acessos a áreas de memória inválidas, o que pode causar comportamentos indefinidos ou falhas na execução.

---

### 2. Exemplo em C usando `malloc`

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *vetor;
    int n = 5;

    vetor = (int*) malloc(n * sizeof(int));

    if (vetor == NULL) {
        printf("Falha na alocação de memória\n");
        return 1;
    }

    for (int i = 0; i < n; i++) {
        vetor[i] = i * 2;
    }

    for (int i = 0; i < n; i++) {
        printf("%d ", vetor[i]);
    }

    free(vetor);
    return 0;
}
```

**Comentário**:

* `malloc` aloca memória para `n` inteiros.
* `free` libera a memória alocada, evitando vazamentos.

---

### 3. Diferenças entre alocação estática, automática e dinâmica

* **Estática**: Definida em tempo de compilação e permanece até o fim do programa. Ex.: `static int x;`
* **Automática**: Criada em tempo de execução, automaticamente destruída ao sair do escopo. Ex.: `int y;`
* **Dinâmica**: Criada e destruída conforme necessidade, usando funções de alocação de memória. Ex.: `malloc`, `calloc`.

---

### 4. Diferença entre `malloc` e `calloc`

* `malloc(size_t size)`: aloca um bloco de memória, mas **não inicializa**.
* `calloc(size_t num, size_t size)`: aloca e **inicializa todos os bytes com zero**.

**Quando usar**:

* Use `malloc` quando não for necessária a inicialização.
* Use `calloc` quando precisar de memória inicializada.

---

### 5. Cópia direta entre estruturas com ponteiros: riscos

Ao copiar diretamente uma estrutura que contém ponteiros, a cópia conterá os **mesmos endereços** (shallow copy), levando à possibilidade de:

* **Modificação não intencional**: Alterações na cópia afetam a original.
* **Problemas de desalocação**: Dupla liberação de memória (`double free`), causando falhas.

**Recomendação**: Para segurança, realizar cópia profunda (**deep copy**), alocando novos blocos de memória e copiando os conteúdos referenciados.

---

## PARTE 3 — Tipos de Dados

### 1. O que são tipos primitivos? Cite 5 tipos primitivos com exemplos de uso.

**Tipos primitivos** são os tipos de dados básicos fornecidos por uma linguagem, sobre os quais outros tipos podem ser construídos.

Exemplos:

* `int` — inteiro: `int idade = 30;`
* `float` — ponto flutuante: `float peso = 65.5;`
* `char` — caractere: `char letra = 'A';`
* `bool` — booleano: `bool ativo = true;`
* `double` — ponto flutuante de maior precisão: `double pi = 3.14159;`

---

### 2. Tipo de subfaixa e enumeração

* **Tipo de subfaixa**: restringe um tipo existente a um subconjunto de seus valores.

Exemplo em Ada:

```ada
type Dias_Semana is range 1 .. 7;
```

* **Enumeração**: define um conjunto nomeado de constantes.

Exemplo em C#:

```csharp
enum Dias { Segunda, Terca, Quarta, Quinta, Sexta };
```

---

### 3. Formas de representação de strings

* **C**: array de caracteres terminado por `\0`.

```c
char str[] = "texto";
```

* **Python**: objeto imutável do tipo `str`.

```python
s = "texto"
```

* **Java**: objeto da classe `String`.

```java
String s = "texto";
```

---

### 4. Arrays com comprimento estático e dinâmico

* **Estático**: tamanho fixo, definido em tempo de compilação.

  * **Vantagens**: simplicidade e eficiência.
  * **Desvantagens**: pouca flexibilidade.

* **Dinâmico**: tamanho variável, definido em tempo de execução.

  * **Vantagens**: flexibilidade.
  * **Desvantagens**: maior complexidade e possível sobrecarga de desempenho.

---

### 5. O que é um array heterogêneo? Quais linguagens suportam?

Array heterogêneo é aquele que permite armazenar elementos de tipos diferentes.

**Exemplos de linguagens que suportam**:

* **Python**: listas permitem múltiplos tipos.

```python
lista = [1, "texto", 3.14]
```

* **JavaScript**: arrays podem conter múltiplos tipos.

```javascript
let arr = [1, "texto", true];
```

* **Ruby**: arrays são heterogêneos por natureza.

Linguagens como C e Java não suportam diretamente arrays heterogêneos; nestes casos, é necessário utilizar ponteiros genéricos ou tipos base como `Object`.

---

## PARTE 4 — Expressões e Atribuições

### 1. Conceito de avaliação em curto-circuito

A **avaliação em curto-circuito** ocorre quando, em uma expressão lógica, a avaliação é interrompida assim que o resultado final é conhecido.

**Exemplo:**

```c
if (ptr != NULL && ptr->valor == 10) {
    // segura: ptr não é NULL
}
```

**Importância:** evita erros como a **desreferenciação de ponteiros nulos**.

---

### 2. Sobrecarga de operadores

**Sobrecarga de operadores** permite redefinir o comportamento de operadores para tipos definidos pelo usuário.

**Utilidade:** melhora a legibilidade e expressividade do código.

**Perigo:** pode causar confusão se o comportamento for inesperado.

**Exemplo em C++:**

```cpp
Complex operator+(const Complex& c);
```

---

### 3. Conversão de tipo: implícita, coerção e casting explícito

* **Conversão implícita:** realizada automaticamente pelo compilador.

```c
int x = 5;
double y = x; // conversão implícita
```

* **Coerção:** conversão automática forçada pelo contexto.

```c
printf("%f", 10); // int coerido para double
```

* **Casting explícito:** realizado pelo programador.

```c
float f = (float) 10 / 3;
```

---

### 4. Efeito colateral funcional

Ocorre quando uma função, além de retornar um valor, **modifica o estado** do programa.

**Exemplo:**

```c
int incremento(int *x) {
    (*x)++;
    return *x;
}

int a = 5;
int b = incremento(&a) + incremento(&a);
```

**Problema:** resultado de `b` depende da ordem de avaliação.

---

### 5. O operador = é "perigoso" em C

Em C, `=` é usado para **atribuição**, mas é frequentemente confundido com `==` (comparação), podendo causar **erros lógicos sutis**.

**Exemplo de erro:**

```c
if (x = 0) {...} // atribuição, não comparação
```

**Alternativa:** Linguagens como **Python** e **Rust** evitam esse problema:

* **Python:** não permite atribuição dentro de expressões condicionais.
* **Rust:** exige `==` e não permite `=` em contexto de comparação.

---
