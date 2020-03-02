# PrivDPI——Literature Notes

$PrivDPI$, which reduces the setup delay while retaining similar privacy guarantee:

The intermediate values generated in each session can be reused across subsequent sessions for repeated tokens, which could further speedup token encryption.

## System Flow

$PrivDPI$ consists of the following six phases:

-  **Setup**: **MB** receives **a set of rule tuples** from **RG**. And,  **C** and **S** establish **a session key** through the TLS handshake protocol.
- **Preprocessing**: **MB** interacts with **C** and **S** to establish **a set of reusable obfuscated rules**.
- **Session Rule Preparation**: the reusable obfuscated rules generated in the Preprocessing phase are used as "seeds" to establish **the session rules** for the TLS session.
- **Token Encryption**: **Each tokens is encrypted**, which will be used for matching during the token detection phase.
- **Token Detection**:  **MB** first generated encrypted rules using the session rules generated in the session rule preparation phase. It then performs token detection based on the encrypted tokens received from **C** and the encrypted rules it generated.

Preliminaries:

- Notation : 
  - PPT: probabilistic polynomial-time
  - $\mathbb{N}$ : natural numbers
  - [N] :  the set {1,....,N}
  - [ i, j] : the set {i, i+1, i+2,....,j}
- Bilinear Maps:
  - $G$ and $G_T$: two multiplicative cyclic groups of prime order $p$.
- Computational Diffie-Hellman (CDH) Assumption.
- Decisional Diffie-Hellman (DDH) Assumption

Notation:

![](.\img\notation.PNG)

### First phase: Setup





