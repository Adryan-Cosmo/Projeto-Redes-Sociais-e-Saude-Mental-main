# Impacto do Uso das Redes Sociais na Saúde Mental  

![Logo do projeto](/images/Banner_Projeto.svg)

## Introdução

O presente projeto de pesquisa visa analisar o impacto do uso excessivo das redes sociais na saúde mental dos indivíduos.

A pesquisa se justifica pela crescente relevância do tema no contexto social atual, onde o uso das redes sociais se tornou onipresente e, em muitos casos, excessivo.

## Objetivo

O objetivo principal da pesquisa é identificar os principais impactos do uso excessivo das redes sociais na saúde mental dos indivíduos.

Dessa forma, iremos ao decorrer desse projeto analisar os dados com o intuito de responder os seguintes questionamentos:

**Questionamento Principal:**

1. Qual é o impacto do uso excessivo das redes sociais na saúde mental dos indivíduos?

**Perguntas Complementares:**

2. Quais são os principais sintomas relacionados ao uso excessivo das redes sociais?

3. Existem variáveis demográficas que influenciam o impacto na saúde mental?

4. Qual é a frequência de uso das redes sociais entre os indivíduos analisados?

5. Há uma relação entre o tipo de conteúdo consumido nas redes sociais e os problemas de saúde mental?

## Metodologia

A pesquisa está sendo realizada com uma amostra de N indivíduos, que serão recrutados através de divulgações do questionário online nas redes sociais.  
Os participantes responderão a um questionário online, composto por 25 perguntas, que abordará os seguintes temas:

- Hábitos de uso das redes sociais;
- Sintomas de transtornos mentais;
- Fatores de risco e proteção para problemas de saúde mental.

O questionário será desenvolvido em uma plataforma online com respostas anônimas e estará disponível para acesso por um período indeterminado.

## Status Atual

- Padronização dos Dados 
- Separação dos dados para validação concluída.
- Análise exploratória dos dados inicial concluída.
- Limpeza e Tratamento de Outliers concluída.
- Analise Univaria e Bivariada concluída.

## Padronização dos Dados

Na observação inicial dos dados, viu-se necessário padronizar e corrigir algumas entradas de dados da nossa base de dados.

Dessa forma, foram criados features simplificadas que representam as perguntas das pesquisas, como também o tratamento de algumas features através do metodo get_dummies, visto que possuiam mais de um valor categorico por feature.

## Análise de Dados

Início da análise exploratória dos dados das variáveis targets: Ansiedade nas Redes Sociais, Preocupação Negativa e Frequência de Depressão.

### A análise univariada incluiu:

#### Visualização da distribuição dos dados:

- Observou-se a necessidade de criar dicionários para simplificar os valores de features como "Consentimento", para melhor visualização dos dados.

- A maioria das features não possui distribuição normal, sendo em sua maioria inclinada à esquerda.

#### Verificação da quantidade de nulos:

- Algumas features como "Nome" sempre terão seus valores nulos por se tratar de uma pesquisa anônima.

#### Identificação de outliers:

- Foi encontrado outliers na feature `DesafiosRedução`

## Limpeza e Tratamento de Outliers:

### **Limpeza dos valores nulos:**

**Variaveis targets:**

  Como nossa base de dados deriva de uma pesquisa e a maioria das perguntas são obrigatorias, ou seja, um ambiente controlado, conseguimos identificar que são poucos os casos onde podem ocasionar em dados nulos.

  Desse modo, é possivel indentificar que não há problemas para a nossa previsão no futuro ao excluir as linhas que possuem valores nulos.


**Demais variaveis:**

  Para as features `MotivaçãoRedução` e `SucessoRedução` e `DesafiosRedução` será imputado o valor `Não tentou reduzir` pois esses valores só poderiam ser preenchidos caso o entrevistado respondesse "Sim" para a pergunta 'Você já tentou reduzir o tempo que passa no celular?"

  Para o restante dos valores nulos presentes na feature `DesafioRedução` será imputado o valor `não quis responder` pois se tratava de uma pergunta não obrigatoria.

### **Tratamento de Outliers**

  O outliers que foi encontrado corresponde a feature `DesafiosRedução` que possui inumeros valores categoricos diferentes, o que não permite uma visão significativa da distribuição dos dados dessa features.

  A solução encontrada para solucionar essa outlier é a criação de outras features para categorizar esses valores com base nas suas simialidades.

### **Tratamento das Features categoricas**
  
  > [!WARNING]
  > Os metodos utilizados para tratar as features categoricas podem mudar ao decorrer do projeto.

 O método para tratar as features targets categoricas `AnsiedadeRedes` e `FrequenciaDepressão` foi a criação de um dicionario para transforma os dados categoricos e valores quantitativos visto a natuzera dos valores presentes nas variaveis targets.

 De modo similar, atráves do metodo **on-off encoding**, foram tratados as features categoricas `DificuldadeConcentração`, `TentativaReduçãoCelular`, `UsaRedesSociais` e `Sexo`.

 As demais features como possuem entre 5 a 7 valores categoricos unicos, foi realizado o tratamento dessas features utilizando o metodo **Target Encoding com Validação Cruzada**, no qual consiste numa tecnica de pré-processamento de dados que pode ser utilizada para codificar features categóricas em valores numéricos, levando em consideração a relação entre as features e as variáveis target.

 Logo, foram tratados as features `TempoRedesSociais`,`FrequenciaUsoRedes`, `DistraçãoRedes`, `SentimentoComparação`, `BuscaValidação`, `DescriçãoMudançaInteresse`, `MotivaçãoRedução` e `SucessoRedução`. Consequentemente sendo feito o drop dessas features do nosso dataset final.

## Features Engineering

Com base no dados obtidos até o momento, conseguimos ter a capacidade de, ou ao menos tentar, responder algumas das perguntas que fizemos inicialmente no projeto.

Por esse motivo, atráves do método Features Enginnering iremos verificar a correlação que duas ou mais features possuem que nos permitem responder os nossos questinamentos.

Nesse sentido, foram criadas as seguintes features:

- Impacto no Sono = Multiplicar as features `ProblemasSono` e `TempoRedesSociais_encoded`
- Nível De Distração = Media entre as features `FacilidadeDistração`, `DificuldadeConcentração`, `DistraçãoRedes_encoded`
- Uso Médio de Redes Sociais = Cálculo do tempo médio gasto em redes sociais utilizando as features `TempoRedesSociais_encoded` e `FrequenciaUsoRedes_encoded`

## Análise Bivariada:

Na etapa da análise bivariada, buscamos identificar as relações que as features da nossa base de dados possui, de modo que, verificamos e corrigimos as features em caso de multicorrelação.

Tendo como foco, a relação das demais variaveis com as nossas variaveis targets, foi observado atráves de heatmaos e da tecnica do sklearn 'SelectKBest' identificamos a variaveis que possuiam maior chance de gerar confusão/ruido no nossos teste de aprendizagem, e logo corrigimos-as.

## Resultados Esperados

A pesquisa espera gerar resultados que contribuam para a compreensão dos efeitos do uso excessivo das redes sociais na saúde mental, tais como:

- Identificação dos principais impactos do uso das redes sociais na saúde mental;
- Elaboração de um modelo preditivo para identificar indivíduos em risco;
- Proposição de medidas de intervenção para prevenir e mitigar os efeitos negativos das redes sociais.

## Impacto e Relevância

A pesquisa espera ter um impacto significativo na área da psicologia e da computação, fornecendo novos conhecimentos sobre os efeitos das redes sociais na saúde mental. Os resultados da pesquisa poderão ser utilizados para:

- Orientar políticas públicas sobre o uso das redes sociais;
- Desenvolver programas de intervenção para prevenir e mitigar os efeitos negativos das redes sociais;
- Informar a sociedade sobre os riscos e benefícios do uso das redes sociais.

## **Contribua para a Pesquisa**

Você pode contribuir para a pesquisa respondendo ao questionário anônimo: [Qestionario](https://forms.office.com/r/VcpnP7WctY).

>**Divulgue a Pesquisa**: Ajude a divulgar a pesquisa para que mais pessoas possam participar e contribuir para a compreensão dos efeitos do uso excessivo das redes sociais na saúde mental.

## Contato

Para mais informações sobre o projeto, entre em contato com:

> Pesquisador:  
> Adryan Cavalcante Cosmo  
> <Adryan.cosmo@ufpr.br>

>Orientador do projeto:  
>Dr. Professor Marcos Vinicius Oliveira de Assis

## Agradecimentos

Agradecemos a todos que estão colaborando com a pesquisa.
