# Hashing Basics

**Data:** 03/08/2026 | **Categoria:** Cryptography

## O que aprendi
- **Diferença entre Hash e Criptografia:** o hash não utiliza chave e não é reversível. Sua finalidade é garantir a integridade dos dados e a verificação de senhas, sem focar em confidencialidade.
- **Efeito Avalanche:** qualquer alteração mínima na entrada modifica completamente a saída gerada.
- **Segurança de Senhas:** armazenar senhas em texto puro ou utilizar hash sem salt é vulnerável a ataques de tabela rainbow. O uso de salt combinado a algoritmos como Bcrypt e Argon2 previne essa fragilidade.
- **Quebra vs. Decriptação:** entendi que quebrar um hash consiste em testar candidatos até encontrar uma correspondência com ferramentas como Hashcat e John the Ripper, enquanto a decriptação não se aplica ao conceito de hash.

## Prática
Gerei e comparei hashes de dois arquivos praticamente idênticos, com apenas 1 bit de diferença entre eles:
```bash
hexdump -C file2.txt
md5sum *.txt
sha1sum *.txt
sha256sum *.txt
```
Resultado: mesmo com a alteração de apenas um bit no arquivo de entrada, os hashes MD5, SHA1 e SHA256 geraram saídas completamente distintas entre os dois arquivos.

Também verifiquei a integridade de uma imagem ISO comparando o hash SHA256 do arquivo baixado com o hash assinado oficialmente:
```bash
sha256sum Fedora-Workstation-Live-x86_64-40-1.14.iso
```

## Referência
https://tryhackme.com/room/hashingbasics
