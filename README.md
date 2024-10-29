# ZK_Project_VeriSync
Assesment for Verisync Lab ZK Research Engineer
# ZKProof Project

## Overview
This project focuses on implementing a zero-knowledge (ZK) proof system to demonstrate the knowledge of a solution for the equation \(x^2 + x + 7 = 9\) without revealing the value of \(x\). The project utilizes the **snarkjs** framework and the **Circom** programming language to design and verify ZK circuits.

## Core Concepts
- **Objective**: Prove knowledge of \(x\) such that \(x^2 + x + 7 = 9\) without disclosing \(x\).
- **ZK Protocol Chosen**: Groth16 due to its efficient proof size and fast verification times.

## Installations

### Prerequisites
- **Node.js** (version 16 or higher)
- **npm** (Node Package Manager)

### Steps to Setup

1. **Clone the Repository**   
   ```bash
   git clone <repository-url>
   cd ZK_Project_VeriSync
2. **Install Dependencies**
   ```bash
   npm install
3. **Compile the circuit **
   ```bash
   circom Equation.circom --r1cs --wasm --sym

4. ** Trusted setup **
   ```bash
   snarkjs powersoftau new bn128 12 pot_final.ptau
   snarkjs groth16 setup Equation.r1cs pot_final.ptau Equation_0000.zkey
   snarkjs zkey contribute Equation_0000.zkey Equation_final.zkey --name="First contribution" -v
   snarkjs zkey export verificationkey Equation_final.zkey verification_key.json

5. **Generate the witness **
   ```bash
   node Equation_js/generate_witness.js Equation_js/Equation.wasm input.json witness.wtns

6. ** Generate the proof **
   ```bash
   snarkjs groth16 prove Equation_final.zkey witness.wtns proof.json public.json

7. ** Verify the proof **
   ```bash
   snarkjs groth16 verify verification_key.json public.json proof.json


  📝 Findings
Inputs Used: The input value for 𝑥
x was set to 3.
Generated Proof: The proof was generated successfully.
Verification Outputs: The verification confirmed that the proof is valid.
Challenges Faced:
Module Dependencies: Encountered issues with module dependencies, resolved by reinstalling snarkjs.
Input Format: Ensured the correct input format for the proof generation.

CIRCUIT :![circom_equation](https://github.com/user-attachments/assets/2658072b-c073-44b4-9463-d9cc6486a01c)

COMPILING CIRCUIT: ![compiling_circuit](https://github.com/user-attachments/assets/95074823-551f-42cf-a2a1-6094a06b944f)

TRUSTED SETUP :![perfrom trusted setup](https://github.com/user-attachments/assets/96c36dee-ec80-48b4-bd88-b9ec7b68a7fc)

WITNESS PROOF GENERATION FILE :![witness](https://github.com/user-attachments/assets/febcc1f5-b457-4aec-a7b7-ed58a66b31fc)

VERIFICATION KEY GENERATION : ![verification key genrated](https://github.com/user-attachments/assets/c34d625c-a4e2-4e4d-a33c-29324d4fd423)






📝 Findings
Inputs Used: The input value for 𝑥
x was set to 3.
Generated Proof: The proof was generated successfully.
Verification Outputs: The verification confirmed that the proof is valid.

OUTPUT OBTAINED FINAL VERIFICATION: ![OUTPUT_!](https://github.com/user-attachments/assets/f68d59a8-1426-4bd9-a00b-7a646055ebb5)
 

Challenges Faced:
Module Dependencies: Encountered issues with module dependencies, resolved by reinstalling snarkjs.
Input Format: Ensured the correct input format for the proof generation.

⚖️ Trade-offs in ZK Protocols
Summary of Trade-offs
Aspect	Groth16	Plonk	STARKs
Proof Generation Time	Moderate to long (dependent on setup)	Fast (due to polynomial commitment)	Longer due to hash computations
Proof Size	Small (around 100 bytes)	Small to moderate	Larger (depending on depth of circuit)
Verification Time	Very fast (a few milliseconds)	Fast, but dependent on the implementation	Moderate (but scalable)
TRADE OFFS:![summary](https://github.com/user-attachments/assets/e2443c01-7d51-4302-a320-b26b9d43d354)


🎯 Conclusion
The project successfully showcases the capabilities of zero-knowledge proofs, particularly through the Groth16 protocol. The implementation emphasizes the potential of ZK technology for privacy-preserving computations across various applications.

🔮 Future Work
Explore Other ZK Protocols: Investigate Plonk and STARKs for further comparisons.
Optimize Proof Generation: Focus on reducing proof size and generation time.

📚 References
snarkjs Documentation
Circom Documentation
