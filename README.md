# Estudo de caso: cancelamento de clientes com Python

Quais características aparecem com mais frequência entre os clientes que cancelam um serviço? Neste estudo, usei Python, pandas e Plotly para explorar uma amostra de dados e formular hipóteses sobre atendimento, pagamentos e duração do contrato.

## Como a análise foi feita

A partir de [cancelamentos_sample.csv](cancelamentos_sample.csv), removi o identificador do cliente da análise e descartei linhas com valores ausentes. Calculei a proporção de cancelamentos na base tratada e comparei, por meio de histogramas, os grupos que cancelaram e os que permaneceram.

## Resultados do exercício

A tabela reproduz os percentuais aproximados registrados na análise. Cada linha aplica um filtro adicional à amostra anterior.

| Recorte analisado | Clientes que cancelaram no recorte |
|---|---:|
| Amostra tratada, antes dos filtros | 56,79% |
| Até quatro ligações ao atendimento | 36,39% |
| Também com até 20 dias de atraso | 26,96% |
| Também com contrato diferente de mensal | 18,35% |

Os percentuais descrevem grupos diferentes de clientes. Excluir registros muda a composição da amostra. Para estimar o efeito de uma ação de retenção, seria preciso aplicá-la e comparar o resultado com um grupo semelhante.

## Hipóteses para testar

- **Atendimento:** acompanhar clientes a partir da terceira ligação e verificar se o problema que motivou os contatos foi resolvido.
- **Pagamentos:** testar um lembrete aos dez dias de atraso e acompanhar a regularização e os cancelamentos.
- **Contratos:** investigar por que clientes escolhem o plano mensal antes de testar incentivos a planos mais longos.

## Como conferir os percentuais

Com Python e pandas instalados, execute este trecho na pasta do repositório. Ele imprime a quantidade de registros e a taxa de cancelamento de cada recorte.

```python
import pandas as pd

clientes = pd.read_csv("cancelamentos_sample.csv").drop(columns="CustomerID").dropna()

def resumir(nome, dados):
    print(f"{nome}: {len(dados)} registros | {dados['cancelou'].mean():.2%} de cancelamento")

resumir("Amostra tratada", clientes)
clientes = clientes.loc[clientes["ligacoes_callcenter"] <= 4]
resumir("Atendimento", clientes)
clientes = clientes.loc[clientes["dias_atraso"] <= 20]
resumir("Atendimento e pagamentos", clientes)
clientes = clientes.loc[clientes["duracao_contrato"] != "Monthly"]
resumir("Atendimento, pagamentos e contrato", clientes)
```

[Renato Faria no GitHub](https://github.com/RenatoFariaDv)
