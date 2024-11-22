# 📊 Guia: Download de Dados do BigQuery via Python CLI

[![Python](https://img.shields.io/badge/Python-3.7+-blue.svg)](https://www.python.org)
[![BigQuery](https://img.shields.io/badge/BigQuery-Cloud-yellow.svg)](https://cloud.google.com/bigquery)
[![Windows](https://img.shields.io/badge/Windows-11-blue.svg)](https://www.microsoft.com/windows)
[![VSCode](https://img.shields.io/badge/VSCode-Latest-blue.svg)](https://code.visualstudio.com/)

## 📋 Pré-requisitos

- Conta Google com acesso ao BigQuery
- Python 3.7+
- Windows 11
- Visual Studio Code
- CMD do Windows (não PowerShell)

## 🚀 Passo a Passo

### 1. Instalação do Google Cloud SDK

1. Baixe o instalador do [Google Cloud SDK](https://cloud.google.com/sdk/docs/install#windows)
2. Execute o instalador e marque a opção "Adicionar ao PATH"

### 2. Configuração do Ambiente Python

```bash
# Criar e ativar ambiente virtual
python -m venv venv
venv\Scripts\activate
```

# Instalar dependências
pip install google-cloud-bigquery pandas db-dtypes

### 3. Autenticação no Google Cloud

No CMD (não PowerShell):

```bash
gcloud auth application-default login 
```

### 4. Código Python para Download

```python

from google.cloud import bigquery
import os
# Configurar cliente
client  = bigquery.Client(project='nome_projeto')  

# Query
query  =  """
SELECT *
FROM `basedosdados.br_sfb_sicar.area_imovel`
"""  
# Criar pasta bigdata se não existir
os.makedirs('data', exist_ok=True)
print("Iniciando download...")
try:
	df  =  client.query(query).to_dataframe()

	df.to_csv('data/tabela.csv', index=False)

	print(f"Download concluído! Registros baixados: {len(df)}")

	print("Arquivo salvo em: bigdata/tabela.csv")

except  Exception  as  e:

print(f"Erro: {str(e)}")
```
### 5. Execute no terminal cli o código python
```python 
python -u arquivo.py
```

## ⚠️ Problemas Comuns e Soluções

1.  **Erro de Módulo não Encontrado**
    
    ```bash    
    ModuleNotFoundError: No module named 'google'`
    ```
    
    Solução:  ```pip install google-cloud-bigquery```
2.  **Erro de Credenciais**
    
    DefaultCredentialsError: Your default credentials were not found
    
    Solução: Execute `gcloud auth application-default login`
3.  **Erro db-dtypes**
  
    `Please install the 'db-dtypes' package`
    
    Solução: `pip install db-dtypes`

4. **Aviso do BigQuery Storage API**
   ```bash
   UserWarning: BigQuery Storage module not found, fetch data with the REST endpoint instead    

## 📝 Notas Importantes

-   O tempo de download depende do tamanho da tabela
-   Certifique-se de ter espaço suficiente em disco
-   Use o CMD do Windows, não o PowerShell
-   A query pode ser obtida diretamente do console do BigQuery

## 👨‍💻 Autor

**Nome:** Aluno Santander Coders  
**Email:** [teophilo@gmail.com](mailto:teophilo@gmail.com)  
**Projeto:** Engenharia de Dados - Trilha Big Data  
**Instituições:** Santander Coders & Ada Tech

## 📚 Documentação Adicional

-   [Google Cloud SDK](https://cloud.google.com/sdk/docs)
-   [BigQuery Python API](https://googleapis.dev/python/bigquery/latest/index.html)
-   [Pandas Documentation](https://pandas.pydata.org/docs/)

## 🤝 Contribuições

Sinta-se à vontade para contribuir com melhorias neste guia através de Pull Requests.

## 📄 Licença

Este projeto está sob a licença MIT.