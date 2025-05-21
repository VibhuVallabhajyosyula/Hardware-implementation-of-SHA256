1. Purpose of the Module
This module implements the SHA-256 cryptographic hash function, which takes a 512-bit input message block and produces a 256-bit fixed-size output known as the hash or digest. It's widely used in security applications like digital signatures and blockchain.

2. Inputs and Outputs
Inputs:

clk: Clock signal to drive the sequential logic.

rst: Reset signal to clear internal state and outputs.

start: Control signal that initiates the hashing process.

M: 512-bit message block (a preprocessed and padded input block).

Outputs:

ready: Goes high when the hashing process is complete.

out: 256-bit hash result corresponding to the input message.

3. Internal Registers
Hash state registers (H[0] to H[7]):
These hold intermediate and final hash values. They are initialized with SHA-256's standard initial values and are updated during processing.

Constants (K[0] to K[63]):
These are 64 fixed 32-bit constants defined by the SHA-256 specification. They're used in each of the 64 rounds.

Message schedule array (w[0] to w[63]):
This array stores the expanded form of the input message block. The first 16 entries are directly taken from the input, and the remaining 48 are calculated using specific bitwise operations.

Working variables (a to h):
These are temporary variables that carry the state during the 64 rounds of compression.

Temporary variables (temp1, temp2):
Used to store intermediate values during each round of the compression function.

4. SHA-256 Logic Breakdown
Initialization
Hash state registers are loaded with standard initial hash values.

Constants K are also initialized to predefined values per SHA-256 spec.

Message Schedule Expansion
The 512-bit message M is divided into 16 32-bit words.

The remaining 48 words are computed using functions that involve bitwise right rotations, shifts, and XORs.

Compression Loop (64 Rounds)
The working variables a to h are initialized from the current hash state.

For each of the 64 rounds:

Two intermediate values temp1 and temp2 are computed using logical functions (Σ, Ch, Maj) and the message schedule + constants.

The working variables are updated in a specific shifting manner.

Final Hash Computation
After all 64 rounds, the working variables are added back to the original hash state registers.

The result is stored in the output out.

5. Operation Flow
On reset (rst = 1), the output and ready signal are cleared.

When start = 1, the hashing process begins:

Message is expanded.

64 rounds of processing occur.

Final digest is calculated and sent to the output.

When the computation completes, ready is set high.
