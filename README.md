## Coursera-Estrutura-Funcionamento-Redes-Computadores

Filtrei as partes que acredito que serão importante para revisão.

## Semana 6

1. Introdução à solução de problemas e o futuro das redes:

   Existem funções integradas para ajudar a evitar alguns desses problemas de redes. Elas são conhecidas como detecção(Error-detection) e recuperação de erros(Error-Recovery).
   
   **Error-detection** é a capacidade de um protocolo ou programa determinar que algo deu errado.
   
   **Error-recovery** é a capacidade de um protocolo ou programa aplicar uma correção.

---------------------------------------------------------------------
2. Verificação da conectividade:

   Caso tenha algum problema de conectividade, como o roteador não esteja conseguindo rotear para um destino ou uma determinada porta esteja inacessível, ou até ser que o TTL de um datagrama IP tenha expirado e até outras situações. O ICMP ou Interactive Control Message Protocol (Protocolo de mensagens de controle interativas), protoco de mensagens de controle da internet, é usado para comunicar esses problemas.
   
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
-------------------------------------------------------------------------------------------------------------------

4. Teste de conectividade de portas

Caso precise verificar se a camada de transporte está funcional, utilize duas ferramentas incrivelmente poderosas:

**netcat (geralmente abreviado para nc) é um utilitário de rede de computadores para leitura e gravação em conexões de rede usando TCP ou UDP. O comando foi projetado para ser um back-end confiável que pode ser usado diretamente ou facilmente conduzido por outros programas e scripts.**

  - Netcat: Para o Linux e Mac OS.

  - Test-NetConnection: Para o Windows.

  Para executar o Netcat utilize o comando **nc** com dois **argumentos obrigatórios, o host e a porta que desejar**. 

  Assim o **nc** tentará estabelecer conexão na porta escolhida daquele host. Se a conexão falhar, o comando será fechado. Se der certo, você verá o cursor piscando, esperando mais dados. Dessa forma você envia dados na **camada de aplicação ao serviço** de escuta do seu teclado.

  Para ter apenas um relatório de status utilize o parâmetro -z, que significa modo de entrada/ saída zero. O parâmetro -v que significa "detalhado", isso tornará a saída do comando mais útil para os nossos olhos. Diferente caso fosse utilizado para um script.

  Agora utilizando o **Test-NetConnection** que é apenas funcional no Windows tem funções semelhantes. Caso você apenas escreva o comando **Test-NetConnection** e o home do host ele funcionará como um **PING** mandando uma mensagem eco de ICMP, mas mostra mais dados, inclusive o protocolo da camada de enlace de dados usado. Ele tem uma vantagem em relação ao Ping. 

  Caso queria utilizar o Test-NetConnection com uma porta específica utiliza o parâmetro "**-port**".

-------------------------------------------------------------------------------------------------------

  5. Desbravando o DNS

   Às vezes pode ser útil fazer essas consultas por conta própria para ver exatamente o que acontece por trás das telas. Por isso utilizamos a ferramenta nslookup. Funciona nos sistemas operacionais Windows, Linux e MacOS.
   - Para utilizar apenas digite nslookup e o nome do host que queira fazer a consulta e o registro A será retornado. Por exemplo nslookup www.google.com.br
     
   <img src=https://github.com/xleofarias/Coursera-Estrutura-Funcionamento-Redes-Computadores/blob/master/Exemplo%20de%20utiliza%C3%A7%C3%A3o%20de%20lookup.png>
   Imagem de exemplo de nslookup</img>

- O lookup também conta com um modelo interativo, para ativa-lo é bem simples apenas digite nslookup e pronto a partir do ">" você pode apenas utilizar parametros e o nome do host que gostaria de consultar. Segue a imagem abaixo.
  
   <img src=https://github.com/xleofarias/Coursera-Estrutura-Funcionamento-Redes-Computadores/blob/master/Exemplo%20de%20utiliza%C3%A7%C3%A3o%20do%20modo%20interativo.png>
   
   Imagem de exemplo do modo interativo</img>

   - Você também pode digitar "set type =" seguido de um tipo de registro de recurso. Por padrão, o nslookup retornará os registros A. Mas com isso, você consegue solicitar explicitamente AAAA ou MX ou até registros de texto associados à máquina. Segue o exemplo da imagem a baixo.

     <img src=https://github.com/xleofarias/Coursera-Estrutura-Funcionamento-Redes-Computadores/blob/master/Exemplo%20de%20utiliza%C3%A7%C3%A3o.png>

     Imagem de exemplo do set type</img>

  - Caso você queira saber tudo bem detelhado pode ta utilizando o comando set debug e depois o nome do host que queira consultar. Segue o exemplo abaixo.
 
    <img src= https://github.com/xleofarias/Coursera-Estrutura-Funcionamento-Redes-Computadores/blob/master/Exemplo%20de%20utiliza%C3%A7%C3%A3o%20do%20set%20debug.png>
    
    Imagem de exemplo de set debug</img>

   - Servidores DNS Públicos

      - É muito importante de um DNS em funcionamente para uma boa rede. Normalmente é apenas necessarios ter um servidor de nome para a comunicação entre dispositivos pela internet. O DNS é necessário para decifrar nomes de máquinas internas. Também tem como o DNS como provedor de serviços. Algumas organizações da Internet usam o que chamamos de servidores DNS públicos, que são servidores de nome configurados para que qualquer um possa usar de graça. O uso desses servidores DNS públicos é uma técnica bem bacana para solucionar diversos problemas de resolução de nome com que você possa se deparar. Algumas pessoas usam esses servidores de nome para todas as necessidades de resolução. A maioria dos servidores DNS públicos é disponibilizado por meio de anycast. Sempre veja se o servidor de nomes é gerenciado por uma empresa de renome e procure usar os servidores de nomes oferecidos pelo seu provedor fora do ambiente de resolução de problemas. A maioria dos servidores DNS públicos também responde a solicitações de eco ICMP, por isso são ótimos para testar a conectividade geral com a Internet usando o ping.
      
   - Registro e expiração de DNS

       - O DNS é um sistema global gerenciado em uma hierarquia de camadas com a ICANN no nível superior. Os nomes de domínio precisam ser globalmente exclusivos para o sistema global funcionar.Para ter tudo organizado já que poderia virar bagunça pelo fato de qualquer pessoa podia dar o nome de um DNS veio a  ideia do registrador, uma organização responsável por atribuir nomes de domínio a outras organizações ou pessoas. No início havia apenas alguns registradores. O mais conhecido era uma empresa chamada Network Solutions Inc. Basicamente, você cria uma conta no registrador, usa a IU web deles para procurar um nome de domínio e ver se ele ainda está disponível, depois você concorda com o preço e com a duração do registro. Depois de ter seu próprio nome de domínio, você pode fazer os servidores de nome do registrador agirem como os servidores de nome autoritativos para o domínio ou você pode configurar próprios servidores para darem autorização. Os nomes de domínio também podem ser transferidos de uma parte a outra e de um registrador a outro, para fazer isso o registrador destinatário gera uma sequência única de caracteres para provar que você detém o domínio e que tem permissão para transferi-lo a alguém. Você insere a sequência em um registro específico das configurações de DNS, normalmente um registro TXT. Quando essa informação for propagada, pode-se confirmar que você detém o domínio e que aprova a transferência. Depois disso, a propriedade passa para o novo proprietário ou registrador. Uma parte importante do registro de nome de domínio é que esses registros têm uma duração específica. É importante ficar de olho no período de expiração dos nomes de domínio porque, depois de expirados, ficam disponíveis para qualquer pessoa que quiser registrá-los.

   - Arquivo de host

     - No inicio os endereços de rede numerados eram correlacionados às palavras por meio de arquivos hosts. Um arquivo host é um arquivo simples que contém um endereço de rede em cada linha, seguido do nome do host que pode ser atribuído a ele. Por exemplo, Uma linha de um arquivo host pode ser: 1.2.3.4 webserver. Isso significa que, no computador em que esse arquivo host está, o usuário pode usar "webserver", em vez de o IP 1.2.3.4. Os arquivos hosts são avaliados pela pilha de rede do próprio sistema operacional. Todos os sistemas operacionais modernos, incluindo os dos celulares e tablets, ainda usam arquivos hosts. Existe um endereço IP especial que é o loopback. Um endereço de loopback é uma forma de enviar tráfego da rede para si mesmo. Enviar tráfego para um endereço de loopback é desviar de toda a infraestrutura de rede, fazendo o tráfego nunca sair do nó.
  
     - O IP de loopback do IPv4 é 127.0.0.1. Ele é configurado em todos os sistemas operacionais modernos com uma entrada em um arquivo host. Quase todos os arquivos hosts existentes terão pelo menos uma linha "127.0.0.1 localhost", provavelmente seguida de ":: 1 localhost", em que "::1" é o endereço de loopback do IPV6. Como o DNS está em todo lugar, os arquivos host não são muito usados mais. Alguns softwares até exigem entradas específicas no arquivo hosts para funcionar corretamente, por mais antiquado que pareça. Por outro lado, os arquivos hosts são uma maneira comum de violação e redirecionamento de tráfego por vírus.

---------------------------------------------------------------------------

6. A nuvem

   - O que é a nuvem?

      - No centro da computação em nuvem, temos o que chamamos de virtualização de hardware. Ela é um conceito central do funcionamento da computação em nuvem. Ela cria a possibilidade de se separar a máquina física da máquina lógica. Com a virtualização, uma única máquina física, chamada de host, executa instâncias virtuais, chamadas de convidados. Um sistema operacional espera poder se comunicar com o hardware em questão de formas específicas. Plataformas de virtualização usam o que chamamos de hipervisor. O hipervisor é o software que executa e gerencia máquinas virtuais e ainda oferece a esses convidados uma plataforma operacional virtual idêntica à do hardware físico. Com a virtualização, um único computador físico pode atuar como host de muitas instâncias virtuais independentes. Cada uma delas tem seu próprio sistema operacional independente e, em muitos aspectos, são idênticas aos sistemas operacionais que rodam no hardware físico.
   
      - Na nuvem podemos usar serviços que ela mesma fornece como, em vez de se preocupar com montar sua própria solução de backup, é só usar a deles. Simples. E se você precisar de um balanceador de carga, é só usar a solução deles. Além disso, se algum hardware quebrar, a empresa transfere sua instância virtual para outra máquina sem você nem notar.Como são servidores e serviços virtuais, você não tem que esperar o hardware físico que comprou chegar.
   
      - Existem tipos de nuvems que irei falar a seguir:
      
         - Nnuvem pública: um grande grupo de máquinas administrado por uma empresa.
         
         - Nuvem privada segue os mesmos princípios, mas é usada totalmente por uma grande corporação e costumam ficar fisicamente nas instalações próprias da empresa.
         
         - Nuvem híbrida, que não é um conceito isolado. É só um termo que descreve casos em que empresas rodam, digamos, suas tecnologias patenteadas mais sigilosas em uma nuvem privada e confiam seus servidores menos sensíveis a uma nuvem pública.
       
   - Tudo como serviço

     Na nuvem existem 3 tipos de serviços:
        - IaaS ou Instraestrutura como Serviço: A ideia por trás da infraestrutura como serviço é que você não deve ter que pensar em construir sua rede ou seus servidores. Basta pagar alguém para prestar esse serviço a você. A infraestrutura como serviço separa a infraestrutura física de que você precisa.
          
        - PaaS ou Plataforma como Serviço: É um subconjunto da computação em nuvem em que uma plataforma é fornecida para que clientes executem seus serviços. Isso basicamente significa que é fornecido um mecanismo de execução para qualquer software que alguém queira executar. Um desenvolvedor web que está criando um novo aplicativo não precisa de um servidor completo com um sistema de arquivos complexo, recursos dedicados e todas essas coisas. Não faz diferença se o servidor é virtual ou não. Ele só precisa de um ambiente para executar o aplicativo web. É isso que a plataforma como serviço oferece. Plataforma como serviço separa as instâncias do servidor de que você precisa.
          
        - SaaS ou Software como Serviço: O software como serviço é uma forma de licenciar o uso do software para outros, mantendo o software hospedado e gerenciado centralmente. O software como serviço se tornou muito popular por alguns motivos. Um ótimo exemplo é o e-mail.

   - Armazenamento na nuvem
        
        - Um sistema de armazenamento em nuvem, o cliente contrata um provedor de armazenamento em nuvem para manter seus dados seguros, acessíveis e disponíveis. Esses dados podem ser simples documentos ou até grandes backups de bancos de dados. O armazenamento em nuvem tem muitos benefícios em ao armazenamento tradicional. Sem ele, você precisa ter o trabalho de gerenciar um array de armazenamento. Também permite duplicar seus dados para vários locais diferentes. Muitos desses provedores são de escala global, dando a chance de você disponibilizar seus dados mais rapidamente a usuários de todo o mundo. Eles oferecem também uma proteção contra perda de dados, para o caso de uma região de armazenamento tiver problemas, para você continuar tendo acesso a seus dados em outra região.

-------------------------------------------------------------------

7. IPv6

   - Endereçamento e sub-redes do IPv6
      
      - IPv6 surgiu em meados dos anos 90, ficava cada vez mais óbvio que faltaria espaço de endereços IPv4 em algum momento. Por isso, um novo protocolo da internet foi desenvolvido, a versão 6 ou IPv6.
      
      - Endereços IPv6 têm 128 bits que seria 2 elevado a 128 geraria um número de 39 dígitos. Existe o nome desse intervalo numérico que é o undecilhão.
      - Os endereços IPv6 geralmente são escrito com 8 grupos de 16 bits cada. Cada um desses grupos é composto de mais quatro números hexadecimais.
      - Tem um método para comprimir um IPv6. Por exemplo o endereço IPv6 2001:4860:4860:0000:0000:0000:0000:8888 comprimido ficaria dessa forma 2001:4860:4860::8888.
         - Regra 1: em um endereço IPv6, uma sequência de quatro zeros (0s) em um hexteto pode ser abreviada como um único zero.
           2001:0404:0001:1000:0000:0000:0EF0:BC00
           2001:0404:0001:1000:0:0:0EF0:BC00 (abreviado com um zero)
         - Regra 2: em um endereço IPv6, os zeros à esquerda em cada hexteto podem ser omitidos, os zero à direita não podem ser omitidos.
           2001:0404:0001:1000:0000:0000:0EF0:BC00
           2001:404:1:1000:0:0:EF0:BC00 (abreviado com zeros à esquerda omitidos)
         - Regra 3: em um endereço IPv6, uma única sequência contínua de quatro ou mais zeros pode ser abreviada como dois pontos em dobro (::). A abreviação de dois pontos em dobro pode ser usada    somente uma vez em um endereço IP.
           2001:0404:0001:1000:0000:0000:0EF0:BC00
           2001:404:1:1000::EF0:BC00 (abreviado com zeros à esquerda omitidos e zeros contínuos substituídos por dois pontos em dobro.
      - Todo endereço IPv6 que começa com 2001:0db8 foi reservado para documentação e ensino ou para livros e cursos. São mais de 18 quintilhões de endereços, muito mais do que todo o espaço de endereços IPv4, reservado só para esse fim.
      - O espaço de endereços IPv6 tem várias outras faixas de endereço reservadas além da faixa para documentação ou para endereços de loopback. Por exemplo, qualquer endereço que comece com FF00:: é usado para multidifusão, que é uma forma de endereçar grupos de hosts de uma só vez.
      - Endereços que começam com FE80:: são usados para unidifusão de link local. Endereços de unidifusão de link local permitem a comunicação de segmentos da rede local e são configurados com base no endereço MAC da máquina. Uma máquina IPv6 usa o endereço de link local para receber a configuração de rede, algo muito parecido com o que acontece no DHCP.
      - No IPv6, o endereço de loopback são 31 zeros e um 1 um no final, o que pode ser condensado para apenas ::1.
      - Os primeiros 64 bits de todo endereço IPv6 é o ID da rede e os segundos 64 bits são o ID de máquina. Isso significa que toda rede IPv6 tem espaço para mais de 9 quintilhões de hosts. Mesmo assim, os engenheiros de rede às vezes dividem a rede por motivos administrativos. A sub-rede IPv6 usa a mesma notação CIDR que você já conhece. Ela é usada para definir uma máscara de sub-rede na parte do ID de rede de um endereço IPv6.

   - Cabeçalhos IPv6
      
      -  O primeiro campo de um cabeçalho IPv6 é o campo de versão. Esse é um campo de 4 bits que define a versão do IP que está em uso.
      -  O próximo campo é chamado de campo da classe de tráfego. Este tem 8 bits e define o tipo de tráfego contido no datagrama IP e permite que cada classe de tráfego receba uma prioridade.
      -  O próximo campo é o identificador de fluxo. Este é um campo de 20 bits usado junto com a classe de tráfego para roteadores tomarem decisões sobre a qualidade do nível de serviço de um datagrama específico.
      -  Depois, temos o campo de tamanho da carga. Esse tem 16 bits e define o tamanho da seção da carga de dados do datagrama.
      -  Depois, temos o campo de próximo cabeçalho. Esse é um conceito exclusivo do IPv6 e pede uma breve explicação. Endereços IPv6 são quatro vezes maiores que endereços IPv4. Isso significa que eles têm mais 1s e 0s, o que quer dizer que demoram mais para transmitir por um link. Para reduzir os problemas com dados adicionais que os endereços IPv6 impõem à rede, o cabeçalho IPv6 foi criado para ser o mais curto possível. Uma maneira de fazer isso era separar todos os campos opcionais do próprio cabeçalho IPv6.
      -  O campo de próximo cabeçalho define o tipo de cabeçalho vem imediatamente após o atual. Esses cabeçalhos adicionais são opcionais, então não são necessários para um datagrama IPv6 completo. Cada um deles contém um campo de próximo cabeçalho e permitem formar uma cadeia de cabeçalhos se houver muita configuração adicional.
      -  Em seguida, temos o campo que chamamos de limite de salto. É um campo de 8 bits com a mesma finalidade do campo TTL dos cabeçalhos IPv4.
      -  Por fim, temos os campos de endereços de origem e destino, cada um com 128 bits. Se o campo próximo cabeçalho especificou outro cabeçalho, ele viria em seguida. Se não, uma carga de dados do mesmo tamanho que o especificado no campo tamanho da carga viria em seguida.

   - Harmonia entre IPv6 e IPv4
      
      - É simplesmente impossível a internet toda e todas as redes conectadas mudarem para IPv6 de uma vez só. Muitos dispositivos antigos que podem nem saber se comunicar com IPv6 ainda precisam de conexão. Então, a única forma de o IPv6 ganhar adoção é desenvolvendo uma forma de os tráfegos de IPv6 e IPv4 coexistirem. Com isso, as organizações fariam a transição individualmente, quando puderem. Um exemplo de como isso pode funcionar é com o que chamamos de espaço de endereços IPv4 mapeados. 
      - As especificações do IPv6 separaram diversos endereços que pode ser diretamente correlacionados a um endereço IPv4. Todo endereço IPv6 que começa com 80 zeros seguidos de 16 uns é entendido como parte do espaço de endereços IPv4 mapeados. Os 32 bits restantes do endereço IPv6 são iguais aos 32 bits do IPv4 que se pretende representar. Isso faz com que o tráfego IPv4 viaje por uma rede IPv6. Mas provavelmente mais importante que isso é o tráfego do IPv6 ter uma forma de viajar pelas redes IPv4. É mais fácil para uma organização mudar para o IPv6 do que as redes do núcleo da internet. Então, apesar de a adoção do IPv6 estar se difundindo, será preciso ter uma forma de viajar pelos remanescentes do IPv4 da espinha dorsal da Internet.
      - A principal forma de se conseguir isso hoje é através de túneis IPv6. O conceito dos túneis IPv6 é bem simples. São servidores de túnel IPv6 em uma das pontas de uma conexão. Esses servidores de túnel IPv6 encapsulam o tráfego IPv6 de entrada dentro de datagramas IPv4 tradicionais. Depois, os datagramas são entregues no espaço de internet IPv4, onde são recebidos por outro servidor de túnel IPv6. Esse servidor desfaz o encapsulamento passa o tráfego IPv6 mais adiante na rede. Junto com tecnologias de túnel IPv6, o conceito de um intermediário de túnel IPv6 também surgiu. São empresas que fornecem pontos finais de encapsulamento IPv6 para você não precisar introduzir mais equipamentos à sua rede.
      - Alguns protocolos que realizaram a migração do IPv4 para IPv6:
         - 6in4:  É um protocolo de encapsulamento que encapsula pacotes IPv6 em links IPv4 especialmente configurados de acordo com as especificações da RFC 4213.
         - Tunnel Setup Protocol (TSP) é um protocolo de controle de rede experimental usado para negociar parâmetros de configuração de túnel IP entre um host de cliente de túnel e um servidor de agente de túnel, os pontos de extremidade de túnel. [1] Um dos principais usos do TSP é nos mecanismos de transição IPv6.
         - Anything In Anything (AYIYA) é um protocolo de rede de computadores para gerenciar protocolos de encapsulamento IP em uso entre redes de protocolo Internet separadas. Ele é mais frequentemente usado para fornecer trânsito IPv6 em um link de rede IPv4 quando a conversão de endereços de rede mascara uma rede privada com um único endereço IP que pode mudar com frequência devido ao provisionamento DHCP por provedores de serviços de Internet.    
