# Relatorio de Eventos Inteli

Pagina estatica para consultar, filtrar e exportar o relatorio interno de eventos do Inteli por trimestre.

O projeto roda direto no navegador e esta preparado para publicacao via GitHub Pages. Nao ha backend nem etapa de build.

## Estrutura

```text
.
|-- index.html
|   Aplicacao inteira: layout, dados processados, filtros e exportacoes.
|
`-- data/
    `-- eventos.csv
        Base original de eventos.
```

## Publicacao no GitHub Pages

Este projeto pode ser publicado como site estatico pelo GitHub Pages.

Configuracao recomendada no GitHub:

1. Abra o repositorio no GitHub.
2. Va em `Settings` > `Pages`.
3. Em `Build and deployment`, selecione:
   - `Source`: `Deploy from a branch`
   - `Branch`: `main`
   - `Folder`: `/root`
4. Salve.

Depois disso, o GitHub Pages publica o `index.html` da raiz do projeto.

Como nao existe build, qualquer mudanca enviada para a branch publicada atualiza o site apos o deploy automatico do GitHub Pages.

## Como atualizar os dados

A base original fica em [data/eventos.csv](data/eventos.csv). O arquivo segue o formato da planilha de eventos, separado por mes, com uma linha de nome do mes e depois o cabecalho das colunas.

Colunas esperadas:

```text
Data do evento,Dia da semana,Evento,,Area demandante,Espaco,Horario,N convidados,Ticket Eventos,Ticket IT Bar,Ticket Facilities,Status
```

Para atualizar:

1. Exporte ou edite a planilha mantendo o mesmo formato do CSV atual.
2. Substitua o arquivo `data/eventos.csv`.
3. Mantenha as datas no formato `DD/MM/AA`, por exemplo `19/01/26`.
4. Mantenha os nomes dos meses como separadores: `Janeiro`, `Fevereiro`, `Marco`, etc.
5. Para eventos sem informacao, use `-` ou deixe o campo vazio.
6. Evite remover ou reordenar colunas.

Importante: a versao atual da pagina nao le o CSV diretamente em tempo de execucao. Os dados exibidos no site ficam embutidos no `index.html`, na constante `ALL_EVENTS`.

Por isso, depois de atualizar `data/eventos.csv`, tambem e necessario sincronizar o bloco `ALL_EVENTS` dentro do `index.html`. Se apenas o CSV for alterado, o GitHub Pages continuara exibindo os dados antigos.

## Campos usados pelo relatorio

Cada evento exibido no site usa estes campos processados:

- `date`: data em formato `AAAA-MM-DD`
- `month`: mes por extenso
- `name`: nome do evento
- `tipo`: tipo ou categoria do evento
- `area`: area demandante
- `espaco`: espaco utilizado
- `horario`: horario do evento
- `convidados`: numero de convidados
- `ticket_ev`: ticket de Eventos
- `ticket_it`: ticket de IT Bar
- `ticket_fac`: ticket de Facilities
- `status`: status do evento
- `drive`: link de pasta, quando existir

## Exportacoes

A pagina permite exportar:

- `PDF`: usa a impressao do navegador.
- `PowerPoint`: gera um `.pptx` editavel no navegador, usando os dados do trimestre selecionado.

O PowerPoint e gerado a partir do periodo ativo na tela. Antes de exportar, selecione `1o Tri 2026`, `2o Tri 2026`, `3o Tri 2026` ou `4o Tri 2026`.

## Teste local

Como e um site estatico, basta abrir o arquivo `index.html` no navegador.

Tambem e possivel servir a pasta localmente com qualquer servidor estatico, por exemplo:

```powershell
python -m http.server 8000
```

Depois acesse:

```text
http://localhost:8000
```

## Cuidados antes de publicar

Antes de enviar para o GitHub Pages:

1. Abra o `index.html` localmente.
2. Confira se os totais do trimestre batem com a base.
3. Teste os filtros e abas principais.
4. Exporte um PDF.
5. Exporte um PowerPoint e confira se o arquivo abre no PowerPoint/Google Slides.
6. Confirme que `data/eventos.csv` e `ALL_EVENTS` estao sincronizados.
