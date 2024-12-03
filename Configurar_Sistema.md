# PROJETO BIG DATA

![Imagem do Projeto](https://via.placeholder.com/800x200.png)

## Descrição

Este projeto faz parte da trilha de dados Big Data do curso de Engenharia de Dados do programa Santander Coders 2024 em parceria com a Ada Tech. Nosso objetivo é criar uma arquitetura robusta para operar em um arquivo CSV de aproximadamente 2GB de dados, realizando operações de ETL (Extract, Transform, Load) utilizando PySpark e outras tecnologias de Big Data.

## Tecnologias Utilizadas

![Python](https://img.shields.io/badge/Python-3.10-blue)
![PySpark](https://img.shields.io/badge/PySpark-3.5.0-red)
![pandas](https://img.shields.io/badge/pandas-2.2.3-green)
![matplotlib](https://img.shields.io/badge/matplotlib-3.9.2-yellow)

## Ambiente de Desenvolvimento

- **Sistema Operacional:** Windows 11
- **IDE:** Visual Studio Code com a extensão Jupyter Notebook
- **Python:** 3.10 (em ambiente virtual)

## Equipe do Projeto

- **Teophilo Silva**
- **Igor Jasmim**
- **Matheus**
- **Leandro**

**Professor:** Igor Garcia

## Instalação das Bibliotecas Necessárias

Para garantir o correto funcionamento do ambiente de desenvolvimento, as seguintes bibliotecas e versões foram utilizadas:

- **pandas:** 2.2.3
- **matplotlib:** 3.9.2
- **Spark:** 3.5.0

Além disso, temos as seguintes ferramentas instaladas localmente:

- **Hadoop**
- **Hive**
- **Spark**

### Caminhos Locais das Ferramentas

Os caminhos das ferramentas instaladas localmente são:

- **SPARK_HOME:** `C:/spark`
- **HADOOP_HOME:** `C:/hadoop`
- **HIVE_HOME:** `C:/hive`

### Baixando e Instalando as Ferramentas

#### Spark

Você pode baixar o Apache Spark do site oficial: [Apache Spark Download](https://spark.apache.org/downloads.html)

1. Escolha a versão apropriada para seu sistema operacional.
2. Extraia os arquivos baixados para `C:/spark`.

#### Hadoop

O Apache Hadoop está disponível para download no site oficial: [Apache Hadoop Download](https://hadoop.apache.org/releases.html)

1. Escolha a versão apropriada para seu sistema operacional.
2. Extraia os arquivos baixados para `C:/hadoop`.

#### Hive

O Apache Hive pode ser baixado no site oficial: [Apache Hive Download](https://hive.apache.org/downloads.html)

1. Escolha a versão apropriada para seu sistema operacional.
2. Extraia os arquivos baixados para `C:/hive`.

### Configuração dos Arquivos

#### Configurando o arquivo `.env`

Certifique-se de que seu arquivo `.env` na raiz do projeto contenha o seguinte:

```env
SPARK_HOME=C:/spark
HADOOP_HOME=C:/hadoop
HIVE_HOME=C:/hive
PATH=%SPARK_HOME%/bin;%HADOOP_HOME%/bin;%PATH%;%HIVE_HOME%/bin
```

## Importância da Configuração do Spark
A configuração da sessão do Spark é crucial para otimizar o processamento de grandes volumes de dados em um ambiente local. Utilizamos diversas configurações para ajustar o desempenho do Spark, incluindo alocação de memória, suporte ao Hive, e ajustes para o Spark Arrow e Adaptive Query Execution.

## Leitura do Arquivo CSV com Spark
Para ler o arquivo CSV de forma eficiente e evitar erros de formatação, é essencial definir corretamente o separador (neste caso, ponto e vírgula).

```python
df_spark = spark.read.csv(
     csv_path, 
     sep=';', # Define o separador como ponto e vírgula 
     header=True, # Indica que o CSV contém cabeçalhos
     inferSchema=True, # Tenta inferir automaticamente o tipo das colunas 
     encoding='utf-8' # Define a codificação do arquivo
)
```
## Configuração do Ambiente para Spark, Hadoop e Hive

Para configurar o ambiente localmente para utilizar Spark, Hadoop e Hive, siga as instruções abaixo:

### 1. Baixando e Instalando as Ferramentas

#### Spark

Você pode baixar o Apache Spark do site oficial: [Apache Spark Download](https://spark.apache.org/downloads.html)

1. Escolha a versão apropriada para seu sistema operacional.
2. Extraia os arquivos baixados para `C:/spark`.

#### Hadoop

O Apache Hadoop está disponível para download no site oficial: [Apache Hadoop Download](https://hadoop.apache.org/releases.html)

1. Escolha a versão apropriada para seu sistema operacional.
2. Extraia os arquivos baixados para `C:/hadoop`.

#### Hive

O Apache Hive pode ser baixado no site oficial: [Apache Hive Download](https://hive.apache.org/downloads.html)

1. Escolha a versão apropriada para seu sistema operacional.
2. Extraia os arquivos baixados para `C:/hive`.

### 2. Configuração das Variáveis de Ambiente

Adicione os seguintes caminhos às variáveis de ambiente do sistema:

#### SPARK_HOME
```sh
setx SPARK_HOME "C:/spark"
```

#### HADOOP_HOME
```sh
setx HADOOP_HOME "C:/hadoop"
```

#### HIVE_HOME
```sh
setx HIVE_HOME "C:/hive"
```

## Atualizando a Variável PATH
Adicione os caminhos das ferramentas à variável PATH para garantir que elas sejam reconhecidas:
```sh
setx PATH "%SPARK_HOME%/bin;%HADOOP_HOME%/bin;%HIVE_HOME%/bin;%PATH%"
```

# 3. Verificando as Instalações
Para verificar se as ferramentas foram instaladas e configuradas corretamente, execute os seguintes comandos no PowerShell:

## Verificar a Versão do Spark
```sh
spark-submit --version
```
## Verificar a Versão do Hadoop
```sh
hadoop version
```
## Verificar a Versão do Hive
```sh
hive --version
```
## Análise de Dados com Hive

Utilizamos Hive SQL para realizar operações de análise no DataFrame. Essas operações nos permitem entender melhor a qualidade dos dados e identificar problemas comuns, como dados nulos, vazios e duplicados.

### Operações Realizadas

#### Total de Linhas

Calculamos o total de linhas no DataFrame para entender a dimensão dos dados.

```sql
SELECT COUNT(*) AS total_linhas FROM temas_ambientais
```
## Linhas Nulas
Identificamos as linhas onde todas as colunas têm valores nulos. Isso é útil para identificar registros que podem ser descartados ou que necessitam de correção.
```sql
SELECT COUNT(*) AS linhas_nulas FROM temas_ambientais WHERE coluna1 IS NULL AND coluna2 IS NULL AND ...

```
## Linhas vazias
Para identificar linhas duplicadas baseadas em uma coluna específica (registro_car), utilizamos a seguinte consulta SQL:
```sql
SELECT COUNT(*) - COUNT(DISTINCT registro_car) AS linhas_duplicadas FROM temas_ambientais
```
## Linhas Duplicadas por Grupo
Para identificar e exibir linhas duplicadas agrupadas pela coluna UF e contando data_ultima_retificacao, utilizamos a seguinte consulta SQL:
```sql
SELECT COUNT(*) - COUNT(DISTINCT registro_car) AS linhas_duplicadas FROM temas_ambientais"
```
### Essas operações com Hive SQL são essenciais para a limpeza e preparação dos dados, permitindo uma análise mais precisa e confiável.

# Instalação do Hadoop no Windows 11

Show Image Show Image Show Image

## Pré-requisitos

-   Windows 11
-   Java Development Kit (JDK) 8
-   Visual Studio Code (opcional)
-   7-Zip (para descompactação)

## Passos de Instalação

### 1. Instalação do Java

1.  Baixar JDK 8

    URL: https://download.oracle.com/otn/java/jdk/8u351-b10/jdk-8u351-windows-x64.exe

2.  Criar pasta de instalação

    Caminho: C:\java

3.  Configurar Variáveis de Ambiente

    Variáveis do Sistema:

-   `JAVA_HOME`: `C:\java\jdk1.8.0_351\bin`
-   Adicionar ao PATH: `C:\java\jdk1.8.0_351\bin`

### 2. Instalação do Hadoop

1.  Baixar Hadoop 3.2.4

URL: https://archive.apache.org/dist/hadoop/common/hadoop-3.2.4/hadoop-3.2.4.tar.gz

2.  Descompactar no Terminal como Administrador

```cmd
tar -xf "caminho_do_arquivo.tar.gz" -C "C:\"
```
3.  Renomear pasta

`De: C:\hadoop-3.2.4 Para: C:\hadoop`

4.  Configurar Variáveis de Ambiente

-   `HADOOP_HOME`: `C:\hadoop\bin`
-   Adicionar ao PATH: `C:\hadoop\bin`

### 3. Configurações Adicionais

## Arquivos de Configuração

1.  hadoop-env.cmd

```set JAVA_HOME=%JAVA_HOME%```

2.  core-site.xml

```xml
<configuration>
   <property>
    <name>fs.default.name</name> 
    <value>hdfs://localhost:9000</value>
   </property> </configuration>
```
3.  `hdfs-site.xml`

```xml

<configuration>
   <property>
    <name>dfs.replication</name>
     <value>1</value>
   </property>
   <property>
    <name>dfs.namenode.name.dir</name>
     <value>C:/hadoop/data/namenode</value>
   </property>
   <property>
    <name>dfs.datanode.data.dir</name>
     <value>C:/hadoop/data/datanode</value>
   </property>
</configuration>
```

### 4. Arquivos Complementares

1.  Baixar `winutils.exe`

    URL: https://drive.google.com/file/d/1nCN_jK7EJF2DmPUUxgOggnvJ6k6tksYz/view

2.  Baixar `MSVCR120.DLL`


    Destino: C:\Windows\System32

    URL: https://pt.dll-files.com/download/b70474fe249402e251a94753b742788c/msvcr120.dll.html

3.  Instalar Pacote Redistribuível do Microsoft Visual C++

    URL: https://aka.ms/vs/17/release/vc_redist.x64.exe

### 5. Inicialização do Hadoop

1.  Formatar NameNode

```cmd
hdfs namenode -format
```

2.  Iniciar Serviços DFS

```cmd
cd hadoop/sbin
.\start-dfs.cmd
```

3.  Iniciar YARN

```cmd
.\start-yarn.cmd
```

## Verificação da Instalação

1.  Verificar Java

```cmd
java -version
```

2.  Verificar Hadoop

```cmd
hadoop version
```

## Solução de Problemas

-   Certifique-se de executar comandos como Administrador
-   Verifique as configurações de variáveis de ambiente
-   Confirme a instalação correta de todos os componentes

## Referências

-   [Documentação Apache Hadoop](https://hadoop.apache.org/docs/)
-   [Guia de Instalação Hadoop no Windows](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-common/WindowsProblems.html)

----------

📌 **Nota**: Este guia é específico para Hadoop 3.2.4 no Windows 11 e requer atenção aos detalhes durante a instalação.

C












