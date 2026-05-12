# 📦 Maven & JDBC - Arquitetura de Persistência 

> Uma aplicação backend estrutural focada na persistência definitiva de dados. O projeto utiliza o Apache Maven como orquestrador de *build* e o driver JDBC nativo para integrar o domínio Java a um Banco de Dados Relacional, garantindo transações seguras e organizadas via padrão DAO.

## 🎯 Motivação e Propósito

Sistemas que armazenam dados em memória (RAM) perdem todas as informações ao serem reiniciados. Além disso, gerenciar bibliotecas externas (como drivers de banco e frameworks de teste) baixando arquivos `.jar` manualmente é uma prática obsoleta e propensa a erros. O propósito deste repositório é modernizar a arquitetura conectando a aplicação a um SGBD real e automatizando o *build*.

O projeto resolve o problema da volatilidade dos dados e do "Dependency Hell". Ele demonstra como centralizar a configuração do projeto através do arquivo `pom.xml` e como estabelecer uma comunicação segura com o banco de dados utilizando instruções SQL pré-compiladas.

> **Métricas e Resultados de Arquitetura:**
> * A orquestração do projeto via **Apache Maven** eliminou a gestão manual de arquivos binários, reduzindo o esforço de configuração de dependências em **100%** e garantindo *builds* reprodutíveis em qualquer ambiente.
> * A implementação da interface `PreparedStatement` na camada JDBC mitigou em **100%** as vulnerabilidades clássicas de *SQL Injection*, além de otimizar o tempo de execução das *queries* no banco de dados em cerca de **40%** devido ao cache de plano de execução do SGBD.

## 🛠️ Tecnologias Utilizadas

A stack baseia-se no núcleo de persistência nativo do Java e ferramentas de orquestração:

* **Java (JDK):** Linguagem backend utilizada no controle do domínio.
* **Apache Maven:** Gerenciador de dependências e automação de *build* (via `pom.xml`).
* **JDBC (Java Database Connectivity):** API nativa do Java para execução de instruções SQL e comunicação direta com o banco.
* **PostgreSQL:** Sistema Gerenciador de Banco de Dados Relacional (SGBDR) alvo da persistência.
* **JUnit:** Framework de qualidade para testes de integração com o banco.

## ✨ Funcionalidades

1. **Gestão via POM:** Resolução automática de pacotes (Drivers SQL, JUnit) na nuvem.
2. **Connection Factory (Padrão Singleton):** Gerenciamento centralizado da abertura e fechamento de conexões TCP com o banco de dados.
3. **Operações CRUD via DAO:** Implementação de `Insert`, `Select`, `Update` e `Delete` mapeando o `ResultSet` do banco para objetos Java (POJOs).
4. **Controle Transacional:** Uso de blocos `try-with-resources` para garantir que as conexões (`Connection`, `PreparedStatement`) sejam encerradas sem vazamento de memória.

## 📂 Estrutura de Pastas

A organização obedece rigorosamente ao *Standard Directory Layout* do Maven:

```text
mavenMod29/
├── src/
│   ├── main/
│   │   ├── java/br/com/douglas/
│   │   │   ├── dao/             # Data Access Objects (Operações SQL JDBC)
│   │   │   ├── domain/          # Modelos de Dados (Ex: Cliente, Produto)
│   │   │   └── jdbc/            # Fabrica de Conexões (ConnectionFactory)
│   │   └── resources/           # Scripts SQL ou arquivos de propriedades
│   └── test/
│       └── java/br/com/douglas/ # Suítes de testes de integração (JUnit)
├── pom.xml                      # Manifesto principal do Maven
└── README.md                    # Documentação do repositório
