# COBOL - Common Business Language

O COBOL foi criado na época do cartão perfurado. E os cartões tinham que ser lidos pela leitora de cartões para poderem entrar no computador para serem processados e executados. A linguagem COBOL é baseada na lingua inglesa.

Hoje a maioria do trabalho em COBOL é de entender e ajustar sistemas existentes. A atividade de entender milhões de linhas de códigos já é para poucos. Existem bilhões de linhas de códigos de COBOL rodando nas grandes empresas, os sistemas Legados.

Enquanto estes sistemas COBOL atenderem às necessidades de processamento das empresas, não haverá a necessidade de reescrevê-los em outra linguagem, pois cada um deles possui milhões de linhas em COBOL.

Existe uma demanda estável para a atividade de ajustas estes sistemas legados em COBOL. a atividade de manter estes sistemas legados é bastante crítica, necessitando de profissionais competentes.

## Ideia básica do COBOL

A linguagem COBOL é dividida em seções de declarações:

- declaração de variáveis, arquivos e etc;
- e o código executável, chamado de Procedure Division

#### Organização de um programa COBOL

Existem 4 divisões em um programa-fonte de COBOL. Cada divisão deve ser colocada em sua devida ordem:

- IDENTIFICATION DIVISION: identifica o programa;
- ENVIROMENT DIVISION: que indica o computador e a configuração usada no programa;
- DATA DIVISION: que define a natureza e as características dos dados a serem processados;
- PROCEDURE DIVISION: que consiste em uma sequência de comodandos a serem executados;

#### Declarando variáveis em COBOL

As declarações do COBOL tem de estar obrigatoriamente na coluna 8 de cada linha. Se as declarações não começarem na coluna 8, vai dar erro ao gerar o programa.

- As variáveis declaradads como PIC 9 ( ) são numéricas;
- As variáveis declaradas como PIC X ( ) são alfanuméricas;
- O valor entre parênteses "PIC 9 (10)" define o número de dígitos da variável;

Todas as variáveis são globais ao programa, não existindo variáveis locais.

Na coluna 7 pode-se colocar "*" para definir uma linha como um comentário. Não afeta em nada o processamento.

#### Programando o código

Este é um programa de processamento BATCH, que é controlado pelo JCL (*Job Control Language*). O JCL é que fornece os dados de entrada e armazena os dados de saída do programa.

Procura-se posicionar os comandos subordinados a outros mais à direita, de forma a facilitar a identificação de quais comandos estão sendo controlados por outros. Isso se chama *identação*.

​	ID DIVISION.

​	PROGRAM-ID. COBO1.

*ESTE PROGRAMA CALCULA CONFORME A OPERACAO INFORMADA*

​	DATA DIVISION.

​	WOKING STORAGE SECTION.

​	01 N1		PIC 9 (09).

​	01 N2		PIC 9 (09).

​	01 N3		PIC 9 (09).

​	01 OP		PIC X (01).

​	PROCEDURE DIVISION

​			DISPLAY " EDICAO ".

​			DISPLAY " ------- INICIO -------------- ".

​			DISPLAY " PRIMEIRO PROGRAMA COBOL ".

​			ACCEPT N1.

​			ACCEPT OP.

​			ACCEPT N2.

​			IF OP EQUAL " + "

​				COMPUTE N3 = N1 + N2

​				DISPLAY " A SOMA DE " N1 " COM " N2 " = " N3

​			END-IF.

​			IF OP EQUAL " D "

​				DIVIDE N1 BY N2 GIVING N3

​				DISPLAY " A DIVISAO DE " N1 " COM " N2 " =  " N3

​			END-IF.

​			IF OP EQUAL " * "

​				COMPUTE N3 = N1 * N2

​				DISPLAY " A MULTIPLICACAO DE " N1 " COM " N2 " = " N3

​			END-IF.

​			IF OP EQUAL " - "

​				COMPUTE N3 = N1 - N2

​				DISPLAY " A SUBTRACAO DE " N1 " COM " N2 " = " N3

​			END-IF.

​			DISPLAY " -------------- FIM ---------------- ".

​			STOP RUN.

​	END PROGRAM COBO1.

O TSO (*Time Sharing Option*) é responsável pela interação entre SIstema e o Operador. Possibilita checar as transações e permite a inserção de comandos no terminal para alocar arquivos e rodar programas. Ele funciona com base no ISPF que provê a interface baseada em menus e o acesso as aplicações do sistema.

O ISPF é uma **aplicação do TSO para usuários de terminais das famílias 3270** (*ou superiores, assim como para VM*) que permitia ao usuário realizar as mesmas tarefas que poderiam ser executadas através da linha de comando do TSO, porém em uma interface orientada a menus e campos, e com um editor em tela cheia e navegador de arquivos.

O editor do TSO possui uma régua para facilitar a identificação das colunas. Basta digitar COLS na linha de command durante a edição que a régua surge. 

Dentro do editor do TSO, se o Scroll for CSR a paginação será em função da posição do cursor. Desta forma, com Scroll = CSR ao acionar o F8 o editor coloca a linha onde estava o cursos como primeira linha visível da tela.

Na **PROCEDURE DIVISION** os comandos de execução começam na coluna 12 em diante.

O comando **DISPLAY** escreve strings ou conteúdo de variáveis no dispositivo de saída. 

**ACCEPT** é um comando que lê dados do dispositivo de entrada e coloca a informação na variável que está à direita. 

O comando **IF** controla a execução dos comandos do **IF** até o **END-IF**, que são considerados comandos compostos. Estes comandos serão executados somente se a condição do **IF** for verdadeira. Os comandos subordinados ao **IF** não possuem ponto, pois o ponto finalizaria o comando de controle. Neste caso somente o **END-IF** possui o ponto finalizador de comando.

**COMPUTE** é um comando que executa operações aritméticas e coloca o resultado na variável informada.

O comando **DIVIDE** efetua a divisão entre dois valores ou variáveis numéricas, colocando o resultado na variável depois do **GIVING**. Caso seja necessário obter o resto da divisão, bastaria acrescentar a palavra **REMAINING** e depois fornecer uma variável numérica para receber o resto da divisão.

**STOP RUN** é um comando para parar o processamento do programa, devolvendo o controle ao JCL que o chamou. 

O **END** apenas informa que o texto do programa acabou, mas não finaliza o processamento do programa.

Exemplo com outro programa:

​	ID DIVISION.

​	PROGRAM-ID. COBO2

​	ENVIROMENT DIVISION.

​	INPUT-OUTPUT SECTION.

​	FILE-CONTROL.

​						SELECT CEPS ASSIGN REG-CEP

​						ORGANIZATION IS SEQUENTIAL.

​	DATA DIVISION.

​	FILE SECTION.

​	FD CEPS

​	DATA RECORD IS REG-CEP.

​	01 REG-CEP.

​				10 COD-CEP			PIC X (08).

​				10 TIPO					PIC X (03).

​				10 LOGRADOURO  PIC X (40).

​				10 BAIRRO			   PIC X (29).

​	WORKING-STORAGE SECTION.

​	01 NOME-BAIRRO 			 PIC X (29) VALUE SPACES.

​	01 WS-FIM 						  PIC X (1) VALUE 'N'.

​	PROCEDURE DIVISION.

​				ACCEPT NOME-BAIRRO.

​				OPEN INPUT CEPS.

​				DISPLAY " BUSCANDO DADOS DO BAIRRO: " NOME-BAIRRO.

​				READ CEPS AT END MOVEE 'S' TO WS-FIM.

​				PERFORM PROCESS-INIC THRU PROCESS-FIM UNTIL WS-FIM = 'S'.

​				CLOSE CEPS.

​				STOP RUN.

​				PROCESS-INIC.

​							IF (BAIRRO IS EQUAL NOME-BAIRRO)

​									DISPLAY " CEP: " COD-CEP

​									DISPLAY " TIPO: " TIPO

​									DISPLAY " LOGRADOURO: " LOGRADOURO

​									DISPLAY " BAIRRO: " BAIRRO

​							END-IF.

​							READ CEPS AT END MOVE 'S' TO WS-FIM.

​				PROCESS-FIM.

Os arquivos utilizados no programa COBOL são declarados na **ENVIROMENT DIVISION**, **INPUT-OUTPUT SECTION**, **FILE-CONTROL** pelo comando **SELECT**.

Cada arquivo declaradado é associado a um registro, de forma que esse registro se comporte como buffer do arquivo.

O *READ* no arquivo preenche automaticamente o registro do arquivo com informações.

No exemplo acima, a estrutura de nível 01 de nome REG-CEP é composta dos campos COD-CEP, TIPO, LOGRADOURO E BAIRRO, de nível 10, declarados a seguir.

Depois que o comando READ é executado, a estrutura REG-CEP recebe o registro lido e as variáveis COD-CEP, TIPO, LOGRADOURO E BAIRRO, são preenchidas com as informações do registro lido do arquivo CEP.

No WORKING-STORAGE foram declaradas duas variáveis. NOME-BAIRRO para armazenar o bairro a ser buscado no arquivo e WS-FIM para controlar a situação de encontrar o fim do arquivo e parar o programa.

Os erros que surgem durante o desenvolvimento do programa são resolvidos sem muita pressão e stress. O desenvolvedor deve resolver estes erros apenas com a preocupação de atender a data de entrega do programa pronto.

Quando da erro em produção e este erro impacta as operações da organização, surge uma urgência na correção deste. Nesta situação o desenvolvedor vai entender a importância a todos esses cuidados que tem que ser tomados ao se programar. Uma demora na correção de um erro de produção pode significar um impacto de milhões em uma organização. Como os sistemas possuem milhões de linhas de código, a organização e documentação é absolutamente necessária.





