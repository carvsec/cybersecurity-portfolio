# Cryptography Basics & Public Key Cryptography

**Data:** 03/08/2026 | **Categoria:** Cryptography

## O que aprendi

Conceitos Fundamentais: Compreendi a terminologia base de criptografia. Plaintext é o dado legível, ciphertext é o dado cifrado, cipher é o algoritmo de conversão e key é a informação secreta que o algoritmo utiliza.  

Criptografia Simétrica vs. Assimétrica: A simétrica utiliza uma única chave para cifrar e decifrar os dados, como ocorre no DES, 3DES e AES. Já a assimétrica emprega um par de chaves composta por chave pública e chave privada, como nos algoritmos RSA, Diffie-Hellman e ECC.  

Operações Matemáticas: Estudei a lógica matemática por trás dos algoritmos, com foco nas operações de XOR e cálculo de módulo.  

Aplicações de Chave Pública: A criptografia assimétrica vai além da confidencialidade. Ela garante autenticação para confirmar a identidade, autenticidade para certificar a origem da mensagem e integridade para assegurar que o dado não foi alterado. Isso se aplica na prática no SSH, certificados SSL e TLS, PGP e GPG.  

## Prática

Apliquei os conceitos de criptografia assimétrica utilizando o GPG com par de chaves para cifrar, decifrar e assinar arquivos:

```bash
gpg --import chave_publica.asc
gpg --encrypt --recipient user@tryhackme arquivo.txt
gpg --decrypt arquivo.txt.gpg
```

Também pratiquei a operação XOR como cifra simétrica simples, utilizando a fórmula C = P XOR K e P = C XOR K para recuperar o texto original. Além disso, trabalhei com cálculo de módulo, que serve de base matemática para algoritmos como o RSA.

Referência
https://tryhackme.com/room/cryptographybasics
https://tryhackme.com/room/publickeycrypto
