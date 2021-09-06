-   Introdução:

``` r

1) Antes da filtragem (antes de fazermos rawdata = FALSE): 

   Tudo antes de '## Download ##' é para rawdata = TRUE

   A partir de '## Download ##' temos a criacao do dataframe 'dat' que é uma mega tabela com todos os dados da comex.

   Se voce quiser os dados brutos (rawdata = TRUE), entao a funcao load_br_trade() vai te retornar exatamente esse 'dat' original.

2) Entretanto, se voce quiser os dados filtrados, serão feitas várias alterações nesse 'dat'.

   A partir do '## Load dictionary ##' inicia-se a configuração para (rawdata = FALSE)
```

-   O que a filtragem faz ?

``` r

A parte do (rawdata = FALSE), ou seja, nosso tratamento da base, começa a partir
de '# Load dictionary #'. Indo para o final do código, você verá que há a funcao
load_trade_dic(), que baixa o dicionário completo do comex, que tem todos os nomes 
em portugues, ingles e espanhol. Na tabela, há quatro classificações (correspondentes a 'hs', 
'cuci', 'isic', 'cgce') de animais: co_sh6, co_sh4, co_sh2, co_ncm_secrom. Para cada uma
dessas classificações tem-se vários grupos de animais que são diferenciados por identificadores 
nessas colunas de classificação. Por fim, cada classificação tem uma versão em 
portugues, ingles e espanhol.

# O objetivo da nossa filtragem é:

1)   Filtrar dados da comex para produtor ou para municipio, conforme o usuário pedir no dataset.

2)   Filtrar o dicionário para a classificação desejada E com a coluna associada em ingles OU portugues, dependendo do que o usuario pedir. Vou pegar 2 colunas no fim das contas.
     Ex: se havia escolhido 'hs', entao vou selecionar do dicionario a coluna 'co_sh4', que possui os identificadores de cada categoria de animais segundo a classificacao 'hs', e,
         por fim, selecionarei também a coluna com os nomes de cada identificador na língua pedida pelo usuário.

3)   Alterar (filtrar) o dataframe 'dat' (que contem as informacoes da comex) a partir do dicionário filtrado: 
obs: tudo abaixo considera que havíamos selecionado no passo (2) as colunas de classificacao 'hs', ou seja,'co_sh4'
3.1) Criar a conexao com o dicionario filtrado. Assim, se uma linha da 'dat' nao for associada a um dos identificadores da coluna da classificação 'hs', entao a linha será excluída: left_join(dic,by='co_sh4')
3.2) Ajeitar os identificadores, pois 0 à esquerda deve constar no identificador. Configurar para ter 4 espaços e se o identificador tiver menos que isso, as casas vazias na esquerda (d) devem ser preenchidas com '0': mutate(co_sh4 = formatC(co_sh4, width = 4, format = 'd', flag = '0')
3.3) Por fim, renomear a coluna dos identificadores só pra facilitar:  rename(co_sh4 = sh4)

4) Tradução: Crio um dataframe 'dat_mod' que é o 'dat' modificado
4.1) Se usuario escolheu portugues, entao devo selecionar de 'dat' apenas as colunas em portugues. Alem disso, devo renomear as colunas com nomes mais simples. Por fim, organizo o dataframe por ano, mes,... com a funcao arrange()
4.2) Se usuario escolheu ingles, o processo é analogo a (4.1) mas para ingles.
```

-   Mas afinal, qual a estrutura mais ‘geral’ do codigo usado na
    filtragem da comex?

``` r

1) Usuário escolhe dados por municipio ou produtor: Dentro desses blocões, muita coisa acontece. No fim das contas, eles vao te cuspir um dataframe tratado chamado 'dat_mod'.

   ## Load Dictionary ##' 

   if (param$dataset == "comex_export_mun" | param$dataset == "comex_import_mun") {...}
   if (param$dataset == "comex_export_prod" | param$dataset == "comex_import_prod"){...}
   return(dat_mod)

2) Dentro de cada um desses dois blocoes {...}, iremos filtrar ainda mais. 

2.1) Primeiro, iremos filtrar o DICIONÁRIO 'dic' pela lingua escolhida:
    
     if (param$language == 'pt'){...}
     if (param$language == 'eng'){...}

2.2) Depois, iremos fazer a conexao entre o dicionario FILTRADO e os dados da comex (que estão na variavel 'dat'). No fim, teremos 'dat' filtrado:

     ## Add Variable Name ##
     Usa-se as funções: left_join(), mutate(), rename()
          
2.3) Depois, crio um dataframe 'dat_mod' que é o 'dat' mais bonitinho. Só com colunas em português ou ingles (dependendo do que o usuario quer), com as colunas com nomes mais simples e com as colunas organizadas a partir de anos, meses, ...

      ## Translation ##
      
      if (param$language == 'pt'){
          ...) %>%                      # obs: nesses '...' é que sao selecionadas e renomeadas as colunas em portugues
          dplyr::arrange(...)}

      
      if (param$language == 'eng'){
          ...) %>%                      # obs: nesses '...' é que sao selecionadas e renomeadas as colunas em ingles
          dplyr::arrange(...)}
```