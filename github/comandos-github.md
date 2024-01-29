# Lista de comandos GitHub

## Comandos básicos

1. **Configuração Inicial:**
   - `git config --global user.name "Seu Nome"`: Configura o nome do usuário.
   - `git config --global user.email "seu@email.com"`: Configura o e-mail do usuário.

1. **Criar Repositório:**
   - `git init`: Inicializa um novo repositório Git.

1. **Clonar Repositório:**
   - `git clone <url>`: Clona um repositório remoto para o seu computador.

1. **Adicionar e Confirmar Mudanças:**
   - `git add <arquivo>`: Adiciona arquivos ao staging area.
   - `git add .` ou `git add -A`: Adiciona todas as mudanças ao staging area.
   - `git commit -m "Mensagem do Commit"`: Confirma as mudanças no repositório local.

1. **Branches:**
   - `git branch`: Lista todas as branches no repositório.
   - `git branch <nome-da-branch>`: Cria uma nova branch.
   - `git checkout <nome-da-branch>`: Muda para uma branch específica.
   - `git checkout -b <nome-da-branch>`: Criar e mudar para uma nova branch ao mesmo tempo.
        - `git checkout`: Muda para uma branch existente ou cria uma nova.
        - `-b`: Indica que você está criando uma nova branch.    
   - `git merge <nome-da-branch>`: Funde uma branch na branch atual.

1. **Status Atual:**
   - `git status`: Mostra o status atual do repositório, indicando arquivos modificados, adicionados ou pendentes de commit.


1. **Atualizações Remotas:**
   - `git pull`: Atualiza o repositório local com as alterações remotas.
   - `git push origin <nome-da-branch>`: Envia as mudanças locais para o repositório remoto.

1. **Histórico:**
   - `git log`: Mostra o histórico de commits.
   - `git diff`: Mostra as diferenças entre versões.

1. **Desfazer Mudanças:**
   - `git reset <arquivo>`: Remove o arquivo do staging area.
   - `git reset --hard HEAD`: Desfaz todas as mudanças locais.
   - `git revert <hash-do-commit>`: Reverte um commit específico.

1. **Tags:**
   - `git tag <nome-da-tag>`: Cria uma nova tag para o commit atual.

1. **Ignorar Arquivos:**
    - Crie um arquivo chamado `.gitignore` para especificar os arquivos a serem ignorados.

---

## Comandos interessantes

### Stash

O comando `git stash` é usado para temporariamente armazenar as mudanças locais que não foram comprometidas ainda, permitindo que você as remova da sua área de trabalho e volte para um estado limpo do repositório. É útil quando você precisa mudar de branch ou fazer algo mais, mas não quer comprometer suas mudanças ainda.

**Exemplo de uso**: Você fez muitas mudanças em um repositório produtivo e na hora de criar uma **Pull Request** percebeu que esqueceu de criar uma branch nova e fez as mudanças na `main`. É inviável reverter as mudanças, já que você gastou muito tempo pensando na solução do problema.  

Solucione o problema da seguinte forma: 

1. Sinalize todas as mudanças 

`git add .`

2. Veja o que foi adicionado *(opcional)*

`git status`

3. Aqui a mágica acontece, vamos colocar todas as mudanças na "mochila" para carregarmos até a **nova branch**.

`git stash`

4. Agora vamos seguir normalmente, começando pela **nova branch**

`git checkout -b <branch_name>`

5. Jogue as alterações na **nova branch**

`git stash pop`

6. Confira se as mudanças foram identificadas *(opcional)*

`git status`

7. Adicione as mudanças 

`git add .`

8. Prepare o **commit**

`git commit -m "mensagem de commit"`

9. Submeta as mudanças

`git push`

ou 

`git push --set-upstream origin branch_name`

**_Nota:_** o comando `git stash show` mostra a lista de comandos possíveis dentro de `stash`.

### Commit Amend

O comando git commit `--amend --no-edit` é utilizado para fazer alterações no commit mais recente sem modificar a mensagem de commit. Muito útil quando você esqueceu de incluir alguns arquivos no commit anterior ou deseja ajustar as alterações antes de finalizar o commit ou mergear um PR.

Para usar: 

1. Certifique-se de estar na mesma branch do commit/PR

2. Faça as modificações necessárias nos arquivos

3. Adicione as mudanças na branch com `git add .`

4. Force a alteração no commit anterior `git commit --amend --no-edit`

Dessa forma, as alterações feitas serão adicionadas ao commit mais recente sem modificar a mensagem de commit. Ao usar `--amend`, você está reescrevendo o histórico do commit


### Push force with lease

O comando `git push --force-with-lease` é usados para forçar a atualização remota, reescrevendo o histórico do repositório remoto com o histórico local. 

O `--force-with-lease` aborda esse problema de uma maneira mais segura. Ele verifica se outros colaboradores já enviaram alterações para o repositório remoto desde a última vez que você o atualizou. Se houver novos commits no repositório remoto, o --force-with-lease recusará a operação de push, impedindo que você sobrescreva involuntariamente os commits de outras pessoas.

Quando estamos trabalhando em um PR que já foi criado e precisamos fazer alguma modifiação, podemos usar o `git push --force-with-lease`.

Para usar: 

1. Siga os passos descritos no tópico [Commit Amend](#commit-amend)

2. Use o comando `git push --force-with-lease`

Dessa forma, garantimos que as mudanças serão refletidas no PR que estamos trabalhando.  

---
### Mensagem de commit
fix:

chore:

---

- *by: Milleny Caroliny de Almeida Santos*
