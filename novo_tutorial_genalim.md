# Tutorial do Índice de Gêneros Alimentícios (GENALIM)

FGV - Núcleo de Índices Privados

---

# Introdução 

---


  

# Como usar a ferramenta? (para **usuários**)

---

## FGV dados

Objetivo: obter os arquivos de input "ipa" e "ipcrj". Assista ao gif:

![](src/img_readme/FGVDados.gif)

## Manipulação inicial dos dados obtidos  

Exemplo de como são estes arquivos e como manipulá-los:

![](src/img_readme/rbind1.gif)

*Exemplo de manipulação de: ALIATA, ALIVAR, ALIPRAT*

![](src/img_readme/rbind2.gif)

*Exemplo de manipulação de: IPA, IPCRJ*

Portanto, para ambos os casos, cada nova base de dados obtida por mês deverá ser acrescentada ao final da última linha da base csv que contém os resultados dos meses passados.

## Relatório no R 

O primeiro passo é abrir o arquivo "Global.R" na pasta do aplicativo "appgenalim". 
Depois disso, o RStudio será inicializado. Basta clicar em "Run App", conforme o exemplo abaixo:

![](src/img_readme/R.gif)

Para dar início à produção, abra o aplicativo, insira a **data** que constará na carta e insira o **número do relatório** que aparecerá na capa do pdf (note que essas instruções também são apresentadas no corpo do aplicativo).

Como a conexão direta com o banco de dados ainda não está disponível, será necessário **fazer o input manual**. São 5 arquivos de entrada no total - 3 arquivos exportados do SIS e 2 séries do IGP - veja:
 
  * ALIPRAT (SIS)
  * ALIATA (SIS)
  * ALIVAR (SIS)
  * IPA (nº da série: 1427032)
  * IPC-RJ (nº da série: 1406445)
  
Os nomes destes arquivos devem estar nomeados exatamente como (letras minúsculas, sem espaço e em formato `csv`):

  - `aliata.csv`
  - `aliprat.csv`
  - `alivar.csv`
  - `ipa.csv`
  - `ipcrj.csv`
  
Insira os dados (inputs) da seguinte forma:
  

![](src/img_readme/processar_local.gif)

Pressionar o botão `Gerar Relatório` para que a rotina de análises seja executada.

Quando a tarefa terminar a seguinte mensagem será exibida:

![](src/img_readme/sucesso.gif)

Após a mensagem de que todos os objetos do relatório foram criados com sucesso, basta clicar em `Download` e fazer o download do relatório:

![](src/img_readme/download.gif)

## Produto final

Ao final do processo, o relatório disponível para a entrega para o cliente terá a seguinte forma:

![](src/img_readme/relatorio_final.gif)


# Glossário

[^SIS]: Sistema de Índices Setoriais: é um local onde são calculados índices. 

[^db]: O termo genérico "banco de dados" diz respeito ao armazenamento de informações de uma forma geral. Geralmente um software que é instalado em um computador (servidor) e tem a função de gerenciar um ou mais bancos de dados.

[^SQL]: A SQL — Structured Query Language, ou linguagem estruturada de consultas — é a linguagem padrão dos chamados Bancos de Dados Relacionais que, por sua vez, são bancos de dados estruturados em forma de colunas e linhas, também chamadas de tuplas, tendo seus dados armazenados em tabelas.

[^input]: O termo é muito utilizado na área da Tecnologia da Informação (TI). Na área da Tecnologia da Informação, existem três fases necessárias para o desenvolvimento de um trabalho: a entrada (INPUT), o processamento e a saída (OUTPUT). A fase de entrada é caracterizada pelo ato de fornecer os dados que o computador irá trabalhar durante o processamento para, finalmente, produzir as informações de saída.