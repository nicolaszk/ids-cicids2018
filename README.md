# **Otimização e Análise Crítica de um Classificador de Ataques de Rede por Similaridade no Dataset CIC-IDS-2018**

Este repositório contém o código-fonte utilizado no artigo **"Otimização e Análise Crítica de um Classificador de Ataques de Rede por Similaridade no Dataset CIC-IDS-2018"**, publicado e apresentado na **ERRC 2025 (Escola Regional de Redes de Computadores)**.

## **Premiação e Publicação**

Este trabalho foi agraciado com o prêmio de **3º Melhor Artigo** da ERRC 2025\.

* **Evento:** 21ª Escola Regional de Redes de Computadores (ERRC 2025).  
* **Publicação:** Anais da ERRC 2025 \- SBC (Sociedade Brasileira de Computação).  
* **DOI:** [10.5753/errc.2025.17835](https://doi.org/10.5753/errc.2025.17835)  
* **Link para o Artigo:** [SOL \- SBC Open Lib](https://sol.sbc.org.br/index.php/errc/article/view/39182)

## **📝 Resumo**

Este trabalho otimiza um modelo de classificação de pacotes de rede baseado em vetores de similaridade para o dataset **CIC-IDS-2018**. Para enfrentar desafios de memória superiores a 100 GB de RAM encontrados na abordagem original baseada em k-NN, foi implementada a biblioteca **FAISS** (Facebook AI Similarity Search), substituindo o algoritmo tradicional e possibilitando a análise em hardware convencional com alta performance.

A replicação dos cenários de teste originais, acrescida de métricas de precisão detalhadas, revelou a baixa efetividade na detecção de ataques sub-representados, ilustrando o paradoxo da acurácia em datasets desbalanceados. Embora as otimizações de tempo e memória tenham sido bem-sucedidas, o estudo conclui que o balanceamento de dados é crucial para sistemas de detecção de intrusão robustos.

**Autores:**

* Nícolas Warmeling (PUCRS)  
* Laura Klippel (PUCRS)  
* Carlo Mantovani (PUCRS)  
* Tiago Ferreto (PUCRS)

## **⚙️ Requisitos e Desempenho**

O código original exigia uma VM de alta performance (160GB+ RAM). Com as otimizações propostas neste trabalho (FAISS \+ Estruturas de Dados Vetorizadas), é possível executar os experimentos em hardware desktop moderno.

### **Benchmark de Execução**

Em nossos testes com a versão otimizada, e com o dataset em sua forma reduzida obtivemos o seguinte desempenho:

* **Processador:** AMD Ryzen 7 7800X3D (8-Core)  
* **Memória RAM:** 32 GB  
* **Tempo Total de Execução:** \~30 minutos (processando todos os cenários de teste).

### **Pré-requisitos de Software**

* **Python 3.8+**  
* **Git**

## **Instalação e Configuração**

Siga os passos abaixo para configurar o ambiente e reproduzir os experimentos.

### **1\. Clonar o Repositório**

git clone \[https://github.com/SEU-USUARIO/NOME-DO-REPO.git\](https://github.com/SEU-USUARIO/NOME-DO-REPO.git)  
cd NOME-DO-REPO

### **2\. Configurar o Ambiente Virtual (Recomendado)**

\# Linux/macOS  
python3 \-m venv venv  
source venv/bin/activate

\# Windows (PowerShell)  
python \-m venv venv  
.\\venv\\Scripts\\Activate.ps1

### **3\. Instalar Dependências**

Instale as bibliotecas necessárias (Pandas, NumPy, Scikit-learn, FAISS-CPU, etc.):

pip install \-r requirements.txt

## **Configuração do Dataset (CIC-IDS-2018)**

Devido ao tamanho massivo do dataset, os arquivos CSV **não estão incluídos** neste repositório. O código foi configurado para processar os arquivos CSV originais do dataset CIC-IDS-2018.

1. Acesse o site oficial: [CSE-CIC-IDS2018 no AWS](https://www.unb.ca/cic/datasets/ids-2018.html).  
2. Baixe os arquivos CSV correspondentes aos dias de tráfego listados abaixo.  
3. Crie uma pasta chamada dataset dentro do diretório src:  
   mkdir \-p src/dataset

4. Mova os arquivos baixados para src/dataset/. O script espera os seguintes nomes de arquivo:  
* Friday-02-03-2018\_TrafficForML\_CICFlowMeter.csv  
* Friday-16-02-2018\_TrafficForML\_CICFlowMeter.csv  
* Friday-23-02-2018\_TrafficForML\_CICFlowMeter.csv  
* Thursday-01-03-2018\_TrafficForML\_CICFlowMeter.csv  
* Thursday-15-02-2018\_TrafficForML\_CICFlowMeter.csv  
* Thursday-22-02-2018\_TrafficForML\_CICFlowMeter.csv  
* Wednesday-14-02-2018\_TrafficForML\_CICFlowMeter.csv  
* Wednesday-21-02-2018\_TrafficForML\_CICFlowMeter.csv  
* Wednesday-28-02-2018\_TrafficForML\_CICFlowMeter.csv

## **Como Executar**

Com o ambiente configurado e os dados na pasta correta, execute o script principal:

python src/main.py

### **O que o script realiza:**

1. **Carregamento e Limpeza:** Lê os CSVs, sanitiza colunas numéricas e remove cabeçalhos repetidos.  
2. **Engenharia de Features:** Seleciona as 23 features mais relevantes, e gera identificadores únicos de fluxo (Flow\_Label).  
3. **Treinamento:** Utiliza IndexFlatIP do FAISS para indexação vetorial.  
4. **Cenários de Teste (Conforme Artigo):**  
   * *Contribuição:* 70% Treino / 30% Teste.  
   * *Teste 1:* Foco em ataques menos comuns (ex: Brute Force Web, SQL Injection).  
   * *Teste 2:* Treino apenas com ataques majoritários, teste com todos.  
   * *Teste 3:* Simulação de larga escala (10% Treino / 90% Teste).

## **📄 Citação**

Se você utilizar este código ou metodologia em sua pesquisa, por favor cite nosso trabalho:

@inproceedings{errc,
 author = {Nícolas Warmeling and Laura Klippel and Carlo Mantovani and Tiago Ferreto},
 title = { Otimização e Análise Crítica de um Classificador de Ataques de Rede por Similaridade no Dataset CIC-IDS-2018},
 booktitle = {Anais da XXII Escola Regional de Redes de Computadores},
 location = {Porto Alegre/RS},
 year = {2025},
 keywords = {},
 issn = {0000-0000},
 pages = {61--67},
 publisher = {SBC},
 address = {Porto Alegre, RS, Brasil},
 doi = {10.5753/errc.2025.17835},
 url = {https://sol.sbc.org.br/index.php/errc/article/view/39182}
}
