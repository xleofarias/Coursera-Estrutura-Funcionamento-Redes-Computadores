# Coursera-Estrutura-Funcionamento-Redes-Computadores
Estou criando essa documentação por acreditar que sinto que aprendo mais escrevendo.

## Semana 6

1. Introdução à solução de problemas e o futuro das redes
   Existem funções integradas para ajudar a evitar alguns desses problemas de redes. Elas são conhecidas como detecção(Error-detection) e recuperação de erros(Error-Recovery).
   <strong Error-detection> é a capacidade de um protocolo ou programa determinar que algo deu errado.
   <strog Error-recovery> é a capacidade de um protocolo ou programa aplicar uma correção.

2. Verificação da conectividade
   Caso tenha algum problema de conectividade, como o roteador não esteja conseguindo rotear para um destino ou uma determinada porta esteja inacessível, ou até ser que o TTL de um datagrama IP tenha expirado e até outras situações. O ICMP, protoco de mensagens de controle da internet, é usado para comunicar esses problemas.
   
   O <strong ICMP> é usado mais por roteadores ou hosts remotos para se comunicar com a origem da transmissão quando ela falha. Ele tem uma composição simples. Ele tem um cabeçalho com alguns campos e uma seção de dados usada pelo host para descobrir quais das transmissões geraram o erro.
   
   O primeiro campo é o campo "tipo" ou "type", ele tem 8 bits e mostra o tipo de mensagem sendo entregue. Alguns exemplos são destinos inacessíveis ou tempo excedido.
   
   O segundo campo é o "código" ou "code",  ele tem 8 bits e mostra um tipo de mensagem mais especifica do que o "tipo". Por exemplo, para o tipo "destino inacessível", ele mostra códigos que existem para rede de destino inacessível e porta de destino inacessível, por exemplo.
   
   O terceiro campo é a "soma de verificação" ou "Checksum", tem 16 bits que é a soma dos dois anteriores.
   
   O quatro campo é o "resto do cabeçalho" ou "Rest of the header", tem 32 bits e ele é opcional para alguns dos tipos e códigos de enviar mais dados.
   
   O quinto campo é o "carga de dados" ou "Data section" de um pacote ICMP, ela existe para que o destinátario das mensagens saiba qual das transmissões causaram o erro relatado. Ele contém todo o cabeçalho IP e os primeiros 8 bytes da seção de carga de dados do pacote problemático.
   
   O ICMP não foi desenvolvido para interação de humanos, por isso utilizamos a ferramenta PING.
   
   O PING é usado para enviar um tipo especial de mensagem ICMP chamado "Solicitação de eco" ou "Echo Request". Enviar uma mensagem de eco ICMP é fazer o ping dizer para o destino "Você está ai?" Se o destino estiver em funcionamento e puder se comunicar na rede ele retornará uma mensagem de resposta de eco ICMP.
   Para utilizar esse comando basta digita no bash "ping e em seguida [O ip de destino]".
