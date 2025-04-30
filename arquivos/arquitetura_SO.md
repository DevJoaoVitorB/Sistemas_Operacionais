## 🛠️ Arquiteturas de Sistemas Operacionais

### 🏗️ 1. O que é Arquitetura de um SO?

A arquitetura de um SO define como seus componentes internos estão estruturados e como interagem entre si. Isso influencia aspectos como desempenho, segurança, modularidade e capacidade de manutenção. A escolha da arquitetura depende do propósito do sistema, seja ele embarcado, desktop, servidor, distribuído ou em tempo real.

<br>

### 🧱 2. Sistemas Monolíticos

> Todos os componentes do SO são compilados juntos e executam no mesmo espaço de memória, com acesso irrestrito ao hardware.

✅ **Vantagens**:
- Alta performance, já que não há troca de contexto ou comunicação entre processos para acessar serviços.
- Implementação relativamente simples.

❌ **Desvantagens**:
- Um erro em qualquer parte pode afetar o sistema inteiro.
- Difícil de manter e atualizar partes específicas sem recompilar o núcleo inteiro.

📌 **Exemplos**: UNIX tradicional, MS-DOS, versões mais antigas do Linux.

<br>

### 🧮 3. Sistemas Micronúcleo (Microkernel)

> O núcleo do sistema contém apenas os serviços essenciais. Todo o restante é movido para processos de usuário, chamados de servidores.

✅ **Vantagens**:
- Alta modularidade e isolamento: erros em servidores não comprometem o núcleo.
- Mais fácil de depurar, atualizar e portar.

❌ **Desvantagens**:
- Desempenho inferior, pois a comunicação entre processos exige mais tempo e processamento.

📌 **Exemplos**: Minix 3, QNX, Mach (utilizado no macOS).

<br>

### 🧗 4. Sistemas em Camadas

> Estrutura hierárquica em que cada camada depende da camada imediatamente inferior e fornece serviços para a camada superior.

✅ **Vantagens**:
- Organização lógica e clara das responsabilidades.
- Boa modularidade para depuração e manutenção.

❌ **Desvantagens**:
- Pode ser difícil separar todas as funcionalidades em camadas puras.
- A sobreposição de chamadas pode comprometer o desempenho.

📌 **Exemplos**: MULTICS, HAL (Windows NT), Android (estrutura parcialmente em camadas).

<br>

### 🔀 5. Sistemas Híbridos

> Integram as vantagens de sistemas monolíticos e de micronúcleo. Serviços críticos permanecem no núcleo; serviços menos essenciais são separados.

✅ **Vantagens**:
- Melhor desempenho que microkernels puros.
- Modularidade razoável.

📌 **Exemplos**: Windows NT, Windows 10, MacOS (núcleo XNU = Mach + BSD).

<br>

## 🚀 6. Arquiteturas Avançadas

### 🖥️ 6.1 Máquinas Virtuais

Permitem rodar vários sistemas operacionais independentes sobre o mesmo hardware. O hipervisor (ou VMM) gerencia o acesso de cada VM aos recursos físicos.

| Tipo               | Característica                                | Exemplo              |
|--------------------|-----------------------------------------------|----------------------|
| Tipo 1 (Bare-metal)| Instala diretamente sobre o hardware físico   | VMware ESXi, Hyper-V |
| Tipo 2 (Hospedado) | Roda sobre um sistema operacional existente   | VirtualBox, VMware   |

<br>

### 📦 6.2 Contêineres

Virtualizam o espaço de usuário em vez do sistema inteiro. Cada contêiner é isolado, mas compartilha o mesmo kernel do sistema hospedeiro. São ideais para aplicações em nuvem e microsserviços.

📌 **Exemplos**: Docker, Kubernetes, LXC, FreeBSD Jails

<br>

### 🔬 6.3 Sistemas Exonúcleo (Exokernel)

> Fornecem o mínimo de abstrações. O kernel apenas controla o acesso ao hardware e distribui os recursos; cabe à aplicação definir suas abstrações, como sistema de arquivos e gerência de memória.

✅ **Vantagens**:
- Máximo desempenho e personalização.
❌ **Desvantagens**:
- Complexidade de desenvolvimento e manutenção.

📌 **Exemplos experimentais**: Aegis/ExOS, Nemesis

<br>

### 🧪 6.4 Sistemas Uninúcleo (Unikernel)

> Compilam sistema, bibliotecas e aplicação em um único binário especializado. São muito leves, rápidos e seguros.

✅ **Vantagens**:
- Tamanho extremamente reduzido.
- Inicialização rápida.
- Baixíssimo consumo de recursos.

📌 **Exemplos**: OSv, MirageOS, IncludeOS, TinyOS

<br>

## 🧾 Resumo Final

| Arquitetura        | Característica Principal                          | Exemplos                          |
|--------------------|---------------------------------------------------|-----------------------------------|
| **Monolítico**     | Núcleo único com todos os serviços                | Linux, FreeBSD, MS-DOS            |
| **Micronúcleo**    | Núcleo mínimo, serviços separados por IPC         | Minix 3, QNX, Mach                |
| **Camadas**        | Organização hierárquica por níveis                | MULTICS, Android (parcial)        |
| **Híbrido**        | Combinação de monolítico e micronúcleo            | Windows NT, MacOS                 |
| **Máquina Virtual**| Emulação completa de sistemas                     | VirtualBox, VMware                |
| **Contêiner**      | Compartilham kernel com isolamento leve           | Docker, Kubernetes, LXC           |
| **Exonúcleo**      | Kernel mínimo, abstrações nas aplicações          | Aegis/ExOS, Nemesis               |
| **Uninúcleo**      | Aplicação + kernel em um binário único            | OSv, MirageOS, TinyOS             |