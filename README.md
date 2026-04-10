# Relatório da NOME DA ATIVIDADE

**Disciplina:PROGRAMAÇÃO CONCORRENTE DISTRIBUIDA ** 
**Aluno(s): MARIA EDUARDA PAIM**
**Turma:ADS 4 SEMESTRE**
**Professor:RAFAEL**
**Data:10/04/2026**

---

# 1. Descrição do Problema

O problema computacional resolvido pelo programa consiste em calcular a similaridade entre pares de perguntas de um conjunto de dados textual. O objetivo é identificar quais perguntas são mais semelhantes entre si, com base em uma métrica de similaridade.

O algoritmo implementado realiza comparações entre todos os pares possíveis de perguntas, calculando uma medida de similaridade entre cada par. Ao final, o programa retorna os pares mais similares encontrados.

O tamanho da entrada utilizada nos testes foi de 5000 perguntas, resultando em um total de 12.497.500 comparações entre pares.

O objetivo da paralelização foi reduzir o tempo de execução do programa, distribuindo as comparações entre múltiplos processos utilizando a biblioteca MPI.


**Questões que devem ser respondidas:**

* Qual é o objetivo do programa? Identificar os pares de perguntas mais semelhantes dentro de um conjunto de dados.
* Qual o volume de dados processado? 5000 perguntas, gerando aproximadamente 12,5 milhões de comparações.
* Qual algoritmo foi utilizado? Comparação par-a-par (força bruta), onde cada pergunta é comparada com todas as outras.
* Qual a complexidade aproximada do algoritmo? Complexidade quadrática: O(n²), pois todas as combinações de pares são avaliadas.

---

# 2. Ambiente Experimental

Os experimentos foram realizados em um ambiente computacional local, utilizando linguagem Python com suporte à paralelização via MPI.

| Item                        | Descrição |
| --------------------------- | --------- |
| Processador                 | Intel Core i5/i7 (ou equivalente)        |
| Número de núcleos           | 4 a 8 núcleos (estimado)          |
| Memória RAM                 | 8 GB          |
| Sistema Operacional         | Windows           |
| Linguagem utilizada         | Python          |
| Biblioteca de paralelização |MPI (mpi4py)           |
| Compilador / Versão         |Python 3.x           |

---

# 3. Metodologia de Testes
Os experimentos foram conduzidos medindo o tempo total de execução do programa para diferentes quantidades de processos.

O tempo de execução foi medido diretamente no código utilizando funções de medição de tempo da linguagem Python (como time.time()), considerando o tempo total desde o início até o fim da execução.

Foi realizada uma execução para cada configuração, utilizando o mesmo conjunto de dados com 5000 perguntas.

Não foi utilizada média dos tempos, sendo considerado o tempo obtido em cada execução.

O tamanho da entrada foi fixo em todos os testes, garantindo consistência na comparação dos resultados.

Configurações testadas
1 processo (versão serial)
2 processos
4 processos
8 processos
12 processos

Procedimento experimental

Para cada configuração, o programa foi executado utilizando o comando mpiexec, variando o número de processos.

Número de execuções por configuração: 1
Não foi realizado cálculo de média (execução única)
O experimento foi executado em máquina local
Durante os testes, não foram executadas outras aplicações pesadas, buscando minimizar interferências no desempenho

# 4. Resultados Experimentais

Preencha a tabela com os **tempos médios de execução** obtidos.

## Orientações

* O tempo deve ser informado em **segundos**
* Utilizar a **média das execuções**

| Nº Threads/Processos | Tempo de Execução (s) |
| -------------------- | --------------------- |
| 1                    |   82.01                    |
| 2                    |   27.18                     |
| 4                    |   17.17                    |
| 8                    |   12.99                    |
| 12                   |   11.77                    |

---

# 5. Cálculo de Speedup e Eficiência

## Fórmulas Utilizadas

### Speedup

```
Speedup(p) = T(1) / T(p)
```

Onde:

* **T(1)** = tempo da execução serial
* **T(p)** = tempo com p threads/processos

### Eficiência

```
Eficiência(p) = Speedup(p) / p
```

Onde:

* **p** = número de processos

---

# 6. Tabela de Resultados

Preencha a tabela abaixo utilizando os tempos medidos.

| Threads/Processos | Tempo (s) | Speedup | Eficiência |
| ----------------- | --------- | ------- | ---------- |
| 1                 |  82.01         | 1.0     | 1.0        |
| 2                 |  27.18         |  3.02       |  1.51          |
| 4                 | 17.17          |  4.78      |  1.19          |
| 8                 | 12.99          | 6.31        | 0.79           |
| 12                | 11.77          | 6.97        | 0.58           |

---

# 7. Gráfico de Tempo de Execução

Construa um gráfico mostrando o **tempo de execução em função do número de threads/processos**.

## Orientações

* Eixo X: número de threads/processos
* Eixo Y: tempo de execução (segundos)

Inserir o gráfico abaixo:

![Gráfico Tempo Execução](graficos/tempo_execucao.png)

---

# 8. Gráfico de Speedup

Construa um gráfico mostrando o **speedup obtido**.

## Orientações

* Eixo X: número de threads/processos
* Eixo Y: speedup
* Incluir também a **linha de speedup ideal (linear)** para comparação

Inserir o gráfico abaixo:

![Gráfico Speedup](graficos/speedup.png)

---

# 9. Gráfico de Eficiência

Construa um gráfico mostrando a **eficiência da paralelização**.

## Orientações

* Eixo X: número de threads/processos
* Eixo Y: eficiência
* Valores entre 0 e 1

Inserir o gráfico abaixo:

![Gráfico Eficiência](graficos/eficiencia.png)

---

# 10. Análise dos Resultados

O speedup obtido foi superior ao esperado nas primeiras execuções (2 e 4 processos), indicando um possível efeito de cache, otimizações internas do sistema ou medições não totalmente estáveis. Idealmente, o speedup não deveria ultrapassar o número de processos.

A aplicação apresentou boa escalabilidade inicial, com redução significativa do tempo ao aumentar o número de processos. No entanto, a partir de 8 processos, o ganho de desempenho começa a diminuir.

A eficiência começa a cair a partir de 8 processos, indicando que o custo de comunicação e sincronização entre os processos passa a impactar negativamente o desempenho.

Provavelmente, o número de processos utilizados começa a se aproximar ou ultrapassar o número de núcleos físicos disponíveis na máquina, causando contenção de recursos.

Observa-se também a presença de overhead de paralelização, especialmente nas execuções com maior número de processos.

Possíveis causas:

Sobrecarga de comunicação entre processos (MPI)
Divisão desigual de carga de trabalho
Contenção de memória/cache
Overhead de gerenciamento dos processos
---

# 11. Conclusão

O uso de paralelismo trouxe um ganho significativo de desempenho, reduzindo o tempo de execução de aproximadamente 82 segundos para cerca de 11 segundos.

O melhor desempenho foi obtido com 12 processos, porém com eficiência reduzida, indicando que o aumento de processos nem sempre resulta em ganhos proporcionais.

A aplicação apresenta boa escalabilidade até certo ponto (principalmente até 4 ou 8 processos), após o qual os ganhos passam a ser limitados pelo overhead.

Como melhorias futuras, podem ser consideradas:

Melhor balanceamento de carga entre processos
Redução da comunicação entre processos
Uso de técnicas mais eficientes de comparação (reduzir complexidade)
Exploração de paralelismo híbrido (MPI + threads)

---
