# 06. Configurar múltiplas contas Git no mesmo computador

Em caso de necessitar logar com duas ou mais contas diferentes do git no mesmo computador, realize as seguintes configurações:

- Configure um arquivo `config` no diretório `~/.ssh/`:

```
$ cd ~/.ssh
$ touch config
```

- Esse arquivo deverá conter um alias para cada usuário, exemplo:

``` 
Host github.com
	HostName github.com
	User git
	IdentityFile ~/.ssh/id_ed25519_usuario-principal

```

A linha `IdentityFile` refere-se ao arquivo de chave privada. Por isso, deverá existir uma chave configurada para cada usuário existente no arquivo.

Ao configurar a chave de cada usuário, uma sugestão, é adicionar o nome do usuário como um sufixo ao nome do arquivo da chave, conforme o exemplo acima.

Desta forma, poderá ir adicionando no `config` essa configuração, na medida que necessitar criar novos usuários do git no computador, exemplo:

``` 
Host github-usuario-secundario
	HostName github.com
	User git
	IdentityFile ~/.ssh/id_ed25519_usuario-secundario

```

Na linha `Host github-usuario-secundario`, definimos o alias utilizado para aquele usuário.

Por fim, quando for criar o repositório local, a url do ssh do origin, será composta com o alias existente na variável Host, do `config`. Exemplo: 

```
$ git remote -v
origin	git@github-usuario-secundario:usuario-secundario/test.git (fetch)
...
```

> Lembrando que para o usuário principal, não é necessário configurar um alias, já que será o usuário padrão.

```
Host github.com
```