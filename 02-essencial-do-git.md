# 02 - Essencial do Git - Parte I

## Inicializando um repositório

> Os exemplos de saída de código, foram extraídos de um prompt no ambiente Linux

Para inicializar um repositório, dentro da pasta do projeto, execute o comando:

```
$ git init
```

Uma estrutura de diretório será criada para monitorar o versionamento. Considerando um diretório chamado `git-e-github-para-iniciantes`, a estrutura seria algo como: 

```
git-e-github-para-iniciantes/
├── .git
│   ├── branches
│   ├── COMMIT_EDITMSG
│   ├── config
│   ├── description
│   ├── HEAD
│   ├── hooks
│   ├── index
│   ├── info
│   ├── logs
│   ├── objects
│   ├── ORIG_HEAD
│   └── refs
└── Readme.md
```

## O ciclo de vida e os status de seus arquivos

- **untracked:** não marcado, o arquivo acabou de ser adicionado no repositório e ainda não foi reconhecido pelo git.

```
$ touch Readme.md
$ git status

On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	Readme.md

nothing added to commit but untracked files present (use "git add" to track)
```

> `touch` é um comando Linux, utilizado para _tocar_ um arquivo. Caso o arquivo existe, a data de modificação é alterada, caso não existe, o arquivo é criado.

- **unmodified:** o arquivo foi adicionado no stage, mas não foi feito o commit.

```
$ git add .
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   Readme.md

```

- **modified:** o arquivo existe no stage, porém ainda existem alterações que devem ser enviadas para o stage/adicionadas.

```
$ echo "Nova linha adicionada" >> Readme.md 
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   Readme.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   Readme.md


```

- **staged:** alterações incluídas no stage, ou seja, o arquivo está disponível para commit.

```
$ git add .
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   Readme.md

```

Nesse caso, para fazer o commit, execute o comando:

```
$ git commit -m 'Add Readme.md'
[master (root-commit) fef5e6e] Add Readme.md
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 Readme.md
$ git status
On branch master
nothing to commit, working tree clean
```

# 02 - Essencial do Git - Parte II

## Visualizando logs

- Para verificar o histório de alterações podemos utilizar:

```
$ git log
commit 39a8f346ebcbcaa6960eb41f4b9f79a1299f9d3d (HEAD -> master)
Author: learnermap <email@gmail.com>
Date:   Thu Jan 23 09:31:31 2020 -0300

    Nova linha add

commit 4abd079354ec6e3546b25a8318776543c9b84642
Author: learnermap <email@gmail.com>
Date:   Thu Jan 23 09:26:48 2020 -0300

    Commit inicial
```

- Informações adicionais no log:

```
$ git log --decorate
```

- Filtro pelo autor

```
$ git log --author="Will"
```

- Log resumido

```
$ git shortlog
```

- Somente quantidade de commits e o nome

```
$ git shortlog -sn
```

- Exibindo em forma gráfica

```
$ git log --graph
```

- Identificando alterações pela hash

```
$ git show 3621c562ca13cd41cde6334c643e8412ab6ac053
```

# 02 - Essencial do Git - Parte III

## Visualizando o diff

- Visualizando mudanças antes do stage.

```
$ git diff
$ echo "Nova linha adicionada 5" >> Readme.md 
learnermap@linux:~/courses/git/test$ git diff
diff --git a/Readme.md b/Readme.md
index ca6549f..0b73485 100644
--- a/Readme.md
+++ b/Readme.md
@@ -4,3 +4,5 @@ Nova linha adicionada
 Nova linha adicionada 1
 Nova linha adicionada 2
 Nova linha adicionada 3
+Nova linha adicionada 4
+Nova linha adicionada 5
```

- Exibindo somente o nome do arquivo modificado.

```
git diff --name-only
```

# 02 - Essencial do Git - Parte IV

## Desfazendo coisas

#### Excluindo alterações antes do stage

```
$ echo "Nova linha adicionada 7" >> Readme.md 
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   Readme.md

no changes added to commit (use "git add" and/or "git commit -a")
$ git diff
diff --git a/Readme.md b/Readme.md
index 654e88c..fba9807 100644
--- a/Readme.md
+++ b/Readme.md
@@ -7,3 +7,4 @@ Nova linha adicionada 3
 Nova linha adicionada 4
 Nova linha adicionada 5
 Nova linha adicionada 6
+Nova linha adicionada 7
```

Alteração adicionada.

```
$ git checkout Readme.md
$ git status
On branch master
nothing to commit, working tree clean
$ git diff
$ 
```

#### Excluindo alterações no stage

```
$ echo "Nova linha adicionada 7" >> Readme.md 
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   Readme.md

no changes added to commit (use "git add" and/or "git commit -a")
$ git add .
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   Readme.md
```

Neste ponto, as modificações já foram enviadas para o stage.

```
$ git reset HEAD
Unstaged changes after reset:
M	Readme.md
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   Readme.md

no changes added to commit (use "git add" and/or "git commit -a")
```

Modificações removidas do stage.

```
$ git checkout Readme.md
$ git status
On branch master
nothing to commit, working tree clean
$ 
```

Modificações removidas do arquivo.

#### Excluindo alterações no commit

- **soft**: remove alterações do commit, deixando no stage. 

```
$ git reset --soft 9936c23
```

- **mixed**: remove alterações do commit e stage, deixando no arquivo.

```
$ git reset --mixed 9936c23
```

- **hard**: remove todas as alterações.

```
$ git reset --hard 9936c23
```

**Importante**: 

- Sempre informar o hash do commit anterior ao que será excluído!
- Utilize o reset hard antes do push.

# 02 - Essencial do Git - Parte VI

## Commitando pastas/diretórios vazios

 Por padrão, o git não reconhece diretórios vazios. Desta forma, existe uma convenção utilizada quando se deseja incluir diretórios vazios que é criar um arquivo chamado `.gitkeep`.

```
$ mkdir diretorio-vazio
$ git status
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)
$ touch diretorio-vazio/.gitkeep
$ git status
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        diretorio-vazio/

nothing added to commit but untracked files present (use "git add" to track)

```
