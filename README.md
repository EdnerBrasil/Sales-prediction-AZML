# 🧙‍♂️Sales-prediction-AZML 🍦 Gelato Mágico - Previsão de Vendas com Machine Learning

Aprendizados e considerações sobre aprendizando de máquina no Bootcamp DP-100 na DIO 

## ℹ️ Cenário
Imagine uma sorveteria chamada **Gelato Mágico**, localizada em uma cidade litorânea. Durante o verão, as vendas disparam, mas existe uma forte correlação entre a temperatura do dia e a quantidade de sorvetes vendidos. A grande dor do negócio é a incerteza em relação as vendas: preparar muitos sorvetes em dias frios pode gerar desgaster como: o desperdício de material e o prejuízo financeiro. Por outro lado, produzir pouco em dias quentes significa perder grandes oportunidades de vendas. O gestor tem uma tabela de dados do total de vendas e a temperatura média do dia, mas apenas com esse volume de dados não consegue tomar boas decisões apesar de conseguir visualizar a correlação de mais vendas em dias quentes

## 🎯 Objetivo do Projeto
O objetivo deste projeto é desenvolver um modelo preditivo de **Machine Learning (Regressão Linear)** para prever a quantidade de sorvetes que serão vendidos com base na temperatura prevista para o dia. Com isso, conseguimos otimizar a produção, evitar desperdícios, garantir estoque suficiente e, consequentemente, salvar tempo e dinheiro.

---

Seguindo a proposta do desafio é utilizamos as ferramentas disponíveis na nuvem Azure, principalmente voltadas para o aprendizado de máquina para treinar modelos preditivos, **neste exercício utilizando modelos de regressão linear**. Com o resultado do treinamento do modelo o objetivo é tê-lo como ferrramenta  que permita prever a quantidade a ser vendidade em função de uma temperatura enviada como input. Esta predição é especialmente útil para o planejamento da sorveteria **Gelato Mágico** que vai consumir o modelo após o treinamento.

## 👨‍💻preparação 

### base de dados para treinamento
Com ajuda do chatGPT gerei uma tabela fictícia de dados totalizando a quantidade de sorvetes vendidos no dia e a temperatura média registrada naquele dia. Uma tabela [[dados.csv]](https://github.com/EdnerBrasil/Sales-prediction-AZML/edit/main/inputs/dados.csv) foi gerada com base no prompt descrito em [[dados.md]](https://github.com/EdnerBrasil/Sales-prediction-AZML/edit/main/inputs/dados.md)

### ⚙️ Passo a Passo da Solução no [[Azure Machine Learning]](https://portal.azure.com)

1. Criação da Estrutura Básica

    - [x] Criar um Grupo de Recursos (Resource Group): É como se fosse uma pasta para organizar seus recursos na nuvem.
    - [x] Criar o Workspace do Azure Machine Learning: Busque pelo serviço "Azure Machine Learning" e crie um novo workspace vinculado ao grupo de recursos criado. Componentes como conta de armazenamento e Application Insights serão criados automaticamente.
    - [x] Acessar o Workspace: Após o provisionamento, clique em "Launch" para entrar no painel do Azure Machine Learning (Studio).

2. Configuração de Computação (Compute)

     - [x] Criar uma Instância de Computação (Compute Instance): No menu lateral, vá em Compute e crie uma instância (geralmente CPU) que servirá para você rodar testes e visualizar Notebooks.
     - [x] Criar um Cluster de Computação (Compute Cluster): Crie também um cluster dedicado. É ele que fará o trabalho pesado e processará o treinamento do seu modelo de forma escalável.

3. Preparação dos Dados

    - [x] Fazer Upload dos Dados: Suba o seu arquivo de [[dados]](https://github.com/EdnerBrasil/Sales-prediction-AZML/edit/main/inputs/dados.csv) para dentro do ambiente do Azure.
    - [x] Criar um Ativo de Dados (Dataset): Crie um novo dataset tabular (ML Table) a partir do arquivo enviado, selecionando apenas as colunas úteis para o modelo: `total_de_sorvetes_vendidos` e `temperatura_media_dia`.

4. Treinamento do Modelo (Exemplo usando Automated ML)

    - [x] Criar um novo Job de ML Automatizado: Inicie um novo experimento escolhendo o tipo de tarefa como Regressão.
    - [x] Definir a Coluna Alvo (Target): Selecione o dataset criado e aponte qual coluna o modelo deve aprender a prever (no caso, a coluna de `total_de_sorvetes_vendidos`).
    - [x] Configurar Parâmetros e Computação: Defina limites de tempo para o treinamento (ex: 15 minutos) e selecione o Compute Cluster criado no passo 2. Submeta o job para execução.

5. Disponibilização do Modelo em Endpoint (API)

    - [ ] Selecionar o Melhor Modelo: Após o fim do treinamento, analise a lista de modelos gerados e escolha o que teve a melhor performance.
    - [ ] Realizar o Deploy (Implantação): Com o melhor modelo selecionado, clique na opção de "Deploy" para um Web service (ou Real-time).
    - [ ] Configurar o Contêiner: Escolha a opção de implantar usando uma instância de contêiner.
    - [ ] Testar e Consumir a API: Assim que o provisionamento terminar, o Azure fornecerá um Endpoint REST (um link) e uma chave de acesso. Você poderá usar esse endpoint para integrar o seu modelo preditivo a aplicativos da web, calculadoras ou outros sistemas.

## 🎨desenvolvimento e aprendizados
1. Criação da Estrutura Básica
<img width="1844" height="937" alt="Captura de tela 2026-03-03 162233" src="https://github.com/user-attachments/assets/0ecd57a8-7004-45f0-b168-11ce83284496" />

Grupo de Recurso: `AZML-DIO-desafio1`
Azure Machine Learning WorkSpace: `AZML-DIO-desafio1`
2. Configuração de Computação (Compute)
<img width="1832" height="936" alt="Captura de tela 2026-03-03 163127" src="https://github.com/user-attachments/assets/eae8beff-29ef-42e3-9a6e-a52c28a35bdd" />
<img width="1846" height="868" alt="Captura de tela 2026-03-03 163223" src="https://github.com/user-attachments/assets/562f1d09-a9bf-4517-a049-b60aacb4eb09" />

3. Preparação dos Dados
<img width="1817" height="947" alt="Captura de tela 2026-03-03 165316" src="https://github.com/user-attachments/assets/dd81a5d9-31ec-443c-8c17-2579e17d601f" />

4. Treinamento do Modelo (Exemplo usando Automated ML)
   Início da configuração e execução do modelo   
<img width="1895" height="1027" alt="image" src="https://github.com/user-attachments/assets/c373ceb2-ae7e-4a9c-971e-3bfab6076b9f" />
   Job em execução
<img width="1868" height="960" alt="image" src="https://github.com/user-attachments/assets/f6742435-f9a6-48a8-95e3-8bcd3e99ed46" />


