# criando-componentes-com-styled-components-react-native

<img src="https://storage.googleapis.com/golden-wind/experts-club/capa-github.svg" />

## Expert

| [<img src="https://avatars.githubusercontent.com/u/6079947?s=460&u=d7af98379f7769fc782b4e99d86a205c44e57f79&v=4" width="75px;"/>](https://github.com/hstrada) |
| :-: |
|[Helena Strada](https://github.com/hstrada)|

# Index

- :rocket: [Sumário](#rocket-sumário)
- 👨‍💻️ [Tecnologias Utilizadas](#%EF%B8%8F-tecnologias-utilizadas)
- 📦️ [Como Clonar e Rodar o Projeto](#%EF%B8%8F-como-clonar-e-rodar-o-projeto)
- :purple_heart: [Desenvolvimento da Solução](#desenvolvimento-da-solução)

---

## :rocket: Sumário

Criar componentes no React Native é uma tarefa diária!

Nesse vídeo vamos utilizar o Styled-Components para criar nossos componentes utilizando props de maneira dinâmica, reutilizáveis e centralizadas para facilitar o desenvolvimento e manutenção do ciclo de vida da sua aplicação.

---
## 👨‍💻️ Tecnologias Utilizadas

This project was developed using the technologies bellow:
  
### Mobile

  - [React Native](https://reactnative.dev/)
  
### Dependencies

  - [Typescript](https://www.typescriptlang.org/)
  - [Styled Components](https://styled-components.com/)
  
### IDE

  - [Visual Studio Code](https://code.visualstudio.com/)

---
 
## 📦️ Como Clonar e Rodar o Projeto

> [Node.js](https://nodejs.org/en/) and [Yarn](https://yarnpkg.com/) or [NPM](https://www.npmjs.com/) are required

To clone the project, use the commands bellow:

```bash
  # Clone the repository
  ❯ git clone https://github.com/rocketseat-experts-club/criando-componentes-styled-components-react-native-2021-02-27.git

  # Enter directory
  ❯ cd criando-componentes-styled-components-react-native-2021-02-27
```

### Mobile

**Emulate in IOS**

```bash
  # Entre na pasta do diretório
  > cd template/Stylert

  # Instale as dependências
  ❯ yarn

  # Instale as referências do iOS
  ❯ npx pod-install ios
  
  # Inicie o projeto
  ❯ yarn ios
```

**Android**

```bash
  # Entre na pasta do diretório
  > cd template/Stylert

  # Instale as dependências
  ❯ yarn
  
  # Inicie o projeto
  ❯ yarn android
```
---
 
## :purple_heart: Desenvolvimento da Solução

Reaproveitamento de código, organização centralizada, manutenção.

## Desafio

<img src=".github/imgs/Stylert-v1.png" />

## Construção do código

Criação do Container

```jsx
// src/components/Card/styles.tsx

import styled from "styled-components/native";

export const Container = styled.View`
  height: 72px;
  padding: 14px;
  margin: 24px;
  border-radius: 4px;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  background-color: ${({ theme }) => theme.colors["neutral-100"]};
`;
```

Utilizando o Container

```jsx
// src/components/Card/index.tsx

import { Container } from "./styles";

<Container>
  <Text>Hello</Text>
  <Text>Hello</Text>
</Container>;
```

<hr/>

### Ganhos

- [x] estilos centralizados;
- [x] escopos locais, ou seja, sem efeitos colaterais dado que a alteração ocorre somente naquele ambiente;
- [x] e algo muito massa, são estilos dinâmicos;

<hr/>

Criação da label e da descrição

```jsx
// src/components/Card/styles.tsx

export const Label = styled.Text`
  font-family: ${({ theme }) => theme.fonts.text};
  font-size: 24px;
  color: ${({ theme }) => theme.colors["neutral-700"]};
`;

export const Description = styled.Text`
  font-family: ${({ theme }) => theme.fonts.text};
  font-size: 24px;
  color: ${({ theme }) => theme.colors["neutral-700"]};
`;
```

```jsx
// src/components/Card/index.tsx

import { Container, Label, Description } from "./styles";

<Container>
  <Label>R$ 100,00</Label>
  <Description>pago</Description>
</Container>;
```

Criando um estilo compartilhado

```jsx
// src/components/Card/styles.tsx

import styled, { css } from "styled-components/native";

const fontVariant = css`
  font-family: ${({ theme }) => theme.fonts.text};
  font-size: 24px;
  color: ${({ theme }) => theme.colors["neutral-700"]};
`;

export const Label = styled.Text`
  ${fontVariant};
`;

export const Description = styled.Text`
  ${fontVariant};
`;
```

### Criando interface

```ts
// src/components/Card/interface.ts

export enum CardStatus {
  PAGO = "pago",
  EM_ABERTO = "em aberto",
}

export interface ICardProps {
  amount: string;
  status: keyof typeof CardStatus;
}
```

### Recebendo as props

```jsx
// src/components/Card/index.tsx

import React from "react";
import { ICardProps } from "./interface";

import { Container, Label, Description } from "./styles";

const Card = ({ amount, status }: ICardProps) => {
  return (
    <Container>
      <Label>{amount}</Label>
      <Description>{CardStatus[status]}</Description>
    </Container>
  );
};

export default Card;
```

### Adicionando os valores no App

```jsx
// src/components/App.tsx

<Card amount="R$ 100,00" status="PAGO" />
```

<hr/>

### Adicionando estilo a label e descrição

```jsx
// src/components/Card/index.tsx

const Card = ({ amount, status }: ICardProps) => {
  const isPaid = status === "PAGO" ? "success-400" : "warning-400";

  return (
    <Container>
      <Label>{amount}</Label>
      <Description color={isPaid}>{CardStatus[status]}</Description>
    </Container>
  );
};
```

```jsx
// src/components/Card/interface.ts
import { colors } from "../../theme/colors";

export interface ICardStyledProps {
 color: keyof typeof colors;
}
```

```jsx
// src/components/Card/styles.tsx

export const Description =
  styled.Text <
  ICardStyledProps >
  `
 ${fontVariant};
 color: ${({ color, theme }) => theme.colors[color]};
`;
```

```jsx
// src/App.tsx

<Card amount="R$ 100,00" status="PAGO" />
<Card amount="R$ 100,00" status="EM_ABERTO" />
```

### Solicitando alterações

<img src=".github/imgs/Stylert-v2.png" />

```jsx
// src/components/Card/index.tsx

import { ICardProps, CardStatus, TCardStatusVariant } from "./interface";

const Card = ({ amount, status }: ICardProps) => {
  // const isPaid = status === "PAGO" ? "success-400" : "warning-400";

  const statusVariant: TCardStatusVariant = {
    PAGO: "success-400",
    EM_ABERTO: "warning-400",
    EM_ATRASO: "error-400",
    REVERTIDO: "neutral-400",
  };

  return (
    <Container>
      <Label>{amount}</Label>
      <Description color={statusVariant[status]}>
        {CardStatus[status]}
      </Description>
    </Container>
  );
};
```

Adicionar os itens a interface

```ts
// src/components/Card/interface.ts
export enum CardStatus {
  PAGO = "pago",
  EM_ABERTO = "em aberto",
  EM_ATRASO = "em atraso",
  REVERTIDO = "revertido",
}

export type TCardStatusVariant = {
  [key in keyof typeof CardStatus]: keyof typeof colors;
};
```

### Adicionando cor dinâmica

```jsx
// src/components/Card/index.tsx

import { ICardProps, CardStatus, TCardStatusVariant } from "./interface";

const Card = ({ amount, status }: ICardProps) => {
  // const isPaid = status === "PAGO" ? "success-400" : "warning-400";

  const isStatusReversed = status === "REVERTIDO";

  const statusVariant: TCardStatusVariant = {
    PAGO: "success-400",
    EM_ABERTO: "warning-400",
    EM_ATRASO: "error-400",
    REVERTIDO: "neutral-400",
  };

  return (
    <Container>
      <Label>{amount}</Label>
      <Description
        strikeThrough={isStatusReversed}
        color={statusVariant[status]}
      >
        {CardStatus[status]}
      </Description>
    </Container>
  );
};
```

Adicionando a interface

```ts
// src/components/Card/interface.ts

export interface ICardStyledProps {
  color: keyof typeof colors;
  strikeThrough: boolean;
}
```

```jsx
// src/components/Card/styles.tsx

${({ strikeThrough, theme, color }) =>
   strikeThrough &&
   css`
     text-decoration: line-through;
     text-decoration-color: ${theme.colors[color]};
   `};

```
