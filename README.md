# Auxílio para comunicação com o Cliq CCEE

A especificação do protocolo de comunicação com o Cliq CCEE usado nesse repositório está disponível em 
[Especificação do XSD_Modulo de Contratos](https://www.ccee.org.br/documents/80415/919484/Especifica%C3%A7%C3%A3o%20do%20XSD_Modulo%20de%20Contratos.doc/9a0ae890-b070-c6d6-32c9-3449af2f8b2f).

No momento da escrita desse documento, a versão do documento é a 5.0 de 28/06/2019.

Esse documento foi adaptado para o formato markdown para facilitar a leitura e a compreensão.

## Isenção de responsabilidade

Esse repositório NÃO é oficial de qualquer entidade pública ou privada! Use o conteúde dessas informações por sua conta e risco.

## Histórico de Versões

| Versão | Data       | Descrição |
|--------|------------|-----------|
| 1.0    | 06/10/2014 | Elaboração Inicial da especificação do arquivo XSD – Módulo de Contratos |
| 2.0    | 27/10/2015 | Alterações das especificações de arquivos XSD para a release 6.0 do Módulo de Contratos |
| 3.0    | 09/10/2017 | Alterações das especificações de arquivos XSD para a release 7.0 do Módulo de Contratos – Inclusão das  Operações – Aplicar Redução Contratual |
| 4.0    | 01/02/2018 | Alterações das especificações de arquivos XSD para a release 8.0 do Módulo de Contratos – Novos tipos de CBR |
| 5.0    | 28/06/2019 | Alterações das especificações de arquivos XSD para a CDT-1129 do Módulo de Contratos – Removido a funcionalidade de validação de registro de contratos, que passou a ser compulsória a partir da validação de todos os montantes médios |

## Introdução

Este documento tem o objetivo de auxiliar os Agentes na construção de aplicações para as criação de arquivos do tipo XML
para importação de criação e edição de contratos no sistema CliqCCEE 7.0.

A CCEE estabeleceu por meio dessa especificação um padrão de arquivo XSD(XML Schema Definition) que são usados para descrever
o "formato/padrão" que um arquivo XML deve seguir, ou seja, ele tem que indicar quais nodes `<node1><subnode1/></node1>`
ele pode conter, quais subnodes e atributos.

## Localização

A localização do gerador de XML em Produção é: \
`CONTEUDO EXCLUSIVO` > `CONTRATOS` > `TIPOS` > `GERADOR XML CONTRATOS - CLIQCCE`.

## Estrutura geral dos elementos

As seções a seguir descrevem cada parâmetro de entrada, com seus respectivos tipos de dados e descrição.

Correções sobre a máscara realizadas no documento original com base na própria especificação foram marcadas com 🩹.

### Contrato CCEAL Firme e CBR

#### Criar contrato CCEAL e CBR - Dados Gerais

| Nome | Tipo | Obrigatório | Tamanho | Máscara | Regra de Preenchimento |
|------|------|-------------|---------|---------|-------------------------|
| Tipo de CCEAL/CBR * | Numérico | Sim | 1 | Não se aplica | Para CCEAL: aceitar somente os valores de `1` a `4`. Firme; Flexível por percentual de consumo; Flexível por percentual de geração; Flexível por prioridade. Para CBR: aceitar somente os valores de `1` a `7`. Chamada Pública; Desverticalização; Mercado Próprio; Supridas e Supridoras; Ant.Lei nº 10.848/2004; Sistema Isolado; Outros CBR; Art. 5º Lei nº 13.182/2015; Art. 10º Lei nº 13.182/2015. Somente para contrato CBR. |
| Tipo de Gravação* | Texto | Sim | 1 | `"R"` ou `"C"` | Aceitar somente os valores - Tipos: "R" – Rascunho, "C" – Concluído |
| Data de Início* | Data | Sim | 13 | `DD/MM/AAAA HH` | Aceitar somente valores maiores ou iguais a `01/01/2000 00`. |
| Data de Fim* | Data | Sim | 13 | `DD/MM/AAAA HH` | Aceitar somente valores maiores ou iguais a `01/01/2000 00`. |
| ID do Comprador* | Numérico | Sim | 5 | Não se aplica | Aceitar somente valores maiores que `0`. |
| ID do Vendedor* | Numérico | Sim | 5 | Não se aplica | Aceitar somente valores maiores que `0`. |
| ID do Submercado de entrega* | Numérico | Sim | 1 | Não se aplica | Aceitar somente os valores de `1` a `4`. `1` - Sudeste; `2` - Sul; `3` - Nordeste e; `4` - Norte |
| Referência | Texto | Não | 30 | Não se aplica | Tamanho Max. 30 caracteres. |
| Direito ao Alívio de Exposição | Numérico | Não | 1 | `0` ou `1` | Aceitar somente os valores `0` – Autoprodução e `1` – Direitos EspeciaisSomente para contrato CCEAL. |
| ID do Submercado de Origem* | Numérico | Sim para contratos de Direitos Especiais | 1 | Não se aplica | Aceitar somente os valores de `1` a `4`. `1` - Sudeste; `2` - Sul; `3` - Nordeste e; `4` - Norte. Somente para contrato CCEAL. |
| Particularidade para Verificação de Lastro | Texto | Não | 1 | `"G"`, `"E"` ou `"D"` | Aceitar somente os valores `G` - Geração Própria; `E` – Exportação; `D` - Lastro de Venda para CCEAR D. Somente para contrato CCEAL. |
| Observação | Texto | Não | 255 | Não se aplica | Tamanho Max. 255 caracteres |

#### Criar contrato CCEAL – Cessão

| Nome | Tipo | Obrigatório | Tamanho | Máscara | Regra de Preenchimento |
|------|------|-------------|---------|---------|-------------------------|
| Contrato de Cessão | Texto | Não | 1 | `"X"` ou `""` |  |
| Número do Contrato Origem | Numérico | Não | 10 | Não se aplica | Aceitar somente valores maiores que `0`. |

#### Criar e editar contrato CCEAL e CBR - Montante Médio

| Nome | Tipo | Obrigatório | Tamanho | Máscara | Regra de Preenchimento |
|------|------|-------------|---------|---------|-------------------------|
| Data de Início do Montante Médio* 🩹 | Data | Sim | 13 | `DD/MM/AAAA HH` | Aceitar somente valores maiores ou iguais a `01/01/2000 00`. Preencher somente até a parcela hora. |
| Data de Fim do Montante Médio* 🩹 | Data | Sim | 13 | `DD/MM/AAAA HH` | Aceitar somente valores maiores ou iguais a `01/01/2000 00`. Preencher somente até a parcela hora. |
| Montante MWmédio* 🩹 | Numérico | Sim | 28,6 | Não se aplica | Aceitar somente valores maiores ou igual que `0`. |
| Validar Montante Médio | Numérico | Não | 1 | `"X"` ou `""` |  |
| Editar contrato CCEAL e CBR - Dados Horários por Patamar |
| Semana* | Numérico | Sim | 1 | Não se aplica | Aceitar somente valores maior ou igual a `1`. Preencher com o número da semana. Ex: `1` para a semana1 e `10` para a semana10 |

#### Editar contrato CCEAL e CBR - Dados Horários por Hora

| Nome | Tipo | Obrigatório | Tamanho | Máscara | Regra de Preenchimento |
|------|------|-------------|---------|---------|-------------------------|
| Mês/Ano* | Numérico | Sim | 7 | `MM/AAAA` | Aceitar somente valores entre 1 e 12 e ano maior que 2000.Preencher com mês e ano. Ex: 01/2014 |
| Dia* | Numérico | Sim | 2 | `DD` | Aceitar somente valores entre 1 e 31. Inserir somente uma vez, em caso de mais de 1 dia. Ex: Dia Hora 01 00010202 0001 |
| Hora Início* | Numérico | Sim | 2 | `HH` | Aceitar somente valores entre `00`e `23`, ou `23*`. Utilizar as horas da seguinte forma: `00`, `01`, `02`, `03`, ... `23`. Usar `23*` para a hora adicional do dia de término do horário de verão |
| MWh* | Numérico | Sim | 28,6 | Não se aplica | Aceitar somente valores maiores ou iguais que `0,000000`. |

#### Editar contrato CCEAL e CBR - Dados Horários Por Patamar

| Nome | Tipo | Obrigatório | Tamanho | Máscara | Regra de Preenchimento |
|------|------|-------------|---------|---------|-------------------------|
| Unidade do Patamar* | Numérico | Sim | 1 | `0` ou `1` | Aceitar somente os valores `0` MWh ou `1` MWmédio. |
| Leve (MWh ou MWmédio) | Numérico | Não | 28,6 ou 28,3 | Não se aplica | Aceitar somente valores maiores ou igual que `0`. Preencher com 3 casas decimais para o tipo Patamar `0` – MWh; Preencher com 6 casas decimais para o tipo `1` – Mwmédio. |
| Médio (MWh ou MWmédio) | Numérico | Não | 28,6 ou 28,3 | Não se aplica | Aceitar somente valores maiores ou igual que `0`. Preencher com 3 casas decimais para o tipo Patamar `0` – MWh; Preencher com 6 casas decimais para o tipo `1` – MWmédio. |
| Pesado (MWh ou MWmédio) | Numérico | Não | 28,6 ou 28,3 | Não se aplica | Aceitar somente valores maiores ou igual que `0`. Preencher com 3 casas decimais para o tipo Patamar `0` – MWh; Preencher com 6 casas decimais para o tipo `1` – MWmédio. |

#### Criar e editar contrato CCEAL e CBR – Modulação

| Nome | Tipo | Obrigatório | Tamanho | Máscara | Regra de Preenchimento |
|------|------|-------------|---------|---------|-------------------------|
| Tipo Modulação | Texto | Não | 1 | `"F"`, `"G"`, `"C"` ou `"M"` | Para CCEAL Firme: Aceita somente os valores listados abaixo: `F` – Flat; `G` – Geração; `C` – Carga ou; `M` – MRE. |
| Montante Mínimo (MWh) | Numérico | Não | 28,3 | Não se aplica |  |
| Montante Máximo (MWh) | Numérico | Não | 28,3 | Não se aplica |  |

#### Criar e editar contrato CCEAL e CBR - Ativo

| Nome | Tipo | Obrigatório | Tamanho | Máscara | Regra de Preenchimento |
|------|------|-------------|---------|---------|-------------------------|
| ID da Parcela do Ativo Para Modulação | Numérico | Não | 9 | Não se aplica | Aceitar somente valores maiores que `0`. Obrigatório caso o tipo da Modulação for `C` - Carga ou `G` - Geração |
| ID da Parcela do Ativo Para Lastro | Numérico | Não | 9 | Não se aplica | Aceitar somente valores maiores que `0`. Somente para contrato CBR. |
| Editar contrato CBR – Ativo |
| Excluir ativo para modulação | Texto | Não | 1 | `"X"` ou `""` | Somente para contrato CBR. |
| Excluir ativo para lastro | Texto | Não | 1 | `"X"`ou `""` | Somente para contrato CBR. |

#### Contrato CCEAL e CBR - Finalizar ou Cancelar

| Nome | Tipo | Obrigatório | Tamanho | Máscara | Regra de Preenchimento |
|------|------|-------------|---------|---------|-------------------------|
| Número do Contrato* | Numérico | Sim | 10 | Não se aplica | Aceitar somente valores maiores que `0`Inserir somente uma vez. |
| Data Finalização Contrato (`DD/MM/AAAA HH`) | Data | Não | 13 | `DD/MM/AAAA HH` | Aceitar somente valores maiores ou iguais a `01/01/2000 00`. Preencher somente até a parcela hora.Não deverá ser preenchido caso o campo "Cancelar Contrato" ou "Validar Cancelamento" for informado. |
| Validar Finalização | Texto | Não | 1 | `"X"`ou `""` | Não deve ser preenchido caso o campo "Cancelar Contrato" for informado. |
| Cancelar Contrato | Texto | Não | 1 | `"X"`ou `""` | Não deve ser preenchido caso o campo "Data Finalização Contrato" ou "Validar Finalização" for informado. |
| Validar Cancelamento | Texto | Não | 1 | `"X"`ou `""` | Não deve ser preenchido caso o campo "Data Finalização Contrato" ou "Validar Finalização" for informado. |

#### Contrato CCEAL e CBR - Validar

| Nome | Tipo | Obrigatório | Tamanho | Máscara | Regra de Preenchimento |
|------|------|-------------|---------|---------|-------------------------|
| Número do Contrato* | Numérico | Sim | 10 | Não se aplica | Aceitar somente valores maiores que `0`. Inserir somente uma vez. |
| Montantes MWmédio |
| Início Vigência do Montante Médio (`DD/MM/AAAA HH`) | Data | Não | 13 | `DD/MM/AAAA HH` | Aceitar somente valores maiores ou iguais a `01/01/2000 00`. Preencher somente até a parcela hora. Inserir somente uma vez em caso de mais de um período. |
| Validar Montante Médio | Campo Texto | Não | 1 | `"X"`ou `""` | Obrigatório se o campo "Início Vigência do Montante Médio" for informado. |

### Contrato CCEAR-Q, Leilão de Ajuste e Proinfa

| Nome | Tipo | Obrigatório | Tamanho | Máscara | Regra de Preenchimento |
|------|------|-------------|---------|---------|-------------------------|
 Número do Contrato* | Numérico | Sim | 10 | Não se aplica | Aceitar somente valores maiores que `0`Inserir somente uma vez. |
| Data Início Vigência * | Data | Sim | 13 | `DD/MM/AAAA HH` | Aceitar somente valores maiores ou iguais a `01/01/2000 00`. |
| Ano* | Numérico | Sim | 4 | `AAAA` | Aceitar somente valores maiores ou iguais a `2000`. Inserir somente uma vez, em caso de mais de 1 ano. |
| Mês* | Numérico | Sim | 2 | `MM` | Aceitar somente valores entre `01` e `12`. |
| Montante Mensal* (MWh) | Numérico | Sim | 28,3 | Não se aplica | Aceitar somente valores maiores ou iguais a 0,000. |
| Validar Sazonalização | Texto | Não | 1 | `"X"`ou `""` |  |
| Validar Modulação | Texto | Não | 1 | `"X"`ou `""` | Somente para contrato Leilão de Ajuste. |
| Dia | Numérico | Não | 2 | `DD` | Aceitar somente valores entre `01` e `31`. Somente para contrato Leilão de Ajuste. |
| Hora | Numérico | Não | 2 | `HH` | Aceitar somente valores entre `01` e `23`, ou `23*`. Somente para contrato Leilão de Ajuste. |
| Dados Horários MWh 🩹 | Numérico | Não | 28,6 | Não se aplica | Aceitar somente valores maiores ou iguais a `0,000000`. Somente para contrato Leilão de Ajuste. |
| Semana | Campo Texto Numérico | Não | 1 | Não se aplica | Aceitar somente valores entre `1` e `6`. Somente para contrato Leilão de Ajuste. |
| Unidade do Patamar | Numérico | Não | 1 | Não se aplica | Aceita somente os valores listados abaixo: `0` – MWh ou `1` – MWmédio. Somente para contrato Leilão de Ajuste. |
| Leve (MWh/ MWmédio) | Numérico | Não | 28,6 ou 28,3 | Não se aplica | Aceitar somente valores maiores ou igual que `0`. Preencher com 3 casas decimais para o tipo Patamar `0` – MWh; Preencher com 6 casas decimais para o tipo `1` – MWmédio. Somente para contrato Leilão de Ajuste. |
| Médio (MWh/ MWmédio) | Numérico | Não | 28,6 ou 28,3 | Não se aplica | Aceitar somente valores maiores ou igual que `0`.Preencher com 3 casas decimais para o tipo Patamar `0` – MWh; Preencher com 6 casas decimais para o tipo `1` – MWmédio. Somente para contrato Leilão de Ajuste. |
| Pesado (MWh/ MWmédio) | Numérico | Não | 28,6 ou 28,3 | Não se aplica | Aceitar somente valores maiores ou igual que `0`. Preencher com 3 casas decimais para o tipo Patamar `0` – MWh; Preencher com 6 casas decimais para o tipo `1` – MWmédio. Somente para contrato Leilão de Ajuste. |

### Contrato CCEAR-Q, CCEEAR-D Redução Contratual

| Nome | Tipo | Obrigatório | Tamanho | Máscara | Regra de Preenchimento |
|------|------|-------------|---------|---------|-------------------------|
| Número do Contrato* | Numérico | Sim | 10 | Não se aplica | Aceitar somente valores maiores que `0`Inserir somente uma vez. |
| Tipo de Redução * | Texto | Sim | 1 | `"T"` ou `"P"` | Aceitar somente valores iguais à `T` (Temporário) ou `P` (Permanente) |
| Início do Período de Redução* | Data | Sim | 7 | `MM/AAAA` | Para o `AAAA` - Aceitar somente valores maiores ou iguais a `2000`. Para o `MM` – Aceitar somente valores entre 1 e 12 |
| Fim do Período de Redução | Data | Não | 7 | `MM/AAAA` | Para o `AAAA` - Aceitar somente valores maiores ou iguais a `2000`. Para o `MM` – Aceitar somente valores entre `01` e `12`. Somente se o tipo de redução for temporária `T` |
| Fator de Redução* 🩹 | Numérico | Sim | 13,12 | Não se aplica | Para redução temporária - Aceitar somente valores maiores que `0` ou menor ou igual a `1`. Para redução permanente – Aceitar somente se o valor maior que `0` e menor que `1` |
| Tipo da Validação* | Numérico | Sim | 1 | `0` ou `1` | Aceitar somente valores iguais à 0 (Redução) ou 1 (Rescisão) |
| Início do Período da Rescisão | Data | Sim | 7 | `MM/AAAA` | Para o `AAAA` - Aceitar somente valores maiores ou iguais a `2000`. Para o `MM` – Aceitar somente valores entre `01` e `12` |
| Tipo Acordo* | Numérico | Sim | 1 | `0` ou `1` | Aceitar somente valores iguais à `0` (Redução) ou `1` (Rescisão) |
| Início do Período da Redução/Rescisão | Data | Sim | 7 | `MM/AAAA` | Para o `AAAA` - Aceitar somente valores maiores ou iguais a `2000`. Para o `MM` – Aceitar somente valores entre `01` e `12` |

## Operações disponíveis

As seções a seguir descrevem as operações disponíveis para cada tipo de contrato.

### Contrato CCEAL Firme

As operações disponíveis para contratos do tipo CCEAL Firme são:

- `1`: Criar contrato com dados gerais e montantes (Rascunho);
- `2`: Criar contrato CCEAL Firme Semanal;
- `3`: Criar contrato CCEAL Firme Mensal;
- `4`: Criar contrato CCEAL Firme Por Período;
- `5`: Criar contrato CCEAL Firme DECLARADO para cada hora;
- `6`: Criar contrato CCEAL Firme DECLARADO por patamar;
- `13`: Editar contrato CCEAL Firme Semanal;
- `14`: Editar contrato CCEAL Firme Mensal;
- `15`: Editar contrato CCEAL Firme Por Período;
- `16`: Editar contrato CCEAL Firme DECLARADO para cada hora;
- `17`: Editar contrato CCEAL Firme DECLARADO por patamar;
- `24`: Validar Montante Médio;
- `25`: Finalizar ou Cancelar Contrato CCEAL.

#### Exemplos de XML para contrato CCEAL Firme

`5`: Criar contrato CCEAL Firme DECLARADO para cada hora

```xml
<ContratosCCEAL tipoGeracao="5" tipoCCEAL="1" sistemaOrigem="Contingencia">
    <Contrato sequencialControle="1" tipoGravação="C" 
        dataDeInicio="01/01/2011 00:00:00" dataDeFim="31/12/2020 23:00:00"
        idComprador="1" idVendedor="2"     idSubMerEntrega="1" referencia="10"
        dirAlivExp="0" idSubMerOrigem="1" partVerLastro="E"
        observação="Anotar o montante e acompanhar" contratoCessao="X"
        idContratoCessao="123">
        <MontanteMédio dataDeInicio=`01/01/2000 00` dataDeFim="31/12/2000 23" 
            validarMontante="X">
            <MontanteMédioContratoCCEALFirme montanteMedio="99999999999999999,999999" />
                <MesAno mesAno="01/2000">
                    <Dia dia="01">
                        <Hora hora="00" montanteHorario="99999999999999999,999" />
                    </Dia>
                </MesAno>
                <AtivoAssociadoModulacao idAtivoAssociadoModulacao="" />
            </MontanteMédio>
    </Contrato>     
</ContratosCCEAL>
```

`13`: Editar contrato CCEAL Firme Semanal

```xml
<ContratosCCEAL tipoGeracao="13" tipoCCEAL="1">
    <Contrato sequencialControle="1" numeroContrato="123" tipoGravação="C">
        <MontanteMédio vigenciaDeInicio=`01/01/2000 00` vigenciaDeFim="31/12/2000 23">
            <semana semana="1" validarMontante="X">
                <MontanteMédioContratoCCEALFirme montanteMedio="99999999999999999,999999" />
                <TipoModulacao tipoModulacao="F"/>
                <LimiteModulacao limiteMinimoModulacao="99999999999999999,999"
                    limiteMaximoModulacao="99999999999999999,999" />
                <AtivoAssociadoModulacao idAtivoAssociadoModulacao="" />
            </semana>
        </MontanteMédio>
    </Contrato>     
</ContratosCCEAL>
```

`24`: Validar Montante Médio

```xml
<ContratosCCEAL tipoGeracao="24">
    <Contrato sequencialControle="1" numeroContrato="123">
        <MontanteMédio vigenciaDeInicio=`01/01/2000 00` validarMontante="X">
    </Contrato>  
</ContratosCCEAL>
```

`25`: Finalizar ou Cancelar Contrato CCEAL

```xml
<ContratosCCEAL tipoGeracao="25">
    <Contrato sequencialControle="1" numeroContrato="123" dataFinalizacao="01/02/2000 00"
        validarFinalizacao="X" cancelarContrato="" validarCancelamento="" />
</ContratosCCEAL>
```

### Contrato CCEAL CBR

As operações disponíveis para contratos do tipo CBR são:

- `1`: Criar contrato com dados gerais (Rascunho);
- `2`: Criar contrato com montante médio semanal;
- `3`: Criar contrato com montante médio mensal;
- `4`: Criar contrato com montante médio por período;
- `5`: Criar contrato DECLARADO por hora;
- `6`: Criar contrato DECLARADO por patamar;
- `7`: Editar contrato com montante médio semanal;
- `8`: Editar contrato com montante médio mensal;
- `9`: Editar contrato com montante médio por período;
- `10`: Editar contrato DECLARADO por hora;
- `11`: Editar contrato DECLARADO por patamar;
- `12`: Finalizar ou Cancelar Contrato CBR;
- `13`: Criar contrato Art 5o da Lei 13.182/2015 mensal;
- `14`: Criar contrato Art 5o da Lei 13.182/2015 horário;
- `15`: Editar contrato Art 5o da Lei 13.182/2015 mensal;
- `16`: Editar contrato Art 5o da Lei 13.182/2015 horário.

#### Exemplo de XML de Contrato CCEAL CBR

`5`: Criar contrato DECLARADO por hora

```xml
<ContratosCBR tipoGeracao="5">
    <Contrato sequencialControle="1" tipoCBR="1" tipoGravação="C" 
        dataDeInicio="01/01/2011 00:00:00" dataDeFim="31/12/2020 23:00:00"
        idComprador="1" idVendedor="2" idSubMerEntrega="1" referencia="10"
        observação="Anotar o montante e acompanhar">
        <AtivoAssociadoLastro idAtivoAssociadoLastro="1" />
        <MontanteMédio dataDeInicio=`01/01/2000 00` dataDeFim="31/12/2000 23" validarMontante="X">
            <MontanteMédioContratoCBR montanteMedio="99999999999999999,999999" />
                <MesAno mesAno="01/2000">
                    <Dia dia="01">
                        <Hora hora="00" montanteHorario="99999999999999999,999" />
                    </Dia>
                </MesAno>
                <AtivoAssociadoModulacao idAtivoAssociadoModulacao="" />
            </MontanteMédio>
    </Contrato>     
</ContratosCBR>
```

`7`: Editar contrato com montante médio semanal

> **Obs.:** No documento original, é mencionado como ¨Editar contrato CBR Semanal¨

```xml
<ContratosCBR tipoGeracao="7">
    <Contrato sequencialControle="1"  numeroContrato="123" tipoGravação="C">
        <MontanteMédio vigenciaDeInicio=`01/01/2000 00` vigenciaDeFim="31/12/2000 23">
            <Semana semana="1" validarMontante="X">
                <MontanteMédioContratoCBR montanteMedio="99999999999999999,999999" />
                <TipoModulacao tipoModulacao="F"/>
                <LimiteModulacao limiteMinimoModulacao="99999999999999999,999"
                    limiteMaximoModulacao="99999999999999999,999" />
                <AtivoAssociadoModulacao idAtivoAssociadoModulacao=""
                    excluirAtivoAssociadoModulacao="" />
            </Semana>
        </MontanteMédio>
    </Contrato>     
</ContratosCBR>
```

`12`: Finalizar ou Cancelar Contrato CBR

```xml
<ContratosCBR tipoGeracao="13">
    <Contrato sequencialControle="1" numeroContrato="123" dataFinalizacao="01/02/2000 00"
        validarFinalizacao="X" cancelarContrato="" validarCancelamento="" />
</ContratosCBR>
```

`13`: Criar contrato Art 5o da Lei 13.182/2015 mensal

```xml
<ContratosCBR tipoGeracao="14">
    <Contrato sequencialControle="1" tipoGravacao="C" dataDeInicio="01/01/2018 00"
        dataDeFim="31/01/2018 23" idComprador="56" idVendedor="26" idSubMerEntrega="1">
        <MontanteMaximoModulacao>
        <MesAno mesAno="01/2018" montanteMaximoModulacao="2222.000000" validarMontante="X">
            <AtivoAssociadoModulacao idAtivoAssociadoModulacao="1108" />
        </MesAno>
        </MontanteMaximoModulacao>
    </Contrato>
</ContratosCBR>
```

`14`: Criar contrato Art 5o da Lei 13.182/2015 horário

```xml
<ContratosCBR tipoGeracao="15">
    <Contrato sequencialControle="1" tipoGravacao="C" dataDeInicio="01/01/2018 00"
        dataDeFim="31/01/2018 23" idComprador="56" idVendedor="26" idSubMerEntrega="1">
        <MontanteMaximoModulacao>
        <MesAno mesAno="01/2018" validarMontante="X">
            <Dia dia="01">
                <Hora hora="00" montanteMaximoHorario="32323.000000" />
            </Dia>
                <AtivoAssociadoModulacao idAtivoAssociadoModulacao="1108" />
        </MesAno>
        </MontanteMaximoModulacao>
    </Contrato>
</ContratosCBR>
```

`15`: Editar contrato Art 5o da Lei 13.182/2015 mensal

```xml
<ContratosCBR tipoGeracao="16">
    <Contrato sequencialControle="1" numeroContrato="2323" tipoGravacao="C">
        <MontanteMaximoModulacao>
        <MesAno mesAno="01/2018" montanteMaximoModulacao="2222.000000" validarMontante="X">
            <AtivoAssociadoModulacao idAtivoAssociadoModulacao="1108" />
        </MesAno>
        </MontanteMaximoModulacao>
    </Contrato>
</ContratosCBR>
```

`16`: Editar contrato Art 5o da Lei 13.182/2015 horário

```xml
<ContratosCBR tipoGeracao="17">
    <Contrato sequencialControle="1" numeroContrato="2323" tipoGravacao="C">
        <MontanteMaximoModulacao>
        <MesAno mesAno="01/2018" validarMontante="X">
            <Dia dia="01">
                <Hora hora="00" montanteMaximoHorario="32323.000000" />
            </Dia>
                <AtivoAssociadoModulacao idAtivoAssociadoModulacao="1108" />
        </MesAno>
        </MontanteMaximoModulacao>
    </Contrato>
</ContratosCBR>
```

### Contrato CCEAR-Q

As operações disponíveis para contratos do tipo CCEAR-Q são: 

- `20`: Editar montantes mensais; 
- `22`: Validar montantes mensais.

#### Exemplo de XML de Contrato CCEAR-Q

`20`: Editar montantes mensais

```xml
<ContratosCCEARQ tipoGeracao="20">
    <Contrato sequencialControle="1" numeroContrato="123456" dataDeInicioVigencia="01/01/2009 00">
        <Ano ano="2011" validarSazonalizacao="X">
            <Mes mes="01" montanteMensal="100,00"></Mes>
            <Mes mes="02" montanteMensal="800,00"></Mes>
        </Ano>
    </Contrato>
</ContratosCCEARQ>
```

`22`: Validar montantes mensais

```xml
<ContratosCCEARQ tipoGeracao="22">
    <Contrato sequencialControle="1" numeroContrato="123456" dataDeInicioVigencia="01/01/2009 00">
        <Ano ano="2011"></Ano>
        <Ano ano="2012"></Ano>
    </Contrato>
</ContratosCCEARQ>
```

### Contrato Leilão de Ajuste

As operações disponíveis para contratos do tipo Leilão de Ajuste são:

- `1`: Editar dados mensais e horários;
- `2`: Editar dados horários por patamar;
- `3`: Validar montantes do contrato.

#### Exemplo de XML de Contrato Leilão de Ajuste

`1`: Editar dados mensais e horários

```xml
<ContratosLeilaoAjuste tipoGeracao="1" > 
    <Contrato sequencialControle="1" numeroContrato="123" dataDeInicioVigencia="01/01/2009 00">
        <Ano ano="2009" validarSazonalização="X">
            <Mes mes="01" montanteMensal="200,000" validarModulacao="X">
                <Dia dia="01">
                    <Hora hora="01" montanteHorario="20,000" />
                    <Hora hora="02" montanteHorario="9,000" />
                </Dia>
            </Mes>
        </Ano>
    </Contrato>                 
</ContratosLeilaoAjuste>
```

`2`: Editar dados horários por patamar

```xml
<ContratosLeilaoAjuste tipoGeracao="2"> 
    <Contrato sequencialControle="1" numeroContrato="123" dataDeInicioVigencia="01/01/2009 00">
        <Ano ano="2009" validarSazonalização="X">
            <Mes mes="01" montanteMensal="200,000" validarModulacao="X" unidadePatamar="0">
                <Semana semana="1" patamarLeve="2,000" patamarMédio="5,000" patamarPesado="7,000" />
                <Semana semana="2" patamarLeve="2,000" patamarMédio="5,000" patamarPesado="7,000" />
                <Semana semana="3" patamarLeve="2,000" patamarMédio="5,000" patamarPesado="7,000" />
            </Mes>
        </Ano>
    </Contrato>                 
</ContratosLeilaoAjuste>
```

`3`: Validar montantes do contrato

```xml
<ContratosLeilaoAjuste tipoGeracao="3"> 
    <Contrato sequencialControle="1" numeroContrato="123" dataDeInicioVigencia="01/01/2009 00">
        <Ano ano="2009" validarSazonalização="X">
            <Mes mes="01" validarModulacao="X" />          
            <Mes mes="02" validarModulacao="X" />
        </Ano>
    </Contrato>             
</ContratosLeilaoAjuste>
```

### Contrato Proinfa

A operação disponível para contrato do tipo Proinfa é:

- `10`: Editar montantes mensais.

#### Exemplo de XML de Contrato Proinfa

`10`: Editar montantes mensais

```xml
<ContratosProinfa tipoGeracao="10">
    <Contrato sequencialControle="1" numeroContrato="123456" dataDeInicioVigencia="01/01/2011 00">
        <Ano ano="2011">
            <Mes mes="01" montanteMensal="100,00"></Mes>
            <Mes mes="02" montanteMensal="800,00"></Mes>
        </Ano>
    </Contrato>
</ContratosProinfa>
```

### Contrato CCEAR-Q, CCEEAR-D Redução Contratual

As operações disponíveis para Redução Contratual de contratos do tipo CCEAR-Q e CCEAR-D são:

- `1`: Aplicar Fator de Redução Contratual;
- `2`: Rescindir Contrato por Redução Contratual;
- `3`: Validar Redução / Rescisão Contratual;
- `4`: Excluir Redução / Rescisão Contratual.

#### Exemplo de XML de Contrato CCEAR-Q, CCEEAR-D Redução Contratual

`1`: Aplicar Fator de Redução Contratual

```xml
<ReducaoContratual tipoGeracao="1">
    <Contrato sequencialControle="1" numeroContrato="123456">
         <FatorReducaoContratual tipoReducao="T" periodoDeInicioReducao="01/2018"
            periodoDeFimReducao="01/2019" fatorReducao="0.123456789" />
    </Contrato>
    <Contrato sequencialControle="2" numeroContrato="654321">
         <FatorReducaoContratual tipoReducao="P" periodoDeInicioReducao="01/2020"
            fatorReducao="0.123456789" />
    </Contrato>
</ReducaoContratual>
```

`2`: Rescindir Contrato por Redução Contratual

```xml
<ReducaoContratual tipoGeracao="2">
    <Contrato sequencialControle="1" numeroContrato="123456" periodoDeInicioRescisao="01/2020">
    </Contrato>
    <Contrato sequencialControle="2" numeroContrato="654321" periodoDeInicioRescisao="01/2022">
    </Contrato>
</ReducaoContratual>
```

`3`: Validar Redução / Rescisão Contratual

```xml
<ReducaoContratual tipoGeracao="3">
    <Contrato sequencialControle="1" numeroContrato="123456">
        <FatorReducaoContratual tipoValidacao="0" periodoDeInicioReducao="01/2020" />
    </Contrato>
    <Contrato sequencialControle="2" numeroContrato="654321">
        <FatorReducaoContratual tipoValidacao="1"/>
    </Contrato>
</ReducaoContratual>
```

`4`: Excluir Redução / Rescisão Contratual

```xml
<ReducaoContratual tipoGeracao="4">
    <Contrato sequencialControle="1" numeroContrato="123456"> 
        <FatorReducaoContratual tipoAcordo="0" periodoInicioReducaoRescisao="01/2020" />
    </Contrato>
    <Contrato sequencialControle="2" numeroContrato="654321"> 
        <FatorReducaoContratual tipoAcordo="1"/>
    </Contrato>
</ReducaoContratual>
```
