# Projeto: Rastreamento de Experimentos com MLflow e Azure ML

Este projeto demonstra uma capacidade fundamental de MLOps: o rastreamento de experimentos de machine learning. Utilizando a biblioteca open-source **MLflow** integrada ao **Azure Machine Learning**, este projeto mostra como registrar, monitorar e organizar execuções de treinamento de modelos.

O objetivo não é apenas treinar um modelo, mas criar um processo **reprodutível** e **auditável**, onde cada parâmetro, métrica e artefato (como o próprio modelo) é salvo e versionado.

## Tecnologias Utilizadas

* **Azure Machine Learning:** Plataforma de nuvem para o ciclo de vida de ML.
* **MLflow:** A ferramenta open-source central para gerenciar o ciclo de vida de ML (usada aqui para Rastreamento).
* **Scikit-learn:** Usado para treinar os modelos de classificação/regressão.
* **Azure ML SDK (v2):** Usado para conectar e interagir com o workspace.
* **Python** & **Jupyter Notebooks**.

## O Processo

1.  **Configuração do Ambiente:** O Workspace do Azure ML, a Instância de Computação e as bibliotecas necessárias (como `mlflow` e `azureml-mlflow`) foram configurados.

2.  **Integração do MLflow:** O notebook utiliza `mlflow.set_tracking_uri(ml_client.workspaces.get(ml_client.workspace_name).mlflow_tracking_uri)` para instruir o MLflow a enviar todos os seus logs diretamente para o workspace do Azure ML, em vez de salvá-los localmente.

3.  **Treinamento e Rastreamento:**
    * Um modelo (`LogisticRegression` ou `RandomForest` do Scikit-learn) é treinado dentro de uma execução `mlflow.start_run()`.
    * **Parâmetros:** Hiperparâmetros (como `alpha` ou `n_estimators`) são registrados usando `mlflow.log_param()`.
    * **Métricas:** Métricas de avaliação (como `Accuracy` ou `RMSE`) são registradas usando `mlflow.log_metric()`.
    * **Artefatos:** O próprio modelo treinado é salvo e registrado usando `mlflow.sklearn.log_model()`.

4.  **Revisão no Azure ML Studio:**
    * Cada execução do notebook que treina um modelo cria um novo **Trabalho (Job)** no Azure ML Studio.
    * Dentro de cada "Trabalho", podemos analisar a aba **"Métricas"** (para ver os gráficos de métricas), **"Parâmetros"** (para ver o que foi usado) e **"Saídas + logs"** (onde o modelo salvo pode ser baixado).

## Principal Vantagem

Este projeto demonstra como o Azure Machine Learning atua como um *backend* centralizado e seguro para o MLflow. Em vez de ter arquivos de log espalhados em máquinas locais, todas as execuções de todos os cientistas de dados são registradas em um único local (o Workspace do Azure), permitindo uma fácil comparação e gerenciamento de modelos.

