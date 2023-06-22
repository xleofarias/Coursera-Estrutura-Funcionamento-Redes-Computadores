##Coursera-Estrutura-Funcionamento-Redes-Computadores

Estou criando essa documentação por acreditar que sinto que aprendo mais escrevendo.

## Semana 6

1. Introdução à solução de problemas e o futuro das redes:

   Existem funções integradas para ajudar a evitar alguns desses problemas de redes. Elas são conhecidas como detecção(Error-detection) e recuperação de erros(Error-Recovery).
   
   **Error-detection** é a capacidade de um protocolo ou programa determinar que algo deu errado.
   
   **Error-recovery** é a capacidade de um protocolo ou programa aplicar uma correção.

---------------------------------------------------------------------
2. Verificação da conectividade:

   Caso tenha algum problema de conectividade, como o roteador não esteja conseguindo rotear para um destino ou uma determinada porta esteja inacessível, ou até ser que o TTL de um datagrama IP tenha expirado e até outras situações. O ICMP, protoco de mensagens de controle da internet, é usado para comunicar esses problemas.
   
   O **ICMP** é usado mais por roteadores ou hosts remotos para se comunicar com a origem da transmissão quando ela falha. Ele tem uma composição simples. Ele tem um cabeçalho com alguns campos e uma seção de dados usada pelo host para descobrir quais das transmissões geraram o erro.
   
   - O primeiro campo é o campo "tipo" ou "type", ele tem 8 bits e mostra o tipo de mensagem sendo entregue. Alguns exemplos são destinos inacessíveis ou tempo excedido.
   
   - O segundo campo é o "código" ou "code",  ele tem 8 bits e mostra um tipo de mensagem mais especifica do que o "tipo". Por exemplo, para o tipo "destino inacessível", ele mostra códigos que existem para rede de destino inacessível e porta de destino inacessível, por exemplo.
   
   - O terceiro campo é a "soma de verificação" ou "Checksum", tem 16 bits que é a soma dos dois anteriores.
   
   - O quatro campo é o "resto do cabeçalho" ou "Rest of the header", tem 32 bits e ele é opcional para alguns dos tipos e códigos de enviar mais dados.
   
   - O quinto campo é o "carga de dados" ou "Data section" de um pacote ICMP, ela existe para que o destinátario das mensagens saiba qual das transmissões causaram o erro relatado. Ele contém todo o cabeçalho IP e os primeiros 8 bytes da seção de carga de dados do pacote problemático.
   
   O ICMP não foi desenvolvido para interação de humanos, por isso utilizamos a ferramenta PING.
   
   O **PING** é usado para enviar um tipo especial de mensagem ICMP chamado "Solicitação de eco" ou "Echo Request". Enviar uma mensagem de eco ICMP é fazer o ping dizer para o destino "Você está ai?" Se o destino estiver em funcionamento e puder se comunicar na rede ele retornará uma mensagem de resposta de eco ICMP.
   Para utilizar esse comando basta digita no bash "ping e em seguida [O ip de destino]".

---------------------------------------------------------------------------------------

3. Traceroute

   - O Traceroute é uma ferramenta/comando que permite descobrir os caminhos entre dois nós ou melhor dizendo o caminho que nossa mensagem pecorrer até chegar no ip destino. Então ele passa de IP por IP até chegar no destino, fazendo saltos. Ele faz isso usando o TTL, a cada TTL é um salto. Para cada salto o traceroute envia três pacotes idênticos.
   
   - O traceroute entrega as seguintes informações
      - primeiro o TTL, número de 1 até o destino caso chegue.
      - segundo o IP de cada roteador que ele está saltando para chegar no destino.
      - o tempo que a mensagem demora para se enviada até cada um dos saltos.
      - E o nome de um host caso o traceroute consiga decifrar um.

   - No Linux e Mac OS o traceroute envia pacotes UDP para portas de número muito alto e no Windows ele usa solicitações de eco ICMP por padrão.

   - Existe outras ferramentas semelhantes ao traceroute o "mtr" no Linux/MacOS e "pathping" no Windows. Ambas atuam como traceroutes de longa duração assim o usuario vê melhor como as coisas mudam com o tempo. O "mtr" trabalha em tempo real e atualiza sua saída constantemente com todos os dados agredados atuais sonbre o "traceroute", isso é comparável ao "pathping" que opera por 50 segundos e exibe todos os dados agregados finais de uma vez.

4. Teste de conectividade de portas

Caso precise verificar se a camada de transporte está funcional, utilize duas ferramentas incrivelmente poderosas:

  - Netcat: Para o Linux e Mac OS.

  - Test-NetConnection: Para o Windows.

Para executar o Netcat utilize o comando **nc** com dois **argumentos obrigatórios, o host e a porta que desejar**. 

Assim o **nc** tentará estabelecer conexão na porta escolhida daquele host. Se a conexão falhar, o comando será fechado. Se der certo, você verá o cursor piscando, esperando mais dados. Dessa forma você envia dados na **camada de aplicação ao serviço** de escuta do seu teclado.

Para ter apenas um relatório de status utilize o parâmetro -Z, que significa modo de entrada/ saída zero. O parâmetro -V que significa "detalhado", isso tornará a saída do comando mais útil para os nossos olhos. Diferente caso fosse utilizado para um script.

Agora utilizando o **Test-NetConnection** que é apenas funcional no Windows tem funções semelhantes. Caso você apenas escreva o comando **Test-NetConnection** e o home do host ele funcionará como um **PING** mandando uma mensagem eco de ICMP, mas mostra mais dados, inclusive o protocolo da camada de enlace de dados usado. Ele tem uma vantagem em relação ao Ping. 

Caso queria utilizar o Test-NetConnection com uma porta específica utiliza o parâmetro "**-port**".

