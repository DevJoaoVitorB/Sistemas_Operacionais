# ⏱️ Escalonamento de Tarefas

O **escalonador de tarefas** é o coração 🫀 da gerência de processos em um sistema operacional. Ele decide a ordem de execução das tarefas prontas, influenciando diretamente a eficiência e a experiência do usuário. 

## 🕰️ Tipos de Tarefas

As tarefas podem ser classificadas por **comportamento temporal** ou **uso de recursos**:

### 📌 Por Comportamento Temporal

1. **Tarefas de Tempo Real** ⏱ 
    * **Técnico:** Exigem respostas dentro de prazos rígidos (ex: controle de robôs industriais). O sistema deve garantir que nenhum atraso ocorra, mesmo sob carga alta.
    * **Mecanismo**: Usam prioridades fixas altas e alocação dedicada de CPU.
    * **Analogia:** Como um maestro regendo uma orquestra 🎻, onde cada nota deve ser tocada no momento exato – um atraso arruína a sinfonia.

2. **Tarefas Interativas** 💻
    * **Técnico:** Priorizam baixa latência (ex: digitar em um editor). O tempo de resposta ideal é <100ms para evitar percepção de lag.
    * **Mecanismo:** Preempção por tempo + prioridade dinâmica (aplicação em foco ganha boost).
    * **Analogia**: Garçom de restaurante movimentado 🍽️ - atende muitos pedidos rapidamente.

3. **Tarefas em Lote** 📦
    * **Técnico:** Executam em segundo plano sem interação (ex: backups). Podem ser interrompidas sem impacto crítico.
    * **Mecanismo:** Quantum longo (200ms+) e prioridade baixa.
    * **Analogia:** Como uma lavadora de roupas 🧺 – você inicia e volta horas depois para pegar o resultado.

<br>

### 📌 Por Uso de Recursos

1. **CPU-bound** 🔄
    * **Técnico:**
        * Tarefas que exigem intenso processamento computacional contínuo
        * Passam >70% do tempo em estado "executando"
        * Exemplos: Cálculos científicos, compressão de arquivos, mineração de criptomoedas
        * Desafio: Podem monopolizar a CPU se não gerenciadas adequadamente
    * **Analogia:** Como um estudante fazendo cálculos complexos de matemática 🧮 - precisa de concentração contínua sem interrupções para manter o raciocínio
2. **I/O-bound** 📥
    * **Técnico:**
        * Tarefas que frequentemente aguardam operações de entrada/saída
        * Passam >60% do tempo em estado "suspenso"
        * Exemplos: Servidores web, editores de texto, sistemas de banco de dados
        * Característica: Geralmente liberam o CPU voluntariamente durante waits
    * **Analogia:** Como um garçom anotando pedidos 🖊️ - passa mais tempo esperando a cozinha preparar os pratos do que efetivamente escrevendo

<br>

## 🆚 Escalonamento Preemptivo vs. Cooperativo

### **Preemptivo** ⏸️
* **Técnico**
    1. **Interrupção por Quantum**: 
        - O timer do SO gera interrupções periódicas (ex: a cada 10ms)
        - Ao receber a interrupção, o scheduler avalia se deve continuar ou trocar a tarefa

    2. **Preempção por Prioridade**:
        - Se uma tarefa de prioridade mais alta ficar pronta (ex: receber dados de rede)
        - O kernel interrompe imediatamente a tarefa atual

    3. **Chamadas de Sistema**:
        - Operações como ler arquivos causam mudança para modo kernel
        - O SO pode decidir não retornar à mesma tarefa

    4. **Vantagens:**
        * ✅ Baixa latência para tarefas críticas (<1ms em sistemas RT)
        * ✅ Isolamento de falhas (uma tarefa travada não congela o sistema)
        * ✅ Suporte nativo a múltiplos núcleos de CPU

* **Analogia**: Como um professor interrompendo alunos durante uma prova ✋ - mesmo quem não terminou precisa parar quando o tempo acaba, garantindo que todos tenham chance

<br>

### **Cooperativo** 🤝
* **Técnico**
    1. **Pontos de Cedência:**
        * Tarefas devem chamar explicitamente `yield()`, liberação de CPU voluntária
        * Ou realizar operações bloqueantes (ex: I/O)

    2. **Limitações Críticas:**
        * ⚠️ Uma tarefa mal-comportada pode travar todo o sistema
        * ⚠️ Difícil garantir tempos de resposta consistentes
        * ⚠️ Complexidade na programação (desenvolvedor deve gerenciar a cooperação)

* **Analogia:** Como um grupo de amigos compartilhando um videogame 🎮 - depende da boa vontade de cada um para passar o controle, sem regras rígidas

<br>

## 📊 Métricas de Desempenho

O escalonador busca equilibrar métricas muitas vezes conflitantes

### 