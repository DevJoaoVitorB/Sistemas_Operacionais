# 💻 Implentação de Tarefas 

## 🏗️ **Estruturas Básicas: TCB e Contexto**  

### **TCB (Task Control Block)**  
- **O que é?** 🏷️  
  Estrutura de dados no núcleo que armazena todas as informações de uma tarefa (processo/thread).  

- **Para que serve?** 🔍  
  Rastrear o estado atual da tarefa (registradores, recursos alocados, prioridade) e permitir trocas de contexto eficientes.  

- **Contém:** 📦  
  - Identificador único (PID).  
  - Estado (pronto, executando, bloqueado).  
  - Contexto do processador (PC, SP, registradores).  
  - Recursos (arquivos abertos, memória alocada).  

**Analogia:** 📖  
Um "prontuário médico" da tarefa, com seu histórico, estado atual e medicamentos (recursos) usados.  

<br>

### 🔄 **Trocas de Contexto**  

**O que é?** \
A troca de contexto (context switch) é o mecanismo pelo qual um sistema operacional interrompe a execução de uma tarefa (processo ou thread), salva seu estado atual e retoma a execução de outra tarefa.

**Como é feito?**  
1. **Interrupção** ⏰: Hardware (timer) ou software (syscall) dispara uma interrupção.  
2. **Salvamento** 💾: Despachante salva o contexto da tarefa atual no TCB.  
3. **Escalonamento** 🎯: Escalonador decide a próxima tarefa (opcional, se não houver fila ordenada).  
4. **Restauração** 🔄: Despachante carrega o contexto da nova tarefa do TCB para o processador.  

**Fórmula de Eficiência:** 📊  
\[ \mathcal{E} = \frac{t_q}{t_q + t_{tc}} \]  
- \( t_q \): Tempo do quantum.  
- \( t_{tc} \): Tempo da troca de contexto.  

**Impacto:**  
Quantum curto → Mais trocas → Menor eficiência (ex: 1ms quantum → 91% eficiência).  

**Analogia:** 🎭  
Trocar de ator em um palco: quanto mais rápida a troca (e menos frequente), mais tempo para a peça (tarefas) brilhar.  

<br>

## 🏗️ **Processos vs. Threads**  

### **Processos** 🏢  
- **Definição Técnica:**  
  Unidade de isolamento com recursos próprios (memória, arquivos). Cada processo tem pelo menos uma thread.  

- **Vantagens:**  
  - **Robustez** 💪: Falha em um processo não afeta outros.  
  - **Segurança** 🔒: Permissões por processo.  

- **Desvantagens:**  
  - **Overhead** 🐢: Criação lenta e consumo alto de memória.  

**Analogia:** 🏘️  
Prédios independentes (processos) com moradores (threads). Se um pegar fogo, os outros não queimam.  

### **Threads** 🧵  
- **Definição Técnica:**  
  Fluxo de execução dentro de um processo, compartilhando recursos (memória, arquivos).  

- **Modelos:**  
  - **N:1** (User Threads): Leve, mas bloqueia todas as threads se uma chamada bloquear.  
  - **1:1** (Kernel Threads): Escalonável pelo SO, paralelismo real.  
  - **N:M** (Híbrido): Balanceia escalabilidade e desempenho.  

**Vantagens:**  
  - **Leveza** 🪶: Criação rápida.  
  - **Compartilhamento** 🤝: Dados acessíveis sem IPC.  

**Desvantagens:**  
  - **Fragilidade** 🥀: Erro em uma thread pode derrubar o processo inteiro.  

**Analogia:** 🏢  
Apartamentos (threads) no mesmo prédio (processo): reformas são fáceis, mas um vazamento afeta todos.  

<br>

## 🛠️ **Gestão de Processos: Criação, Hierarquia e Comunicação**

### 🔄 **Ciclo de Vida de um Processo**
**Como é feito na prática?**
- **Criação**: 
  - No Linux: `fork()` clona o processo atual → `execve()` carrega novo código.
  - No Windows: `CreateProcess()` cria e carrega em uma única chamada.
- **Término**: 
  - `exit()` (Linux) ou `ExitProcess()` (Windows) liberam recursos.
  - Processos podem ser forçados a terminar (`kill()`/`TerminateProcess()`).

### **Tabela Comparativa Linux vs Windows**
| Ação                | Linux                  | Windows             |
|---------------------|------------------------|---------------------|
| Criar processo      | `fork()` + `execve()`  | `CreateProcess()`   |
| Encerrar processo   | `exit()`               | `ExitProcess()`     |
| Matar processo      | `kill()`               | `TerminateProcess()`|

<br>

### 🌳 **Hierarquia de Processos**

**O que é?**
No núcleo dos sistemas operacionais modernos, os processos se organizam em estruturas hierárquicas que determinam relações de parentesco e controle. Essa hierarquia é fundamental para:
- Gerenciamento de recursos
- Comunicação interprocessos
- Controle de permissões

#### **Modelo UNIX (Árvore)**
- Processos formam uma estrutura pai-filho.
- Quando o pai morre, os filhos viram "órfãos" (adotados pelo `init`).
- Comando `pstree` mostra essa relação visualmente.

**Como funciona:**
1. **Tudo começa no INIT** (PID 1)
    - Primeiro processo que liga quando o computador inicia
    - Pai de todos os outros processos

2. **Cada novo processo é um FILHO**
    - Criado pelo comando `fork()` (como um clone)
    - Herda características do pai (arquivos abertos, configurações)

3. **Exemplo de árvore** (como no comando `pstree`):
    ```text
    init
    └──login───bash───firefox
    └─ssh───bash
    ```

**Analogia**: 🏡  
Uma família onde os filhos (processos filhos) herdam características dos pais, mas podem seguir caminhos diferentes.

<br>

#### **Modelo Windows (Plano)**
- Todos os processos são independentes, sem relação hierárquica.
- O gerenciamento é feito via identificadores (PID).

**Analogia**:  
Enquanto no UNIX processos são como uma árvore genealógica, no Windows são como apartamentos num mesmo prédio - vizinhos, mas sem parentesco.

<br>

#### 🆚 **Linux vs Windows: A Diferença**
| Característica | Linux/Unix           | Windows              |
|----------------|----------------------|----------------------|
| **Estrutura**  | Árvore familiar      | Todos independentes  |
| **Criação**    | `fork()` + `exec()`  | `CreateProcess()`    |
| **Herança**    | Completa	            | Parcial              |
| **Órfãos**	   | Adotados pelo init	  | Terminados           |

<br>

### 📡 **Comunicação Entre Processos (IPC)**
🔒 **O Problema Fundamental:** \
Processos são como **casas com muros altos** - por padrão, um não pode:
- 🚫 Ver o que acontece dentro do outro
- 🚫 Pegar objetos da memória alheia
- 🚫 Conversar diretamente

**Por quê?** Segurança! Se um programa travar ou for malicioso, não afeta os outros.

🛠️ **As 3 Soluções Práticas:**

1. 🖍️ **Quadro Branco Compartilhado (Memória Compartilhada)**
  - **Como funciona?**
    - Cria-se uma área de memória "especial" que vários processos podem acessar
    - Todos leem e escrevem no mesmo espaço

  - **Prós e Contras:**
    - ✅ **Super rápido** (como anotar num quadro visível a todos)
    - ❌ Precisa de **trava** (sincronização) para não ter confusão

2. 📜 **Bilhetes na Porta (Pipes/Tubos)**
  - **Como funciona?**
    - Cria um "túnel" onde um processo escreve e outro lê
    - Funciona como uma fila (primeiro a entrar, primeiro a sair)
    - Sempre unidirecional (como um tubo de água)
  - **Tipos:**
    - **Pipes Anônimos** (`|` no terminal): Temporários
      ```bash
      ls | grep ".txt"  # Passa a saída do 'ls' para o 'grep'
      ```
    - **Pipes Nomeados**: Permanecem no sistema como arquivos
      ```bash
      mkfifo meu_pipe
      echo "Olá" > meu_pipe &  # Escreve
      cat < meu_pipe           # Lê
      ```
3. 💨 Sinais de Fumaça (Sinais)
  - **Como funciona?**
    - Envia notificações simples entre processos
    - Números pré-definidos (ex: 15 = SIGTERM, 9 = SIGKILL)
  - **Comandos Úteis:**
    ```bash
    kill -15 1234  # Pedido educado para terminar (PID 1234)
    kill -9 1234   # Mata imediatamente (sem chance de limpeza)
    ```
  - **Exemplo de Sinais Comuns:**
    | Número | Nome    | Efeito                   |
    |--------|---------|--------------------------| 
    | 2      | SIGINT	 | Interrupção (Ctrl+C)     |
    | 9	     | SIGKILL | Terminação forçada       |
    | 15     | SIGTERM | Pedido de término gentil |

💡 **Quando Usar Cada Um?**
| Técnica               |	Melhor Para...               | Cuidados                   |
|-----------------------|------------------------------|----------------------------|
| Memória Compartilhada |	Dados que mudam rápido       |	Use travas (semáforos)    |
| Pipes                 |	Processar dados em sequência |	Só uma direção            |
| Sinais                |	Avisos urgentes              |	Não envia dados complexos |

**Analogia**: 📨  
Como colegas de escritório em salas separadas (processos) que se comunicam por:
- Quadro branco compartilhado (memória)
- Bilhetes passados sob a porta (pipes)
- Sinais de fumaça (sinais)

<br>

### ⚠️ **Pontos Críticos**
1. **Zumbis**: Processos que terminaram mas ainda constam na tabela de processos.
   - Solução: Pai deve usar `wait()` para "enterrar" filhos.

2. **Órfãos**: Processos cujo pai terminou antes deles.
   - No UNIX, são adotados pelo `init` (PID 1).

3. **Race Conditions**: Concorrência no acesso a recursos compartilhados.

**Dica Profissional**: 🛡️  
Sempre limpe processos filhos e use mecanismos de sincronização em IPC!

<br>

### 🏆 **Por Que Isso Importa?**
- **Robustez**: Isolamento previne falhas em cascata.
- **Segurança**: Permissões podem ser gerenciadas por processo.
- **Eficiência**: IPC permite cooperação sem compartilhar tudo.

**Exemplo Real**:  
Navegadores modernos usam processos separados por aba - se uma travar, as outras continuam.

<br>

## ❓ **Exercícios com Respostas**

### 1. **O que é um TCB e qual sua função?**
**Resposta:**  
Estrutura que armazena todas as informações de uma tarefa (PID, estado, registradores, recursos) para gerenciamento pelo SO.

### 2. **Quais são os passos de uma troca de contexto?**
**Resposta:**  
Salva estado da tarefa atual → Escalona nova tarefa → Restaura seu estado. Quanto mais rápido, melhor a eficiência (𝓔 = tₚ/(tₚ + tₜₛ)).

### 3. **Qual a diferença fundamental entre processos e threads?**
**Resposta:**  
  - Processo: unidade isolada com recursos próprios. 
  - Thread: fluxo de execução que compartilha recursos do processo.

### 4. **Quais são os modelos de implementação de threads?**
**Resposta:**  
N:1 (todas no mesmo núcleo), 1:1 (uma thread por núcleo), N:M (híbrido). Linux/Windows usam 1:1.

### 5. **Como funciona a hierarquia de processos no Linux?**
**Resposta:**  
Árvore com init (PID 1) como raiz. Processos criados por fork() herdam recursos do pai. Órfãos vão para init.

### 6. **Como o Windows difere no gerenciamento de processos?**
**Resposta:**  
Processos independentes sem hierarquia. Criados por CreateProcess(), sem herança como no Linux.

### 7. **Quais são os 3 métodos principais de IPC?**
**Resposta:**  
Memória compartilhada (rápida), pipes (fluxo unidirecional), sinais (notificações simples como kill).

### 8. **Quando usar cada método de IPC?**
**Resposta:**  
Memória: dados dinâmicos. Pipes: processamento em sequência. Sinais: comandos urgentes.

### 9. **O que são processos zumbis e como evitá-los?**
**Resposta:**  
Processos terminados que ainda aparecem na tabela. Evitar com wait() no processo pai.

### 10. **Por que navegadores usam processos+threads?**
**Resposta:** 
Processos isolam abas (segurança), threads aceleram tarefas paralelas (desempenho).
