# Batch-Input-ABAP-SAP

### Batch Input Básico

```abap

REPORT ZPROG_BATCH_TESTE_02.

SELECTION-SCREEN BEGIN OF BLOCK b1 WITH FRAME TITLE TEXT-001.
  PARAMETERS: p_cat TYPE c LENGTH 20.
SELECTION-SCREEN END OF BLOCK b1.

DATA wa_bdcdata TYPE bdcdata. "WORKAREA
DATA it_bdcdata TYPE TABLE OF bdcdata.
DATA opt TYPE ctu_params. "ESTRUTURA INTERNA

CLEAR wa_bdcdata. "LAYOUT INICIAL DA TELA
wa_bdcdata-program = 'SAPLSD_ENTRY'. "NOME DO PROGRAMA CORRESPONDENTE A TRANSAÇÃO
wa_bdcdata-dynpro = '1000'. "NÚEMRO DA TELA CORRESPONDENTE A TRANSAÇÃO
wa_bdcdata-dynbegin = 'X'. "APLICAÇÃO DIZENDO QUE EU QUERO EDITAR ESSA TELA
APPEND wa_bdcdata TO it_bdcdata.

CLEAR wa_bdcdata."CATEGORIA DE DADOS
wa_bdcdata-fnam = 'RSRD1-DDTYPE'. "NOME DO CAMPO DATA TYPE SE11
wa_bdcdata-fval = 'X'. "VALOR DO CAMPO , X POR CONTA DA MARCAÇÃO DO RADIO BUTTON
APPEND wa_bdcdata TO it_bdcdata.

CLEAR wa_bdcdata."PUXANDO O PARAMETER PARA O CAMPO
wa_bdcdata-fnam = 'RSRD1-DDTYPE_VAL'. "NOME DO CAMPO ESCRITO SE11
wa_bdcdata-fval = p_cat. "VALOR DO CAMPO, BUSCA A TRANSAÇÃO CORRESPONDENTE AO NOME
APPEND wa_bdcdata TO it_bdcdata.

CLEAR wa_bdcdata."EXIBIR A TELA
wa_bdcdata-fnam = 'BDC_OKCODE'. "SIGNIFICA ENTER OU CLIQUE DE SELEÇÃO
wa_bdcdata-fval = 'WB_DISPLAY'. "NOME DO BOTÃO DE DISPLAY DA TELA SE11
APPEND wa_bdcdata TO it_bdcdata.

opt-dismode = 'E'. "SÓ MOSTRA O POP-UP DE CONFIRMAÇÃO CASO DER ERRO
"OUTROS: A = SEMPRE / N = NUNCA

CALL TRANSACTION 'SE11' USING it_bdcdata OPTIONS FROM opt. "CHAMAR A TRANSAÇÃO ATRAVÉS DA VARIÁVEL E USANDO A CONFIGURAÇÃO DO POP-UP

```
