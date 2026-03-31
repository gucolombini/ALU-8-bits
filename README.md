# ALU-8-bits
Unidade de Lógica e Aritmética para entrada e saída 8 bits em simulador.

<img width="3926" height="2026" alt="8bit_alu" src="https://github.com/user-attachments/assets/17fd79ee-0d3b-436a-bdc5-448c6d15b2f3" />

[Vídeo demonstração](https://drive.google.com/file/d/1WFhapyYoE33MdLRWk5QlaW8zfDG4UkJv/view?usp=sharing)

Inclui o arquivo do circuito da ALU principal, assim como todos os componentes utilizados para constituir ela.

## Execução

1. Baixe todos os arquivos do repositório em uma mesma pasta. 
2. Instale o [Digital](https://github.com/hneemann/digital) e abra o arquivo *'8bit_alu.dig'*.
3. Inicie a simulação.

## Operações em 8-bit
| OP | Operação |
|--- |---       |
| 0  | AC + N   |
| 1  | AC - N   |
| 2  | AC * N  (resultado 16-bit) |
| 3  | AC / N  (resto e quociente) |
| 4  | AC shift lógico esquerda |
| 5  | AC shift lógico direita |
| 6  | AC NAND N|
| 7  | AC XOR N |

## Arquitetura

A ALU possui 4 entradas:
- N (8-bit): Input; valor que irá passar pelo circuito
- OP (3-bit): Operation; seleciona a operação
- CLK (1-bit): Clock; ativação do circuito
- En (1-bit): Enable; permite que o circuito seja ativado pelo CLK

O usuário deve ativar o circuito ligando EN, selecionar o número que desejar em N e a operação a ser realizada em OP, e então clicar CLK. Ao fazer isso, o resultado da operação será guardado em seus respectivos registradores.

- AC (8-bit): Registrador acumulador; resultado de soma, subtração, shifts lógicos, NAND e XOR. Além disso, representa os LSB da multiplicação e resto da divisão.
- MQ (8-bit): Registrador de multiplicação e divisão; guarda os MSB de uma multiplicação ou o quociente de uma divisão.

As operações aritméticas da ALU foram implementadas em circuitos integrados, armazenados em arquivos separados, mantendo funcionalidade mas evitando repetição e desorganização na estrutura principal.

- Somador / Subtrator: Calcula a soma de inputs A e B por meio do uso de somadores e meio somadores em cadeia. Também possui input CTR que converte B para sua forma complemento de 2, permitindo a subtração de A por B no mesmo circuito.
- Multiplicador: Calcula o produto de A por B; design de um multiplicador combinacional, que faz uso de vários somadores carry-save em sequência para multiplicar cada um dos algarismos e somá-los corretamente. O resultado do circuito é em 16-bit, que é separado em dois na ALU.
- Divisor: Calcula o quociente e resto da divisão de A por B; Algoritmo de divisão restaurador, tira vantagem do componente do somador/subtrator 8-bit para facilitar o processo. Outputs para resto e quociente, 8-bit cada.
