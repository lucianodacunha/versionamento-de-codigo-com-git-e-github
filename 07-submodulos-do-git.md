# 07. Submódulos do git

Basicamente, com submódulos é possível ter um diretório como um repositório.

Essa é uma forma de manter um projeto como dependência de um projeto principal.

## Comandos

- Adicionar um submódulo

```
git submodule add https://url-do-submodulo.git nome-do-diretorio
```

Um novo diretório é criado, além de um arquivo .gitmodules. 

- Atualizando o submódulo

Todas os pushes realizados no submodulo serão enviados para o repositório principal. 

Desta forma, para atualizar o repositório hospedeiro, será necessário commitar as alterações na raiz e empurrar para o origin

```
sub1$ cd ..
host$ git add .
host$ git commit -m 'sub updated.'
host$ git push origin main
```

- Clonando o hospedeiro

Quando clonamos um repositório, os submódulos não serão atualizados automaticamente. É preciso ser explícito utilizando `--recursive`.

```
$ git clone --recursive git@url-do-repo-.git
```

ou atualizar os submódulos posteriormente:

```
$ git clone git@repo-.git
$ git cd repo
$ git submodulo update --init --recursive
```
## Outras referências

- [Como trabalhar com submodulos git](https://www.tabnews.com.br/wrasilva/como-trabalhar-com-submodulos-git)
- [Git Submodules basic explanation](https://gist.github.com/gitaarik/8735255)
- [Submódulos do Git](https://www.atlassian.com/br/git/tutorials/git-submodule)
- [Submódulos do Git](https://lente.dev/posts/submodulos-git/)
  