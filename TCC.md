# Segurança em ambiente de banco de dados Oracle em conformidade com a LGPD.

### RESUMO
Este é um resumo do artigo que elaborei e apresentei no meu Trabalho de Conclusão de Curso de Especalização de Engenharia e Administração de Banco de Dados na Unicamp, com o tema "Segurança em ambiente de banco de dados Oracle em conformidade com a LGPD", onde aponto os principais aspectos de segurança da informação das ferramentas da plataforma de banco de dados Oracle e demais técnicas e soluções de gerenciamento e de tratamento dos dados pessoais, contribuintes para o desenvolvimento de Sistemas de Gestão da Segurança Informação, para a blindagem e controle absoluto da informação quanto aos processos de coleta, armazenamento, ciclo de existência da informação e geração de relatórios comprobatórios gerenciais, sob as responsabilidades empresariais e organizacionais, com o foco em atender os princípios impostos das legislações brasileiras sancionadas, a Lei nº 13.709/2018 (LGPD), que regulamenta as atividades de tratamento de dados pessoais e que também complementa e atualiza as regulamentações da Lei nº 12.965/2014 (Marco Civil da Internet), que estabelece vários princípios, garantias, direitos e deveres para a utilização da Internet em nosso país.

## INTRODUÇÃO

### 1. Contexto
A LGPD (Lei Geral de Proteção dos Dados) entrou em 
vigor na sexta-feira, dia 18 de setembro de 2020, o que obriga 
juridicamente as empresas e organizações a seguirem uma série 
de atribuições e responsabilidades no tocante à coleta, 
armazenamento, tratamento e a segurança da informação e 
dados pessoais de seus clientes e colaboradores, onde 
contempla ao proprietário do dado ou informação o direito ao 
consentimento de retenção, impeditivo à divulgação, sigilo na 
forma isolada ao objetivo, tratamento e exclusão destas 
informações quanto à sua decisão. Se desrespeitada e 
infringida, as empresas serão advertidas e até penalizadas, com 
multas que podem chegar até 2% do faturamento, sob o limite 
de até R$ 50 milhões [1]. Em virtude da pandemia do 
coronavírus (Covid-19), a aplicação desta penalidade foi adiada 
para agosto de 2021 decretada pela Lei nº 14.010, criada em 
junho deste ano. [2]
A LGPD será fiscalizada pela ANPD (Autoridade Nacional 
de Proteção de Dados), que é um órgão público da 
administração pública federativa do Brasil. A Lei brasileira foi 
baseada na Lei 2016/679 GDPR (General Data Protection 
Regulation) elaborada pela União Europeia, com os mesmos 
princípios dos direitos e deveres propostos.
Segundo estudo publicado pelo IAPP - International 
Association of Privacy Professionals (2016), a estimativa do 
aquecimento no surgimento de novas vagas no mercado de 
trabalho com a entrada destas novas leis de proteção de dados,
são de 75.000 novos empregos no mundo, dos quais 28.000 
levantados somente para a União Europeia, onde surge a 
crescente demanda e necessidade de contratação de 
profissionais encarregados da segurança da informação, o DPO (Data Protection Officer). [3]
Para assegurar a proteção no ambiente empresarial, 
usualmente os bancos de dados são mantidos e administrados 
através de Sistemas de Gerenciamento de Banco de Dados 
(SGBD), que independentemente do modelo e da plataforma da 
fornecedora, ambos devem oferecer de modo integral o suporte,
segurança, controle de acessos, compartilhamento de dados,
normalização, padronização, backup e recuperação, e 
escalabilidade para a produtividade e disponibilidade.

### 2. Objetivo
O objetivo geral deste trabalho é apresentar as estratégias e 
técnicas gerenciais existentes na plataforma de banco de dados 
Oracle, e direcionar a obtenção da conformidade aos princípios
obrigatórios decretados na LGPD, através de utilização dos 
recursos e ferramentas da plataforma de banco de dados, para o 
gerenciamento dos mecanismos de segurança e tratamento de 
privacidade dos dados pessoais dos clientes e colaboradores da 
organização, serão abordados também as principais normas da 
família ISO/IEC 27000, as normas 27001 e 27002, comumente
exercidas em conjunto, a 27001 é a única norma da família que 
é passível de certificação acreditada, no geral estas normas da 
série 27000, apresentam diretrizes para a implantação, 
gerenciamento, monitoramento, melhoria contínua e revisão 
como boas práticas, para o funcionamento de um Sistema de 
Gestão de Segurança da Informação (SGSI).
O processo de tratamento abordados na Lei, consiste no
mapeamento e nos cuidados para a finalidade e retenção segura 
destes dados na posse da organização, contemplando a
anonimização e criptografia de dados sensíveis e identificáveis, 
controle para o ciclo de vida e exclusão sob o consenso do 
proprietário da informação, monitoramento e rastreamento das 
atividades regulares e de riscos dos ativos, e geração de 
relatórios de auditoria e resguardo jurídico para possíveis 
acompanhamentos e questionamentos de fiscalizações da 
ANPD, [5] que é o órgão federal que vai editar normas e 
fiscalizar procedimentos sobre proteção de dados pessoais.
Como objetivo específico, o estreitamento deste trabalho 
será focado no desenvolvimento do recurso de mascaramento 
de dados (Data Masking), que será apresentada de forma 
concisa e objetiva em uma base de dados fictícia, para a 
proteção de dados sensíveis e confidencias nas formas de dados 
estáticos e dinâmicos.

### 3. Motivação
A motivação para a realização deste trabalho é auxiliar e 
orientar empresas e profissionais da área ao enquadramento das 
exigências da Lei Geral de Proteção de Dados mediante os 
recursos e ferramentas da plataforma Oracle, e precaver dos 
indícios e riscos existentes, fortalecendo as camadas de 
segurança e proteção, orientado dos recursos de monitoria e 
gerenciamento de atividades de banco de dados, criptografia e 
mascaramento dos dados, controle de acessos e atividades, 
relatórios gerenciais para auditoria, sobre o seu principal ativo 
considerado, as informações e dados pessoais de seus clientes e 
colaboradores. 

### 4. Materiais
Este trabalho foi realizado utilizando os seguintes recursos tecnológicos:

  - Notebook Dell Inspiron 15 5000, i7 8th Gen, 8Gb RAM, 1TB HD, OS Win10 Pro 64Bits;
  - VM Linux Oracle 8 - Oracle Database 12c Enterprise Edition Release 12.2.0.1.0 - 64x;
  - Oracle SQL Developer - Versão 19.2.1.247;
  - Oracle Advanced Security;
  - Oracle Data Redaction Pack;
  - Oracle Data Masking and Subsetting Pack.

### 5. Metodologia do Trabalho
Este trabalho foi realizado nas seguintes etapas:
  - Coleta de informações e necessidades de adaptações corporativas;
  - Estudo de conteúdo, normas e legislação brasileira correlacionadas à Segurança da Informação;
  - Estudo das ferramentas de gerenciamento e controle da plataforma Oracle e definição do recurso foco para o trabalho;
  - Modelagem e definição de banco de dados de fonte fictícia;
  - Estudo da documentação da plataforma e desenvolvimento de códigos e scripts ETL (Extract Transform Load), para a criação da tablespace, usuários, permissões, tabela, e para testes das funcionalidades dos recursos na implantação do mascaramento de dados, e visualização em tempo real.
 

## II. REVISÃO DE TECNOLOGIAS E PRÁTICAS
### 1. Lei Geral de Proteção de Dados Pessoais (LGPD)
O processo deu início em 2010 junto aos Ministérios Público 
e Legislativo, através de uma consulta pública sobre o tema que 
abrange a segurança e a proteção dos dados pessoais, resultando 
a propositura do PL 5276/2016, anexado ao PL 4060/2012, 
perante a Câmara dos Deputados. No dia 10 de julho de 2018, 
foi aprovado no plenário do Senado Federal o PLC 53/2018, o 
qual dispõe sobre a proteção de dados pessoais e altera a Lei 
12.965/16 (Marco Civil da Internet), consolidando-se assim 
como a Lei Geral de Proteção de Dados brasileira (LGPD). [7]
A LGPD entrou em vigor em agosto de 2020, e estabelece 
regras, padrões e princípios para as organizações cujo suas 
atividades são exercidas em território nacional, para o formal
tratamento dos dados pessoais sob tal posse, com os principais 
objetivos de regulamentar à segurança e proteção dos direitos 
fundamentais de liberdade e privacidade dos dados 
identificáveis e sensíveis da pessoa natural. Determinando ao 
titular do dado, o direito da gratuidade aos privilégios 
majoritários e especiais de pertinência à sua informação, de seu 
ciclo de existência e armazenamento, da conscientização de uso
e finalidade, ter conhecimento e cobertura de quais foram os 
acessos e para quem estes dados foram compartilhados, e como 
está sendo gerenciada a forma de tratamento e se as medidas 
adotadas para a prevenção da integridade e segurança de seus
dados pessoais estão em conformidade com as normativas de 
Segurança da Informação e da vigência da Lei.
Inspirada na Lei da União Europeia, aprovada em 15 de abril 
de 2016, e após dois anos, sua entrada em vigor ocorreu em 25 
de maio de 2018, o Regulamento Geral de Proteção de Dados 
(GDPR), regulamento (EU) 2016/6791. Neste ano de 2018, 
após o escândalo de utilização indevida de dados de usuários do 
Facebook pela empresa Cambridge Analytica, a pauta passou a 
ocupar destaque na mídia internacional e a preocupar governos 
e empresas em geral. O escândalo levou o FBI a investigar 
possíveis irregularidades na eleição norte-americana, 
demonstrando a importância do tema. No Brasil, o assunto foi 
escolhido como tema para a redação do ENEM, que se focou na 
manipulação de comportamento dos usuários pelos controles de 
dados da Internet. [8]

### 2. Autoridade Nacional de Proteção de Dados (ANPD)
Após ementa de alteração promovida pela Lei n° 13.853 de 
09 de julho de 2019, foi criada a autoridade pública autônoma 
e independente para a supervisão da aplicação de lei. [9]
Declarou Secretaria Geral da Presidência da República por 
meio de uma nota: "A criação da ANPD é um importante passo 
tanto para dar a segurança jurídica necessária aos entes públicos 
e privados que realizam operações de tratamento de dados 
pessoais e que terão que se adequar ao previsto pela LGPD, 
como também para viabilizar transferências internacionais de 
dados que sigam parâmetros adequados de proteção à 
privacidade, o que pode abrir novos mercados para empresas 
brasileiras". [10]

### 3. Família de Normas ISO 27000 – Padrões de Segurança da Informação

Os dados e informações para as organizações em geral são 
consideradas ativos de grande importância para o sucesso e 
sustentação dos negócios, devido ao crescimento em massa 
destes dados e a acessibilidade pública de recursos tecnológicos
conectados globalmente, a preocupação em manter a segurança 
tem sido um assunto preocupante e pautado nas organizações.
As normas ISO 27000, foram desenvolvidas para o dar 
suporte e consistência às organizações, através de uma 
sistemática de boas práticas, na proteção de dados e 
informações, implementando como principal elemento, o 
Sistema de Gestão de Segurança da Informação – SGSI, 
composto por orientações e definições de processos, políticas, 
planejamento, gerenciamento de ativos e tomadas decisórias 
com o objetivo de garantir e assegurar o atendimento dos 
principais pilares e princípios da segurança da informação, a 
confidencialidade, integridade e disponibilidade - CID.
Como requisito a norma 27001 atende uma organização 
visando a implementação e melhora na gestão da segurança da 
informação (SI) atendendo aos princípios do CID e suas 
informações que demandam tanto o contexto da organização 
quanto as inserções de elementos de segurança no ambiente de 
negócios, em relação ao planejamento estratégico, à operação e 
à auditoria. Influenciando na definição dos controles de 
segurança, planejamento e gestão da SI, além dos processos 
executados pela equipe operacional, avaliação do desempenho 
e melhoria contínua da gestão de segurança na organização. 
Análise de documentação do SGSI e seus diferentes elementos 
de implementação e modelos de gestão. 
A norma ISO 27002, são orientações que reúnem boas 
práticas que facilitam a implementação efetiva de todos os 
controles de segurança da informação (SI) requeridos pela
norma ISO 27001, garantindo um nível apropriado de 
segurança nas organizações. 

Estruturada em seções, e itens que tratam da aplicação das 
normas ISO 27000, aplicação das práticas políticas de 
segurança, organização interna, dispositivos móveis, trabalhos
remotos, segurança de recursos humanos, gestão de ativos, 
controles de acessos físico e lógico, criptografia, segurança de 
operações e comunicação, manutenção de sistemas e gestão de 
incidentes e conformidade com as normas e a legislação. [11]

### 4. Ferramentas e Aspectos de Segurança - Oracle Database 
As ferramentas tecnológicas da Oracle dispõem de diversas 
técnicas e camadas de segurança para o monitoramento de 
atividades e avaliações de riscos, proteção no armazenamento
para anonimização e mascaramento dos dados, prevenção de
vazamentos e corrupção, controle e armazenamento seguro de 
chaves criptografadas, criptografia de dados transparente, 
firewall de controle de acessos, auditorias e monitoramento das 
atividades realizadas nos bancos de dados. Com base nos 
princípios da LGPD, a plataforma Oracle dispõe de todos os 
recursos perante os requisitos exigidos abordados pelas Leis
mundiais de proteção de dados.


## III.  DESENVOLVIMENTO

Nesta seção são apresentadas detalhadamente as etapas de desenvolvimento do trabalho, onde serão segmentadas as diferentes formas e tipos acessíveis de mascaramento dos dados sensíveis, onde a principal vantagem é de anonimizar os dados reais de forma dinâmica e direcionada ao usuário, fornecendo e garantindo a segurança da informação destes cadastrados. 
Para a realização dos processos e testes, foi elaborado um dataset fictício na forma randômica e aleatória, totalizando 200 tuplas, as colunas FIRST_NAME e LAST_NAME, são registros aleatórios de nomes Americanos mais comuns, utilizados entre as décadas de 70 e 80, não existem referências físicas dos dados pessoais apresentados, não condizem com nenhum sujeito, faixa salarial da ocupação, endereço de e-mail, situação matrimonial, total de filhos, idade, telefones e número de credencial apresentados.
A funcionalidade de mascaramento em tempo de execução o Oracle Data Redaction, que utilizado através da package DBMS_REDACT, lançada a partir da versão Oracle Database 12c, e faz parte do pacote Advanced Security, com a função de preservar os conteúdos e informações em tempo real ao usuário ou aplicação destinada, no momento de sua execução/exibição, onde sua base real armazenada é preservada e inalterada. [18]

A função compõe seis procedures administrativas:

  -	DBMS_REDACT.ADD_POLICY - Adiciona uma política;
  -	DBMS_REDACT.ALTER_POLICY - Altera as políticas existentes;
  -	DBMS_REDACT.DISABLE_POLICY - Desativa uma política existente;
  -	DBMS_REDACT.DROP_POLICY - Elimina uma política existente;
  -	DBMS_REDACT.ENABLE_POLICY - Habilita uma política existente;
  -	DBMS_REDACT.UPDATE_FULL_REDACTION_VALUES - Altera o valor default de retorno para Full Redaction, este sendo necessário a reinicialização do banco para o efeito.

Os métodos para a proteção das colunas, consistem nos seguintes tipos de mascaramento: 

  - FULL REDACTION - Todo conteúdo da coluna é mascarado, os campos numéricos serão retornados valor zero, e os campos dos tipos caracteres, será retornado um espaço em branco;
  - PARTIAL REDACTION - Apenas uma parte da informação definida é substituída por outros caracteres;
  - REGULAR EXPRESSIONS – Utilização de expressões regulares para identificar cadeias de caracteres, palavras ou padrões de dados para a anonimização da informação;
  - RANDOM REDACTION – Mascaramento randômico e aleatório dos dados, retornando valores diferentes para cada pesquisa efetuada;
  - NO REDACTION – Método de verificação e testes de funcionamento das políticas antes de sua implantação efetiva.

### 1.	Mascaramento completo de dados – Full Redaction 

Para executar o modo de mascaramento Oracle Data Redaction - Full, como boas práticas administrativas e gerenciais, é indicado atribuir a permissão à um usuário de perfil (definições das figuras controladora ou operadora indicadas sob as reponsabilidades na Lei) gestor/supervisor conforme adotadas nas políticas internas de Segurança da Informação da organização. O mascaramento completo dos dados, afetará a visualização de todos os caracteres contidos nas colunas selecionadas, no exemplo, os parâmetros redigidos serão lançados em uma coluna do tipo varchar2.

Permissões necessárias dadas pelo administrador do banco para a execução da package Data Redaction:
SYSBDA> GRANT EXECUTE ON SYS.DBMS_REDACT TO PAULO;

Listando todos os dados reais da tabela ‘TCC_TEST’ como referência e ordenando a saída de forma crescente pela coluna ‘FIRST_NAME’.

``` PAULO> SELECT * FROM TCC_TEST ORDER BY FIRST_NAME ```

![](img/figura7.png)

Figura 7. Resultado parcial da seleção completa da tabela TCC_TEST sem a política de mascaramento.

A estrutura do código a seguir, mostra a função utilizada para a criação da política de mascaramento do Data Redaction, no exemplo os parâmetros, indico o nome do esquema como ‘PAULO’, nome do objeto ‘TCC_TEST’ que é o objeto tabela, nome da coluna a ser mascarada ‘CREDENTIAL’, nomeação da política ‘REDACT_ASSOCIATED’, o tipo da função indicando o parâmetro de mascaramento completo dos dados ‘DBMS_REDACT.FULL’, e a expressão ‘1 = 1’ significa que a redação sempre ocorrerá, estas expressões situacionais podem ser definidas também usando a função ‘SYS_CONTEXT’. 

![](img/figura8.png)
Figura 8. Função para a criação da política de mascaramento completa para a coluna CREDENTIAL.

Logo, em uma sessão iniciada como um usuário criado com privilégios de conexão de sessão e consulta dadas pelo administrador do banco de dados, valido o funcionamento da política de mascaramento full na coluna ‘CREDENTIAL’, note que este campo é do tipo varchar, os campos retornados aparecem somente espaço vazios, caso a coluna seja do tipo number eles apareceriam o numérico zero.

![](img/figura9.png)
Figura 9. Consultando todos os registros da tabela e conferindo o resultado da política na coluna ‘CREDENTIAL’

Na próxima figura, altero a expressão lógica da política para o desmascaramento dos dados da coluna ‘CREDENTIAL’ para o user ‘PAULO’, desta forma a política permanecerá habilitada no banco de dados para os demais usuários, com exceção do usuário ‘PAULO’ que é proprietário do schema e que visualizará todos os dados reais da coluna.

![](img/figura10.png)
Figura 10. Desabilitando a política de mascaramento para um determinado usuário

![](img/figura11.png)
Para excluir uma política de mascaramento existente, utiliza-se o script a seguir, informando corretamente os nomes da política, objeto e schema.
Figura 11. Exclusão da política

### 2. Mascaramento parcial de dados – Partial Redaction
O mascaramento parcial dos dados, se define pela substituição dos dados reais por caracteres especiais, e a liberação apenas de alguns dos dados reais para simples conferência ou confirmação dependo da regra de aplicação ou negócio implementado na organização. No exemplo utilizo a coluna ‘PHONE’ do tipo varchar2 e a anonimização para o campo aplicada até o sexto caractere do registro. Note que os parâmetros utilizados, V corresponde ao caractere ‘*’ e F ao ‘-‘.

![](img/figura12.png)
Figura 12. Adicionando uma nova política parcial de mascaramento de dados

Com a sessão iniciado com um usuário de perfil leitura, executo a query para analisar o funcionamento, selecionando apenas as colunas ‘PHONE’, ‘FIST_NAME’ e ‘LAST_NAME’ para visualizar a funcionalidade da política atribuída na coluna ‘PHONE’.

![](img/figura13.png)
Figura 13. Consultando o estado dos dados mascarados parcialmente da coluna ‘PHONE’

Nesta sessão complemento a política, adicionando a coluna ‘CREDENTIAL’ com a mesma função de máscara, anonimizando os 7 primeiros caracteres deste campo, note que nos parâmetros da função, o V é o caractere que será acoplado por um asterisco, e o F como um hífen separador.

![](img/figura14.png)
Figura 14. Adicionando a coluna ‘CREDENTIAL’ na política de mascaramento parcial


![](img/figura15.png)
Figura 15. Query de consulta dos campos mascarados.

Nesta alteração estou utilizando como parâmetros os valores limites máximos para mascar a coluna ‘SALARY’, desta forma apesar de estar alocado em um tipo de mascaramento parcial, os dados numéricos até 7 dígitos serão mascarados pelo zero.

![](img/figura16.png)
Figura 16. Adicionando a coluna ‘SALARY’ na política.

![](img/figura17.png)
Figura 17. Consulta completa para comparar a coluna ‘SALARY’ na política

### 3.	Mascaramento randômico de dados – Random Redaction

Nesta sessão será apresentada exemplos de definição de uma política de mascaramento de dados do tipo randômico, como recurso de estratégia, estes dados são gerados aleatoriamente cada vez que são consultados e exibidos em uma query de usuário ou aplicação com privilégios de acesso limitado. Aproveitando todo os processos de mascaramento de dados anteriores, feito na política ‘REDACT_ASSOCIATED’, adiciono a coluna ‘OCCUPATION’ no modo randômico, e destinando o usuário proprietário.

![](img/figura18.png)
Figura 18. Script alterando a política existente e adicionando a coluna ‘OCCUPATION’ no modo randômico.

![](img/figura19.png)
Figura 19. Consulta efetuada após a atribuição do recurso randômico na política.

### 4.	Mascaramento de dados baseado em expressões regulares

O mascaramento de dados baseado nas expressões regulares, permite a adoção do mascaramento nos padrões conforme a necessidade de exposição dos dados considerados sensíveis, nesta sessão, agora na coluna ‘EMAIL’, apresento o modelo do tipo de mascaramento do endereço do email e mantenho apenas o domínio.

![](img/figura20.png)
Figura 20. Adicionando o recuso de mascaramento através dos padrões regulares na política.

![](img/figura21.png)
Figura 21. Consultas efetuadas após a atribuição dos recursos de expressões regulares na coluna ‘EMAIL’.

## IV.  RESULTADOS E ANÁLISE

A ideia central deste estudo, é demonstrar os conceitos fundamentais de proteção interna dos dados pessoais sensíveis e/ou identificáveis, armazenados sob a responsabilidade e custódia das organizações públicas ou privadas, com o desenvolvimento focal e conciso no recurso de mascaramento dos dados, cuidados estes que resguardam e protegem a visualização indesejada e não autorizada dos dados e informações consideradas importantes para o sigilo e segurança da informação que consequentemente impacta no potencial da reputação da organização e nos ativos dos negócios, conquistando a conformidade nas Leis globais vigentes de proteção de dados, e sobre a importância da certificação nas normas internacionais, citada a família de normas ISO/IEC 27000.

### 1.	Políticas Ativas
A visualização das políticas ativas tem como objetivo a auditoria casual para a checagem e listagem rápida dos acessos e das funções ativas destinadas, que poderá auxiliar no gerenciamento e planejamento de definição das formas de mascaramento dos dados e seus permissionamentos dos acessos das aplicações e usuários. Note que o resultado do script abaixo, corresponde a política nomeada como ‘redact_associated’, criada nos processos anteriores apresentados no capítulo de desenvolvimento, onde seleciono as colunas necessárias para apreciação da atividade da função de mascaramento, visualizada na tabela ‘redaction_policies’ para listagem dos parâmetros e referências.

![](img/figura22.png)
Figura 22. Script para a verificação das políticas existentes 

O script na sequência, permite a visualização das colunas ativas, os parâmetros e o tipo da função de mascaramento ativo no objeto correspondente. 

![](img/figura23.png)
Figura 23. Script para a verificação das colunas habilitadas

## V.  CONCLUSÃO

  O trabalho realizado permite avaliar a importância da usabilidade do serviço de mascaramento dos dados, recurso este que complementa e auxilia nas estratégias e formas de proteção necessárias para manter a anonimização e proteção dos dados armazenados e em percurso, a importância também deve ser constantemente periodizada nas formas de realizações frequentes de auditorias internas planejadas e surpresas, e no monitoramentos da atividade gerais, acessos e permissões dos sistemas e usuários, conceituando e assegurando o atendimento ao sigilo das informações, e formulações transparente explícita do objetivo de uso dos dados para apreciação e consenso do cliente. Complementando e ressaltando a conclusão, somente o uso do recurso de mascaramento de dados apresentado neste, não é o suficiente para a total garantia da segurança da informação e dos dados, evidentemente não atenderá por integral os princípios exigidos pela Lei Geral de Proteção de Dados. O assunto é extenso e deverá ser rigorosamente analisado, levantando todas as questões de segurança para a implantação ou readequação de um Sistema de Gestão de Segurança da Informação, abordados nas normas da família ISO/IEC 27000.

### 1.	Dificuldade Encontradas
Uma das principais dificuldades encontradas foi nas tentativas de reprodução do trabalho em ambiente com infraestrutura necessária na OCI (Oracle Cloud Infraestruct) de forma gratuita em contas temporárias para testes, onde existem limitações dos recursos e serviços Always Free da plataforma, para o desenvolvimento e transposição do recurso de mascaramento dos dados, contudo, com as limitações expostas de recursos de hardware e licenciamentos, o trabalho foi induzido à produção on-promises, utilizando recursos locais na versão Oracle 12c instalada, que condizentemente as formas de ativação e as lógicas de programação dos recursos de mascaramento, são equivalentes, executadas por back-end pelas ferramentas em Cloud, que na plataforma são visualmente apresentáveis por interface gráfica para dinamicidade do gerenciamento e facilidades de visualização dos recursos e ativos.

### 2.	Aplicabilidade do Trabalho

O trabalho possui aplicabilidade ampla aos diversos processos e fases de planejamento para o desenvolvimento inicial, e na gestão de um banco de dados existente e em ambientes de produção, direcionado para o gestor ou mantenedor responsável pelo banco de dados e também da segurança da informação nas organizações, com o propósito de evolução e da busca de maturidade nos processos para o gerenciamento responsável, boas práticas e controle em sistemas gestor de segurança da informação, mediante uma visão geral abordada da LGPD, o tema exposto é também voltado para o perfil de profissional iniciante na carreira e nos estudos para obtenção do conhecimento, contribuinte no enriquecimento das pesquisas.

## VI.  BIBLIOGRAFIA

[1] Lei Geral de Proteção de Dados Pessoais (LGPD). LEI Nº 13.709, DE 14 DE AGOSTO DE 2018. Disponível em: <http://www.planalto.gov.br/ccivil_03/_Ato2015-2018/2018/Lei/L13709.htm>. Acesso em: ago. 2020.

[2] DIARIO OFICIAL DA UNIÃO. LEI Nº 14.010, DE 10 DE JUNHO DE 2020. Disponível em: <https://www.in.gov.br/en/web/dou/-/lei-n-14.010-de-10-de-junho-de-2020-261279456>. Acesso em: set. 2020.

[3] HEIMES, Rita; PFEIFLE, SAM. Study: GDPR’s global reach to require at least 75,000 DPOs worldwide. 2016. Disponível em: <https://iapp.org/news/a/study-gdprs-global-reach-to-require-at-least-75000-dpos-worldwide/#>. Acesso em: set, 2020.

[4] Oracle Database Security. 2020. Disponível em: <https://www.oracle.com/database/security/>. Acesso em: set, 2020.

[5] Lei que cria Autoridade Nacional de Proteção de Dados é sancionada com vetos. Disponível em: <https://www12.senado.leg.br/noticias/materias/2019/07/09/lei-que-cria-autoridade-nacional-de-protecao-de-dados-e-sancionada-com-vetos>. Acesso em: set. 2020.

[6] CARVALHO, Luiz et al. Desafios de Transparência pela Lei Geral de Proteção de Dados Pessoais. In: Anais do VII Workshop de Transparência em Sistemas. SBC, 2019. p. 21-30.

[7] MONTEIRO, Renato Leite. Lei Geral de Proteção de Dados do Brasil: análise contextual detalhada. 2018. Disponível em: <https://www.jota.info/opiniao-e-analise/colunas/agenda-da-privacidade-e-da-protecao-de-dados/lgpd-analise-detalhada-14072018>. Acesso em: set. 2020.

[8] WILLEMIN, Andrea. A importância do avanço nas leis de proteção de dados. 2019. Disponível em: <https://www.conjur.com.br/2019-jan-28/opiniao-importancia-avanco-leis-protecao-dados>. Acesso em: set. 2020.

[9] LEI Nº 13.853, DE 8 DE JULHO DE 2019. Disponível em: <https://www2.camara.leg.br/legin/fed/lei/2019/lei-13853-8-julho-2019-788785-norma-pl.html>. Acesso em: set. 2020.

[10] Com dois anos de atraso, governo cria estrutura de agência de proteção de dados. 2020. Disponível em: <https://www.conjur.com.br/2020-ago-27/dois-anos-atraso-governo-cria-estrutura-anpd>. Acesso em: set. 2020.	

[11] International Organization for Standardization. Licence Agreement for Publicly Available Standards. Disponível em: <https://standards.iso.org/ittf/PubliclyAvailableStandards/c073906_ISO_IEC_27000_2018_E.zip>. Acesso em: out. 2020.

[12] Oracle Data Safe. 2020. Disponível em: <https://www.oracle.com/database/technologies/security/data-safe.html>. Acesso em: set. 2020.

[13] Oracle Data Safe Technical Architecture. 2020. Disponível em: <https://www.oracle.com/webfolder/technetwork/tutorials/architecture-diagrams/data-safe/v1/index.html>. Acesso em: set. 2020.

[14] Oracle Advanced Security. 2020. Disponível em: <https://www.oracle.com/br/database/technologies/security/advanced-security.html >. Acesso em set. 2020.

[15] Encryption and Redaction with Oracle Advanced Security. 2019. Disponível em: <https://www.oracle.com/a/tech/docs/dbsec/aso/advanced-security-wp-19c.pdf >. Acesso em: set. 2020.

[16] Elmasri, R., Navathe, S. B. (2019) “Sistemas de Banco de Dados”, 7ª edição (versão traduzida), editora Pearson Universidades.

[17] Oracle Database Vault. 2019. Disponível em: <https://www.oracle.com/a/tech/docs/dbsec/dbv/wp-dv-19c.pdf>. Acesso em: set. 2020.

[18] Funcionalidade Data Redaction - Oracle Database 12c. Disponível em: <https://www.oracle.com/br/technical-resources/articles/idm/functionality-data-redaction-12c.html>. Acesso em: out. 2020.

  
