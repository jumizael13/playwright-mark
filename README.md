# 🎭 Playwright Mark — Automação de Testes Web e API

Projeto de automação de testes desenvolvido com **Playwright e TypeScript**, contemplando testes de interface Web, integração com API para preparação e limpeza de dados, Page Object Model (POM), fixtures e execução automatizada por meio do GitHub Actions.

O projeto automatiza os principais fluxos de uma aplicação de gerenciamento de tarefas, validando funcionalidades de cadastro, atualização, exclusão e regras de negócio.

---

## 📋 Sobre o projeto

Este projeto foi desenvolvido com o objetivo de aplicar boas práticas de automação de testes utilizando o Playwright.

A estratégia de automação combina testes de interface Web com requisições de API para controlar o estado dos dados antes da execução dos cenários. Essa abordagem contribui para testes mais independentes, previsíveis e eficientes.

Entre as práticas implementadas estão:

- Automação de testes Web com Playwright.
- TypeScript para tipagem e organização do código.
- Page Object Model (POM).
- Fixtures para gerenciamento da massa de testes.
- API Request Context para criação e exclusão de dados.
- Separação entre lógica de testes, páginas, helpers e massa de dados.
- Assertions para validação da interface e das regras de negócio.
- Integração contínua com GitHub Actions.

---

## 🧪 Cenários automatizados

### Disponibilidade da aplicação

Valida se a aplicação está online e verifica se o título esperado da página é exibido corretamente.

### Cadastro de tarefas

Valida que uma nova tarefa pode ser cadastrada com sucesso e que ela é exibida corretamente na interface.

### Validação de tarefa duplicada

Valida que o sistema não permite o cadastro de uma tarefa com nome duplicado e verifica a exibição da mensagem:

```text
Task already exists!
```

### Validação de campo obrigatório

Valida o comportamento da aplicação quando é realizada uma tentativa de cadastrar uma tarefa sem informar seu nome.

Mensagem esperada:

```text
This is a required field
```

### Conclusão de tarefa

Cria uma tarefa por meio da API como pré-condição, conclui a tarefa pela interface e valida visualmente seu estado como finalizada.

### Exclusão de tarefa

Cria uma tarefa por meio da API como pré-condição, realiza sua exclusão pela interface e valida que ela não está mais disponível na lista.

---

## 🏗️ Arquitetura do projeto

O projeto utiliza uma estrutura organizada para separar as aplicações Web e API da suíte de testes automatizados, mantendo responsabilidades bem definidas entre testes, páginas, helpers, modelos e massas de dados.

```text
playwright-mark/
│
├── .github/
│   └── workflows/
│       └── playwright.yml
│
├── apps/
│   ├── api/
│   │   ├── src/
│   │   ├── ormconfig.json
│   │   ├── package.json
│   │   └── yarn.lock
│   │
│   └── web/
│       ├── assets/
│       ├── index.html
│       ├── package.json
│       └── yarn.lock
│
├── tests/
│   ├── fixtures/
│   │   ├── task.model.ts
│   │   └── tasks.json
│   │
│   ├── support/
│   │   ├── pages/
│   │   │   └── tasks/
│   │   │       └── index.ts
│   │   └── helpers.ts
│   │
│   ├── home.spec.ts
│   └── tasks.spec.ts
│
├── .gitignore
├── Insomnia_mark1.json
├── package.json
├── playwright.config.ts
└── yarn.lock
```

---

## 🧩 Page Object Model

O projeto utiliza o padrão **Page Object Model (POM)** para centralizar os elementos e as ações realizadas na página de tarefas.

A classe `TasksPage` é responsável por operações como:

- Acessar a página de tarefas.
- Criar uma nova tarefa.
- Concluir uma tarefa.
- Excluir uma tarefa.
- Validar a existência de uma tarefa.
- Validar a ausência de uma tarefa.
- Validar mensagens de alerta.
- Validar visualmente a conclusão de uma tarefa.

Essa abordagem reduz a duplicação de código, melhora a manutenção e facilita a evolução dos testes.

---

## 🔌 Integração com API

O projeto utiliza o `APIRequestContext` do Playwright para realizar requisições diretamente à API da aplicação.

As funções auxiliares implementadas permitem:

- Criar tarefas via API.
- Excluir tarefas via API.
- Preparar os dados necessários antes da execução dos testes.
- Remover dados existentes para garantir independência entre os cenários.

A API é utilizada principalmente para preparar as pré-condições necessárias, permitindo que a interface Web seja utilizada especificamente para validar o comportamento que está sendo testado.

Essa estratégia contribui para testes mais rápidos, independentes e confiáveis.

---

## 📦 Massa de dados e tipagem

Os dados utilizados nos testes são armazenados no arquivo:

```text
tests/fixtures/tasks.json
```

A massa contempla diferentes cenários:

- `success`: cadastro realizado com sucesso.
- `duplicate`: tentativa de cadastro duplicado.
- `required`: validação de campo obrigatório.
- `update`: conclusão de uma tarefa.
- `delete`: exclusão de uma tarefa.

A estrutura dos dados é tipada através da interface `TaskModel`:

```typescript
export interface TaskModel {
    name: string
    is_done: boolean
}
```

Essa abordagem proporciona melhor organização, reutilização da massa de testes e segurança de tipos com TypeScript.

---

## 🛠️ Tecnologias utilizadas

| Tecnologia | Utilização |
|---|---|
| Playwright | Framework de automação de testes Web e API |
| TypeScript | Linguagem utilizada no desenvolvimento dos testes |
| Node.js | Ambiente de execução JavaScript |
| Page Object Model | Padrão para organização e manutenção das páginas |
| JSON | Gerenciamento das massas de dados |
| GitHub Actions | Integração contínua e execução automatizada dos testes |
| Git | Controle de versão |
| GitHub | Hospedagem e versionamento do projeto |

---

## ⚙️ Pré-requisitos

Antes de executar o projeto, é necessário possuir:

- Node.js instalado.
- Yarn instalado.
- Git instalado.
- Navegadores do Playwright instalados.

Para verificar as versões instaladas:

```bash
node --version
yarn --version
git --version
```

---

## 📥 Instalação

Clone o repositório:

```bash
git clone https://github.com/jumizael13/playwright-mark.git
```

Acesse a pasta do projeto:

```bash
cd playwright-mark
```

### Instale as dependências dos testes

Na raiz do projeto:

```bash
yarn install
```

Instale os navegadores e as dependências necessárias do Playwright:

```bash
yarn playwright install --with-deps
```

### Instale as dependências da API

```bash
cd apps/api
yarn install
```

### Instale as dependências da aplicação Web

A partir da raiz do projeto:

```bash
cd apps/web
yarn install
```

---

## 🚀 Inicialização do ambiente

Para executar os testes localmente, é necessário manter a **API** e a **aplicação Web** em execução.

Recomenda-se utilizar três terminais separados:

### Terminal 1 — Iniciar a API

A partir da raiz do projeto:

```bash
cd apps/api
yarn dev
```

A API utilizada pelos testes estará disponível em:

```text
http://localhost:3333
```

### Terminal 2 — Iniciar a aplicação Web

A partir da raiz do projeto:

```bash
cd apps/web
yarn dev
```

A aplicação estará disponível em:

```text
http://localhost:8080
```

### Terminal 3 — Executar os testes

Na raiz do projeto:

```bash
yarn playwright test
```

---

## ▶️ Execução dos testes

Com a API e a aplicação Web em execução, os testes podem ser executados através dos seguintes comandos:

### Executar todos os testes

```bash
yarn playwright test
```

### Executar os testes em modo visual

```bash
yarn playwright test --headed
```

### Executar apenas os testes de tarefas

```bash
yarn playwright test tests/tasks.spec.ts
```

### Executar apenas o teste de disponibilidade da aplicação

```bash
yarn playwright test tests/home.spec.ts
```

### Executar com a interface gráfica do Playwright

```bash
yarn playwright test --ui
```

### Visualizar o relatório HTML da última execução

```bash
yarn playwright show-report
```

---

## 📊 Estratégia de testes

A estratégia utilizada busca garantir testes independentes e confiáveis por meio da combinação de diferentes camadas:

1. **Preparação do estado via API:** as tarefas necessárias para determinados cenários são criadas diretamente através da API.

2. **Interação pela interface Web:** as ações correspondentes ao comportamento testado são executadas através da interface.

3. **Validação do resultado esperado:** assertions verificam a presença ou ausência das tarefas, mensagens de validação e alterações visuais de estado.

4. **Limpeza e isolamento dos dados:** tarefas preexistentes são removidas quando necessário para evitar interferência entre execuções.

Essa abordagem torna os testes mais rápidos, previsíveis e menos dependentes uns dos outros.

---

## 🔄 Integração contínua com GitHub Actions

O projeto possui um workflow de integração contínua configurado em:

```text
.github/workflows/playwright.yml
```

A pipeline é executada automaticamente nos seguintes eventos:

- Push nas branches `main` e `master`.
- Pull requests destinados às branches `main` e `master`.

Durante a execução, o GitHub Actions:

1. Realiza o checkout do código-fonte.
2. Configura o ambiente com a versão LTS do Node.js.
3. Instala as dependências do projeto.
4. Instala os navegadores e dependências necessárias do Playwright.
5. Executa os testes automatizados.
6. Publica o relatório HTML do Playwright como artifact.

O relatório é armazenado por **30 dias** e permanece disponível mesmo quando existem falhas nos testes, facilitando a análise dos resultados da execução.

---

## 📈 Boas práticas aplicadas

- Separação de responsabilidades.
- Page Object Model (POM).
- Reutilização de métodos e componentes.
- Massa de dados externa.
- Tipagem com TypeScript.
- Preparação de pré-condições via API.
- Limpeza de dados para isolamento dos cenários.
- Assertions específicas para cada regra de negócio.
- Integração contínua com GitHub Actions.
- Geração de relatórios de execução.
- Versionamento com Git e GitHub.

---

## 👩‍💻 Autora

**Julia Caetano Mizael dos Santos**

QA Engineer | Quality Assurance | Test Automation

- LinkedIn: www.linkedin.com/in/julia-mizael
- GitHub: github.com/jumizael13

Projeto desenvolvido como parte do aprimoramento contínuo em automação de testes, qualidade de software, Playwright, TypeScript e CI/CD.