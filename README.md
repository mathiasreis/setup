# Configuração inicial de um projeto back-end:
Configure o projeto com:
- Express e TypeScript
- ts-node-dev
- ESLint
- Prettier

Use o `Yarn` como gerenciador de pacotes.

## Express e TypeScript
Inicalize o projeto com o comando para gerar o `package.json`:
```bash
yarn init -y
```
Em seguida, adicione o **express**:
```bash
yarn add express
```
Para o TS reconhecer os tipos do **express**, é preciso executar o seguinte comando:
```bash
yarn add @types/express -D
```

Agora, instale a dependência do **TypeScript**:
```bash
yarn add typescript -D
```
Inicialize o projeto TS. Será gerado um arquivo `tsconfig.json`:
```bash
yarn tsc --init
```
Abra esse arquivo, e altere algumas configurações:
```json
  {
    "compilerOpttions": {
      "target": "es2021", //Versão do ECMAScript
      "experimentalDecorators": true,
      "emitDecoratorMetadata": true, 
      "module": "commonjs", // Modo de compilação
      "resolveJsonModule": true, // Permite a importação de arquivos .json
      "outDir": "./dist", //pasta onde os arquivos serão gerados
      // "strict": true,

    } 
  }
```

## ts-node-dev
Para auxiliar o desenvolvimento, instale a biblioteca `ts-node-dev` para que as alterações nos arquivos .ts sejam convertidas para .js em tempo de desenvolvimento:
```bash
yarn add ts-node-dev -D
```
Abra o arquivo `package.json` e adicione o seguinte script:
```json
"scripts": {
    "dev": "ts-node-dev --inspect --transpile-only --ignore-watch node_modules --respawn src/server.ts",
  },
```

## ESLint
Antes de iniciar de fato a configuração do ESLint, é preciso instalar a **extensão** do ESLint no VSCode.
Em seguida, adicione uma opção chamada `codeActionsOnSave` nas configurações, assim como mostrado abaixo:
```json
"editor.codeActionsOnSave": {
  "source.fixAll.eslint": true
}
```

Instale o **ESLint** como uma dependência de desenvolvimento.
```bash
yarn add eslint -D
```
Após a instalação, inicialize o **ESLint** pra inserir as configurações dentro do projeto.
```bash
yarn eslint --init
```
Ao inserir a linha acima, serão feitas algumas perguntas para configuração do projeto:
**1 - How would you like do use Eslint?** (Qual a forma que eu quero utilizar o **Eslint**)

- **To check syntax only** ⇒ Checar somente a sintaxe
- **To check syntax and find problems** ⇒ Checar a sintaxe e encontrar problemas
- **To check syntax, find problems and enforce code style** ⇒ Checar a sintaxe, encontrar problemas e forçar um padrão de código

Escolha a última opção `To check syntax, find problems and enforce code style`.

**2 - What type of modules does your project use?** (Qual tipo de módulo seu projeto usa?)

- **JavaScript modules (import/export)**
- **CommonsJS (require/exports)**

Como o projeto utiliza o **Typescript,** selecione a **primeira** opção `Javascript modules (import/export)`

**3 - Which framework does your project use?** (Qual framework seu projeto está utilizando?)

- **React**
- **Vue.JS**
- **None of these**

Como está sendo configurando o **backend** escolha a opção `None of these`

**4 - Does your project use TypeScript?** (Seu projeto está utilizando Typescript?)

- **No**
- **Yes**

Selecione a opção `Yes`.

**5 - Where does your code run?** (Onde seu código está rodando?)

- **Browser**
- **Node**

Selecione a opção **Node**, para isso, utilize a tecla `Espaço` para desmarcar o **Browser** e selecione a opção `Node`

**6 - How would you like to define a style for your project?** (Qual guia de estilo você qyuer utilizar?) 

- **Use a popular style guide ⇒** Padrões de projetos já criados anteriormente por outra empresa
- **Answer questions about your style ⇒** Criar seu próprio padrão de projeto

Vamos selecionar a primeira opção `Use a popular style guide`

**7 - Which style guide do you want to follow?** (Qual guia de estilo você deseja seguir?)

- **Airbnb: [https://github.com/airbnb/javascript](https://github.com/airbnb/javascript)**
- **Standard: [https://github.com/standard/standard](https://github.com/standard/standard)**
- **Google: [https://github.com/google/eslint-config-google](https://github.com/google/eslint-config-google)**

Utilize a primeira opção `Airbnb`. Com ela, é definido que o projeto utilizará **ponto e vírgula** ao final de cada linha, utilizará **aspas simples** e algumas outras configurações. Para saber todas as possíveis configurações, acessar a documentação da guia desejada. 
Lembrando que, não há um padrão correto, nós iremos utilizar o **Airbnb**, porém você pode utilizar qualquer guia, desde que seu time todo também esteja utilizando.

**8 - What format do you want your config file to be in?** (Qual formato de configuração do Eslint que você deseja salvar?)

- **Javascript**
- **YAML**
- **JSON**

Selecione a opção `JSON`.

Depois que responder as perguntas, o **ESLint** irá informar quais as dependências necessárias de acordo com a sua configuração e pedir para instalá-las automaticamente.

**9 - Would you like to install them now with npm?** (Você deseja instalar as dependências agora utilizando npm?)

 Caso estivesse utilizando o **NPM** a resposta seria `Yes`, mas como está sendo utilizado o **Yarn** responda `No` e adicione manualmente as dependências.

```bash
Checking peerDependencies of eslint-config-airbnb@latest
The config that you\'ve selected requires the following dependencies:

@typescript-eslint/eslint-plugin@latest eslint-config-airbnb-base@latest 
eslint@^5.16.0 || ^6.8.0 || ^7.2.0 eslint-plugin-import@^2.22.1 
@typescript-eslint/parser@latest
? **Would you like to install them now with npm?** No
```

Para adicionar manualmente as dependências, basta seguir os passos abaixo:

- Inicie o comando com `yarn add` para instalar as dependências e a tag `-D` para adicioná-las como desenvolvimento;
- Copiar os pacotes listados [acima](https://www.notion.so/ESLint-822d59afeafc47e39527be8cabb80b00) removendo o `eslint@^5.16.0 || ^6.8.0 || ^7.2.0` pois o **ESLint** já está instalado.

O comando final deve ter essa estrutura :

<aside>
💡  <b>Não copie o comando abaixo. Utilize isso apenas como exemplo, pois as versões podem mudar</b>
</aside>

```bash
yarn add -D @typescript-eslint/eslint-plugin@latest eslint-config-airbnb-base@latest eslint-plugin-import@^2.22.1 @typescript-eslint/parser@latest
```

É preciso também instalar um plugin que irá te auxiliar a organizar a ordem dos imports dentro dos arquivos e outro para permitir importações de arquivos TypeScript sem que precisemos passar a extensão do arquivo:

```bash
yarn add -D eslint-plugin-import-helpers eslint-import-resolver-typescript
```

Com as dependências instaladas crie na raiz do projeto um arquivo `.eslintignore` com o conteúdo abaixo para ignorar o Linting em alguns arquivos:

```
/*.js
node_modules
dist
```

Agora comece a configuração do arquivo que foi gerado na inicialização do **ESLint**, o `.eslintrc.json` , a primeira coisa a ser feita é adicionar dentro de `"env"` a linha:

```json
"jest": true
```

Ainda dentro de `"env"`, verifique se a primeira linha está como `"es2020": true`, caso contrário faça a alteração deixando assim.

O próximo passo é adicionar dentro de `"extends"` a linha:

```json
"plugin:@typescript-eslint/recommended"
```

Agora, é preciso configurar o plugin que foi instalado para que seja usado pelo ESLint. Para isso, adicione o seguinte dentro de `"plugins"`:

```json
"eslint-plugin-import-helpers"
```

Em seguida, adicione dentro de `"rules"` as seguintes configurações:

```json
"camelcase": "off",
"import/no-unresolved": "error",
"@typescript-eslint/naming-convention": [
  "error",
  {
    "selector": "interface",
    "format": ["PascalCase"],
    "custom": {
      "regex": "^I[A-Z]",
      "match": true
    }
  }
],
"class-methods-use-this": "off",
"import/prefer-default-export": "off",
"no-shadow": "off",
"no-console": "off",
"no-useless-constructor": "off",
"no-empty-function": "off",
"lines-between-class-members": "off",
"import/extensions": [
  "error",
  "ignorePackages",
  {
    "ts": "never"
  }
],
"import-helpers/order-imports": [
  "warn",
  {
    "newlinesBetween": "always",
    "groups": ["module", "/^@shared/", ["parent", "sibling", "index"]],
    "alphabetize": { "order": "asc", "ignoreCase": true }
  }
],
"import/no-extraneous-dependencies": [
  "error",
  { "devDependencies": ["**/*.spec.js"] }
]
```

Por fim, para que o **Node.js** consiga entender arquivos **Typescript** é necessário acrescentar uma configuração adicional nas importações pois por padrão vai ser apresentado um erro dizendo que as importações de arquivos **Typescript** não foram resolvidas. Para resolver isso basta adicionar logo **abaixo** das `"rules"` no `.eslintrc.json` o seguinte:

```json
"settings": {
    "import/resolver": {
      "typescript": {}
    }
  }
```

Para finalizar e aplicar todas as mudanças, feche o VS Code e reabra na **pasta raiz** do projeto, pois senão o **ESLint** não vai reconhecer as dependências instaladas e aplicar as regras de Linting.

Feito isso, para verificar se está realmente funcionando basta reabrir qualquer arquivo do projeto e tentar errar algo no código para que ele mostre o erro e formate automaticamente quando o arquivo for salvo.

O arquivo `.eslintrc.json` finalizado com todas as mudanças tem que ficar assim:

```json
{
    "env": {
        "es2020": true,
        "node": true,
				"jest": true
    },
    "extends": [
        "airbnb-base",
        "plugin:@typescript-eslint/recommended"
    ],
    "parser": "@typescript-eslint/parser",
    "parserOptions": {
        "ecmaVersion": 12,
        "sourceType": "module"
    },
    "plugins": [
        "@typescript-eslint",
        "eslint-plugin-import-helpers"
    ],
    "rules": {
      "camelcase": "off",
			"import/no-unresolved": "error",
			"@typescript-eslint/naming-convention": [
			  "error",
			  {
			    "selector": "interface",
			    "format": ["PascalCase"],
			    "custom": {
			      "regex": "^I[A-Z]",
			      "match": true
			    }
			  }
			],
			"class-methods-use-this": "off",
			"import/prefer-default-export": "off",
			"no-shadow": "off",
			"no-console": "off",
			"no-useless-constructor": "off",
			"no-empty-function": "off",
			"lines-between-class-members": "off",
			"import/extensions": [
			  "error",
			  "ignorePackages",
			  {
			    "ts": "never"
			  }
			],
			"import-helpers/order-imports": [
			  "warn",
			  {
			    "newlinesBetween": "always",
			    "groups": ["module", "/^@shared/", ["parent", "sibling", "index"]],
			    "alphabetize": { "order": "asc", "ignoreCase": true }
			  }
			],
			"import/no-extraneous-dependencies": [
			  "error",
			  { "devDependencies": ["**/*.spec.js"] }
			]
    },
    "settings": {
        "import/resolver": {
            "typescript": {}
        }
    }
}
```

## Prettier

<aside>
💡  Antes de começar a configuração é importante que você se certifique de remover a extensão <b>Prettier - Code Formatter</b> do seu VS Code, ela pode gerar incompatibilidades com as configurações que vamos fazer.

</aside>

A primeira coisa para a configuração do **Prettier** é a instalação dos pacotes no projeto, então execute:

```bash
yarn add prettier eslint-config-prettier eslint-plugin-prettier -D
```

Esse comando vai adicionar 3 dependências que serão as responsáveis por fazer a formatação do código e também integrar o **Prettier** com o **ESLint**.

Com a instalação feita modifique o arquivo `.eslintrc.json` adicionando no `"extends"` as seguintes regras:

```json
"prettier",
"plugin:prettier/recommended"
```

Nos `"plugins"` adicione apenas uma linha com:

```json
"prettier"
```

E nas `"rules"` adicione uma linha indicado para o **ESLint** mostrar todos os erros onde as regras do **Prettier** não estiverem sendo seguidas, como abaixo:

```json
"prettier/prettier": "error"
```

O arquivo final vai ficar assim:

```json
{
	...
  "extends": [
		...
    "prettier",
    "plugin:prettier/recommended"
  ],
  ...
  "plugins": [
    ...
    "prettier"
  ],
  "rules": {
    ...
		"prettier/prettier": "error"
  },
  ...
}
```

E a configuração está finalizada. Para garantir que o código seja formatado corretamente, você pode abrir os arquivos do projeto e salvar eles novamente.

### Problemas no Windows
É provável que você enfrente alguns problemas de conflito entre o ESLint e o tipo de quebra de linha no Windows. Isso acontece porque quando usamos a quebra de linha no Windows, ela é interpretada como `\r\n` enquanto em sistemas Unix é `\n`. Como o ESLint tenta sempre corrigir para `\n`, esse conflito acaba acontecendo.

Para padronizar o tipo de quebra de linha usada pelo VS Code no Windows, instale uma extensão chamada **[EditorConfig for VS Code](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig)**. Com ela instalada, na pasta raiz dos projetos, clique com o botão direito do mouse e escolha a opção `Generate .editorconfig`. Com o arquivo criado você já está pronto para continuar. Todas as quebras de linha estarão no formato esperado pelo ESLint.
