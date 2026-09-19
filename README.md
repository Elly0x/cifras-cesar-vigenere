# Cifras de César e Vigenère interativas

Ferramenta web pra cifrar, decifrar e quebrar duas cifras clássicas, mostrando cada letra sendo trocada em um log estilo terminal.

**Demo:** https://elly0x.github.io/cifras-cesar-vigenere/

> Projeto educacional. Essas cifras são fáceis de quebrar e não servem pra proteger dados reais.

## O problema

Criptografia costuma ser explicada só com teoria, e fica difícil enxergar o que acontece de verdade com cada letra. Este projeto deixa o processo visível: você digita um texto, escolhe a chave e acompanha a conta de cada caractere. Depois, na aba de quebra, vê por que a cifra de César não aguenta um ataque de força bruta.

## Funcionalidades

- **César:** deslocamento de 1 a 25 (slider e botões + e -), com o alfabeto de entrada e de saída lado a lado. As letras usadas no seu texto ficam marcadas.
- **Vigenère:** palavra-chave que se repete sob o texto, mostrando qual letra da chave age em cada letra.
- **Quebrar César:** testa os 25 deslocamentos de uma vez. Ao tocar numa linha que faz sentido, a página abre na aba César com aquele deslocamento.
- **Log da operação:** cada letra vira uma linha, por exemplo `[01] S(18) + 3 = V(21)`.
- Cifrar, decifrar, copiar o resultado e reaproveitar a saída como entrada.
- Funciona bem em tablet e celular.
- Tudo roda no navegador. Nenhum texto é enviado pra internet.

## Como funciona

Cada letra do alfabeto vira um número: A = 0, B = 1, ... Z = 25.

**César** soma um deslocamento fixo `k`:

```
cifrar:   E(x) = (x + k) mod 26
decifrar: D(x) = (x - k) mod 26
```

Exemplo com `k = 3`:

```
Segredo bem guardado  ->  Vhjuhgr ehp jxdugdgr
```

**Vigenère** usa um deslocamento diferente pra cada letra, definido por uma palavra-chave de tamanho `m` que se repete:

```
cifrar:   E(x_i) = (x_i + chave[i mod m]) mod 26
decifrar: D(x_i) = (x_i - chave[i mod m]) mod 26
```

Exemplo com a chave `LUA`:

```
ATAQUE
LUALUA
------
LNABOE
```

Regras de tratamento do texto:

- Acentos são removidos antes de cifrar (`ação` vira `acao`).
- Maiúsculas e minúsculas são mantidas.
- Números, espaços e pontuação passam sem mudar.
- Na chave do Vigenère, só letras contam. O índice da chave só avança em letras do texto.

## Por que essas cifras são quebráveis

- **César:** existem só 25 chaves possíveis. Testar todas leva um instante, e é exatamente o que a aba **Quebrar César** faz.
- **Vigenère:** resiste ao teste simples de todas as chaves, mas cai com **análise de frequência** e com o **método de Kasiski**, que descobre o tamanho da chave repetida e reduz o problema a vários Césares.

Hoje, criptografia de verdade usa algoritmos como AES, com chaves enormes e décadas de análise pública.

## Como rodar

Não precisa instalar nada. Baixe o repositório e abra o `index.html` no navegador.

## Estrutura

```
cifras-cesar-vigenere/
├── index.html   (página, estilo e lógica em um arquivo só)
└── README.md
```

## Tecnologias

HTML, CSS e JavaScript puros, sem bibliotecas. A fonte JetBrains Mono vem do Google Fonts, com fallback pra fontes mono do sistema.

## Próximas ideias

- Análise de frequência de letras pra atacar o Vigenère.
- Método de Kasiski pra estimar o tamanho da chave.
- Outras cifras simples: Atbash, ROT13 e cifra de substituição.
- Modo de exercício: a página gera um texto cifrado e você tenta descobrir a chave.
