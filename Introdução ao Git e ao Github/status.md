## Status Github
Acho que podemos entender melhor estes estados criando um projeto do zero. Primeiro vou criar uma pasta chamada "projeto" e entrar nela:

$ mkdir projeto
$ cd projeto/
Por enquanto ela está vazia. Vou usar git init para inicializá-la como um repositório Git:

$ git init
Initialized empty Git repository in C:/Users/usuario/projeto/.git/
Agora vou começar meu projeto adicionando um arquivo (com o conteúdo "hello world" dentro dele), e em seguida verificar o status deste arquivo com git status:

$ echo "hello world" > hello.txt

$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        hello.txt

nothing added to commit but untracked files present (use "git add" to track)
Veja que o arquivo hello.txt está listado como "Untracked files". Ou seja, o Git não está "trackeando" este arquivo. Podemos dizer que o Git não está controlando o ciclo de vida deste arquivo (e confesso que não sei se "ciclo de vida" é o termo tecnicamente correto).

É como se o Git dissesse: "Vi que que tem um arquivo aqui, mas eu não sou responsável por ele".

Para que o Git passe a ser responsável por este o arquivo, use git add:

$ git add hello.txt

$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   hello.txt
Agora o arquivo está listado como "Changes to be committed", ou seja, ele fará parte do próximo commit. Diz-se então que o arquivo está "staged" (ou está na staging area, ou no index, ou no cache, não sei pra que tantos nomes para a mesma coisa).

De qualquer forma, repare que há inclusive uma instrução para retirar o arquivo do staging area (use "git rm --cached <file>..." to unstage - nas versões mais novas do Git a mensagem é "git restore --staged <file>... to unstage").

Em vez de unstagear o arquivo, vamos commitá-lo (adoro esses estrangeirimos...)

$ git commit -m"Primeiro commit"
[master (root-commit) ccc2a05] Primeiro commit
 1 file changed, 1 insertion(+)
 create mode 100644 hello.txt

$ git status
On branch master
nothing to commit, working tree clean
Após o commit, o git status diz que não há o que mostrar ("nothing to commit, working tree clean"), ou seja, todos os arquivos estão atualizados: o seu conteúdo bate com o último commit, não houve nenhuma alteração). Pode-se dizer então que o arquivo hello.txt está unmodified (não há modificações, se comparado com o último commit).

Então vamos alterar o arquivo, adicionando algum texto ao seu final:

$ echo "Novo texto" >> hello.txt

$ cat hello.txt
hello world
Novo texto
Agora o arquivo tem 2 linhas, vamos ver o que o git status mostra:

$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   hello.txt

no changes added to commit (use "git add" and/or "git commit -a")
Ele mostra que o arquivo está modified, ou seja, foi modificado, se comparado ao último commit. Mas repare que esta modificação não estará no próximo commit, pois o arquivo está listado como "Changes not staged for commit" e no final ainda aparece a mensagem "no changes added to commit".

Eu posso ver as modificações usando git diff:

$ git diff
diff --git a/hello.txt b/hello.txt
index 3b18e51..7d34649 100644
--- a/hello.txt
+++ b/hello.txt
@@ -1 +1,2 @@
 hello world
+Novo texto
O trecho +Novo texto indica que esta linha foi adicionada (+). Para a alteração ficar disponível no próximo commit, basta usar git add:

$ git add hello.txt

$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   hello.txt
Repare que o arquivo continua com status "modified" (afinal, ele está diferente do último commit), mas agora estará no próximo commit ("Changes to be committed").

Ou seja, ele está ao mesmo tempo modified (diferente se comparado ao último commit) e staged (pois está na staging area).

O fato de estar na staging area faz com que git diff não mostre mais as diferenças:

$ git diff
(não mostra nada)
Para saber o que mudou, deve-se usar a opção --cached, que compara o staging area (também chamado de cache) com o último commit:

$ git diff --cached
diff --git a/hello.txt b/hello.txt
index 3b18e51..7d34649 100644
--- a/hello.txt
+++ b/hello.txt
@@ -1 +1,2 @@
 hello world
+Novo texto
A propósito, --cached é equivalente a --staged - ou seja, compara os arquivos que estão staged com o último commit.

Resumindo:

untracked: o git não sabe nada a respeito do arquivo. Quer dizer, até sabe que ele existe, mas não vai controlar seu ciclo de vida
staged: os que estão no staging area/index/cache. São os que estarão no próximo commit
modified: os que foram alterados, se comparados ao último commit
unmodified: os que não foram alterados
Por fim, vale lembrar que a documentação diz que na verdade só existem dois estados: tracked e untracked. 
  Ou seja, ou o Git está controlando o ciclo de vida do seu arquivo (tracked) ou não está (untracked). 
  Sendo que um arquivo no estado tracked pode estar staged, modified ou unmodified.
