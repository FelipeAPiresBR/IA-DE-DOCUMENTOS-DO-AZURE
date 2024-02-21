### IA de pesquisa na prática utilizando ferramentas do AZURE🤖

Neste tópico,iremos utilizar as ferramentas do [Azure](https://portal.azure.com/#home) para realizar uma solução de mineração para uma rede de cafés nacionais chamada Fourth Coffee,os exemplos  e o problema proposto a seguir,foram todos retirados da plataforma de documentos da Microsoft,os links e matériais utilizado encontra-se logo ao final do tópico .

#### Recursos do Azure necessários que iremos criar para a implantação final :

* Um recurso do Azure AI Search , que gerenciará a indexação e a consulta.
* Um recurso de serviços de IA do Azure , que fornece serviços de IA para habilidades que sua solução de pesquisa pode usar para enriquecer os dados na fonte de dados com insights gerados por IA.

**OBS**: Os recursos do Azure AI Search e dos serviços Azure AI devem estar no mesmo local!

* Uma conta de armazenamento com contêineres de blobs, que armazenará documentos brutos e outras coleções de tabelas, objetos ou arquivos.

### 1️⃣Crie um recurso no Azure AI Search
Pesquise Azure AI Search e crie um recurso Azure AI Search,clique em **+Criar um recurso** 
![Criar um recurso ai search](https://github.com/FelipeAPiresBR/IA-DE-DOCUMENTOS-DO-AZURE/blob/main/inputs/azure%20ai%20search%20criar.png?raw=true)
#### Coloque as seguintes configurações :

* Assinatura : sua assinatura do Azure .
* Grupo de recursos : Selecione ou crie um grupo de recursos com um nome de sua preferência .
* Nome do serviço : um nome exclusivo  .
* Localização : Escolha East US,devido os custos serem menores que no brasil .
* Nível de preços : Básico

![Config dos recursos](https://github.com/FelipeAPiresBR/IA-DE-DOCUMENTOS-DO-AZURE/blob/main/inputs/alternar%20tipo%20de%20pre%C3%A7o.png?raw=true)
 * Em seguida selecione **Revisar + Criar** , aguarde a validação e depois clique novamente em **Criar** ,esse serviço pode demorar de **05 até 10** minutos,aguarde aparecer a menssagem :     
 ✅ **A implantação foi concluida**
 * Agora iremos voltar para tela inicial do Azure e criar um recurso de IA do Azure , Sua solução de pesquisa usará esse recurso para aumentar e enriquecer os dados no armazenamento gerados por IA .

 #### 2️⃣ Na tela inicial,selecione : +Criar um recurso 

  Logo em seguida,selecione **IA + Machine Learning** ,Serviços cognitivos e clique em criar .
  ![Serviços cognitivos](https://github.com/FelipeAPiresBR/IA-DE-DOCUMENTOS-DO-AZURE/blob/main/inputs/servi%C3%A7os%20cognitivos%20doc.png?raw=true)
  #### Coloque as seguintes configurações : 
* Assinatura : sua assinatura do Azure .
* Grupo de recursos : O mesmo grupo de recursos que seu recurso do Azure AI Search feito anteriormente .
* Região : o mesmo local do recurso do Azure AI Search que colocamos no anterior.
* Nome : Um nome exclusivo de sua preferência .
* Nível de preços : Padrão S0
* Ao marcar esta caixa, confirmo que li e compreendi todos os termos abaixo : Selecionado
![Nome dos recursos ai search config.png](https://github.com/FelipeAPiresBR/IA-DE-DOCUMENTOS-DO-AZURE/blob/main/inputs/Nome%20dos%20recursos%20ai%20search%20config.png?raw=true)
* Clique em **Examinar + Criar** aguarde a validação .
* Depois da validação,clique em **Criar** ,aguarde de **05 até 10** minutos até aparecer a menssagem : 
 ✅ **A implantação foi concluida** 

#### 3️⃣Agora iremos criar uma conta de armazenamento .
* Retorne à página inicial do portal do Azure e pesquise  **Contas de armazenamento** ou **Storage accounts**
* Selecione  **+ Criar** 
#### Coloque as seguintes configurações :
* Assinatura : sua assinatura do Azure .
* Grupo de recursos : O mesmo grupo de recursos que os recursos do **Azure AI Search** e dos serviços **Azure AI** colocados anteriormente .
* Nome da conta de armazenamento : um nome exclusivo a seu critério,lembrando que tem que ser um nome que ainda não exista .
* Localização : Escolha a mesma localização para economizar  .
* Desempenho : Padrão 
* Redundância : armazenamento com redundância local (LRS)



![config storage accounts.png](https://github.com/FelipeAPiresBR/IA-DE-DOCUMENTOS-DO-AZURE/blob/main/inputs/config%20storage%20accounts.png?raw=true)
*  Clique em **Examinar** depois **Criar**,aguarde de **05 até 10** minutos até aparecer a menssagem : 
 ✅ **A implantação foi concluida** 

* Volte a tela incial do **Azure**,Pesquise  **Contas de armazenamento** ou **Storage accounts**
* Selecione a conta de armazenamento que acabamos de criar .
![Contas de armazenamento selecionada.png
](https://github.com/FelipeAPiresBR/IA-DE-DOCUMENTOS-DO-AZURE/blob/main/inputs/Contas%20de%20armazenamento%20selecionada.png?raw=true)
* Clique em cima dela para abrir o menu,procure Configurações do lado esquerdo,Selecione **Configuração** :
* Procure : Permitir acesso anônimo ao Blob :
* Marque **Habilitado** depois **Salvar**
![Config blob.png
](https://github.com/FelipeAPiresBR/IA-DE-DOCUMENTOS-DO-AZURE/blob/main/inputs/Config%20blob.png?raw=true)

#### 4️⃣ Carregar documentos para o armazenamento do Azure
* No painel do menu esquerdo,selecione **Containers** depois  **+Contêiner**  para criar um novo e adicione as seguintes configurações : 
* Nome : coffeereviews
* Nível de acesso público : Contêiner (acesso de leitura anônimo para containers e blobs)
* Avançado : sem alterações .
* Clique em Criar e aguarde seu Contêiner ser criado .

![Conteiner](https://github.com/FelipeAPiresBR/IA-DE-DOCUMENTOS-DO-AZURE/blob/main/inputs/config%20containers.png?raw=true)

* Em uma nova guia do navegador, baixe as **avaliações de café compactadas** em https://aka.ms/mslearn-coffee-reviewse extraia os arquivos para a pasta de avaliações .
* No portal do Azure, selecione o contêiner de avaliações de café que acabamos de criar .   
* Clique em **Carregar**
![Container bob](https://github.com/FelipeAPiresBR/IA-DE-DOCUMENTOS-DO-AZURE/blob/main/inputs/upload%20arquivo%20bob.png?raw=true
)
Depois que o upload for concluído, você poderá fechar o painel Upload blob . Seus documentos estão agora em seu contêiner de armazenamento de avaliações de café .

![Config Caf](https://github.com/FelipeAPiresBR/IA-DE-DOCUMENTOS-DO-AZURE/blob/main/inputs/review%20docs.png?raw=true)

### 5️⃣ Indexar os documentos
* Depois de armazenar os documentos, você poderá usar o Azure AI Search para extrair insights dos documentos. O portal do Azure fornece um assistente de importação de dados . Com este assistente, você pode criar automaticamente um índice e um indexador para fontes de dados suportadas. Você usará o assistente para criar um índice e importar seus documentos de pesquisa do armazenamento para o índice do Azure AI Search.
* No portal do **Azure**, navegue até o recurso **Azure AI Search**. Na página Visão geral , selecione o seu recurso que criamos e depois  **Importar dados** .
 Importe os dados e coloque as seguintes configurações :
* Fonte de dados : Armazenamento de Blobs do Azure
* Nome da fonte de dados : coffee-customer-data
* Dados a extrair : Conteúdo e metadados
* Modo de análise : Padrão
* Cadeia de conexão : **Selecione** :  Escolha uma conexão existente . **Selecione** sua conta de armazenamento, **selecione** o contêiner de avaliações de café e clique em Selecionar .
Autenticação de identidade gerenciada : Nenhuma
* Nome do contêiner : esta configuração é preenchida automaticamente depois que você escolhe uma conexão existente .
* Pasta Blob : deixe em branco .
* Descrição : Avaliações sobre Fourth Coffee Shops.
![Config avaliação coff bob](https://github.com/FelipeAPiresBR/IA-DE-DOCUMENTOS-DO-AZURE/blob/main/inputs/coff%20bobs%20config.png?raw=true)

#### 6️⃣ Selecione Próximo: Adicionar habilidades cognitivas (opcional) .
* Na secção Anexar Serviços Cognitivos , selecione o seu recurso de serviços Azure AI.

* Na seção Adicionar enriquecimentos : Altere o nome da qualificação para coffee-skillset .
* Marque a caixa de seleção **Habilitar OCR** e mesclar todo o texto no campo merged_content .
* **OBS:** É importante selecionar **Habilitar OCR** para ver todas as opções de campo enriquecido.

* Certifique-se de que o campo Dados de origem esteja configurado como merged_content .
* Altere o nível de granularidade de enriquecimento para Páginas (blocos de 5.000 caracteres) .
* Não selecione Habilitar enriquecimento incremental
### Selecione os seguintes campos enriquecidos:

* Habilidade Cognitiva	Parâmetro	Nome do campo
* Extraia nomes de locais	/ 	Localizações
* Extraia frases-chave	 	frases chave
* Detectar sentimento	 	sentimento
* Gerar tags de imagens	 	imagemTags
* Gere legendas de imagens	 	legenda da imagem
![Campos de img](https://github.com/FelipeAPiresBR/IA-DE-DOCUMENTOS-DO-AZURE/blob/main/inputs/imagem_2024-02-21_190835187.png?raw=true)

#### Em Salvar enriquecimentos em um armazenamento de conhecimento , selecione:
* Projeções de imagem
* Documentos
* Páginas
* Frases chave
* Entidades
* Detalhes da imagem
* Referências de imagem
* Selecione projeções de blob do Azure: Documento . Uma configuração para o nome do contêiner com as exibições preenchidas automaticamente do contêiner de armazenamento de conhecimento . 
* Não altere o nome do contêiner.
![Coff container](https://github.com/FelipeAPiresBR/IA-DE-DOCUMENTOS-DO-AZURE/blob/main/inputs/Screenshot_6.png?raw=true)
* Selecione **Próximo: Personalizar índice de destino**
* Altere o nome do índice para coffee-index .
* Certifique-se de que a chave esteja configurada como metadata_storage_path . Deixe o nome do sugeridor em branco e o modo de pesquisa preenchido automaticamente.
* Revise as configurações padrão dos campos de índice.  
* Selecione filtrável para todos os campos que já estão selecionados por padrão.

![Filtravel](https://github.com/FelipeAPiresBR/IA-DE-DOCUMENTOS-DO-AZURE/blob/main/inputs/filtravel.png?raw=true)

* Selecione Próximo: Criar um indexador .
* Altere o nome do indexador para coffee-indexer .
* Deixe a programação definida como Once .  
* Expanda as opções avançadas . Certifique-se de que a opção **Base-64 Encode Keys** esteja selecionada, pois as chaves de codificação podem tornar o índice mais eficiente.
* Selecione Enviar para criar a fonte de dados, o conjunto de habilidades, o índice e o indexador. O indexador é executado automaticamente e executa o pipeline de indexação, que:
* Extrai os campos de metadados do documento e o conteúdo da fonte de dados.
* Executa o conjunto de habilidades cognitivas para gerar campos mais enriquecidos.
* Mapeia os campos extraídos para o índice.
#### Agora ,Volte à página de recursos do Azure AI Search. No painel esquerdo, em Gerenciamento de pesquisa , selecione Indexadores . Selecione o indexador de café recém-criado . Espere um minuto e selecione ↻ Atualize até que o Status indique sucesso.

![Legenda](https://github.com/FelipeAPiresBR/IA-DE-DOCUMENTOS-DO-AZURE/blob/main/inputs/Screenshot_7.png?raw=true)

* Selecione o nome do indexador para ver mais detalhes, **Pronto,agora você já pode realizar suas próprias consultas** . 

# Epílogo 
 Chegamos ao fim de mais um Resumão,simples,mas eficiente, de como Criar uma IA capaz de realizar uma solução de mineração de documentos,esse tutorial foi dedicado a pessoas que ainda não conhecem a ferramenta e estão em busca de algo prático.

 Em breve será disponibilizado 	[novos artigos](https://github.com/FelipeAPiresBR/ReconhecimentoFacial_Metamorfose-De-Imagens-Em-Dados.git) sobre IA e criação dos mais variados tipos para te auxiliar no dia-a-dia.

 O máterial de apoio que utilizei para realizar esse artigo se encontra aqui :  
https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/11-ai-search.html#query-the-index


#### Qualquer dúvida ou Sugestão e muito bem vinda!🔁








