# Cripto-ALU: Unidade Lógica e Aritmética Criptográfica

Este projeto consiste no desenvolvimento de uma Unidade Lógica e Aritmética (ULA / ALU) especializada em criptografia e descriptografia de dados em tempo real, modelada e simulada utilizando o software **Logisim (versão 2.7.1)**. 

O sistema foi desenhado de forma totalmente modularizada, garantindo a separação limpa entre os blocos de entrada de dados, o núcleo de processamento criptográfico e as saídas textuais.

## 👥 Integrantes do Grupo
* **Guilherme Alves Barbosa** - RA: 082220014
* **Murilo Umbelino Oliveira dos Santos** - RA: 082230013
* **Lucas Junqueira Gonçalves** - RA: 082230029
* **Victor Mendes de Andrade Ferreira** - RA: 082230015

---

## 🛠️ Algoritmos Implementados

O circuito possui um seletor de 2 bits (`SEL[1:0]`) que define qual das quatro operações lógicas ou aritméticas será executada sobre o caractere digitado (8 bits/ASCII):

| SEL[1:0] | Algoritmo | Descrição |
| :---: | :--- | :--- |
| **00** | **XOR** | Operação lógica bit a bit com uma chave configurável (mesmo circuito codifica e decodifica). |
| **01** | **Cifra de César** | Operação aritmética binária pura. Soma uma constante (Encrypt) ou subtrai (Decrypt) via blocos somadores/subtratores de 8 bits. |
| **10** | **Inversão de Bits** | Aplicação do complemento de bits (Porta lógica NOT). |
| **11** | **Permutação de Bits** | Reordenação fixa e cruzada de fiação utilizando Splitters: $[b_7 b_6 b_5 b_4 b_3 b_2 b_1 b_0] \rightarrow [b_0 b_2 b_4 b_6 b_1 b_3 b_5 b_7]$. O modo Decrypt aplica a fiação inversa. |

---

## 🚀 Passo a Passo: Como Usar e Testar o Programa

Siga rigorosamente as instruções abaixo para executar a simulação e verificar a reversibilidade dos algoritmos.

### 1. Preparação do Ambiente
1. Certifique-se de ter o **Logisim 2.7.1** instalado no seu computador.
2. Abra o Logisim, vá em `File -> Open` e selecione o arquivo do circuito: `criptoULA.circ`.
3. Certifique-se de que você está visualizando o circuito principal dando um duplo clique em **`main`** na árvore de circuitos do painel esquerdo.

### 2. Ativação do Clock Automático
Para que o Teclado (Keyboard) e a Tela (TTY) funcionem de forma sincronizada através do circuito de pulso implementado:
1. No menu superior, clique em **Simulate** (Simulação).
2. Clique em **Ticks Enabled** (Habilitar Pulsos de Clock) ou use o atalho **Ctrl + K**.
3. (Opcional) No mesmo menu, vá em **Tick Frequency** e configure para **4 Hz** ou **8 Hz** para respostas mais rápidas.

### 3. Configurando as Chaves Estáticas
Antes de digitar, defina os parâmetros nos pinos de entrada localizados no circuito `main`:
* **Chave do XOR / Deslocamento de César:** Altere os pinos de entrada binária de 8 bits para definir a chave (Ex: `00001111` para XOR ou `00000011` para deslocamento de 3 posições no César).
* **Pino CryptDecrypt (Modo):** Deixe em **0** para Criptografar (Encrypt) ou mude para **1** para Descriptografar (Decrypt).

### 4. Digitação e Execução do Teste
1. Selecione a ferramenta de interação **Poke Tool** (ícone da Mãozinha 👆 no canto superior esquerdo).
2. Clique uma vez bem no centro do componente **Keyboard** (Teclado) para ativá-lo. Uma pequena barra vertical (cursor) aparecerá no teclado.
3. Comece a digitar as letras utilizando o teclado físico do seu computador.
4. **O que observar:**
   * O texto original digitado fluirá pelo circuito.
   * O display **TTY de Saída** imprimirá imediatamente o caractere já processado de acordo com o algoritmo selecionado nas chaves `SEL`.

---

## 🧪 Roteiro Prático de Teste (Exemplo: Palavra "Gemini")

Para validar o funcionamento completo e demonstrar a reversibilidade exigida, configure a chave de deslocamento do César como **3** e a chave do XOR como **0x0F**, coloque o pino `CryptDecrypt` em **0** (Encrypt), mude o seletor `SEL` e digite `Gemini`:

* **Modo XOR (`SEL=00`):** O TTY exibirá o texto codificado `Hjbfaf`. 
  * *Para reverter:* Mude `CryptDecrypt` para **1**, clique no Teclado e digite `Hjbfaf`. O TTY restaurará `Gemini`.
* **Modo César (`SEL=01`):** O TTY exibirá o texto codificado `Jhplql`.
  * *Para reverter:* Mude `CryptDecrypt` para **1**, clique no Teclado e digite `Jhplql`. O TTY restaurará `Gemini`.
* **Modo Permutação (`SEL=11`):** O TTY exibirá o texto embaralhado `XRV ^`.
  * *Para reverter:* Mude `CryptDecrypt` para **1**, clique no Teclado e digite o conteúdo embaralhado para ver `Gemini` reaparecer no display.

---
