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
- [ACLS18]:  [PIR with compressed queries and amortized query processing](https://eprint.iacr.org/2017/1142.pdf)
- Youtube Video: https://www.youtube.com/watch?v=GljDWxdu0tI
- Code: https://github.com/microsoft/SealPIR
- Summary: SealPIR is a very classic PIR scheme based on the BFV. Its core technology is the introduction of the Expand algorithm, which compresses n query Ciphertext into 1. The SealPIR scheme has a profound impact on subsequent PIR schemes.


### Preprocessing
