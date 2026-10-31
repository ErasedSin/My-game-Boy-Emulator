# Erased Player

Player de Game Boy Advance no navegador, feito em HTML, CSS e JavaScript. Usa o mGBA compilado para WebAssembly como núcleo de emulação. O meu trabalho está na interface e na integração: carregamento do jogo, controles, saves e instalação.

**Este projeto não inclui jogos nem BIOS.** Cada pessoa escolhe o arquivo do jogo que possui, e ele fica guardado apenas no navegador dela.

## Recursos
- Tela de título no estilo de abertura de jogo (estrelas em canvas, cartucho desenhado pixel a pixel, efeito de monitor antigo), com a autoria e o propósito do projeto. Ela mostra a checagem real de cada etapa e espera a pessoa apertar Enter ou clicar. Se algo falha, explica o motivo
- Interface de ferramenta: barra lateral com arquivo, emulação, estados, saves, escala, tela cheia e volume
- Leitura do cabeçalho do jogo no próprio navegador (título, código e marca de validade)
- Saves guardados no navegador (IndexedDB), com sincronização automática
- Baixar e enviar o arquivo de save (.sav)
- Escala de vídeo inteira (1x a 5x) ou ajustada à tela
- Registro de eventos, que pode ser copiado
- Teclado no computador e controles na tela no celular

## Tecnologias
- HTML, CSS e JavaScript puro
- [mGBA](https://mgba.io) em WebAssembly, pelo pacote `@thenick775/mgba-wasm`
- `coi-serviceworker`, para publicar no GitHub Pages (o núcleo usa threads e exige isolamento de origem)

## Rodar no computador
O arquivo precisa ser aberto por um servidor, não direto do disco:

```bash
python -m http.server 8000
```

Abra http://localhost:8000. Na primeira visita a página recarrega sozinha uma vez.

## Publicar no GitHub Pages
Settings > Pages > Deploy from a branch > main / root. Aguarde cerca de 1 minuto e abra o site. Se aparecer a mensagem de preparo do navegador, atualize com Ctrl+Shift+R.

## Limitações
- Teste em navegadores recentes (Chrome, Edge e Firefox). O Safari pode não funcionar por causa dos requisitos de threads.
- O arquivo de save enviado precisa ter o mesmo nome do jogo, terminando em `.sav`.

## Créditos e licenças
Veja o [NOTICE.md](NOTICE.md). O código desta interface usa a licença MIT. O mGBA usa a MPL-2.0, e o código-fonte da versão usada está em https://github.com/thenick775/mgba.
