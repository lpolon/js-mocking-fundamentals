# monkey-patching

## src/no-framework/monkey-patching

exemplo de um stub que torna o teste
determinístico para testar a função thumbwar.

monkey-patching é o assigning e reassigning da utils.getWinner para o stub e
depois de volta para a função original.

# mock-fn

## src/\_\_tests\_\_/mock-fn

Afirmações sobre COMO uma função está sendo chamada,
por exemplo: a função não está sendo chamada com os argumentos esperados.

Ele sugere que isso ajuda a testar a implementação. Entra na discussão sobre o
que testar, responsabilidades, etc.. Precisei checar chamadas na palestra de
ruby

mock setup:

```javascript
const originalGetWinner = utils.getWinner
utils.getWinner = jest.fn((p1, p2) => p1)

// cleanup
utils.getWinner = originalGetWinner
```

# spyOn

## /src/\_\_tests\_\_/spy.js
Nos casos nos casos onde utilizamos o mock e depois
"restauramos" a implementação original, podemos, alternativamente, utilizar o
spyOn

```javascript
jest.spyOn(utils, 'getWinner')

// opcional
utils.getWinner.mockImplementation((p1, p2) => p1)

// cleanup
utils.getWinner.mockRestore()
```

# mock de um módulo inteiro, ao invés de apenas uma função:

## /src/\_\_tests__/inline-module-mock
Todos os exemplos até agora, ainda são uma forma de monkey patching.
Tipo, fazemos o mock de utils.getWinner e thumb-war chama essa função, mas sem dependency injection.

```javascript
jest.mock('../utils', 
// factory function returns the mocked version of the module
() => {
  return {
    getWinner: jest.fn((p1, p2) => p1)
  }
})

  // cleanup
  utilsMock.getWinner.mockReset()
```

# _\_\Mocks__
serve para compartilhar mocks entre arquivos de teste.
O arquivo precisa ter o nome do módulo que queremos mockar.

ver exemplo no arquivo para utils.