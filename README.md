# Processo Seletivo – Intensivo Maker | IoT

### Vítor Massena dos Santos
### github.com/masssena

## Projeto de Sistema de Monitoramento de Temperatura e Abertura de Porta (SmartCooler / Estufa) | TEMPERATURE Scenario

Este projeto foi desenvolvido em python no simulador Wokwi, executado em virtualização em docker disponibilizado pelo PNAAT, como etapa do processo seletivo da fase LabMaker.

O projeto consiste em uma construção de um dispositivo que verifica duas principais variáveis externas: abertura de porta e temperatura ambiente. O objetivo principal é a análise constante destes fatores que podem afetar o isolamento térmico de um ambiente, como o caso de uma estufa ou um freezer, comunicando com o usuário (por serial) o status e os avisos do sistema. Caso a porta fique aberta por muito tempo, estourando o limite estabelecido de 5 segundos, ou a temperatura aumente além do aceitável determinado em código (3°C), o sistema enviará avisos ao usuário, bem como quando ocorre a normalização das variáveis.

---

### Construção do firmware

Escrito em micropython, o firmware está localizado no *src/main.py* e possui um fluxo simples de loop e determinações por funções.

1. **Primeiramente, o sistema faz a preparação do hardware**, inicializando os componentes físicos, determinando valores iniciais e aguardando que esteja tudo pronto para o seu funcionamento. Essa etapa ocorre tanto na declaração de variáveis quanto na função *setup()*.
2. **Em seguida, o sistema entra no loop principal**, que ocorre em *while True*, onde acontecem as verificações constantes dos periféricos conectados às suas variáveis específicas. Estas verificações ocorrem em funções específicas para cada componente físico do sistema. Para a porta (botão) verifica-se a abertura, e para a temperatura (sensor MPU6050) é lida a temperatura ambiente a cada iteração.
3. **Caso seja percebida alguma variação**, ela é comparada com os limites (de tempo de abertura da porta e de variação de temperatura) estabelecidos e, se os ultrapassarem, flags de alerta serão acionados, que levarão, ao aviso na saída Serial, os alarmes em texto. O sistema, ao verificar o retorno às condições normais do ambiente (simultaneamente das duas variáveis analisadas), avisa ao usuário a normalização do Status.

### Construção do hardware

Foram utilizados os componentes:

1. Microcontrolador ESP32 (board-esp32-devkit-c-v4)
2. Leitor de Temperatura (MPU 6050)
3. Botão

O ESP32 é responsável pelo controle e comunicação serial e entre dispositivos. Para a comunicação Serial, utiliza-se as conexões em TX e RX, enquanto as demais portas definidas no *diagram.json* são utilizadas para comunicação com os outros dispositivos.

### Decisões técnicas

O código, por ser de simples execução, foi construído em um só arquivo e se utiliza do loop principal para previamente estabelecer os valores genéricos e iniciais das variáveis. A utilização de funções foi feita para simplificar o entendimento.

## Resultados Obtidos

O projeto atendeu a todos os requisitos esperados. Todos os testes pessoais e automatizados foram feitos e os resultados foram satisfatórios. O firmware não possui erros evidentes ou de funcionamento e a construção da simulação de hardware está em bom desempenho. Mesmo que, com mais disponibilidade de tempo, fosse possível otimizar tanto o funcionamento do firmware quanto o do hardware, o projeto atingiu bons resultados.
