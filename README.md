# HackTheBox (Zed)

Extensão de **temas** para o [Zed](https://zed.dev), com as famílias **HackTheBox** (cores alinhadas ao tema homónimo do VS Code) e **HackTheBlue**(Cruzeiro Esporte Clube).

## Criar o repositório no GitHub e enviar o código

O Git local já está inicializado na branch `main` com um commit inicial.

1. No GitHub: **New repository** → nome sugerido: `hackthebox-zed-theme` → **público** → **sem** README/License (já existem aqui).
2. Confirma que o campo `repository` em `extension.toml` bate certo com a URL do repo (hoje: `https://github.com/b00tk1ll/hackthebox-zed-theme`).
3. Na pasta do projeto:

   ```bash
   git remote remove origin 2>nul
   git remote add origin https://github.com/SEU_USUARIO/hackthebox-zed-theme.git
   git push -u origin main
   ```

   (Se o `origin` já estiver correto, basta `git push -u origin main`.)

## Instalação local (desenvolvimento)

1. Abra o Zed → **Extensions** → **Install Dev Extension**.
2. Selecione a pasta raiz deste repositório (onde está o `extension.toml`).

Documentação: [Developing Extensions](https://zed.dev/docs/extensions/developing-extensions).

## Publicar na loja oficial do Zed

O registo de extensões é o repositório [**zed-industries/extensions**](https://github.com/zed-industries/extensions). Resumo do processo descrito na documentação:

### Pré-requisitos

- Repositório **Git** público no GitHub só com esta extensão (ou com o `extension.toml` na raiz).
- **`LICENSE`** na raiz com uma licença aceite (este repo usa **GNU GPLv3**). Desde 1 out 2025 é obrigatório para novas submissões.
- **`extension.toml`** completo: `id`, `name`, `version`, `schema_version`, `authors`, `description`, `repository`.
- O **`id`** não pode conter as palavras `zed`, `Zed` ou `extension`.
- Temas: o **`id` deve terminar em `-theme`**.
- URL do **`repository`** em HTTPS (não `git@`).

### Passos

1. Crie um repositório no GitHub (ex.: `hackthebox-zed-theme`), faça push deste conteúdo e **substitua** em `extension.toml` o valor de `repository` pela URL real.
2. **Faça fork** de [zed-industries/extensions](https://github.com/zed-industries/extensions) para a sua **conta pessoal** (recomendado pela equipa do Zed para agilizar o PR).
3. No clone do fork:

   ```bash
   cd extensions
   git submodule add https://github.com/SEU_USUARIO/hackthebox-zed-theme.git extensions/hackthebox-theme
   ```

4. Edite o **`extensions.toml`** na raiz do fork e adicione (ajuste a versão à do seu `extension.toml`):

   ```toml
   [hackthebox-theme]
   submodule = "extensions/hackthebox-theme"
   version = "0.1.0"
   ```

5. Na raiz do fork, execute **`pnpm sort-extensions`** para ordenar `extensions.toml` e `.gitmodules`.
6. Abra um **Pull Request** para `zed-industries/extensions`.

Após o merge, a extensão é empacotada e publicada no registo do Zed. Para **atualizações**: suba um novo commit no seu repo, aumente `version` no `extension.toml`, depois no fork de `extensions` atualize o submódulo e o campo `version` na entrada em `extensions.toml`.

Guia completo: [Developing Extensions – Publishing your extension](https://zed.dev/docs/extensions/developing-extensions#publishing-your-extension).

## Estrutura

- `extension.toml` — manifesto da extensão.
- `themes/*.json` — famílias de tema (schema v0.2.0).

## Temas incluídos

| Ficheiro        | Nome no Zed   |
|-----------------|---------------|
| `hackthebox.json`  | HackTheBox    |
| `hacktheblue.json` | HackTheBlue   |
