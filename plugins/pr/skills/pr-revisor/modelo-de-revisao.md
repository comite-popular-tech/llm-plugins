# Modelo de revisão

## Corpo do review

```markdown
**Veredito:** Aprovar | Aprovar com ressalvas | Pedir mudanças
**Antes do merge:** <uma linha por item que precisa mudar; "nada" se não houver>

**Para quem revisa:** <como o bloco do PR foi atendido: decidido, conferido ou ausente>
**Como testar:** <passou | falhou no passo N: o que aconteceu | ausente>
**Conferi:** <commit `abc1234`; o que foi lido e rodado, com contagem de testes; falhas que também falham na main; o que não foi rodado ou lido>

**Pode melhorar**
- <item de uma linha, com link para o arquivo no commit>
- <sugestão que amplia escopo: https://github.com/<org>/<repo>/issues/<n>>
```

Um "ótimo" curto no veredito é ok. Aprovar sem dizer o que foi conferido, não.

## Comentário inline

````markdown
**<Resumo do problema em uma linha>**

<Cenário que quebra: entrada, saída errada, consequência.> <Correção em uma ou duas linhas.>

```suggestion
<código sugerido, quando aplicável>
```
````

Nit: comece com "pode melhorar:" e diga que não trava o merge.

## Rascunho de issue (sugestão que amplia o escopo)

Só quando não existe issue que cubra a sugestão. Mostre à pessoa antes de abrir.

```markdown
**Título:** <imperativo ou "decidir X", curto>

<Contexto em duas ou três linhas, com link para o PR e para o trecho no commit.>

**Proposta:** <o que fazer, uma frase>
**Fora do PR porque:** <por que não é condição de merge>
```

## Resposta a thread

`Corrigido em abc1234.` ou uma frase com o motivo de não proceder.
