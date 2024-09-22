<!--
 * @Description: 
 * @Author: Qixian Zhou
 * @Date: 2024-09-22 18:35:23
-->
# awesome-pir
---

This repo is a paper summary for **private information retrieval** (PIR). Please note that the main focus here is on **Single-Server PIR**. Besides a simple summary of the papers related PIR, I will provide a summary of the key technical constructions for each PIR scheme.


##  PIR papers

We categorize the current PIR schemes into two types based on whether they have a preprocessing phase: those without preprocessing and those with preprocessing.


### Without Preprocessing


#### SealPIR [S&P-2018]
- ACLS18:  [PIR with compressed queries and amortized query processing](https://eprint.iacr.org/2017/1142.pdf)
- Youtube: https://www.youtube.com/watch?v=GljDWxdu0tI
- Code: https://github.com/microsoft/SealPIR
- Summary: SealPIR is a very classic PIR scheme based on the BFV. Its core technology is the introduction of the Expand algorithm, which compresses n query Ciphertext into 1. The SealPIR scheme has a profound impact on subsequent PIR schemes.

#### MulPIR [USENIX-2021]
- ALPR21: [Communication–Computation Trade-offs in PIR](https://www.usenix.org/system/files/sec21-ali.pdf)
- Youtube: https://www.youtube.com/watch?v=1sbIHz7gHQ8
- Code: https://github.com/OpenMined/PIR
- Summary: Modification of SEAL-PIR: 
  - The Expand operation has been optimized, allowing multi-dimensional queries to compress the `d` query ciphertexts required by SealPIR into **one**; 
  - In the vector inner product calculation phase, the operation directly uses `ciphertext * ciphertext`, compressing the `F`ciphertexts needed for Response in SealPIR into one. But this will increase server's computation cost.

#### FastPIR [USENIX-OSDI-2021]
- AYAA21: Addra: [Metadata-private voice communication over fully untrusted infrastructure](https://www.usenix.org/conference/osdi21/presentation/ahmad)
- Youtube: https://www.youtube.com/watch?v=RAlPCWZnVJA
- code: https://github.com/anysphere/anysphere-messaging
- Summary: The SIMD+Rotate construction is a different approach compared to SealPIR. While it can reduce the communication of the Response, it increases the computational cost on the server side.

#### OnionPIR [CCS-2021]
- OnionPIR: [Response Efficient Single-Server PIR](https://eprint.iacr.org/2021/1081.pdf)
- Code: https://github.com/mhmughees/Onion-PIR
- Summary: The core contribution is the introduction of the **extern product** operation between BFV ciphertext and RGSW ciphertext, which significantly reduces the noise growth in ciphertext multiplication. This replaces the Decompose operation on intermediate ciphertexts in SealPIR, reducing the response size from $F^{d-1}$ in SealPIR to a single BFV ciphertext.

#### Pantheon [VLDB-2022]
- Pantheon: [Private Retrieval from Public Key-Value Store](https://www.vldb.org/pvldb/vol16/p643-ahmad.pdf)
- Summary: The core is to perform an equality test on the keyword, which computes a Selection Vector. This is then used for ciphertext dot products with the database value vector. However, the experimental results are not very solid, and the FHE parameters used are quite large.

#### Constant-weight PIR [USENIX-2022]
- MK22: [Constant-weight PIR: Single-round Keyword PIR via Constant-weight Equality Operators](https://www.usenix.org/conference/usenixsecurity22/presentation/mahdavi)
- Youtube: https://www.youtube.com/watch?v=OSMpwmVlZBs
- Code: https://github.com/RasoulAM/constant-weight-pir
- Summary: First, encode the data, then perform ciphertext matching row by row to compute a selection vector. This vector can then be used for inner products with the database. However, the experimental data of the paper shows that the performance of this PIR is very slow.

#### Spiral [S&P-2022]
- Spiral: [Fast, High-Rate Single-Server PIR via FHE Composition](https://eprint.iacr.org/2022/368)
- Youtube: https://www.youtube.com/watch?v=bI7lmKCAmA0
- Code: 
  - https://github.com/blyssprivacy/sdk/tree/main/lib/spiral-rs
  - https://github.com/menonsamir/spiral-rs



### Preprocessing

#### Pai [Cryptology ePrint Archive 2024-03-03]
- Pai: [Private Retrieval with Constant Online Time,Communication, and Client-Side Storage for Data Marketplace.](https://eprint.iacr.org/2023/1619)
- Summary: The client needs to download and upload the entire server database for processing.The online query performance is quite high, capable of querying 10 million data entries of 256 bytes within 1 ms.

#### SimplePIR & DoublePIR [USENIX-2023]

- Paper: [One Server for the Price of Two: Simple and Fast Single-Server Private Information Retrieval](https://www.usenix.org/system/files/sec23summer_27-henzinger-prepub.pdf)
- Youtube: https://www.youtube.com/watch?v=ODdWD_gvbN8&t=11s
- Code: https://github.com/ahenzinger/simplepir
- Summary: SimplePIR takes full advantage of Regev's ciphertext structure and the shape of the database by precomputing the parts that are independent of the queries.


#### Piano [S&P-2024]
- [Piano: Extremely Simple, Single-Server PIR with Sublinear Server Computation](https://eprint.iacr.org/2023/452)
- Youtube: https://www.youtube.com/watch?v=1EBY6VcCH0E
- Code: https://github.com/pianopir/Piano-PIR



## Other materials

- [011 Single-server private information retrieval using homomorphic encryption w/ Muhammad Haris](https://www.youtube.com/watch?v=pRkSYjOuhdk&t=1076s)
- [How Practical is Single-Server Private Information Retrieval?](https://ethz.ch/content/dam/ethz/special-interest/infk/inst-infsec/appliedcrypto/education/theses/semester-project_sophia-artioli.pdf)