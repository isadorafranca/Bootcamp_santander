# Introdução ao Git

## GUI X GLI

Gui - graphic user interface

Cli - command line interface 

## O que vamos aprender?

- Mudar pastas
- Listar as pastas
- Criar pastas
- Delete pastas

## Comandos

- Dir - listar os diretórios.
- cd / - navegar para outra pasta específica.
- Cd.. voltar no comando cd
- Cls - limpar tela
- Mkdir - criar uma pasta
- Criar arquivos:
    - Echo frase
        - Echo frase > frase.txt
- Del - deletar arquivos
- Rmdir - apagar diretório
- Obs: tab atalho pra autocompletar.

## Objetos internos do Git

Blobs

Trees

Commits 

## FORMAS DE AUTENTICAÇÃO

## Chave SSH e Token

Criar chave ssh: 

Abrir git bash e executar os comandos:

- ssh-keygen -t ed25519 -c “seu email”

Ir no diretório da chave e usar o comando:

- cat id_ed25519.pub

Logo depois:

- eval $(ssh-agent -s)

## Token de acesso pessoal

## Iniciando o git e criando commit

- git init
- git add
- git commit

Para começar vá até a pasta pra criar e siga a sequência de comandos 

Git init

Ls

Ls -a.

Se for primeira vez usando git vc precisar dar um email e um nome para o git:

Git config --global [user.email](http://user.email) “seuemail.com”

Git config --global [user.name](http://user.name) Nome

## Adicionando arquivo

Git add *

Git commit -m “nomecommit”

### Git status monitorar status

git status 

Mover arquivo para outro repositório:

mv “arquivo” ./nomedapasta/

## Comandos de alteração de email e username do Git

- Git config - - list → mostrar configurações gerais do Git.
- Git config - -global - - unset [user.name](http://user.name) → tira os atributos globais de user.name
- Git config - - global [user.name](http://user.name) “nomedoname”

## Empurrando versão do repositório local para repositório remoto

Adicionar origem:

- Git remote add origin “linkgithub”

Listar repositório cadastrados:

- Git remote -v

Empurrando ára repositorio remoto:

- git push origin master

obs: um comando também muito imporante é o “git pull origin master”: puxar arquivos de um repositorio remoto para seu repositorio local.

obs: comando para clonar repositorio remoto no git:

- git clone “linkdorep”
