# 01. Configurando o Git

## Instalando o Git

Em sistemas linux baseados no Debian:

```
# apt install git
```

## Configuração inicial do Git

Existem diversas configurações possíveis para o git. Inicialmente, podemos utilizar:

- Nome do usuário:

```
$ git config --global user.name 'Seu nome de Usuário'
```

- Email:

```
$ git config --global user.email 'email@email.com'
```

- Editor:

```
$ git config --global core.editor 'sublime'
```

Ao final das configurações, podemos listar os valores:

```
$ git config --list
```

- Configurando o nome da branch principal padrão

```
$ git config --global init.defaultBranch main
```