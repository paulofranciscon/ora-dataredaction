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


