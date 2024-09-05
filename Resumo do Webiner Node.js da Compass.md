
- TÓPICOS IMPORTANTES VISTOS:
Projeto de Simulação de Compras Online
- Solução do Projeto
![[Pasted image 20240613093719.png]]
- Conceitos de API
*IMPORTANTE*
![[Pasted image 20240613093805.png]]
-> INTEGRANDO BLOCKCHAIN COM APIs
![[Pasted image 20240613094056.png]]
-> MIDDLEWARES
![[Pasted image 20240613094137.png]]
![[Pasted image 20240613094430.png]]
Middleware é um tipo de software que atua como uma camada intermediária entre sistemas ou componentes de software, facilitando a comunicação e o gerenciamento de dados entre eles. Ele não é uma aplicação final por si só, mas serve para conectar diferentes sistemas ou partes de um sistema, permitindo que eles funcionem juntos de maneira eficiente. Aqui estão alguns pontos-chave sobre middleware:

1. **Intermediação de Comunicação**: Middleware permite que diferentes aplicações, que podem estar rodando em diferentes plataformas ou linguagens de programação, comuniquem-se entre si de forma transparente.

2. **Integração de Sistemas**: Ele é frequentemente usado para integrar sistemas legados com novas aplicações, permitindo que empresas aproveitem suas infraestruturas existentes enquanto adotam novas tecnologias.

3. **Serviços Comuns**: Middleware pode fornecer serviços comuns e utilitários como autenticação, autorização, gerenciamento de transações, filas de mensagens, serviços de diretório, monitoramento, e logging.

4. **Tipos de Middleware**:
   - **Middleware de Mensagens**: Facilita a troca de mensagens entre sistemas distribuídos, como os sistemas de filas de mensagens (ex: RabbitMQ, Apache Kafka).
   - **Middleware Orientado a Objetos**: Permite que objetos em diferentes aplicações se comuniquem como se estivessem no mesmo programa (ex: CORBA, Java RMI).
   - **Middleware de Transação**: Gerencia transações distribuídas entre múltiplos sistemas de banco de dados ou serviços (ex: Tuxedo).
   - **Middleware Orientado a Banco de Dados**: Facilita o acesso e a gestão de diferentes bancos de dados distribuídos (ex: ODBC, JDBC).
   - **Middleware de Aplicação**: Suporta a execução e o gerenciamento de aplicações distribuídas (ex: WebLogic, JBoss).

5. **Casos de Uso**:
   - **E-commerce**: Integração de sistemas de pagamento, gestão de inventário e plataformas de marketing.
   - **Telecomunicações**: Conectando sistemas de faturamento, CRM e infraestrutura de rede.
   - **Saúde**: Integração de sistemas de registros eletrônicos de saúde com outros sistemas hospitalares.

Exemplo prático: em um sistema de e-commerce, o middleware pode ser usado para conectar o front-end do site com o sistema de gestão de inventário, processamento de pagamentos e serviços de envio, garantindo que todas as partes do sistema se comuniquem eficientemente e em tempo real. Em resumo, middleware é um componente crucial em arquiteturas de sistemas modernos, fornecendo a cola que mantém diferentes partes de um sistema integradas e funcionando harmonicamente.

Exemplo de  Middleware -> 
Claro! Vamos criar um exemplo prático de middleware em uma aplicação Node.js usando o framework Express. Vamos criar um middleware simples que loga informações sobre cada requisição recebida pelo servidor.

### Passos

1. **Instalar o Express**: Primeiro, precisamos instalar o Express usando npm.
2. **Configurar o Servidor**: Configurar um servidor básico com Express.
3. **Criar Middleware**: Implementar um middleware para logar informações da requisição.

### 1. Instalar o Express

Se você ainda não tem um projeto Node.js, crie um diretório e inicialize o npm:

```bash
mkdir myapp
cd myapp
npm init -y
```

Depois, instale o Express:

```bash
npm install express
```

### 2. Configurar o Servidor

Crie um arquivo `index.js` e configure um servidor básico:

```javascript
const express = require('express');
const app = express();
const port = 3000;

// Middleware de logging
app.use((req, res, next) => {
    console.log(`${req.method} ${req.url}`);
    next(); // Passa a requisição para o próximo middleware ou rota
});

// Rota simples
app.get('/', (req, res) => {
    res.send('Hello, World!');
});

app.listen(port, () => {
    console.log(`Servidor rodando em http://localhost:${port}`);
});
```

### 3. Criar Middleware

No exemplo acima, já criamos um middleware simples que loga o método HTTP (`req.method`) e a URL (`req.url`) de cada requisição recebida.

### Explicação do Middleware

1. **`app.use((req, res, next) => { ... })`**: Esta linha registra um middleware. O middleware é uma função que tem acesso ao objeto de requisição (`req`), ao objeto de resposta (`res`) e a uma função `next` que deve ser chamada para passar o controle para o próximo middleware ou rota.

2. **`console.log(`${req.method} ${req.url}`)`**: Esta linha loga o método HTTP e a URL da requisição.

3. **`next()`**: Esta linha é crucial. Chamar `next()` indica que este middleware terminou seu trabalho e passa o controle para o próximo middleware ou rota. Se você não chamar `next()`, a requisição ficará pendente e não será processada.

### Executando o Servidor

Para executar o servidor, use o comando:

```bash
node index.js
```

Agora, quando você acessar `http://localhost:3000` no seu navegador, você verá "Hello, World!" e o console do terminal mostrará algo como:

```plaintext
GET /
```

### Adicionando Mais Funcionalidades

Você pode adicionar mais middlewares para diferentes propósitos, como autenticação, manipulação de erros, ou parsing de dados. Aqui está um exemplo com um middleware adicional para tratar erros 404:

```javascript
// Middleware de logging
app.use((req, res, next) => {
    console.log(`${req.method} ${req.url}`);
    next();
});

// Middleware de parsing de JSON
app.use(express.json());

// Rota simples
app.get('/', (req, res) => {
    res.send('Hello, World!');
});

// Middleware de tratamento de erro 404
app.use((req, res, next) => {
    res.status(404).send('Página não encontrada');
});

// Middleware de tratamento de erros gerais
app.use((err, req, res, next) => {
    console.error(err.stack);
    res.status(500).send('Algo deu errado!');
});

app.listen(port, () => {
    console.log(`Servidor rodando em http://localhost:${port}`);
});
```

Este exemplo adiciona um middleware para parsing de JSON e dois middlewares de tratamento de erros. O primeiro middleware trata erros 404 (página não encontrada) e o segundo trata erros gerais, logando o stack trace e respondendo com uma mensagem de erro.

*PROMISES: Garantia de Transações*
![[Pasted image 20240613095917.png]]
Callback Hell, também conhecido como "Pyramid of Doom", é um problema comum no desenvolvimento JavaScript, especialmente quando se trabalha com operações assíncronas usando callbacks. Ele ocorre quando você tem múltiplas operações assíncronas que precisam ser executadas em sequência, e você aninha vários callbacks dentro de outros callbacks. Isso resulta em código difícil de ler, entender e manter.
### Exemplo de Callback Hell

Aqui está um exemplo de Callback Hell com operações assíncronas aninhadas:

```javascript
function doSomething(callback) {
    setTimeout(() => {
        console.log("Fez algo");
        callback();
    }, 1000);
}

function doSomethingElse(callback) {
    setTimeout(() => {
        console.log("Fez outra coisa");
        callback();
    }, 1000);
}

function doAnotherThing(callback) {
    setTimeout(() => {
        console.log("Fez mais uma coisa");
        callback();
    }, 1000);
}

// Callback Hell
doSomething(() => {
    doSomethingElse(() => {
        doAnotherThing(() => {
            console.log("Tudo feito!");
        });
    });
});
```

### Tratando o Callback Hell

Existem várias maneiras de tratar o Callback Hell em JavaScript, incluindo Promises, async/await e bibliotecas utilitárias. Vamos explorar cada uma dessas abordagens.

### 1. Usando Promises

Promises são uma maneira de lidar com operações assíncronas de forma mais legível e gerenciável. Elas permitem encadear operações assíncronas usando `then()` e `catch()`.

```javascript
function doSomething() {
    return new Promise((resolve) => {
        setTimeout(() => {
            console.log("Fez algo");
            resolve();
        }, 1000);
    });
}

function doSomethingElse() {
    return new Promise((resolve) => {
        setTimeout(() => {
            console.log("Fez outra coisa");
            resolve();
        }, 1000);
    });
}

function doAnotherThing() {
    return new Promise((resolve) => {
        setTimeout(() => {
            console.log("Fez mais uma coisa");
            resolve();
        }, 1000);
    });
}

// Encadeamento de Promises
doSomething()
    .then(doSomethingElse)
    .then(doAnotherThing)
    .then(() => {
        console.log("Tudo feito!");
    });
```

### 2. Usando async/await

O `async/await` é uma sintaxe mais moderna e limpa para lidar com Promises, introduzida no ECMAScript 2017. Ele permite escrever código assíncrono de forma síncrona.

```javascript
function doSomething() {
    return new Promise((resolve) => {
        setTimeout(() => {
            console.log("Fez algo");
            resolve();
        }, 1000);
    });
}

function doSomethingElse() {
    return new Promise((resolve) => {
        setTimeout(() => {
            console.log("Fez outra coisa");
            resolve();
        }, 1000);
    });
}

function doAnotherThing() {
    return new Promise((resolve) => {
        setTimeout(() => {
            console.log("Fez mais uma coisa");
            resolve();
        }, 1000);
    });
}

// Usando async/await
async function doAll() {
    await doSomething();
    await doSomethingElse();
    await doAnotherThing();
    console.log("Tudo feito!");
}

doAll();
```

### 3. Usando Bibliotecas Utilitárias

Existem bibliotecas como `async.js` que facilitam o gerenciamento de operações assíncronas sem cair no Callback Hell. Aqui está um exemplo usando `async.js`:

Primeiro, instale a biblioteca `async`:

```bash
npm install async
```

Depois, use-a no seu código:

```javascript
const async = require('async');

function doSomething(callback) {
    setTimeout(() => {
        console.log("Fez algo");
        callback();
    }, 1000);
}

function doSomethingElse(callback) {
    setTimeout(() => {
        console.log("Fez outra coisa");
        callback();
    }, 1000);
}

function doAnotherThing(callback) {
    setTimeout(() => {
        console.log("Fez mais uma coisa");
        callback();
    }, 1000);
}

// Usando async.series para evitar Callback Hell
async.series([
    doSomething,
    doSomethingElse,
    doAnotherThing
], (err) => {
    if (err) {
        console.error(err);
    } else {
        console.log("Tudo feito!");
    }
});
```

Essas abordagens ajudam a evitar o Callback Hell, tornando o código assíncrono mais legível e fácil de manter.

-> ASYNC/AWAIT NA BLOCKCHAIN
![[Pasted image 20240613100941.png]]
-> CONTRATOS
- REGRAS DE NEGÓCIO
![[Pasted image 20240613101046.png]]
Contratos inteligentes === Codigo executado dentro de uma rede blockchain

Um **smart contract** (ou contrato inteligente) é um programa que roda em uma blockchain e automaticamente executa, controla ou documenta eventos e ações de acordo com os termos de um contrato ou acordo. Ele permite que transações e acordos ocorram entre partes anônimas sem a necessidade de uma autoridade central, sistema legal ou mecanismo externo de fiscalização.

### Características dos Smart Contracts

1. **Auto-executáveis**: Uma vez que as condições especificadas no contrato sejam atendidas, o smart contract executa automaticamente as ações predefinidas.
2. **Imutabilidade**: Depois de implantados na blockchain, os contratos inteligentes não podem ser alterados, garantindo que os termos acordados sejam cumpridos.
3. **Transparência**: Todas as partes envolvidas podem ver o código do contrato e suas execuções, garantindo transparência.
4. **Segurança**: Utilizam criptografia para garantir que as transações sejam seguras e que os dados não possam ser manipulados.

### Exemplo Prático de Uso de Smart Contracts

**1. Tokens ERC-20**

Um dos usos mais comuns de smart contracts é a criação de tokens digitais. No ecossistema Ethereum, o padrão ERC-20 é usado para criar tokens fungíveis, que são iguais entre si e podem ser trocados. Um token ERC-20 pode representar qualquer ativo digital, como moeda, pontos de fidelidade, propriedade ou até mesmo outros ativos de blockchain.

### Exemplo de um Token ERC-20

Aqui está um exemplo básico de um smart contract ERC-20 escrito em Solidity, a linguagem de programação usada para escrever contratos inteligentes no Ethereum:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract MyToken is ERC20 {
    constructor(uint256 initialSupply) ERC20("MyToken", "MTK") {
        _mint(msg.sender, initialSupply);
    }
}
```

Neste exemplo:

- `@openzeppelin/contracts/token/ERC20/ERC20.sol` é um contrato padrão ERC-20 fornecido pela OpenZeppelin, uma biblioteca amplamente utilizada para contratos inteligentes.
- `MyToken` é o nome do nosso token e `MTK` é o seu símbolo.
- O construtor (`constructor`) inicializa o contrato e cria a quantidade inicial de tokens (`initialSupply`) que são atribuídos ao endereço que implantou o contrato (`msg.sender`).

### Como Usar Este Smart Contract

1. **Configurar Ambiente**: Primeiro, você precisa configurar um ambiente de desenvolvimento Ethereum, como Truffle ou Hardhat.
2. **Compilar e Implantar**: Compile o contrato usando uma ferramenta como o Remix IDE ou Hardhat e, em seguida, implante-o em uma rede Ethereum (pode ser uma rede de teste ou a mainnet).
3. **Interagir com o Contrato**: Depois de implantado, você pode interagir com o contrato usando um endereço Ethereum e uma carteira, como MetaMask, para transferir tokens, verificar saldo, etc.

### Outros Usos Comuns de Smart Contracts

1. **ICO/Token Sales**: Empresas podem usar smart contracts para criar e vender tokens como parte de uma Initial Coin Offering (ICO).
2. **DeFi (Finanças Descentralizadas)**: Smart contracts são a base de muitas aplicações DeFi, como exchanges descentralizadas (DEX), protocolos de empréstimos e poupança, e seguros.
3. **NFTs (Non-Fungible Tokens)**: Tokens não fungíveis, que são únicos e não intercambiáveis, são criados e gerenciados por smart contracts. Exemplos incluem colecionáveis digitais, arte digital e itens de jogos.
4. **Supply Chain Management**: Smart contracts podem ser usados para rastrear produtos ao longo da cadeia de suprimentos, garantindo transparência e autenticidade.

### Conclusão

Smart contracts são uma tecnologia poderosa que está transformando muitos setores, oferecendo formas automatizadas, seguras e transparentes de realizar transações e acordos. O exemplo do token ERC-20 ilustra como um contrato inteligente pode ser usado para criar ativos digitais que podem ser transferidos e negociados na blockchain.
-> *COMO ELE FUNCIONA*:
![[Pasted image 20240613101219.png]]
#COMOEXPANDIROPROJETO
![[Pasted image 20240613101329.png]]
PARTE TEÓRICA FINALIZADA.
PARTE PRÁTICA
![[Pasted image 20240613101852.png]]

