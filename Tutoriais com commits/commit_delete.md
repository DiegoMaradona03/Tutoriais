# Tutorial para deletar commits no GitHub usando rebase

## 1. Abrir o terminal
1.1. Abra o **Git Bash** ou um **terminal pelo VSCode** na pasta do projeto.  
1.2. Execute o comando para iniciar um rebase interativo:  
```
git rebase -i --root
```
> Use `--root` se quiser incluir o **primeiro commit** na lista de commits a serem editados.  

> Como alternativa, você pode rebasear a partir de qualquer commit que deseja manter como por exemplo:  
```
git rebase -i b898f07
```
> Somente os commits posteriores ao commit especificado poderão ser alterados.

1.3. Caso haja algum problema ou rebase anterior não finalizado, use:  
```
git rebase --abort
```
> Depois disso, tente novamente o comando anterior.

---

## 2. Entender a tela de rebase
Após executar o rebase interativo, aparecerá algo semelhante a isto:  
```
pick numeração do commit 1 Mensagem do commit 1
pick numeração do commit 2 Mensagem do commit 2
pick numeração do commit 3 Mensagem do commit 3

# Comandos disponíveis:
# p, pick = manter o commit
# r, reword = manter, mas editar a mensagem
# e, edit = parar para alterar o commit
# s, squash = juntar com o commit anterior
# f, fixup = juntar, mantendo só a mensagem anterior
# x, exec = executar comando shell
# b, break = parar o rebase
# d, drop = deletar commit
# ...
```
> Observação: **esses comandos não são digitados ainda**, você precisa entrar no modo de edição.

---

## 3. Entrar no modo de edição
3.1. Clique dentro do terminal e pressione a tecla `i` para entrar no **modo de inserção**.  

---

## 4. Modificar os commits
4.1. Substitua `pick` por `drop` para deletar ou por outro comando nos commits que desejar fazer alguma alteração:  
```
pick numeração do commit 1 Mensagem do commit 1
drop numeração do commit 2 Mensagem do commit 2
drop numeração do commit 3 Mensagem do commit 3
```
> O commit marcado como `drop` será **removido permanentemente** do histórico.

---

## 5. Salvar e sair
5.1. Pressione `Esc` para sair do modo de inserção.
5.2. Digite manualmente o comando para salvar e sair:  
```
:wq
```
> - Não copie e cole; digite manualmente e pressione `Enter`.
> - O comando **parece invisível enquanto você digita**, mas isso é normal e **não significa que ele não está sendo registrado**.
> - Após digitar, pressione `Enter`. O rebase continuará com os commits que você manteve e removerá os que marcou como `drop`.

---

## 6. Confirmar as alterações
6.1. Para enviar as alterações ao GitHub, no terminal use uma das opções abaixo:

- **Forçar push padrão**:  
```
git push --force
```
> ⚠️ Sobrescreve o histórico remoto. Só faça isso se tiver certeza de que ninguém mais está trabalhando nessa branch.

- **Forçar push seguro (recomendado)**:  
```
git push --force-with-lease
```
> ✅ Só sobrescreve se ninguém tiver enviado novos commits no remoto desde seu último pull. Evita apagar alterações de outras pessoas inadvertidamente.

---

## ⚠️ Aviso de extrema importância
Após executar o rebase interativo e entrar no modo de edição não tire em hipótese alguma todos os commits que aparecerem lista, isso irá apagar todos de uma só vez! ao invés disso use apenas drop! aqui um exemplo abaixo do que você deve ou não fazer:

### Exemplo simplificado:
Você é um programador que deseja deletar o **sétimo commit** em seu projeto.  
Para isso, você utiliza o comando:

```bash
git rebase -i HEAD~9
```

Com isso, aparecerão todos os commits já realizados no projeto dentro do terminal, junto com a lista de comandos disponíveis:

```
pick numeração do commit 1 Mensagem do commit 1
pick numeração do commit 2 Mensagem do commit 2
pick numeração do commit 3 Mensagem do commit 3
pick numeração do commit 4 Mensagem do commit 4
pick numeração do commit 5 Mensagem do commit 5
pick numeração do commit 6 Mensagem do commit 6
pick numeração do commit 7 Mensagem do commit 7
pick numeração do commit 8 Mensagem do commit 8
pick numeração do commit 9 Mensagem do commit 9

# Comandos disponíveis:
# p, pick = manter o commit
# r, reword = manter, mas editar a mensagem
# e, edit = parar para alterar o commit
# s, squash = juntar com o commit anterior
# f, fixup = juntar, mantendo só a mensagem anterior
# x, exec = executar comando shell
# b, break = parar o rebase
# d, drop = deletar commit
# ...
```

Após isso, você entrará no **modo de edição**, mas vamos supor que não saiba o modo correto para deletar o commit desejado:

---

### ✅ O que você pode fazer

```
pick numeração do commit 1 Mensagem do commit 1
pick numeração do commit 2 Mensagem do commit 2
pick numeração do commit 3 Mensagem do commit 3
pick numeração do commit 4 Mensagem do commit 4
pick numeração do commit 5 Mensagem do commit 5
pick numeração do commit 6 Mensagem do commit 6
drop numeração do commit 7 Mensagem do commit 7
pick numeração do commit 8 Mensagem do commit 8
pick numeração do commit 9 Mensagem do commit 9

# Comandos disponíveis:
# p, pick = manter o commit
# r, reword = manter, mas editar a mensagem
# e, edit = parar para alterar o commit
# s, squash = juntar com o commit anterior
# f, fixup = juntar, mantendo só a mensagem anterior
# x, exec = executar comando shell
# b, break = parar o rebase
# d, drop = deletar commit
# ...
```

---

### ⚠️ O que você não deve fazer

```
drop numeração do commit 7 Mensagem do commit 7

# Comandos disponíveis:
# p, pick = manter o commit
# r, reword = manter, mas editar a mensagem
# e, edit = parar para alterar o commit
# s, squash = juntar com o commit anterior
# f, fixup = juntar, mantendo só a mensagem anterior
# x, exec = executar comando shell
# b, break = parar o rebase
# d, drop = deletar commit
# ...
```
