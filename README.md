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

