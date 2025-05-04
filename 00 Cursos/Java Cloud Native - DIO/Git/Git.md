***
**Criado em**: 2025-03-10  
**Modificado em**: 08:22
**Topico**: #git
***
HEAD ➡ Ponteiro q aponta para a branch atual, que por sua vez, aponta para o commit atual
***
```git restore <arquivo>```  ➡ restaura as alteraçoes não commitadas<br>
```git --amend -m <msg>```  ➡ muda a msg do ultimo commit   
***
```git reset --soft <hash>```  ➡ desfaz o commit o posterior  ao hash indicado, mas mantem a área de preparo
↪
- HEAD aponta para o commit indicado  
---
```git reset --soft <hash>``` ➡ desfaz o commit posterior e a alteraçoes adicionadas, ou seja, desfaz a área de preparo
↪
- HEAD aponta para o commit indicado
---
```git reset --hard <hash>``` ➡ desfaz o commit posterior, a área de preparo e atualizar a área de trabalho para ser equivalente ao commit indicado
↪
- Apaga todos os arquivos não pertencentes ao commit
- HEAD aponta para o commit indicado
---
```git reset <arg>```  ➡ remove o arquivo da área de preparação
```git restore --staged```  ➡ remove o arquivo da área de preparação
***
```git reflog``` ➡ log das alterações executadas
***
```git checkout -b <name>``` ➡ cria uma nova branch aponta para ela 
```git merge <name>``` ➡ mesclar os arquivos branch indicada com a atual
```git branch -d <name>``` ➡ deleta a branch indicada  
***
```git fetch origin main``` ➡ baixa as alterações do repo remoto sem mesclar com o local
```git diff <arg> <arg>``` ➡ mostra as diferencas entre os dois arg
***
```git clone <url> --branch <name> --single-branch``` ➡ clona a branch indicada
***
```git stash``` ➡ arquiva uma alteração feita
- util quando se quer mudar de branch sem levar essa alteração junto
```git stash apply``` ➡ Apos mudar de branch dnv, mantem a alteração na lista  

