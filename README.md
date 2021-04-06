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

## 3. Família de Normas ISO 27000 – Padrões de Segurança da Informação

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

4. Ferramentas e Aspectos de Segurança 
- Oracle Database 
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
