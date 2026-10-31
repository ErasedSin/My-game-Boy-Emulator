# GBA Player

![Tela de abertura](docs/abertura.png)

Um player de Game Boy Advance que roda dentro do navegador, sem instalar nada. O emulador por baixo é o mGBA, compilado para WebAssembly. O que eu fiz foi tudo em volta dele: abrir o jogo, controles, saves, escala de vídeo e uma abertura que explica o que está errado quando o emulador não sobe.

Site no ar: https://erasedsin.github.io/My-game-Boy-Emulator/

O repositório não traz jogo nenhum. Cada pessoa escolhe o arquivo do próprio cartucho, e ele fica guardado só no navegador dela.

![Interface do player](docs/interface.png)

## O que ele faz

Abre jogos em .gba, .gb, .gbc ou dentro de um .zip. Antes de entregar o arquivo ao emulador, a página lê os primeiros 192 bytes e mostra na lateral o título interno, o código do jogo e se o cabeçalho de GBA é válido. Se o emulador recusar o arquivo, a mensagem aparece na tela e o motivo vai para o registro.

Os saves ficam no IndexedDB do navegador. Uma sincronização roda a cada 15 segundos, quando a aba é escondida e quando a página fecha, então fechar sem querer não perde o progresso. Dá para baixar o arquivo .sav, levar para outro aparelho e enviar de volta (o nome precisa ser o mesmo do jogo). Existe também um slot de estado, que guarda uma foto de tudo que está na memória do emulador e é diferente do save interno do jogo.

No computador valem as teclas padrão do mGBA: setas, X e Z para A e B, A e S para L e R, Enter e Backspace para Start e Select. Em aparelhos de toque aparecem botões na tela. Eles acendem quando a tecla correspondente é apertada, o que ajuda a ver o que está sendo lido.

A escala do vídeo é sempre inteira, de 1x a 5x, para os pixels ficarem nítidos, ou automática conforme a janela. Tem tela cheia e volume de 0 a 200%.

Um painel de registro mostra o que aconteceu desde que a página abriu: se o navegador liberou as threads e o WebGL2, onde estão os arquivos do núcleo, quanto tempo levou para copiar o jogo e o resultado do loadGame. Dá para copiar o texto e mandar para alguém quando algo não funciona.

A abertura é uma tela de título em pixel art, com cartucho, estrelas e um filtro de monitor antigo, tudo desenhado por código, sem imagens. Enquanto espera a pessoa apertar Enter, ela roda as checagens do ambiente. Se alguma falha, o botão vira "entrar mesmo assim" e o erro fica à vista.

## Por dentro

O mGBA-wasm usa threads, e o navegador só libera isso em páginas isoladas pelos cabeçalhos COOP e COEP. O GitHub Pages não deixa configurar cabeçalhos, então uso o coi-serviceworker, que injeta os cabeçalhos por meio de um service worker. É por isso que a primeira visita recarrega a página sozinha.

O resto é HTML, CSS e JavaScript puro, num único index.html.

## Limites

Testado no Edge e no Chrome. O Safari eu não testei, e pelos requisitos de threads pode não funcionar. Em notebook antigo o desempenho depende da placa de vídeo e da aceleração gráfica estar ligada. As teclas ainda não são remapeáveis, e só existe um slot de estado.

## O que falta

Vários slots de estado, remapear teclas, controle USB pela Gamepad API, acelerar e câmera lenta (o núcleo já tem a função) e testes automatizados.

## Créditos

O emulador é o mGBA, de Vicki Pfau, sob a licença MPL-2.0. A versão em WebAssembly vem do pacote @thenick775/mgba-wasm (2.6.0). O coi-serviceworker é de Guido Zuidhof (MIT). O código desta página usa a licença MIT. Os detalhes estão no [NOTICE.md](NOTICE.md).

Game Boy Advance é marca registrada da Nintendo, e este projeto não tem relação com a empresa.
