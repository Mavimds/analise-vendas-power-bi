# Análise de Vendas | Dashboard Power BI

## Sobre o projeto

Este projeto apresenta um dashboard interativo desenvolvido no Power BI com o objetivo de analisar o desempenho comercial de uma empresa fictícia, considerando indicadores de receita, lucro, vendas e rentabilidade.

A análise permite comparar os resultados realizados com as estimativas e explorar o desempenho dos produtos, canais de venda e regiões, transformando os dados em informações que apoiam a interpretação dos resultados e a tomada de decisões.

## Contexto e aprendizado

O desenvolvimento deste projeto foi inspirado nos conhecimentos adquiridos no módulo de **Storytelling com Dados**, da Formação em Engenharia e Análise de Dados, realizada pela MCIO em parceria com a Leega.

Os conceitos aprendidos foram aplicados na preparação, análise e visualização dos dados, buscando construir um dashboard que apresentasse informações de maneira clara, organizada e objetiva.

## Ferramentas e tecnologias

- **Power BI:** desenvolvimento do dashboard e visualização dos dados.
- **Power Query:** preparação e transformação dos dados.
- **DAX (Data Analysis Expressions):** criação de medidas, colunas calculadas e tabela calendário.
- **Modelagem de dados:** construção de relacionamentos entre as tabelas.

## Modelagem e transformação dos dados

A etapa de preparação e modelagem envolveu:

- Tratamento e organização das bases de Produtos, Vendas e Estimativas.
- Extração do ano a partir da data original da tabela de estimativas.
- Criação da coluna calculada `Data Estimativa`, utilizando o ano para gerar uma data de referência.
- Criação de uma tabela calendário com informações de data, ano, mês e número do mês.
- Configuração da ordenação dos meses pelo número correspondente.
- Criação de relacionamentos entre as tabelas Produtos, Vendas, Estimativas e Calendário, permitindo a integração das informações e a aplicação de filtros nas análises.

### Tabela calendário

A tabela calendário foi criada com DAX utilizando `CALENDARAUTO()` e `ADDCOLUMNS()`:

```dax
Calendario =
ADDCOLUMNS(
    CALENDARAUTO(),
    "Ano", YEAR([Date]),
    "Mês", FORMAT([Date], "MMMM"),
    "Número do Mês", MONTH([Date])
)
```

### Coluna calculada

Para integrar as estimativas à tabela calendário, foi criada a seguinte coluna:

```dax
Data Estimativa = DATE('Estimativas'[Ano], 1, 1)
```

## Medidas DAX

Foram desenvolvidas medidas para calcular os principais indicadores de desempenho comercial.

**1. Receita Realizada**

```dax
Receita Realizada = SUM('Vendas'[Receita])
```

**2. Receita Estimada**

```dax
Receita Estimada = SUM('Estimativas'[Receita])
```

**3. Variação da Receita**

```dax
Variação da Receita = [Receita Realizada] - [Receita Estimada]
```

**4. Variação Percentual da Receita**

```dax
Variação Percentual =
DIVIDE(
    [Variação da Receita],
    [Receita Estimada],
    0
)
```

**5. Lucro Realizado**

```dax
Lucro Realizado = SUM('Vendas'[Lucro])
```

**6. Lucro Estimado**

```dax
Lucro Estimado = SUM('Estimativas'[Lucro])
```

**7. Variação do Lucro**

```dax
Variação do Lucro = [Lucro Realizado] - [Lucro Estimado]
```

**8. Variação Percentual do Lucro**

```dax
Variação Percentual do Lucro =
DIVIDE(
    [Variação do Lucro],
    [Lucro Estimado],
    0
)
```

**9. Margem de Lucro**

```dax
Margem de Lucro =
DIVIDE(
    [Lucro Realizado],
    [Receita Realizada],
    0
)
```

## Estrutura do dashboard

O dashboard foi organizado em duas páginas principais:

### 1. Visão Geral

Apresenta os principais indicadores e permite acompanhar o desempenho comercial da empresa por diferentes perspectivas:

- Receita realizada e receita estimada.
- Variação absoluta e percentual da receita.
- Comparação anual entre receita realizada e estimada.
- Receita por linha de produto.
- Receita por canal de venda.
- Distribuição da receita por estado.

### 2. Análise de Produtos

Apresenta uma análise detalhada da performance dos produtos, considerando:

- Receita realizada por produto.
- Lucro realizado por produto.
- Margem de lucro por produto.
- Quantidade vendida por produto.

## Principais resultados

Considerando os resultados gerais da base analisada:

| Indicador | Resultado |
|---|---:|
| Receita realizada | R$ 8,70 bilhões |
| Receita estimada | R$ 8,52 bilhões |
| Variação da receita | +R$ 181,58 milhões |
| Variação percentual da receita | +2,13% |
| Lucro realizado | R$ 3,16 bilhões |
| Lucro estimado | R$ 2,65 bilhões |
| Variação do lucro | +R$ 513,24 milhões |
| Variação percentual do lucro | +19,40% |

Os resultados indicam que a receita realizada superou a estimada em aproximadamente 2,13%, enquanto o lucro apresentou uma variação positiva de aproximadamente 19,40%.

## Fonte dos dados e referências

A base de dados utilizada neste projeto foi disponibilizada no contexto da **Formação em Engenharia e Análise de Dados**, realizada pela **MCIO em parceria com a Leega**.

Os dados foram utilizados para fins educacionais e aplicados no desenvolvimento de análises e visualizações no Power BI.

Os conhecimentos de Storytelling com Dados adquiridos durante a formação também serviram como referência para a construção do dashboard.

## Autora

**Maria Vitória Monteiro**

Estudante de Engenharia de Produção na Universidade Federal de Pernambuco (UFPE), com interesse em Análise de Dados e Engenharia de Dados.

