# Por que estas regras

As regras desta skill saíram de testes comparados, com o mesmo modelo de IA, medindo tempo e qualidade de cada peça. Abaixo, o que cada teste ensinou, sem os nomes das marcas usadas.

## Rodada 1: cinco peças sem skill
| Peça | Como foi pedida | Tempo | Resultado |
|---|---|---|---|
| Institucional para telão (16:9, 18 s) | O pedido **ditou o visual**: "pontos, linhas e formas suaves que se conectam", "palavras aparecerão com transições fluidas" | 14,6 min | **Ruim**: a mesma composição o filme inteiro, partículas, palavras soltas em fade, logo centralizado |
| App de delivery (9:16, 10 s) | Só a ideia e a ação: o pedido é confirmado, a moto atravessa o mapa, o contador cai até zero | 7,2 min | **Bom**: história com começo, meio e fim, tudo desenhado em código |
| O mesmo delivery **com as regras do estúdio** | Mesma ideia, com as regras da seção 6 | 12,1 min | **Muito bom**: um acento, tipografia forte, câmera seguindo a moto, um aviso novo a cada 2 s, som na grade |
| Lançamento de marca no estilo de uma referência com pessoas e texturas | Pediu prints e logo reais do site e copiou a referência inteira | **85 min** | **Horrível**: colagem de 3 a 4 linguagens, fotos de pessoas com logo cortado, prints ilegíveis |
| Lançamento de produto no estilo de uma referência de interface e tipografia | Referência como norte, sem pessoas, logo SVG e fonte oficial | 27,8 min | **Muito bom**: peça limpa, coerente, só tipografia, cards e interface |

### O que ficou provado
1. **Descrever o movimento no pedido piora o resultado.** O pedido deve dizer o que acontece (a ideia e a ação), nunca como anima. "Formas que se conectam" e "transições fluidas" produziram exatamente os clichês.
2. **História com verbo.** "Pedido confirmado → moto → contador → entregue" é uma mudança de estado que o olho acompanha; "tecnologia, estratégia, conexão" é uma lista.
3. **Regras do estúdio transformam um bom rascunho em peça.** A proibição de clichês tirou o confete e o fade; "um acento" limpou a paleta; "algo novo a cada 2 a 4 s" gerou ritmo; a folha de contato pegou leitura ruim (nota 5 corrigida para 8).
4. **Mídia real derruba a qualidade e o tempo.** Foto, vídeo e print só se movem, cortam e desfocam: vira apresentação de slides. No teste de 85 min, 44 min foram perdidos com a captura travando por grão em `mix-blend-mode` sobre imagens grandes.
5. **A referência precisa vir com o porquê.** Sem saber o que agradou, a IA copia a superfície e mistura estilos. Referência de interface e tipografia se traduz em código; de pessoas e texturas físicas, não.
6. **A nota da própria IA não basta.** Todos os testes terminaram com 8 em tudo, inclusive o reprovado. Por isso existem checagens objetivas que reprovam sozinhas.
7. **Referência é opcional.** O teste muito bom sem referência mostra que ideia + regras já bastam.
8. **Velocidade vem de não reinventar:** procurar ffmpeg e Chrome custava 2 a 4,5 min por teste (hoje: cache); escrever render e áudio do zero, 1 a 3 min (hoje: modelos); render refeito, 4,5 a 10 min (hoje: uma vez só, com rascunho antes).

## Rodada 2: mais de dez filmes completos para um mesmo cliente
Sequência: demonstrativo → imersivo → publicitário → "um dia" → minimalista → sete versões finais. O que serve para qualquer motion:

9. **O objetivo da peça vale mais que a técnica.** Quatro versões contaram a história errada sobre o que o cliente faz e foram refeitas. Por isso o briefing pergunta o que a pessoa precisa sentir ou entender, e para quem é.
10. **Demonstrativo cansa; publicitário prende.** Mostrar cada função foi "demonstrativo demais"; títulos fortes e menos informação por tela funcionaram.
11. **"Informação demais" foi a crítica mais repetida.** Uma ideia por tela.
12. **Partículas foram rejeitadas.** O "nascer do nada" ficou melhor com texto que decodifica, card escaneado por uma linha do acento e símbolo desenhado por traço.
13. **Minimalismo pontual funciona:** "Apresentando" com o nome, número grande que embaralha, slogan com troca de palavra, entre momentos densos.
14. **Tensão → virada é o melhor gancho:** fragmentos do problema tremendo, um traço do acento que organiza tudo e uma palavra gigante de virada.
15. **O campo de cor com texto em tinta é o melhor respiro** e prepara o slogan e o fecho.
16. **Defeitos aparecem no meio do movimento.** Um card cruzando o título e outro encostando no texto não apareciam na folha por batida. Daí `--marcos` e `--colisao`.
17. **Flash longo vira véu cinza.** Só curto e na camada de cima.
18. **Palavra gigante corta na borda.** A 520 px saía do quadro; a 330 px coube.
19. **MP4 em gravação parece corrompido.** O arquivo foi aberto durante o render duas vezes; o render agora grava `.parcial` e renomeia no fim.
20. **Dados reais não entram.** Tudo com dados fictícios, o que também permite animar cada elemento.
21. **A fonte certa muda tudo.** Com a fonte de sistema no lugar da oficial, a peça parecia de outra marca.
22. **Opções boas mudam de propósito em dois eixos ou mais;** a mistura definitiva usou a opção mais bem construída como espinha e trouxe momentos pontuais da mais criativa.
23. **Edição por `sed` com template strings quebra o código.** Use a ferramenta de edição ou scripts Node.
