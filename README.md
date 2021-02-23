# criando-componentes-com-styled-components-react-native

## Motivação

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
  background-color: ${({ theme }) => theme.colors["neutral-100"]};
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
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
