# Guia de Git para o Projeto

## Objetivo
Este projeto usa um fluxo baseado em **features**, com as branches:

- `master`: versão estável / produção
- `develop`: base de desenvolvimento
- `feature/*`: branch criada para cada tarefa, melhoria ou correção

A ideia é simples:
1. ninguém desenvolve direto em `master`
2. ninguém desenvolve direto em `develop`
3. toda alteração deve nascer em uma `feature/*`
4. ao finalizar, a `feature/*` volta para `develop`
5. quando a `develop` estiver validada, ela pode ser mesclada em `master`

---

## Estrutura das branches

### `master`
Branch principal do projeto.

Uso:
- somente código estável
- somente versões prontas
- sem desenvolvimento direto

### `develop`
Branch de integração do time.

Uso:
- recebe merge das `feature/*`
- concentra o desenvolvimento em andamento
- serve como base para novas features

### `feature/nome-da-feature`
Branch individual para desenvolvimento de uma tarefa.

Exemplos:
- `feature/login`
- `feature/menu-inicial`
- `feature/inventario`
- `feature/correcao-bug-loja`

---

## Regras do time

1. Sempre criar a feature a partir da `develop`
2. Nunca trabalhar direto na `master`
3. Evitar trabalhar direto na `develop`
4. Cada tarefa deve ter sua própria branch `feature/*`
5. Sempre manter a `develop` atualizada antes de criar uma nova feature
6. Ao terminar uma feature, fazer merge dela de volta na `develop`
7. Se possível, usar Pull Request para revisão antes do merge

---

## Fluxo padrão de trabalho

## 1. Atualizar a `develop`
Antes de começar qualquer tarefa:

```bash
git checkout develop
git pull origin develop
```

---

## 2. Criar uma nova feature
Criar a branch da tarefa a partir da `develop`:

```bash
git checkout -b feature/nome-da-feature
```

Exemplo:

```bash
git checkout -b feature/Estrutura-Torreta-Teste
```

---

## 3. Trabalhar normalmente
Durante o desenvolvimento, usar commits frequentes.

Exemplo:

```bash
git add .
git commit -m "Criado calculos de dano para torreta teste"
```

---

## 4. Subir a feature para o repositório remoto
Na primeira vez que enviar a feature:

```bash
git push -u origin feature/nome-da-feature
```

Exemplo:

```bash
git push -u origin feature/tela-login
```

Depois disso, os próximos pushes podem ser só:

```bash
git push
```

---

## 5. Manter a feature atualizada com a `develop`
Se outras alterações entrarem na `develop` enquanto você trabalha, atualize sua feature:

```bash
git checkout develop
git pull origin develop
git checkout feature/nome-da-feature
git merge develop
```

Se houver conflito, resolver antes de continuar.
Atenção ao resolver conflitos para não perder código.

---

## 6. Finalizar a feature
Quando terminar a tarefa:

### Atualizar a `develop`
```bash
git checkout develop
git pull origin develop
```

### Fazer merge da feature
```bash
git merge feature/nome-da-feature
```

### Enviar a `develop`
```bash
git push origin develop
```

---

## 7. Remover a feature após o merge
Depois que a feature já foi integrada:

### Apagar branch local
```bash
git branch -d feature/nome-da-feature
```

### Apagar branch remota
```bash
git push origin --delete feature/nome-da-feature
```

---

## Exemplo completo

### Criar e trabalhar em uma feature
```bash
git checkout develop
git pull origin develop
git checkout -b feature/Criar-Hub-Central

git add .
git commit -m "Criado chamada para o Hub Central"
git push -u origin feature/Criar-Hub-Central
```

### Finalizar a feature
```bash
git checkout develop
git pull origin develop
git merge feature/Criar-Hub-Central
git push origin develop

git branch -d feature/Criar-Hub-Central
git push origin --delete feature/Criar-Hub-Central
```

---

## Boas práticas de commit

Preferir mensagens objetivas, descrevendo o que foi feito.

Exemplos:
- `Cria tela de login`
- `Adiciona menu principal`
- `Corrige erro ao salvar inventario`
- `Ajusta validacao de cadastro`

Evitar mensagens como:
- `alteracoes`
- `teste`
- `ajustes`
- `commit novo`

---

## O que fazer em caso de erro

### Estou em uma branch errada
Ver branch atual:

```bash
git branch
```

Trocar de branch:

```bash
git checkout develop
```

---

### Minha `develop` está desatualizada
Atualizar:

```bash
git checkout develop
git pull origin develop
```

---

### Já comecei algo e esqueci de criar a feature
Se você alterou arquivos sem criar a feature, primeiro tente criar a branch antes de mudar para outra:

```bash
git checkout -b feature/nome-da-feature
```

Assim suas alterações atuais passam para a nova feature.

---

### Deu conflito no merge
Quando houver conflito:
1. abrir os arquivos com conflito
2. corrigir manualmente
3. adicionar os arquivos corrigidos
4. concluir o merge

Exemplo:

```bash
git add .
git commit -m "Resolve conflito de merge"
```

---

## Fluxo para integração com a `master`

A `master` não deve receber alterações de features diretamente.

Fluxo correto:

```text
feature/* -> develop -> master
```

Ou seja:
1. Desenvolvedor cria `feature/*`
2. termina a tarefa
3. merge na `develop`
4. quando a `develop` estiver estável e validada, ela pode ser mesclada na `master`

---

## Resumo rápido

### Iniciar tarefa
```bash
git checkout develop
git pull origin develop
git checkout -b feature/nome-da-feature
```

### Salvar e enviar
```bash
git add .
git commit -m "Descricao da alteracao"
git push -u origin feature/nome-da-feature
```

### Finalizar
```bash
git checkout develop
git pull origin develop
git merge feature/nome-da-feature
git push origin develop
git branch -d feature/nome-da-feature
git push origin --delete feature/nome-da-feature
```

---

## Observação final
Este projeto segue um fluxo simples e organizado para evitar conflito entre desenvolvedores.

Regra principal:

**Toda alteração deve ser feita em uma branch `feature/*`, criada a partir da `develop`, e depois integrada novamente na `develop`.**
