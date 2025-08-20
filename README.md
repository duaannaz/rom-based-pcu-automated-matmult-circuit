# ROM-based-PCU-Automated-MatMult-Circuit
It is an automated ROM-based Program Control Unit Circuit to perform Matrix Multiplication.

## Data flow of the Circuit
- The program counter starts and sends the first instruction from the Instruction RAM to the Instruction Splitter.
- The instruction splitter splits the instruction into opcode, address of A, address of B, and flag.
- OPCODE tells what to perform in the circuit. (OPCODE is sent to the ROM) The flag represents the inner dimension of the matrix.
#### Depending on the OPCODE, this is how a matrix multiplication operation is performed:
- The input matrices A and B (tensor form) are stored in RAMs A1, A2, and B1, B2.
- A 2x2 block row from A1 and A2, and a 2x2 block column from B1 and B2 is then sent to Register Banks sequentially.
- Two values from each A and B RAMs are sent to the register banks. (A1, A2, B1, and B2 are used for this purpose, where A1, A2, and B1, B2 contains the same values)
- The values from register banks are then sent to the core of the 16x16 matrix multiplication, which can execute a maximum of one 2x2 block row and column of 16x16 matrices at a time.
- The core produces one 2x2 block of output matrix C, stored in Output Bank.
- The values from the output bank are then transferred to a final Output RAM, where values are stored in tensor form.

## Functionality (Instructions) of the Circuit
- DIM: This instruction tells the dimension of the input matrices, which are stored in the respective registers.
- BLOCK LOAD: This transfers the values from input RAMs to register banks sequentially.
- EXECUTE: This sends the values to the core to perform mat mult and store values in the output bank.
- LOOP: This repeats the Block Load and Execute operations in a loop until the whole matrix multiplication operation is done.
- BLOCK STORE: This stores the values from the output bank to the final RAM in tensor form.

### The circuit can perform up to four sequences of Matrix Multiplication of a maximum dimension of 16x16.
### It is connected with the ROM (Control unit) to control the operations.
### The DIM instruction is catered to optimize the circuit.

Software used to make the circuit: Logism Evolution


