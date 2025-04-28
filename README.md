# Sistemas Operacionais

## Conceitos Básicos
- Hardware: Composto por circuitos eletrônicos (processadores, memória, portas de entrada/saida, etc.) e periféricos eletro-ópticos-mecânicos (teclados, mouses, discos rígidos, unidades de disquete, CD ou DVD, dispositivos USB, etc.)
- Software: Composto por programas destinados ao usuário do sistema com finalidades destintas (editores de texto, navegadores de internet, jogos, etc.)

### Objetivos de um Sistema Operacional
> Hardwares são complexos e por sua vez acessados atráves de interface de baixo nível (portas de entrada/saida de processadores) e possuem algumas variedades de características que depende da tecnológia usada em sua construção. Para evitar problemas enquanto sua complexidade e distinções os softwares devem busca uma forma homogênea de acesso a esse meio físico.

#### ⚠️ Solução -> Sistema Operacional
É uma camada de software que opera entre o hardware e os programas aplicativos. O SO incorpora tanto aspectos de baixo nível (drivers de dispositivos e gerência de memória física) e de alto nível (programas utílitarios e interface gráfica). Os objetivos sintetizados podem ser definidos como:
- Abstração de Recursos: O Sistema Operacional deve prover interfaces abstratas facilitando o uso de interfaces de baixo nível, como exemplo, a leitura de dados de um disco rígido que em um programa de aplicação usa o conceito de `arquivo`, visão abstrata do disco rígido, o que evita o acesso direto ao disco o que aumentariá a complexidade da tarefa. Além disso, com interface abstratas os aplicativos se tornam independentes dos hardwares e também defini uma generalização a qual independente da tecnólogia usada nos aplicativos acontece o acesso as funcionalidades do hardware por eles.
- Gerência de Recursos: Os programas aplicativos usam hardware para atingir seus objetivos e o Sistema Operacional deve gerir os conflitos no uso de recursos de hardware, como exemplo, a distribuição de tempo de execução de tarefas feitas no hardware por aplicativos evitando que um aplicativo prejudique a tarefa que deve ser executada por outro aplicativo. Além disso, o Sistema Operacional também deve definir uma fila de trabalhos seguindo a forma sequencial FIFO (First in, First out) para hardwares que dependem de apenas a interveção de um aplicativo por vez. Outrossim, Também é de responsábilidade do Sistema Operacional de evitar que todos os recursos do sistema sejam monopolizados por apenas um usuário.

### Funcionalidades
> Um Sistema Operacional deve atuar em várias frentes, dessa forma os recursos do sistema possui particularidades distintas o que impõe exigências específicas de funcionalidade.

#### Gerência de Processador | Processos | Tarefas | Atividades
- Distribuição da capacidade de processamento de maneira justa (levando em conta a necessidade de cada aplicação) entre as aplicações, evitando a monopolização desse recurso e respeitando as prioridades definidas pelos usuários.
- O Sistema Operacional produz uma ilusão de independencia de processadores para a realização de tarefas facilitando os programadores de aplicação em criar sistemas mais interativos.
- Também deve prover abstrações para sincronizar tarefas interdependentes e proporciona formas de comunicação entre elas.

#### Gerência de Memória
- Objetivo de prover uma área de memória própria para cada aplicação.
- Melhorias na estabilidade e segurança do sistema (Evitar a interferência de outras aplicações que podem ser maliciosas no funcionamento de outra aplicação).
- Pode ser feito um aumento de memória caso a quantidade de Memória RAM seja insuficiente para o funcionamento de uma aplicação usando um espaço disponivel em um armazenamento secundário, como exemplo, um disco rígido.

#### Gerência de Dispositivos | Entrada/Saida
- Busca resolver as particularidades que os perífericos possuem entre sí.
- Implementa a interação com cada dispositivo por meio de `drivers` e criar modelos de abstração que possibilitam o agrupamento de dispositivos similares sob a mesma interface de acesso.

#### Gerência de Arquivos
- Construída sobre a `gerência de dispositivos` tem como objetivo criar arquivos e diretórios por meio da definição de interfaces de acesso e regras de uso.
- Possui uma difusão que vai além da limitação dos recursos desenvolvidos na funcionalidade, como exemplo, as conexões de redes (Nos sistemas UNIX e Windowns cada socket TCP é visto como um descritor de arquivo podendo ler ou escrever dados).

#### Gerência de Proteção
- Objetivo de definir os recursos que devem ser acessados por cada usuário, as formas de acesso (leitura, escrita, etc.) e garantir o cumprimento dessas definições.
- Existem 4 passos utilizados por essa gerência para garantir a segurança dos recursos de um sistema de acessos indevidos:
    1. Definição de usuários e grupos de usuários;
    2. Identifiação de usuários do sistema por meio de autenticação;
    3. Definir regras de controle de acesso aos recursos em todas as tangentes (usuários, recursos e formas de acesso) regras essas aplicadas por procedimentos de autorização;
    4. Registro de uso de recursos pelos usuários, para fins de auditoria e contabilização.

> [!WARNING]
> Outras funcionalidades modernas para cobrir aspectos complementares: `interface gráfica`, `suporte de rede`, `fluxos multimídias`, `fontes de energia`, etc. \
> Normalmente as funções do Sistema Operacional são interdependentes.

#### Politica X Mecanismo
> Uma regra importante na construção de um sistema operacional e a distinção entre os conceitos de `politica` e `mecanismo`. Por meio dessa destinção é possivel flexibilizar o Sistema Operacional levando a mudanças de personalidade (sistema + interátivo ou + eficiente) sem alteração no código que interage diretamente com o hardware.

- Politica: Aspectos de decisões mais abstratos resolvidos por algoritmos de alto nível, como exemplo, a definição do uso de memória de uma aplicação.
- Mecanismo: Procedimentos de baixo nível que buscam as implementações das `politicas`, como exemplo, atribuir ou retirar memória de uma aplicação. Devem ser genéricos para evitar a restruturação do mecanismo após uma mudança na politica relacionada.

### Categorias
> Os Sistemas Operacionais podem ser classificados usando parâmetros e aspectos, como exemplo, tamanho de código, velocidade, suporte a recursos específicos, acesso à rede, etc. Os SO podem ter mais de uma classificação. 

#### Batch (de lote)
- Sistemas Operacionais + antigos
- Os programas a executar eram colocados em uma fila, com seus dados e demais informações para execução.
- Sem interação dos processadores com o usuário ao receber e processar os programas, permitindo um alto grau de uso do sistema.
- Atualmente sistema que fazem uso dessa categoria são sistemas que processam tarefas sem a interação com o usuário, sistema de processamento de transação bancária.
- Termo `em lote` também é usado para designar um conjunto de comandos que devem ser executados de maneira sequencial.

#### Rede
- Deve fornecer suporte à operações em rede, ou seja, a capacidade de oferecer às aplicações locais os recursos de outros dispositivos conectados a rede.
- Também deve oferecer à outros dispositivos da rede de recursos da aplicação local de maneira controlada.
- Os Sistemas Operacionais modernos em sua maioria possuem essa funcionalidade.

#### Distribuido
- Recursos de cada dispositivo estão disponiveis de maneira trasparente para todos na rede.
- Em uma aplicação o usuário tem acesso apenas a interface, porém não tem conhecimento da localidade de processamento.
- Atualmente utilizadas em aplicações de nuvem.

#### Multiusuário
- Suporte de identificação de administrador de cada recurso (arquivos, processos, áreas de memória, etc.), possibilitando a negação de acesso a usuários não autorizados.
- Garanti a segurança de Sistemas Operacionais de Rede e Distribuidos.
- Os Sistemas Operacionais modernos em sua maioria possuem essa funcionalidade.

#### Servidor
- Permiti gestão eficiente de grandes quantidade de recursos (disco, memória, processadores, etc.), impondo prioridades e limites sobre o uso desses recursos pelo usuário e pela aplicação.
- Normalmente faz parte de Sistemas Operacionais que possuem suporte a rede e multiusuários.

#### Desktop
- Voltado para atendimento ao usuário para a realização de tarefas do dia-a-dia, como exemplo, edição de textos, navegação com internet, reprodução de mídia, etc.
- Possuem interface gráfica, suporte a interatividade e operações de rede
- Exemplos de Sistemas Operacionais Desktop (`de mesa`) são: Windowns, MacOS e Linux.

#### Móvel
- Usado em equipamentos de uso pessoal (`smartphones` e `tablets`).
- Possuem gestão de energia (bateria), múlticonectividade de rede (wifi, bluetooth, etc.) e interações com múltiplos sensores (GPS, leitor de digitais, tela de toque, etc.).
- Exemplos de Sistemas Operacionais Móveis são: Android e iOS.

#### Embarcado
- Construído para operar em um hardware com poucos recursos de processamento, armazenamento e energia.
- Mais comumente usado em sistemas de automação e controladores de uso doméstico (leitores de DVD, TVs, fornos microondas, etc.)
- Exemplos de Sistemas Operacionais Embarcados | Embutidos | Embedded são LynxOS, TinyOS, Contiki e VxWorks.

#### Tempo Real
- Sistema Operacionais que o tempo é essencial.
- Objetivo primordial não consiste em um sistema ultrarrápido, mas um sistema que possui um comportamento temporal previsivel de operações realizadas.
- Busca minimizar as esperas e latências imprevisíveis, como exemplo, acesso a disco e sincronização excessiva.
- Exemplos de Sistemas Operacionais de Tempo Real são: QNX, RT-Linux e VxWorks.
- Normalmente sistemas embarcados e de tempo real possui relação com base em suas características.
- Tipos de Sistemas Operacionais de Tempo Real:]
    - `Críticos` (`hard real-time systems`) -> Perda de prazo pode causar danos ao sistema físico. Exemplo: Freios ABS.
    - `Não-Críticos` (`soft real-time systems`) -> Perda de prazo não possui tantos danos ao sistema físico. Exemplo: Softwares de Reprodução de Música.
