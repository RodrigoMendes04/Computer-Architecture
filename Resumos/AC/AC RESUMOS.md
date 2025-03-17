# #5 : Basic Components
Any logical function can be constructed using AND gates, OR gates, and inverters.
![[Pasted image 20240617212552.png]]

The two common inverting gates are called NOR and NAND and correspond to inverted OR and AND gates.
![[Pasted image 20240617212633.png]]
![[Pasted image 20240617221328.png]]
![[Pasted image 20240617221539.png]]

A decoder is a logic block that has an N-bit input and 2Noutputs, where only one output is asserted for each input combination.
![[Pasted image 20240617212655.png]]

A multiplexor is a logic block that has an N-bit input and 1 output, where the output is one of the inputs that is selected accordingly to a control value.
![[Pasted image 20240617212744.png]]

The 1-bit ALU for AND, OR and addition is implemented with a multiplexor that selects ‘a AND b’, ‘a OR b’ or ‘a + b’, depending on whether the value of Operation is 0, 1 or 2.
![[Pasted image 20240617213018.png]]

Clocks are needed in sequential logic to decide when an element that contains state should be updated.
![[Pasted image 20240617213258.png]]

The S-R (set-reset) latch is the simplest type of memory cell as it does not have any clock input. It is built from a pair of NOR gates where the outputs represent the value of the stored state (Q) and its complement. State changes when S or R are turned on and remains unaltered when both S and R are off. State may be undefined if both S and R are turned on simultaneously.
![[Pasted image 20240617215714.png]]

In a D latch, the internal memory state is changed whenever the appropriate inputs change and the clock is asserted. The inputs are the data value to be stored (D) and a clock signal (C) that indicates when the latch should read the value on D and store it. The outputs are simply the value of the internal state (Q) and its complement.
![[Pasted image 20240617215803.png]]

The D flip-flop is the basic building block for memory cells since its output only changes on the clock edge. A D flip-flop is constructed from a pair of D latches and can be built so that it triggers on either the rising or falling clock edge. The output is stored when the clock edge occurs.
![[Pasted image 20240617215827.png]]

Reading Registers
![[Pasted image 20240617215903.png]]

Writing Registers
![[Pasted image 20240617220448.png]]

Register File
![[Pasted image 20240617220506.png]]

SRAMs are simply memory arrays integrated circuits. An SRAM chip has a specific configuration in terms of the number of addressable locations, as well as the width of each addressable location. • A 2M×16 SRAM provides 2M entries, each of which is 16bits wide – it thus requires 21 address lines (2M = 221), a 16-bit data input line and a 16-bit output line
![[Pasted image 20240617220543.png]]

Large SRAMs cannot be built in the same way as a register file because the usage of a giant multiplexor/decoder is totally impractical. Instead, large memories are implemented with shared output lines, which multiple memory cells in the memory array can assert.
For example, in a 4M×8 SRAM, we would need a 22-to-4M decoder and 4M word lines (required to enable the individual flip-flops). To circumvent this problem, large memories are organized as rectangular arrays and use a two-step decoding process.

DRAMs store the charge on a capacitor, it cannot be kept indefinitely and must periodically be refreshed (that is why this memory is called dynamic).

### Exercicios

![[Pasted image 20240617222120.png]]
![[Pasted image 20240617222137.png]]

![[Pasted image 20240617222156.png]]
![[Pasted image 20240617222207.png]]

![[Pasted image 20240617222230.png]]
![[Pasted image 20240617222243.png]]

![[Pasted image 20240617222259.png]]
![[Pasted image 20240617222309.png]]
![[Pasted image 20240617222319.png]]
![[Pasted image 20240617222329.png]]
![[Pasted image 20240617222342.png]]
![[Pasted image 20240617222351.png]]
![[Pasted image 20240617222404.png]]
![[Pasted image 20240617222415.png]]

# #6 : Performance

The algorithm determines both the number of source-level statements and the number of I/O operations executed. 
The programming language, compiler and architecture determines the number of machine instructions executed per each source-level statement. 
The processor and memory system determines how fast instructions are executed. 
The I/O system (hardware and operating system) determines how fast I/O operations are executed.

Existem 2 classes distintas de métricas de desempenho:
• Métricas de desempenho para processadores – avaliam o desempenho de uma unidade de processamento, normalmente feita medindo a velocidade ou o número de operações que ela realiza em um determinado período de tempo 
• Métricas de desempenho para aplicações paralelas – avaliar o desempenho de uma aplicação paralela, normalmente feito comparando o tempo de execução com múltiplas unidades de processamento com o tempo de execução com apenas uma unidade

![[Pasted image 20240617223146.png]]

Elapsed time – total response time to complete a task:
• Includes everything – disk accesses, memory accesses, input/output (I/O) activities, operating system overhead, idle time;
CPU time – CPU time spent processing a given task: 
• Excludes time spent waiting for I/O or running other programs;
CPU time can be further divided in: 
• User CPU time – time spent in the program itself (user’s code); 
• System CPU time – time spent in the operating system performing tasks on behalf of the program (system calls);

![[Pasted image 20240617223403.png]]
![[Pasted image 20240617223414.png]]
![[Pasted image 20240617223432.png]]
![[Pasted image 20240617223447.png]]
![[Pasted image 20240617223530.png]]
![[Pasted image 20240617223546.png]]

# #7 : MIPS Implementation

### Exercicios

![[Pasted image 20240617225529.png]]
![[Pasted image 20240617230027.png]]
![[Pasted image 20240617230217.png]]
![[Pasted image 20240617230232.png]]
- Ciclo único: todas as etapas necessárias para executar uma instrução (IF, ID, EX, MEM, WB) ocorrem dentro de um único ciclo de relógio. Portanto, o tempo de execução de cada instrução é igual ao tempo de um ciclo de relógio, que é 1200 ps.
- Multi-Ciclo:
   -  **ADD $s0, $s1, $s2**
    - IF: Busca a instrução (300 ps)
    - ID: Decodifica a instrução e lê os registradores (300 ps)
    - EX: Executa a operação de soma (300 ps)
    - WB: Escreve o resultado de volta no registrador (300 ps)
    - **Total: 4 ciclos × 300 ps = 1200 ps**
  -  **LW $s0, 100($s1)**
	- IF: Busca a instrução (300 ps)
	- ID: Decodifica a instrução e calcula o endereço efetivo (300 ps)
	- EX: Calcula o endereço de memória (300 ps)
	- MEM: Lê o dado da memória (300 ps)
	- WB: Escreve o dado no registrador (300 ps)
	- **Total: 5 ciclos × 300 ps = 1500 ps**
 -  **SW $s0, 100($s1)**
	- IF: Busca a instrução (300 ps)
	- ID: Decodifica a instrução e calcula o endereço efetivo (300 ps)
	- EX: Calcula o endereço de memória (300 ps)
	- MEM: Escreve o dado na memória (300 ps)
	- **Total: 4 ciclos ×\times× 300 ps = 1200 ps**
  - **BEQ $s0, $s1, _label**
	- IF: Busca a instrução (300 ps)
	- ID: Decodifica a instrução e lê os registradores (300 ps)
	- EX: Compara os registradores e calcula o desvio (300 ps)
	- **Total: 3 ciclos ×\times× 300 ps = 900 ps**
 - **J _label**
	- IF: Busca a instrução (300 ps)
	- ID: Decodifica a instrução e calcula o endereço do desvio (300 ps)
	- EX: Calcula o endereço de destino (300 ps)
	- **Total: 3 ciclos ×\times× 300 ps = 900 ps**
- Pipeline: Para cada instrução, a execução no pipeline ideal (desconsiderando stalls e hazards) leva 5 ciclos de 300 ps, totalizando 1500 ps
![[Pasted image 20240617230901.png]]
![[Pasted image 20240617230918.png]]

![[Pasted image 20240618000028.png]]
![[Pasted image 20240618000342.png]]

# #8 Memory Hierarchy

### Exercicios

![[Pasted image 20240618001653.png]]
![[Pasted image 20240618001710.png]]
![[Pasted image 20240618001719.png]]

![[Pasted image 20240618001734.png]]
1. **Identificar o Tamanho do Bloco**: O tamanho do bloco é indicado pelo número de bits usados para o ‘Byte offset’. Por exemplo, se o byte offset usa 2 bits, então o tamanho do bloco é de 2^2 = 4 bytes.
    
2. **Determinar o Número de Conjuntos**: O número de conjuntos é indicado pelo número de linhas na tabela da cache. Por exemplo, se há 1024 linhas (0 a 1023), então há 1024 conjuntos na cache.
    
3. **Calcular o Número de Bits para o Índice**: O número de bits para o índice é log2 do número de conjuntos. Por exemplo, se há 1024 conjuntos, então são necessários log2(1024) = 10 bits para o índice.
    
4. **Determinar a Tag**: Os bits restantes do endereço são usados para a tag. Por exemplo, se você tem um endereço de 32 bits, e já determinou que 2 bits são para o byte offset e 10 bits são para o índice, então os restantes 32 - 2 - 10 = 20 bits são para a tag.

Resumo: Ver esta parte de cima e dividir
TAG: 31 - 12 | INDEX: 11 - 2
![[Pasted image 20240618020303.png]]
TAG: 31 - 14 | INDEX: 13 - 6
![[Pasted image 20240618020405.png]]
TAG: 31 - 10 | INDEX: 9 - 2
![[Pasted image 20240618020423.png]]
![[Pasted image 20240618001801.png]]
![[Pasted image 20240618001806.png]]
![[Pasted image 20240618001812.png]]
![[Pasted image 20240618001821.png]]

![[Pasted image 20240618014319.png]]
![[Pasted image 20240618014336.png]]
2 b) Temos que ver o numero que esta a ir desde o inicio até à coluna V. Na c é vezes 4 porque sao 4 tabelas.
2 c) Quando nao tem nada a sair do offset metemos 2^2 quando temos metemos 2^2+(o numero que estiver a sair) ???
2 d) Alinea c vezes a alinea b
2 e) Soma do numero das setas que estao a sair de cada coluna da tabela e depois multiplicas tudo pelo que deu na alinea b
![[Pasted image 20240618014344.png]]
![[Pasted image 20240618014355.png]]
![[Pasted image 20240618014428.png]]
![[Pasted image 20240618014413.png]]
![[Pasted image 20240618014444.png]]
![[Pasted image 20240618014452.png]]
![[Pasted image 20240618014459.png]]
5 a) So pegar em cada numero e dividir por 4

# #9 Análise de Desempenho (??)

### Exercicios

![[Pasted image 20240618022850.png]]
![[Pasted image 20240618022901.png]]
![[Pasted image 20240618022909.png]]
Clock cycles: Frequencia do relogio ×Tempo de execuçao
Number instructions: a) vezes 10
![[Pasted image 20240618022915.png]]

![[Pasted image 20240618022924.png]]
![[Pasted image 20240618022936.png]]
![[Pasted image 20240618022942.png]]
![[Pasted image 20240618022949.png]]
