**Estrutura do Código:**

- **Modo Rigoroso:** O código começa com `'use strict';`, que impõe declarações de variáveis ​​mais rígidas e evita alguns erros silenciosos.
- **Declarações de Variáveis:**
    - `display`: Referencia o elemento HTML com o ID `'display'`, onde a saída da calculadora é mostrada.
    - `numeros`: Uma matriz de todos os elementos HTML com IDs começando com `'tecla'`, representando os botões numéricos da calculadora.
    - `operadores`: Uma matriz de todos os elementos HTML com IDs começando com `'operador'`, representando os botões de operador da calculadora.
    - `novoNumero`: Flag booleana que indica se um novo número está sendo inserido.
    - `operador`: Armazena o operador atualmente selecionado (por exemplo, `+`, `-`, etc.).
    - `numeroAnterior`: Armazena o número anterior usado em um cálculo.
- **Funções Auxiliares:**
    - `operacaoPendente()`: Verifica se um operador está selecionado no momento. Retorna `true` se um operador estiver definido, `false` caso contrário.
    - `calcular()`: Executa o cálculo com base no operador selecionado e nos números armazenados. Atualiza o display com o resultado.
        - Verifica se há uma operação pendente.
        - Analisa o número atual do display, removendo separadores decimais e convertendo para um número.
        - Executa o cálculo usando `eval`.
        - Atualiza o display com o resultado calculado.
    - `atualizarDisplay(texto)`: Atualiza o display da calculadora com o texto fornecido, formatando-o com vírgulas para números grandes (usando `toLocaleString('BR')` para o local do Brasil).
        - Se `novoNumero` for `true`, define o conteúdo do display para o texto fornecido (inicia um novo número).
        - Caso contrário, anexa o texto ao conteúdo existente do display.
        - Define o foco para o botão "igual" para acessibilidade.
- **Ouvintes de Eventos para Botões da Calculadora:**
    - **Números:** Cada botão numérico recebe um ouvinte de evento de clique usando `forEach`. Quando clicado, a função `inserirNumero` atualiza o display com o conteúdo do texto do botão.
    - **Operadores:** Cada botão de operador recebe um ouvinte de evento de clique usando `forEach`. Quando clicado, a função `selecionarOperador` faz o seguinte:
        - Se `novoNumero` for `false` (significando que um número está sendo inserido no momento), ele calcula a operação anterior (usando `calcular`).
        - Define `novoNumero` como `true` para indicar que um novo número está começando.
        - Armazena o conteúdo do texto do operador clicado em `operador`.
        - Analisa o número atual do display e o armazena em `numeroAnterior`.
    - **Igual (`=` ou Enter):** O botão "igual" (ou tecla Enter) aciona a função `ativarIgual`, que calcula o resultado e limpa a variável `operador`.
    - **Limpar Display (`C`):** O botão "Limpar Display" aciona a função `limparDisplay`, que simplesmente limpa o conteúdo do display.
    - **Limpar Cálculo (`Esc`):** A tecla Escape aciona a função `limparCalculo`, que limpa o display, `operador`, define `novoNumero` como `true` e limpa `numeroAnterior`.
    - **Backspace:** A tecla Backspace aciona a função `removerUltimoNumero`, que remove o último caractere do display.
    - **Decimal (`.`):** O botão decimal aciona a função `inserirDecimal`, que verifica se um ponto decimal já existe e, se não, anexa um ponto decimal ao display.

**Mapeamento do Teclado:**

- `mapaTeclado`: Um objeto que mapeia as teclas do teclado para os IDs correspondentes dos botões da calculadora.
- `mapearTeclado(evento)`: Esta função manipula eventos de teclado. Ele verifica se a tecla pressionada é uma tecla válida mapeada em `mapaTeclado`. Se sim, simula um clique no botão da calculadora correspondente usando `document.getElementById(mapaTeclado[tecla]).click()`.
