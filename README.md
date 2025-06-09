# 📊 Análise de Cancelamento de Clientes (Churn) com Python

## Visão Geral do Projeto

Este projeto de análise de dados foi desenvolvido para uma empresa com uma base de mais de 800 mil clientes. O desafio principal é que a maioria dos clientes atuais são inativos, ou seja, já cancelaram o serviço. Fui contratado para mergulhar nos dados com o objetivo de **entender os principais motivos por trás desses cancelamentos** e **propor ações eficientes para reduzir o número de clientes que deixam de usar o serviço (churn)**.

Este trabalho visa não apenas identificar padrões, mas também fornecer insights acionáveis que possam levar a uma melhor retenção de clientes e, consequentemente, a uma melhoria nos resultados da empresa.

## Fonte de Dados

Os dados utilizados nesta análise foram fornecidos pela empresa e estão disponíveis no arquivo `cancelamentos_sample.csv`.
Você pode acessar o dataset original neste link: [https://drive.google.com/drive/folders/1uDesZePdkhiraJmiyeZ-w5tfc8XsNYFZ?usp=drive_link](https://drive.google.com/drive/folders/1uDesZePdkhiraJmiyeZ-w5ftc0lSxNYFZ?usp=drive_link)

## Metodologia e Passos da Análise

A análise foi conduzida utilizando Jupyter Notebook e a linguagem Python, seguindo uma abordagem estruturada:

1.  **Importação da Base de Dados:**
    * Carregamento inicial do arquivo `cancelamentos_sample.csv` para um DataFrame Pandas.

2.  **Visualização e Tratamento da Base de Dados:**
    * **Exploração Inicial:** Visualização das primeiras linhas do DataFrame (`display(tabela)`) para compreender as informações contidas e identificar possíveis problemas.
    * **Limpeza de Dados:**
        * Verificação das informações detalhadas da tabela (`display(tabela.info())`) para identificar tipos de dados, contagens de valores não nulos e uso de memória.
        * Remoção de colunas consideradas inúteis para a análise (Ex: `CustomerID`, que não foi utilizado após a importação, resultando em 11 colunas).
        * Tratamento de valores ausentes (`tabela = tabela.dropna()`) para garantir a consistência dos dados.

3.  **Análise Inicial do Churn:**
    * **Contagem de Cancelamentos:** Quantificação de clientes que cancelaram (1.0) e não cancelaram (0.0) o serviço (`tabela["cancelou"].value_counts()`).
    * **Cálculo da Porcentagem de Churn:** Determinação da proporção de clientes que cancelaram em relação ao total (`tabela["cancelou"].value_counts(normalize=True)`).
        * **Insight Inicial:** Aproximadamente **56.79%** dos clientes na base original haviam cancelado o serviço, um número que evidencia a urgência do problema.

4.  **Análise da Causa dos Cancelamentos (Análise Exploratória de Dados - EDA):**
    * Foram gerados gráficos de histograma (`plotly.express.histogram`) para cada coluna do dataset, com o `cancelou` como dimensão de cor, para visualizar o impacto de cada variável no cancelamento.

    * **Principais Observações da EDA:**
      
        * **Chamadas para o Call Center (`ligacoes_callcenter`):** Clientes que realizaram **mais de 4 ligações para o call center** demonstraram uma alta propensão a cancelar.
        * **Atraso no Pagamento (`dias_atraso`):** Clientes que apresentaram **mais de 20 dias de atraso** no pagamento também exibiram uma alta taxa de cancelamento.
        * **Duração do Contrato (`duracao_contrato`):** Foi observado que **todos os clientes com contrato "Monthly" (Mensal)** possuíam uma taxa de cancelamento significativamente alta, sugerindo que este tipo de contrato é um forte indicador de churn.

5.  **Simulação de Impacto das Ações Propostas:**
    Para entender o potencial de redução do churn, foram feitas simulações removendo os "problemas" identificados:

    * **Remoção de Clientes com Mais de 4 Ligações ao Call Center:** A taxa de cancelamento **caiu para aproximadamente 36.39%**.
    * **Remoção de Clientes com Mais de 20 Dias de Atraso:** A taxa de cancelamento **caiu para aproximadamente 26.96%**.
    * **Remoção de Clientes com Contrato "Monthly":** A taxa de cancelamento **caiu drasticamente para aproximadamente 18.35%**.

## Conclusões e Ações Propostas

Com base na análise, as seguintes ações podem ser consideradas para reduzir a taxa de cancelamento:

* **Alerta de Call Center:** Implementar um sistema de alerta para o time de atendimento/relacionamento quando um cliente atingir a **terceira ligação** ao call center, permitindo uma intervenção proativa.
* **Incentivo a Contratos Mais Longos:** Oferecer **descontos ou benefícios** para clientes que optarem por contratos de duração maior (Anual ou Trimestral), desencorajando o contrato mensal.
* **Alerta de Atraso no Pagamento:** Acionar um alerta para o time de cobrança quando um cliente atingir **10 dias de atraso** no pagamento, permitindo uma abordagem mais cedo e eficaz para evitar o cancelamento.

A implementação dessas ações, combinada com o monitoramento contínuo, tem o potencial de reduzir a taxa de churn para menos de 20%, impactando positivamente a sustentabilidade da base de clientes da empresa.

## Tecnologias Utilizadas

* **Python 3.x**
* **Jupyter Notebook** (para o desenvolvimento e execução da análise)
* **Bibliotecas Python:**
    * `pandas` para manipulação e análise de dados.
    * `numpy` (usado indiretamente por pandas).
    * `plotly.express` para criação de visualizações interativas.
    * `openpyxl` (mencionado no notebook, para leitura/escrita de arquivos Excel, embora não usado diretamente neste snippet).
    * `ipykernel`, `nbformat` (para ambiente Jupyter).

## Como Rodar o Projeto

1.  Clone este repositório:
    ```bash
    git clone [https://github.com/RenatoFariaDv/analise-cancelamento-clientes.git](https://github.com/RenatoFariaDv/analise-cancelamento-clientes.git)
    ```
2.  Navegue até a pasta do projeto:
    ```bash
    cd analise-cancelamento-clientes
    ```
3.  Instale as dependências necessárias (usando o `requirements.txt` que criamos):
    ```bash
    pip install -r requirements.txt
    ```
4.  Abra o Jupyter Notebook:
    ```bash
    jupyter notebook initial.ipynb
    ```

## Autor

Renato Faria
Perfil no LinkedIn: https://www.linkedin.com/in/renato-faria-b96aa0322/

---
