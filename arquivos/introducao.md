## 🚀 Conceitos Básicos

- **⚙️ Hardware**: Composto por circuitos eletrônicos (processadores, memória, portas de entrada/saída etc.) e periféricos eletro-óptico-mecânicos (teclados, mouses, discos rígidos, unidades de disquete, CDs, DVDs, dispositivos USB etc.).
- **💡 Software**: Composto por programas destinados aos usuários do sistema com finalidades distintas (editores de texto, navegadores de internet, jogos etc.).

<br>

## 🎯 Objetivos de um Sistema Operacional

> Os hardwares são complexos e acessados através de interfaces de baixo nível (portas de entrada/saída dos processadores) e possuem variedades de características que dependem da tecnologia utilizada em sua construção. Para evitar problemas relacionados à complexidade e às diferenças entre dispositivos, os softwares devem buscar uma forma homogênea de acesso a esse meio físico.

### ✅ Solução: Sistema Operacional

O Sistema Operacional (SO) é uma camada de software que opera entre o hardware e os programas aplicativos. Ele incorpora tanto aspectos de baixo nível (drivers de dispositivos e gerenciamento de memória física) quanto de alto nível (programas utilitários e interface gráfica).

**🎯 Objetivos principais:**

- **Abstração de Recursos**: Facilita o uso de interfaces de baixo nível, como a leitura de dados de um disco rígido por meio do conceito de `arquivo`. Isso evita o acesso direto ao disco, reduzindo a complexidade da tarefa e tornando os aplicativos independentes das características específicas do hardware.

- **Gerência de Recursos**: Administra os conflitos de uso de hardware entre os aplicativos, distribuindo tempo de execução e recursos de forma justa. Implementa filas de trabalho (FIFO - First In, First Out) para dispositivos que necessitam de acesso exclusivo e evita o monopólio dos recursos por um único usuário.

<br>

## 🛠️ Funcionalidades

> Um Sistema Operacional atua em diversas frentes, pois cada recurso do sistema possui particularidades e impõe exigências específicas de funcionalidade.

### 🧠 Gerência de Processador | Processos | Tarefas | Atividades

- Distribui a capacidade de processamento entre as aplicações de forma justa, respeitando as prioridades.
- Proporciona a ilusão de múltiplos processadores, facilitando a criação de sistemas interativos.
- Provê abstrações para sincronizar e comunicar tarefas interdependentes.

### 💾 Gerência de Memória

- Oferece uma área de memória dedicada para cada aplicação.
- Melhora a estabilidade e segurança, evitando interferência entre aplicações.
- Permite aumento de memória usando armazenamento secundário (memória virtual).

### 🖥️ Gerência de Dispositivos | Entrada/Saída

- Resolve as particularidades dos periféricos.
- Implementa drivers e cria modelos de abstração, agrupando dispositivos similares sob a mesma interface.

### 📁 Gerência de Arquivos

- Baseada na gerência de dispositivos, cria arquivos e diretórios com interfaces e regras de acesso.
- Vai além de arquivos locais, abrangendo operações em rede (sockets TCP como descritores de arquivos em UNIX e Windows).

### 🔒 Gerência de Proteção

- Define quem pode acessar quais recursos e de que forma (leitura, escrita etc.).

**📝 Processo em 4 passos:**

1. Definição de usuários e grupos de usuários;
2. Identificação de usuários via autenticação;
3. Definição e aplicação de regras de controle de acesso (autorização);
4. Registro de uso de recursos para auditoria e contabilização.

> ⚠️ **ATENÇÃO**
> - **Outras funcionalidades modernas**: Interface gráfica, suporte de rede, fluxos multimídia, gestão de energia etc.
> - As funcionalidades do SO são interdependentes.

### 💬 Política x Mecanismo

> A distinção entre política e mecanismo é essencial para tornar o Sistema Operacional mais flexível e adaptável a mudanças.

- **Política**: Define o "o quê" fazer (exemplo: qual aplicação recebe memória).
- **Mecanismo**: Implementa "como" fazer (exemplo: alocar ou liberar memória para uma aplicação).

<br>

## 📚 Categorias de Sistemas Operacionais

> Os Sistemas Operacionais podem ser classificados segundo vários critérios: tamanho de código, velocidade, suporte a recursos específicos, acesso à rede, entre outros. Um mesmo SO pode ter múltiplas classificações.

### 📦 Batch (de lote)

- Sistemas Operacionais antigos.
- Programas eram colocados em fila para execução sequencial, sem interação com o usuário.
- Altamente eficientes no uso do sistema.
- Usados atualmente em sistemas de processamento automático (ex.: transações bancárias).
- "Em lote" também designa conjuntos de comandos executados sequencialmente.

### 🌐 Rede

- Suporte a operações em rede.
- Disponibiliza recursos locais e remotos de forma controlada.
- Presente na maioria dos sistemas modernos.

### 🔄 Distribuído

- Recursos de dispositivos distribuídos estão disponíveis de forma transparente.
- O usuário interage apenas com a interface, sem saber onde ocorre o processamento.
- Base de aplicações em nuvem.

### 👥 Multiusuário

- Permite gestão de usuários, recursos e restrições de acesso.
- Garante a segurança em sistemas de rede e distribuídos.
- Presente na maioria dos sistemas modernos.

### 🖥️ Servidor

- Gerencia eficientemente grandes quantidades de recursos.
- Impõe prioridades e limites de uso.
- Comum em sistemas com suporte a rede e multiusuários.

### 🖥️🖱️ Desktop

- Voltados para tarefas cotidianas (edição de textos, navegação na internet, reprodução de mídia).
- Possuem interface gráfica, alta interatividade e suporte a operações de rede.
- Exemplos: Windows, macOS e Linux.

### 📱 Móvel

- Usados em smartphones e tablets.
- Gerenciam energia, conectividades (Wi-Fi, Bluetooth etc.) e sensores (GPS, leitor de digitais, tela de toque).
- Exemplos: Android e iOS.

### 🤖 Embarcado

- Projetados para dispositivos com poucos recursos de processamento, armazenamento e energia.
- Usados em automação e eletrônicos domésticos (DVD players, TVs, micro-ondas).
- Exemplos: LynxOS, TinyOS, Contiki e VxWorks.

### 🕓 Tempo Real

- Priorizam o comportamento temporal previsível sobre a velocidade.
- Minimiza latências imprevisíveis (acesso a disco, sincronização excessiva).
- Exemplos: QNX, RT-Linux e VxWorks.

**📝 Tipos de Sistemas de Tempo Real:**

- `Críticos (Hard Real-Time Systems)`: Perda de prazo pode causar danos (ex.: Freios ABS).
- `Não-Críticos (Soft Real-Time Systems)`: Perda de prazo não é tão prejudicial (ex.: Software de reprodução de música).
