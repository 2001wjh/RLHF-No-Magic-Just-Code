---
license: cc-by-4.0
task_categories:
- text-generation
- question-answering
- table-question-answering
language:
- en
tags:
- SQL
- code
- NLP
- text-to-sql
- context-sql
- spider
- wikisql
- sqlglot
pretty_name: sql-create-context
size_categories:
- 10K<n<100K
---

#### Overview
This dataset builds from [WikiSQL](https://huggingface.co/datasets/wikisql) and [Spider](https://huggingface.co/datasets/spider).

There are 78,577 examples of natural language queries, SQL CREATE TABLE statements, and SQL Query answering the question using the CREATE statement as context. This dataset was built with text-to-sql LLMs in mind, intending to prevent hallucination of column and table names often seen when trained on text-to-sql datasets. The CREATE TABLE statement can often be copy and pasted from different DBMS and provides table names, column names and their data types. By providing just the CREATE TABLE statement as context, we can hopefully provide better grounding for models without having to provide actual rows of data, limiting token usage and exposure to private, sensitive, or proprietary data.

#### Cleansing and Augmentation
Cleansing and data augmentation has been done on the combined WikiSQL and Spider data. I used [SQLGlot](https://github.com/tobymao/sqlglot) on queries from Spider and WikiSQL and parsed them into different tables and columns, I then inferred column data types based on usage of `>` `<` operators as well as the use of `MIN()` `MAX()` `AVG()` `SUM()` on columns. While this isn't perfect, it increases the likelihood of inferring the correct datatype for a column, the columns otherwise default to VARCHAR type. These tables and columns are then used to generate CREATE TABLE statements using the inferred types. SQLGlot is used again to ensure both the SQL queries and CREATE TABLE statements parse without errors.

Some queries that do not have column names, e.g. SELECT * FROM table, have a default Id column added to the CREATE TABLE statement. Some other queries which use the generic `table` as the FROM table have instead been changed to a variation of `table_name_1` or some other number which is also reflected in the CREATE TABLE statement. 

#### TODO
- Further augment the data by converting queries and CREATE TABLE statements into different SQL dialects, this can be done with SQLGlot. Reference to the dialect might also be added to the question.
- Support other informative contexts beyond CREATE TABLE
- Better parse datatypes to clean up things like numbers for column names and other numbers as strings

If you have any edits you'd like to see in a version 2 of this dataset, let me know.

Random sample:
```json
  {
    "question": "Please show the themes of competitions with host cities having populations larger than 1000.",
    "context": "CREATE TABLE city (City_ID VARCHAR, Population INTEGER); CREATE TABLE farm_competition (Theme VARCHAR, Host_city_ID VARCHAR)",
    "answer": "SELECT T2.Theme FROM city AS T1 JOIN farm_competition AS T2 ON T1.City_ID = T2.Host_city_ID WHERE T1.Population > 1000"
  },
  {
    "question": "Please show the different statuses of cities and the average population of cities with each status.",
    "context": "CREATE TABLE city (Status VARCHAR, Population INTEGER)",
    "answer": "SELECT Status, AVG(Population) FROM city GROUP BY Status"
  },
```


#### Citing this work

```TeX
@misc{b-mc2_2023_sql-create-context,
  title   = {sql-create-context Dataset},
  author  = {b-mc2}, 
  year    = {2023},
  url     = {https://huggingface.co/datasets/b-mc2/sql-create-context},
  note    = {This dataset was created by modifying data from the following sources: \cite{zhongSeq2SQL2017, yu2018spider}.},
}
```

#### Datasets used to create this dataset

```TeX
@article{zhongSeq2SQL2017,
  author  = {Victor Zhong and Caiming Xiong and Richard Socher},
  title   = {Seq2SQL: Generating Structured Queries from Natural Language using Reinforcement Learning},
  journal = {CoRR},
  volume  = {abs/1709.00103},
  year    = {2017}
}

@article{yu2018spider,
  title   = {Spider: A large-scale human-labeled dataset for complex and cross-domain semantic parsing and text-to-sql task},
  author  = {Yu, Tao and Zhang, Rui and Yang, Kai and Yasunaga, Michihiro and Wang, Dongxu and Li, Zifan and Ma, James and Li, Irene and Yao, Qingning and Roman, Shanelle and others},
  journal = {arXiv preprint arXiv:1809.08887},
  year    = {2018}
}
```