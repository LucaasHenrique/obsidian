***
**Criado em**: 2025-05-04  
**Modificado em**: 20:36
**Topico**: #
***
# 📘 Vim Cheatsheet

Este repositório contém um guia prático com os principais comandos do **Vim**, organizados por categoria e nível de uso. Ideal para iniciantes, intermediários e quem quer revisar o básico com rapidez.

---

## 🧭 Modos do Vim

- `ESC` → Modo normal
- `i`, `I`, `a`, `A`, `o`, `O` → Modo de inserção
- `v`, `V`, `Ctrl+v` → Modo visual
- `:` → Modo de comando
- `/` ou `?` → Busca

---

## 🔁 Navegação

| comando             | Descrição                                   |
| ------------------- | ------------------------------------------- |
| `h`, `j`, `k`, `l`  | Movimentação esquerda, baixo, cima, direita |
| `w`, `b`            | Avança / volta uma palavra                  |
| `0`, `^`, `$`       | Início, 1º caractere, fim da linha          |
| `gg`, `G`           | Início / fim do arquivo                     |
| `Ctrl+d` / `Ctrl+u` | Scroll meio para baixo / cima               |
| `H`, `M`, `L`       | Topo, meio, fim da tela                     |

---

## ✍️ Inserção e Edição

| Comando       | Ação                                                |
| ------------- | --------------------------------------------------- |
| `i`, `I`      | Inserir antes do cursor / da linha                  |
| `a`, `A`      | Inserir depois do cursor / no fim da linha          |
| `o`, `O`      | Nova linha abaixo / acima                           |
| `r`, `R`      | Substitui caractere / entra no modo de substituição |
| `x`, `X`      | Deleta caractere (↓ / ↑)                            |
| `dd`, `D`     | Deleta linha / até fim da linha                     |
| `yy`, `Y`     | Copia linha                                         |
| `p`, `P`      | Cola depois / antes                                 |
| `u`, `Ctrl+r` | Desfazer / refazer                                  |

---

## 🔍 Busca e Substituição

| Comando             | Ação                          |
| ------------------- | ----------------------------- |
| `/texto`, `?texto`  | Busca para frente / trás      |
| `n`, `N`            | Próxima / anterior ocorrência |
| `:s/velho/novo/g`   | Substitui na linha            |
| `:%s/velho/novo/g`  | Substitui no arquivo          |
| `:%s/velho/novo/gc` | Substitui com confirmação     |

---

## 📁 Arquivos e Buffers

| Comando           | Ação                        |
| ----------------- | --------------------------- |
| `:w`, `:q`, `:wq` | Salvar, sair, salvar e sair |
| `:q!`             | Sair sem salvar             |
| `:e arquivo.txt`  | Abrir arquivo               |
| `:ls`             | Listar buffers              |
| `:bN`             | Mudar para buffer N         |

---

## 📐 Modo Visual

| Comando            | Ação                              |
| ------------------ | --------------------------------- |
| `v`, `V`, `Ctrl+v` | Seleção caractere / linha / bloco |
| `y`, `d`, `c`      | Copiar, deletar, alterar          |
| `>` / `<`          | Indentar / desindentar            |

---

## 🔁 Macros e Marcas

| Comando                    | Ação                                    |
| -------------------------- | --------------------------------------- |
| `ma`                       | Marca posição atual com 'a'             |
| `'a`, `` `a ``             | Vai para linha / exata posição da marca |
| `q{letra}` → comando → `q` | Gravar macro                            |
| `@{letra}`                 | Executar macro                          |
| `@@`                       | Repetir última macro                    |

---

## ⚙️ Outros úteis

| Comando               | Ação                                        |
| --------------------- | ------------------------------------------- |
| `:set nu`             | Mostrar números                             |
| `:set relativenumber` | Números relativos                           |
| `:syntax on`          | Ativar sintaxe                              |
| `:noh`                | Limpa destaque da busca                     |
| `:%y+`                | Copia tudo para o clipboard (se disponível) |

---

## 💾 Recursos extras

- [Documentação oficial do Vim](https://vimhelp.org/)
- [Vim Adventures (jogo)](https://vim-adventures.com/)
- [The Primeagen no YouTube](https://www.youtube.com/c/ThePrimeagen) – dicas avançadas

---
