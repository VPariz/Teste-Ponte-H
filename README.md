# Teste de Acionamento de Motores com Ponte H (STM32 BluePill)

Projeto embarcado para validação de sinais de controle de motores DC e passos utilizando microcontrolador **STM32F103C8T6 (BluePill)** e módulo de potência **Ponte H (L298N / L293D)**.

---

## Objetivo

Gerar sinais digitais em quadratura e pulsos sincronizados (ON/OFF) nas portas GPIO do microcontrolador para testar a comutação dos transistores da Ponte H, verificando a inversão de rotação e acionamento de carga com indicador visual através de LED embarcado (PC13).

---

## Esquema de Conexão Física (Pinout)

Conecte as saídas GPIO da placa BluePill às entradas de controle da Ponte H conforme o mapeamento abaixo:

| Pino STM32 (BluePill) | Entrada da Ponte H | Função de Controle |
| :---: | :---: | :--- |
| **PA0** | **IN4** | Controle Motor B (Sentido Reverso) |
| **PA1** | **IN3** | Controle Motor B (Sentido Direto) |
| **PA2** | **IN2** | Controle Motor A (Sentido Reverso) |
| **PA3** | **IN1** | Controle Motor A (Sentido Direto) |
| **GND** | **GND** | Referência Comum Obrigatória |
| **LED Verde (PC13)** | — | Indicador de ciclo de execução ativo |

> ⚠️ **Importante:** Sempre mantenha o terra (**GND**) da placa STM32 e da fonte de alimentação dos motores conectados no mesmo potencial de referência.

---

## Procedimento de Gravação (Flash Firmware)

1. Conecte o programador **ST-Link V2** aos pinos SWD da BluePill (`SWDIO`, `SWCLK`, `3.3V`, `GND`).
2. Abra o utilitário **STM32CubeProgrammer**.
3. Selecione a interface **ST-LINK** e clique em **Connect**.
4. Carregue o arquivo de firmware compilado (`.elf` ou `.bin`).
5. Execute a operação de **Program / Verify**.
6. Pressione o botão de Reset na placa para iniciar a execução do loop de testes.

---

## Funcionamento do Loop

* O firmware executa um loop infinito comutando os pinos `PA0` a `PA3` em sequência periódica para validação das pontes em H.
* O LED indicador verde embarcado pisca sincronicamente a cada transição de estado, confirmando a saúde do clock e do processamento do microcontrolador.
