# 🖨️ Controle de Impressora Térmica Elgin em C
 
Programa em linguagem C que controla uma impressora térmica **Elgin i8 / i9** por meio da biblioteca oficial da Elgin (`E1_Impressora01.dll`). O usuário faz login, escolhe uma opção em um menu e o programa envia o comando para a impressora: imprimir texto, QR Code, código de barras, cupom SAT, abrir a gaveta, emitir sinal sonoro e mais.
 
Trabalho desenvolvido para a disciplina de **Construção de Algoritmos e Programação** — UNASP.
 
---
 
## 📋 O que o programa faz
 
- Carrega a `E1_Impressora01.dll` dinamicamente (`LoadLibraryA` / `GetProcAddress`).
- Pede **login** (até 3 tentativas, mostrando as restantes).
- Exibe um **menu em laço** até o usuário escolher sair.
- Bloqueia qualquer pergunta de impressão quando a **conexão está fechada**.
- Confere o **retorno de cada comando** e mostra mensagem de sucesso ou erro.
- Libera a memória (`free`) dos arquivos XML lidos.
- Não quebra se forem digitadas letras onde se espera número.
---
 
## 🔐 Login de teste
 
| Usuário | Senha |
|---------|-------|
| `admin` | `1234` |
 
---
 
## 📑 Opções do menu
 
| Nº | Opção |
|----|-------|
| 1 | Configurar conexão |
| 2 | Abrir conexão |
| 3 | Fechar conexão |
| 4 | Imprimir texto |
| 5 | Imprimir QR Code |
| 6 | Imprimir código de barras |
| 7 | Imprimir XML SAT |
| 8 | Imprimir XML de cancelamento SAT |
| 9 | Abrir gaveta (Elgin) |
| 10 | Abrir gaveta |
| 11 | Sinal sonoro |
| 0 | Sair |
 
---
 
## 📁 Estrutura do projeto
 
```
.
├── main.c                 # Código-fonte do programa
├── E1_Impressora01.dll    # Biblioteca da Elgin (versão x64)
├── XMLSAT.xml             # XML de teste para o cupom SAT
├── CANC_SAT.xml           # XML de teste para o cancelamento SAT
└── README.md
```
 
---
 
## ⚙️ Como compilar e executar
 
### Requisitos
 
- Windows
- Compilador **gcc** (MinGW / MSYS2)
- Impressora Elgin i8 ou i9 ligada e conectada por cabo USB
### 1. Descobrir se o seu compilador é 32 ou 64 bits
 
```bash
gcc -dumpmachine
```
 
| Resultado | Compilador | DLL a usar |
|-----------|------------|------------|
| `x86_64-w64-mingw32` | 64 bits | **x64** (a que já está neste repositório) |
| `mingw32` ou `i686-w64-mingw32` | 32 bits | **x86** (ver observação abaixo) |
 
> ⚠️ A DLL e o compilador precisam ter a **mesma arquitetura**. A `E1_Impressora01.dll` deste repositório é a versão **x64 (64 bits)**. Se o seu compilador for de 32 bits, substitua-a pela versão **x86** da biblioteca fornecida pela Elgin / pelo professor.
 
### 2. Compilar
 
Dentro da pasta do projeto:
 
```bash
gcc main.c -o impressora.exe
```
 
### 3. Executar
 
```bash
impressora.exe
```
 
> A DLL e os arquivos XML precisam estar na **mesma pasta de onde o programa é executado**.
 
### 4. Uso básico
 
1. Faça login (`admin` / `1234`).
2. Opção **1** — configure a conexão (para teste: tipo `1`, modelo `i9`, porta `USB`, parâmetro `0`).
3. Opção **2** — abra a conexão.
4. Use as demais opções.
5. Opção **0** — fecha a conexão e encerra o programa.
---
 
## 🛠️ Possíveis erros
 
| Mensagem | Causa provável |
|----------|----------------|
| `erro 126` ao carregar a DLL | DLL fora da pasta de execução |
| `erro 193` ao carregar a DLL | DLL com arquitetura diferente do compilador (32 x 64 bits) |
| `Comando '...' nao encontrado na DLL` | DLL errada ou de outra versão |
| Erro ao abrir conexão (código negativo) | Impressora desligada, cabo solto ou configuração errada |
| `Nao foi possivel ler o XML` | XML fora da pasta de execução |
 
---
 
## 📚 Documentação
 
- [Documentação oficial da Elgin](https://elgindevelopercommunity.github.io/group___m1.html)
---
