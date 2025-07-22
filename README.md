# embarcados-2025

# Projeto: Chrome Dino Game para ARM Cortex-A9

## Visão Geral

Este projeto implementa uma versão simplificada do popular jogo "Chrome Dino Game" (também conhecido como "T-Rex Run") para a plataforma ARM Cortex-A9, especificamente para a placa DE10-Standard. O jogo simula a experiência clássica onde um dinossauro deve pular sobre obstáculos (cactos) e desviar de inimigos (pássaros) em um cenário que se move continuamente. O objetivo é alcançar a maior pontuação possível.

## Funcionalidades

* **Gráficos Simplificados:** Utiliza sprites bitmap para o dinossauro, cactos e pássaros.
* **Movimentação do Dinossauro:** O dinossauro pode pular para evitar obstáculos.
* **Geração de Obstáculos:** Cactos e pássaros aparecem aleatoriamente no caminho.
* **Detecção de Colisão:** O jogo detecta colisões entre o dinossauro e os obstáculos.
* **Sistema de Pontuação:** A pontuação é incrementada à medida que o jogo avança.
* **Telas de Início e Fim de Jogo:** Apresenta uma tela de início e uma tela de "Game Over".
* **Controle de Entrada:** Controlado via entradas do hardware (provavelmente botões da placa DE10-Standard, como KEY0 para pular e KEY1 para reiniciar).

## Requisitos de Hardware

* Placa de desenvolvimento **Intel DE10-Standard** (com processador ARM Cortex-A9).
* Monitor ou tela conectada à saída de vídeo da placa.
* Teclado (para depuração via Semihosting, se configurado) ou botões integrados na placa para controle do jogo.

## Requisitos de Software

* **Intel FPGA Monitor Program** ou ambiente de desenvolvimento compatível com ARM Cortex-A9 para compilação e deployment.
* **GNU ARM Embedded Toolchain** (ou similar) para compilação cruzada.
* Sistema operacional (Windows/Linux) com drivers e ferramentas para a placa DE10-Standard.

## Estrutura do Projeto

Os principais arquivos do projeto são:

* `video.c`: Contém a lógica principal do jogo, funções de renderização gráfica (desenho de sprites, caixas, texto), movimentação do dinossauro, geração de obstáculos, detecção de colisão e gerenciamento do estado do jogo (início, execução, game over).
* `dino_sprite.h`: Arquivo de cabeçalho contendo os dados bitmap do sprite do dinossauro.
* `cactus_sprite.h`: Arquivo de cabeçalho contendo os dados bitmap do sprite dos cactos.
* `bird_sprite.h`: Arquivo de cabeçalho contendo os dados bitmap do sprite dos pássaros.
* `address_map_arm.h`: Define os endereços de memória para os periféricos da placa ARM (como display de vídeo, LEDs, botões, etc.), essenciais para a interação com o hardware.
* `makefile`: O arquivo makefile para automatizar o processo de compilação do código-fonte (`.c`) em um executável (`.axf`) para a arquitetura ARM.
* `Dino.amp`: Arquivo de configuração do Intel FPGA Monitor Program, que descreve o projeto, os arquivos fonte, as opções de compilação e como o programa deve ser carregado na placa.
* `video.axf`: O arquivo executável binário gerado após a compilação, pronto para ser carregado e executado no processador ARM Cortex-A9 da placa.
* `video.axf.objdump`: O disassembly do arquivo executável, útil para depuração e análise do código de máquina.

## Como Compilar e Rodar

1.  **Configure o Ambiente:** Certifique-se de que o Intel FPGA Monitor Program e o GNU ARM Embedded Toolchain estão instalados e configurados corretamente em seu sistema.
2.  **Navegue até o Diretório:** Abra um terminal ou prompt de comando e navegue até o diretório raiz do projeto onde o `makefile` está localizado.
3.  **Compilar o Projeto:** Execute o comando `make` no terminal. Isso usará o `makefile` para compilar os arquivos `.c` e criar o executável `video.axf`.
    ```bash
    make
    ```
4.  **Carregar na Placa:**
    * Conecte sua placa DE10-Standard ao computador via USB Blaster.
    * Abra o Intel FPGA Monitor Program.
    * Carregue o arquivo `Dino.amp` no Monitor Program.
    * No Monitor Program, use a opção para carregar e executar o `video.axf` na placa ARM Cortex-A9. O Monitor Program geralmente cuida de reiniciar o processador e iniciar a execução.

## Jogabilidade

* **Iniciar o Jogo:** Na tela inicial, pressione o botão **KEY1** (ou o botão configurado para iniciar/reiniciar) na sua placa DE10-Standard.
* **Pular:** Para fazer o dinossauro pular e evitar os obstáculos (cactos e pássaros), pressione o botão **KEY0** (ou o botão configurado para pular).
* **Game Over:** O jogo termina se o dinossauro colidir com um cacto ou um pássaro.
* **Reiniciar:** Após o "Game Over", pressione **KEY1** novamente para reiniciar o jogo.

