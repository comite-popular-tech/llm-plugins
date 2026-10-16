# Modelo de corpo de PR

Se o repo tem template, use o dele e ponha "Para quem revisa" e "Como testar" no topo; as seções de teste do template ficam como estão, para o relato do autor. Senão, use este. Omita as seções que não se aplicam, sem preencher com "N/A".

```markdown
## Para quem revisa
- O que a pessoa que revisa precisa ler ou decidir, em uma ou duas linhas por item.
- Exemplos: "decidir X"; "conferir o arquivo Y"; "nada a decidir: só conferir o plano".

Fecha https://github.com/<org>/<repo>/issues/<n>
Parte de <URL do épico ou da issue maior>
Depende de / conflita com: <URLs>
Origem do pedido: <conversa, link ou quem pediu; só se não houver issue>
Fork: sem CI nem plano completos; precisa de alguém com acesso para rodar <o quê>.

## Como testar
1. `<comando ou clique exato>` → <resultado esperado>.
2. <2 a 5 passos, rápidos de seguir>.

## Antes do merge
<só se houver pré-requisito: token, segredo, permissão, ordem>
O que falta, quem tem acesso para fazer e o que quebra se o merge vier antes. Só nomes e permissões, nunca valores.

## Por quê
O problema real, com número ou link do log. Duas a quatro linhas. Decisões tomadas e as alternativas descartadas, quando importam.

## O que muda
- Para quem usa: uma ou duas frases do ponto de vista de quem usa (ou "nada ainda, chega desligado").
- No código: lista curta, arquivos entre crases.

## O que o merge faz
Liga, desliga ou não faz nada. Como vai ao ar (aplica no merge ou alguém publica à mão) e quem publica. Jobs agendados entram? Em qual conta?

## Resultado dos testes
- `<comando>`: <resultado e contagem>.
- Cenários em tabela, quando houver.
- Falhas que já existiam na main: <quais>.
- Não conferi: <o que e por quê>.

## Depois do merge
1. <passo e quem faz>.

## Como conferir
- `<comando>` deve devolver <resultado esperado>.

## Se algo der errado
<obrigatório em infra e deploy> Como voltar atrás, passo a passo.

## Fica de fora
O que não entra, por quê, e a issue onde está registrado: https://github.com/<org>/<repo>/issues/<n>
```

Lembretes
- "Para quem revisa" e "Como testar" são as duas seções que todo PR tem. Se não há nada a decidir, diga isso.
- "Como testar" é o roteiro de quem revisa (2 a 5 passos, com resultado esperado). "Resultado dos testes" é o seu relato: comando, contagem, falhas antigas, o que não conferiu.
- Referências sempre por URL completa; fechamento com a palavra: `Fecha https://...`.
- Sem segredo, e-mail pessoal, caminho de máquina, dado de produção ou de terceiros.
- Grave o texto num arquivo e abra com `gh pr create --body-file`.
