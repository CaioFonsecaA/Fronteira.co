# Fronteira.co com Tailwind CSS

Este projeto usa Tailwind CSS v4 em um site HTML estático.

## 1. Pré-requisitos

Instale o Node.js. Depois, confirme no terminal:

```powershell
node --version
npm --version
```

Os comandos devem mostrar as versões instaladas.

## 2. Entrar na pasta do projeto

Abra o terminal na pasta que contém o arquivo `package.json`:

```powershell
cd "C:\caminho\para\AFronteira.co"
```

No VS Code, também é possível abrir o terminal integrado pelo menu **Terminal > New Terminal**. Confirme a pasta atual com:

```powershell
Get-Location
```

## 3. Criar a configuração npm

Se o projeto ainda não tiver `package.json`, crie-o com:

```powershell
npm init -y
```

Esse comando cria a configuração básica do projeto. Ele deve ser executado uma única vez na raiz do projeto.

## 4. Baixar o Tailwind

Instale o Tailwind e a CLI oficial como dependências de desenvolvimento:

```powershell
npm install -D tailwindcss @tailwindcss/cli
```

A instalação cria ou atualiza:

- `node_modules/`: pacotes baixados localmente.
- `package.json`: dependências e comandos do projeto.
- `package-lock.json`: versões exatas instaladas.

Depois que o projeto já tiver esses arquivos, em outro computador basta executar:

```powershell
npm install
```

Não é necessário instalar o Tailwind globalmente.

## 5. Criar o arquivo de entrada

Crie `style/input.css` com este conteúdo:

```css
@import "tailwindcss";
@source "../view";
```

A primeira linha carrega o Tailwind. A segunda informa que o Tailwind deve procurar classes nos arquivos da pasta `view/`.

## 6. Configurar os comandos

No `package.json`, adicione estes scripts:

```json
"scripts": {
  "build:css": "tailwindcss -i ./style/input.css -o ./style/output.css --minify",
  "watch:css": "tailwindcss -i ./style/input.css -o ./style/output.css --watch"
}
```

Neste projeto, o fluxo é:

```text
style/input.css -> Tailwind CLI -> style/output.css -> view/index.html
```

## 7. Carregar o CSS no HTML

No `<head>` de `view/index.html`, carregue o CSS gerado:

```html
<link rel="stylesheet" href="../style/output.css">
```

O caminho é relativo ao arquivo `view/index.html`. Por isso, `../style/output.css` sobe uma pasta e entra em `style/`.

## 8. Aplicar Tailwind no HTML

Use as classes utilitárias diretamente no atributo `class`:

```html
<header class="flex items-center justify-between bg-black px-8 py-4 text-white">
  <h1 class="text-2xl font-bold">FRONTEIRA</h1>
  <a class="text-sm hover:opacity-60" href="#">Produtos</a>
</header>
```

Cada classe aplica uma regra de estilo. Por exemplo:

- `flex`: ativa Flexbox.
- `items-center`: alinha os itens no centro vertical.
- `justify-between`: distribui espaço entre os itens.
- `bg-black`: aplica fundo preto.
- `px-8` e `py-4`: adicionam espaçamento horizontal e vertical.
- `text-white`: aplica texto branco.
- `text-2xl`: aumenta o tamanho do texto.
- `font-bold`: aplica negrito.
- `hover:opacity-60`: reduz a opacidade ao passar o mouse.

## 9. Gerar o CSS

Para gerar o arquivo uma vez, execute na raiz do projeto:

```powershell
npm run build:css
```

O comando lê `style/input.css` e gera ou atualiza `style/output.css`.

## 10. Desenvolvimento automático

Para não executar o build manualmente a cada alteração, mantenha este comando aberto:

```powershell
npm run watch:css
```

Enquanto ele estiver rodando, o Tailwind observa os arquivos em `view/` e atualiza `style/output.css` quando uma classe é adicionada ou removida.

Para parar o monitoramento, pressione `Ctrl + C` no terminal.

## 11. Abrir o site

Abra `view/index.html` no navegador. Para atualização automática, use a extensão Live Server do VS Code e clique com o botão direito no HTML, escolhendo **Open with Live Server**.

Se o estilo antigo continuar aparecendo, atualize com `Ctrl + F5`.

## 12. O que não fazer

Não edite `style/output.css` diretamente. Ele é um arquivo gerado e será substituído no próximo build.

Edite:

- `view/index.html` para adicionar ou remover classes Tailwind.
- `style/input.css` para alterar a entrada do Tailwind ou adicionar CSS próprio.

Classes como `hero`, `hero-image` e `hero-content` não são classes nativas do Tailwind. Elas só terão efeito se receberem regras CSS próprias em `style/input.css`, ou se forem substituídas por classes utilitárias do Tailwind.

## 13. Solução de problemas

### `Could not read package.json`

Execute o comando dentro da pasta errada ou o arquivo ainda não existe. Entre na raiz do projeto e execute:

```powershell
npm init -y
npm install -D tailwindcss @tailwindcss/cli
```

### `Specified input file does not exist`

Confira se existem:

```text
style/input.css
style/output.css
```

E confirme que os scripts do `package.json` usam `./style/input.css` e `./style/output.css`.

### As classes não aparecem no resultado

Confira se `style/input.css` contém:

```css
@source "../view";
```

Depois rode:

```powershell
npm run build:css
```

Também confirme se `view/index.html` carrega:

```html
<link rel="stylesheet" href="../style/output.css">
```
