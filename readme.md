# Guia de usuário e desenvolvedor do appIDFBR

FGV - Innovation Lab

---

**Ao final deste manual o leitor estará apto a responder:**

*Por que a ferramenta foi criada?*

*Como operar a ferramenta?*

*Como corrigir ou modificar a ferramenta?*

**Nome do app:** *appIDFBR*

**Cliente:** *FGV - IBRE - SCI - NIP*

**Última atualização:** 30/11/2018

**Responsável:** *Luiz Fernando Coelho Passos* 

Informações da sessão:

```
> sessionInfo()
R version 3.5.0 (2018-04-23)
Platform: x86_64-w64-mingw32/x64 (64-bit)
Running under: Windows 7 x64 (build 7601) Service Pack 1

Matrix products: default

locale:
[1] LC_COLLATE=Portuguese_Brazil.1252 
[2] LC_CTYPE=Portuguese_Brazil.1252   
[3] LC_MONETARY=Portuguese_Brazil.1252
[4] LC_NUMERIC=C                      
[5] LC_TIME=Portuguese_Brazil.1252    

attached base packages:
[1] stats     graphics 
[3] grDevices utils    
[5] datasets  methods  
[7] base     

other attached packages:
 [1] bindrcpp_0.2.2    
 [2] webshot_0.5.1     
 [3] rmarkdown_1.11    
 [4] officer_0.3.2     
 [5] flextable_0.4.4   
 [6] magrittr_1.5      
 [7] zoo_1.8-4         
 [8] xlsx_0.6.1        
 [9] readxl_1.1.0      
[10] dplyr_0.7.8       
[11] purrr_0.2.5       
[12] lubridate_1.7.4   
[13] data.table_1.11.8 
[14] shinyWidgets_0.4.4
[15] stringr_1.3.1     
[16] shiny_1.2.0       

loaded via a namespace (and not attached):
 [1] tinytex_0.11    
 [2] tidyselect_0.2.5
 [3] xfun_0.6        
 [4] rJava_0.9-10    
 [5] lattice_0.20-35 
 [6] colorspace_1.3-2
 [7] htmltools_0.3.6 
 [8] yaml_2.2.0      
 [9] base64enc_0.1-3 
[10] rlang_0.3.0.1   
[11] later_0.7.5     
[12] pillar_1.3.0    
[13] glue_1.3.0      
[14] gdtools_0.1.7   
[15] uuid_0.1-2      
[16] bindr_0.1.1     
[17] munsell_0.5.0   
[18] cellranger_1.1.0
[19] zip_1.0.0       
[20] evaluate_0.12   
[21] knitr_1.21      
[22] callr_3.2.0     
[23] ps_1.3.0        
[24] httpuv_1.4.5    
[25] xlsxjars_0.6.1  
[26] Rcpp_1.0.0      
[27] xtable_1.8-3    
[28] promises_1.0.1  
[29] scales_1.0.0    
[30] jsonlite_1.6    
[31] mime_0.6        
[32] packrat_0.5.0   
[33] digest_0.6.18   
[34] stringi_1.2.4   
[35] processx_3.3.0  
[36] grid_3.5.0      
[37] tools_3.5.0     
[38] tibble_1.4.2    
[39] crayon_1.3.4    
[40] pkgconfig_2.0.2 
[41] xml2_1.2.0      
[42] assertthat_0.2.0
[43] rstudioapi_0.8  
[44] R6_2.3.0        
[45] compiler_3.5.0
```

# Introdução 

---

Este documento é um manual 2 em 1 que busca atender usuários e desenvolvedores do aplicativo appIDFBR.

  * A seção [Como usar a ferramenta? (para **usuários**)](#usuario) é voltada aos **usuários** que acessarão a ferramenta sem precisar entender o que há por trás dela. 

  * A seção [Como editar a ferramenta? (para **desenvolvedores**)](#desenvolvedor) é destinada a **desenvolvedores** que buscam modificar a ferramenta, seja para fazer alguma correção ou melhoria.
  
  Os autores buscaram construir a ferramenta de tal modo que o funcionamento básico fosse intuitivo aos usuários. Acreditando no sucesso desse objetivo, imagino que você seja um **desenvolvedor** em busca de informações sobre a edição do aplicativo. Este documento não tem como finalidade substituir um treinamento que capacite o uso avançado das ferramentas utilizadas, porém diversas referências para consultas serão deixadas ao longo do documento.

**Hitchhiker, grab your towel and don't panic!** O manual foi produzido com a finalidade de te guiar em qualquer modificação da ferramenta sem que você precise da ajuda de ninguém, mas, caso necessário, a equipe de desenvolvedores ficará muito feliz em responder seu e-mail:

  * <gustavo.lopo@fgv.br>
  * <fellipe.gomes@fgv.br>
  * <luiz.passos@fgv.br>
  
Críticas e sugestões também são bem-vindas.

## Síntese do projeto

Todo mês o NIP produz um relatório para avaliar o índice de dutos flexíveis - BR. Antes da existência dessa ferramenta, os relatórios eram produzidos de maneira manual e envolviam basicamente as seguintes etapas:

  1. Obtenção dos dados pelo sistema
  2. Análises
  3. Confecção de tabelas
  4. Escrever e formatar os relatórios e planilhas
  5. Exportar relatórios em PDF e planilhas em XLSX
  
Como os relatórios gerados a cada mês contêm os mesmos objetos (tabelas), variando apenas a data de referência da amostra coletada, projetou-se a automação das etapas de 1 a 5. Espera-se com isso acelerar a produção dos relatórios e evitar possíveis erros decorrentes de manipulação humana dos arquivos.


### Limitações atuais do aplicativo (21/12/2018)

Antes de prosseguir, é importante que você saiba que a consulta direta ao banco de dados[^db] via SQL[^SQL] ainda está **indisponível**. No momento ela só está disponível para os [desenvolvedores do aplicativo](#desenvolvedores_bbmp).

A razão disso é que o acesso ainda está em desenvolvimento e por enquanto só é possível o acesso local de forma individual. Futuramente esperamos que este acesso possa ser feito de forma geral. Isto é, qualquer pessoa com um login poderá utilizar o aplicativo hospedado no servidor.

### Próximos passos para o desenvolvimento

O acesso à base de dados no servidor ainda está indisponível e por conta disso as seguintes tarefas ainda estão pendentes e devem ser concluídas após a [liberação do acesso geral](#limitações).

  * Os dados obtidos do banco de dados via SQL são (d-1), isto é, são os dados de preço do dia anterior. Solicitar a TIC os dados disponibilizados em d, isto é, no dia para que o relatório gere os resultados mais atuais possíveis.
  * Combinar com a área que faz uso do aplicativo o momento para o fechamento dos cálculos realizados na base SIS[^SIS].
  
# Como usar a ferramenta? (para **usuários**)

---

## Obter dados

**Atenção:** Como a conexão direta com o banco de dados ainda **não está disponível**, será necessário fazer o input manual. Para gerar o relatório a partir de input[^input] manual utiliza-se os dados de 1 arquivo exportado do SIS:
 
  * IDFBR (SIS)
  
Os arquivos devem estar, respectivamente, nomeados exatamente como:

  - `idfbr.xlsx`
  
O arquivo acima é da seguinte forma (note que não é necessária nenhuma manipulação), veja:

![](src/img_readme/input1.gif)

*Exemplo de como é a base idfbr.xlsx*

## Processamento dos dados 

A primeira parte do processamento do app envolve a manipulação (internamente) dos dados, criação das planilhas, gráficos e tabelas e tudo isso é feito automaticamente ao pressionar o botão **Gerar Relatório**.

Para dar início à produção, insira a **data** que constará na carta (Data de hoje para gerar o mês passado).

**Obs.:** Caso queira fazer para datas passadas, clique sobre o botão acima de “Insira a data que constará na carta:” para liberar o uso de datas passadas.

Insira o **número do relatório** que aparecerá na capa do relatório, **para inserir a base de dados** selecione o arquivo e arraste-o e clique em **Gerar Relatório** (Note que essas instruções também são apresentadas no corpo to aplicativo). Observe atentamente os gifs abaixo para melhor entendimento.

**OBS:**

  - **1)** Nas **taxas de câmbio** não adicione o \%, digite apenas os números. É possível gerar o relatório sem digitar as taxas.
  - **2)** Os relatórios foram separados por abas, ou seja, digite o **número do relatório** para cada relatório clicando sobre as abas para mudar.
  - **3)** Primeiro clique em **Gerar Relatório**, após a notificação de sucesso, clique em **Download** mudando as abas baixando um por um. 
  

No caso, para algum mês passado faça da seguinte maneira:

![](src/img_readme/mes_passado.gif)

Ao clicar no botão **Gerar Relatório** será dado início à criação dos gráficos e tabelas (que serão armazenados temporariamente), quando eles estiverem prontos, a seguinte mensagem será exibida:

![](src/img_readme/sucesso.gif)

## Produto final

Ao final do processo, os relatórios disponíveis para a entrega para o cliente serão da seguinte maneira:

![](src/img_readme/relatorio_final_technip.gif)

*Exemplo do Relatório de Entrega - Technip*

![](src/img_readme/relatorio_final_ge.gif)

*Exemplo do Relatório de Entrega - GE OILGAS*

![](src/img_readme/relatorio_final_nov.gif)

*Exemplo do Relatório de Entrega - NOV*

![](src/img_readme/relatorio_final_petrobras.gif)

*Exemplo do Relatório de Entrega - Petrobras*

![](src/img_readme/relatorio_final_prysmian.gif)

*Exemplo do Relatório de Entrega - Prysmian*

# Como editar a ferramenta? (para **desenvolvedores**)

---

## Quem está apto a editar esse aplicativo?

O aplicativo foi pensado com dois conceitos desafiadores por trás:

* O aplicativo deverá ser facilmente editado.
* A edição não demandará um especialista em TI, podendo ser feita por um "cientista de dados iniciante". Como diria o famoso lema do Chef Gusteau, "qualquer um pode cozinhar" ([spoiler](https://www.youtube.com/watch?v=wasHFSVP6vQ/)).

Essas premissas foram buscadas até as últimas consequências e esperamos que um estagiário dedicado com pouco tempo de faculdade esteja apto a cozinhar. Segue descrição dos conhecimentos mínimos para cada tarefa.

Boa vontade, e talvez um pouco de sagacidade, será suficiente para editar a carta do relatório ou qualquer trecho de texto corrido. Conhecimentos em programação não serão necessários aqui.

Conhecimento básico em linguagem de programação [R](https://www.r-project.org/) será necessário caso deseje modificar alguma manipulação de dados e conhecimento básico da linguagem [$\LaTeX$](https://www.latex-project.org/) caso deseje modificar o documento PDF.

Para usuários mais experientes, que tenham interesse em modificar funcionalidades da ferramenta, será necessário algum conhecimento em [Shiny](https://shiny.rstudio.com/) e no caso da necessidade de modificar o estilo/aparência da ferramenta será necessário conhecimento básico da técnica de linguagem de programação web [CSS](https://pt.wikipedia.org/wiki/Cascading_Style_Sheets).

Isso é possível devido à arquitetura do aplicativo que pode ser segmentada em 3 compartimentos:

  i) Código para gerar os objetos do relatório (gráficos, tabelas, figuras e outros).
  ii) Código para compilar o documento PDF com os objetos gerados.
  iii) Código para gerar a interface amigável ao usuário que irá operar a ferramenta.

## Estrutura do diretório 

Veja a seguir como a pasta está organizada e sua descrição:

```
.
├─ appidfbr.Rproj 	        (Arquivo para abrir e organizar o projeto)        
├─ global.R                 (Configuracoes gerais do app)        
├─ ui.R                     (Interface do usuario)        
├─ server.R                 (Servidor do app)        
├─ src/                     (dependencias p/ processamento do app)
│   └─ img_output/          (Imagens geradas pelo script generate_image.R)
│   └─ img_readme/          (Imagens para readme)
│   └─ temp_zip/            (Arquivos temporarios para download no .zip de apoio)
│   └─ templates_pdf/       (Imagens para template do relatorio pdf final)
│   └─ functions/           (Funcoes desenvolvidas para o uso do app)
│   └─ generate_excel.R 	  (Script que gera as planilhas)
│   └─ generate_image.R 	  (Script que gera as imagens do relatorio)
│   └─ report_prysmian.Rmd  (Arquivo Rmarkdown que compila o relatorio .pdf)
│   └─ report_petrobras.Rmd (Arquivo Rmarkdown que compila o relatorio .pdf)
│   └─ report_nov.Rmd       (Arquivo Rmarkdown que compila o relatorio .pdf)
│   └─ report_ge_oilgas.Rmd (Arquivo Rmarkdown que compila o relatorio .pdf)
│   └─ report_technip.Rmd   (Arquivo Rmarkdown que compila o relatorio .pdf)
│   └─ date.txt			        (Criado pelo app: data informada pelo usuário)
│   └─ matriz_just.rds		  (Criado pelo app: matriz com as justificativas informadas pelo usuario)
├─ www                      (Dependencias p/ customizar o app)
│   └─ css                  (Pasta com arquivo css)
│   └─ fonts                (Arquivos de formatacao do css)
│   └─ images               (Imagens utilizadas no css)
│   └─ template.html        (Template html para app)
├─ data                     (Pasta para armazenas dados de entrada do app)
│   └─ dep                  (Arquivos Excel que servem template e persistencia de dados )
│   └─ input_e_entregas     (Backup de arquivos utilizados como carga para o app e outputs)
└─ readme.md                (Este manual)
```

Os arquivos que você provavelmente terá interesse em editar são:

  * **global.R**: Arquivo que contem configuracoes de inicializacao do app como carregar pacotes, carregar dependencias, informacoes delogin etc
  * **ui.R**: É o script que compila a interface do usuário
  * **server.R**: É o script que renderiza os scripts de acordo com a interacao do usuário
  * **generate_excel.R**: Script que é renderizado quando o usuário pressiona o botao `Gerar Relatório`, este arquivo você deve editar caso deseje fazer alterações nas planilhas, você verá mais informações em: [Planilhas](#planilhas)
  * **generate_image.R**: Script que é renderizado quando o usuário pressiona o botao `Gerar Relatório`, este arquivo você deve editar caso deseje fazer alterações nos gráficos e tabelas do relatório, você verá mais informações em: [Gráficos](#graficos) e [Tabelas](#tabelas)
  * **report_[...].Rmd**: é o arquivo que você deve editar caso deseje fazer alguma alteração no texto ou na aparência do arquivo PDF, você verá mais informações em: [Conteúdo do texto](conteudo_texto)

## Como o aplicativo funciona?

O esquema seguinte sintetiza a lógica do aplicativo:

![](src/img_readme/pipeline_app.png)

É possível notar que na primeira etapa ocorre a **Entrada** dos dados através do input manual dos dados (como apresentado na Seção [Como usar o aplicativo](#como_usar_o_app)).

Na parte da **Execução** do app temos o script `app.R` que contém informações da interface do usuário e do servidor que chama as rotinas `generate_excel.R` e `generate_image.R` que criam os objetos para os relatórios. Esses objetos criados são salvos temporariamente na pasta `src/img_output` e em conjunto com os objetos do template do relatório na pasta `src/img_template_pdf/`.

Junto com o template do relatório, que está na pasta `src/img_template_pdf/`, esses objetos são combinados nos scripts finais `report_ge_oilgas.Rmd`, `report_nov.Rmd`, `report_petrobras.Rmd`, `report_prysmian.Rmd` e `report_technip.Rmd`, que preparam os documentos PDF para download na **Saída** do app.

# Realizar alterações

---

### Ambiente do RStudio 

A linguagem de programação R, como muitas outras linguagens de programação, trabalha com o conceito de [pacotes](http://r-pkgs.had.co.nz/intro.html) que reúnem códigos, dados, documentação, testes e são fáceis de compartilhar com outras pessoas.

Neste projeto foram utilizadas versões específicas de pacotes do R e suas versões podem ser conferidas no documento ao final deste documento.


## Planilhas {#planilhas}

O pacote utilizado para gerar as planilhas é o `xlsx`. Este pacote foi escolhido porque era o úncio que atendia as exigências para fazer as planilhas Excel.

Referência para ajudar a entender como utilizar o xlsx e gerar planilhas elegantes: <http://www.sthda.com/english/wiki/r-xlsx-package-a-quick-start-guide-to-manipulate-excel-files-in-r> e <https://cran.r-project.org/web/packages/xlsx/xlsx.pdf>.

As planilhas Excel são geradas pelo script `generate_excel.R`. No início do script é feita a leitura e parte da manipulação dos dados e em seguida inicia-se a seção de `# #### Escrever Excel #### #` onde as planilhas são geradas, veja um esquema para facilitar o entendimento:

![](src/img_readme/pipeline_excel.png)

OBS: foi utilizado o exemplo do ICSP porque segue a mesma lógica para construção das planilhas.

Os arquivos gerados aqui são armazenados na pasta: `src/temp_zip/`.

### Tabelas

Referência para ajudar a entender como utilizar o flextable para gerar as tabelas: <https://davidgohel.github.io/flextable/articles/overview.html>

As tabelas são geradas de maneira muito semelhante aos gráficos. Todas as tabelas que aparecem no relatório PDF são geradas pelo script `generate_image.R` na seção `#### TABELAS ####`, onde as tabelas do relatório são geradas. Veja um esquema para facilitar o entendimento:

![](src/img_readme/pipeline_figuras.png)

Os arquivos gerados aqui também são temporariamente armazenados na pasta `src/img_output` para serem obtidos posteriormente e inseridos no relatório PDF.

### Conteúdo do texto 

No momento que os dados já foram obtidos e todos os objetos que irão fazer parte do relatório já estão prontos, chega a hora de juntar tudo em um único arquivo RMarkdown. Mais informações sobre RMarkdown na página oficial em <https://rmarkdown.rstudio.com/> e no livro do autor do pacote: <https://bookdown.org/yihui/rmarkdown/>.

**Mas por que RMarkdown?**

Arquivos RMarkdown (com a extensão `.Rmd`, como `report.Rmd`) permitem que o desenvolvedor una em um único documento “pedaços” de texto (Utilizando linguagens apropriadas para alta formatação, como `Markdown`,`LaTeX`, `CSS` dentre outros ) e “pedaços” de código (como `R`, `Python`, `SQL` etc), possibilitando a criação de um documento que faz o uso de rotinas elaboradas por diferentes desenvolvedores, utilizando diferentes linguagens de programação e obtendo o melhor de cada uma delas.


Para alterações no conteúdo do texto, basta abrir o arquivo `report.Rmd` e fazer as alterações necessárias no texto e clicar em `Run app`, como ilustrado no gif da seção [Como usar o aplicativo](#como_usar_o_app)

![](src/img_readme/pipeline_texto.png)

### Aparência do documento

Para alterar as imagens do template (cabeçalho, rodapé, logo, etc.)  acesse a pasta `src/template_pdf` e substitua a imagem indesejada por um arquivo homônimo com a mesma extensão.

# Como fazer novas publicações no Servidor Interno da FGV (em um container Docker)

---

Para hospedar uma nova versão do aplicativo no servidor interno da FGV em um container Docker serão necessários alguns passos:

1.	Tenha certeza de todas as funcionalidades da ferramenta estão funcionando de acordo com o esperado
2.	Após isso, junte todos os arquivos necessários para o funcionamento em um arquivo .zip
3.	Envie este arquivo zip para o responsável na TIC pelas publicações (em caso de dúvidas à quem enviar, [entre em contato com os desenvolvedores](#desenvolvedores_bbmp))
4.	Caso o arquivo seja grande demais para enviar por e-mail, coloque os arquivos em um pendrive e leve-os para o responsável pela publicação
5.	Lembre-se sempre de enviar junto ao zip um documento .txt com as informações da última sessão R na qual o aplicativo funcionou (para obter tal informação, rode no console do R o comando: `sessionInfo()`

# FAQ

---

*Quais precauções devo tomar ao editar o aplicativo?*

Como mencionado na seção [Como fazer as alterações mencionadas com segurança?](#fazer_alteracoes) é altamente recomendado que o responsável pelas alterações desta ferramenta faça uma cópia de segurança da última versão funcionando (Selecionar, Ctrl+C, Ctrl+V).

*Como editar a carta?*

  * Releia a seção [Conteúdo do texto](#conteudo_texto)

*Como editar a imagem da capa?*

  * Releia a seção [Conteúdo do texto](#conteudo_texto)

*Como mudar o rodapé ou cabeçalho?*

  * Releia a seção [Conteúdo do texto](#conteudo_texto)

*Como alterar uma figura\tabela do relatório?*

  * Releia as seções [Gráficos](#graficos) e [Tabelas](#tabelas)

*Como mudar um pedaço de texto do relatório?*

  * Releia a seção [Conteúdo do texto](#conteudo_texto)

*Como sei se minha edição no código deu certo?*

  * Releia a seção [Como testar as alterações?](#testar_alteracoes)

*Estou com problemas com os pacotes do R, como resolver?*

  * Releia a seção [Ambiente do RStudio](#ambiente_rstudio)

# Autores

---

O aplicativo foi desenvolvido pelo BBMP da FGV IBRE. Trabalharam nesse projeto:

  * Gustavo Lôpo Andrade
  * Fellipe Gomes
  * Luiz Fernando Passos
  
*Li tudo e ainda estou inseguro para editar a ferramenta.*

  * Leia novamente, pesquise sua dúvida no [Stackoverflow](https://stackoverflow.com/), [deixe sua dúvida para o desenvolvedor do pacote no Github](https://help.github.com/articles/creating-an-issue/), leia as documentações dos pacotes no [help do R](https://www.r-project.org/help.html), pesquise no [Google do R](https://rseek.org/)... Respire fundo e **may the force be with you!**
  
# Glossário

[^SIS]: Sistema de Índices Setoriais: é um local onde são calculados índices. 

[^db]: O termo genérico "banco de dados" diz respeito ao armazenamento de informações de uma forma geral. Geralmente um software que é instalado em um computador (servidor) e tem a função de gerenciar um ou mais bancos de dados.

[^SQL]: A SQL — Structured Query Language, ou linguagem estruturada de consultas — é a linguagem padrão dos chamados Bancos de Dados Relacionais que, por sua vez, são bancos de dados estruturados em forma de colunas e linhas, também chamadas de tuplas, tendo seus dados armazenados em tabelas.

[^input]: O termo é muito utilizado na área da Tecnologia da Informação (TI). Na área da Tecnologia da Informação, existem três fases necessárias para o desenvolvimento de um trabalho: a entrada (INPUT), o processamento e a saída (OUTPUT). A fase de entrada é caracterizada pelo ato de fornecer os dados que o computador irá trabalhar durante o processamento para, finalmente, produzir as informações de saída.
