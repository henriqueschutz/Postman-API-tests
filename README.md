# 📚 Testes Automatizados de API - Books (Collection EBAC)

Este repositório contém a suíte de testes E2E (End-to-End) desenvolvida no **Postman** para validar os endpoints da API de gerenciamento de livros (`/api/books`).

## 🚀 Tecnologias Utilizadas

* **Node.js / Express** (API REST)
* **SQLite** (Banco de dados relacional)
* **Postman** (Execução e asserções dos testes de API)
* **Newman** *(opcional, para execução via linha de comando/CI)*

---

## 📋 Pré-requisitos

1. **API rodando localmente:**
   Certifique-se de que o servidor da API esteja ativo na porta `3000` (`http://localhost:3000/api`).
   ```bash
   npm install
   npm start
   ```
2. **Postman instalado** em sua máquina (ou via Web com Desktop Agent).

---

## 🛠️ Como Importar e Executar no Postman

1. Abra o **Postman** e clique no botão **Import** (no canto superior esquerdo).
2. Selecione o arquivo `.json` da collection exportada neste repositório.
3. Configure a variável de ambiente ou da collection:
   * **`baseUrl`**: `http://localhost:3000/api/`
4. Para rodar todos os testes em sequência (fluxo E2E):
   * Clique nos três pontinhos (`...`) ao lado do nome da collection (**Collection EBAC**).
   * Selecione **Run** (ou *Run collection*).
   * Clique em **Run Collection EBAC** e acompanhe os resultados das asserções.

---

## 🧪 Cenários Cobertos

* **Listagem e Ordenação (`GET /books`):** Valida filtros de disponibilidade, paginação (`limit` e `offset`) e ordenação crescente/decrescente por `id`.
* **Criação de Livro (`POST /books`):** Valida o cadastro com dados dinâmicos (`{{$random...}}`), status code `201 Created`, mensagem de retorno e persistência determinística no **ID 5** para garantir a estabilidade do fluxo E2E.
* **Consulta, Atualização e Exclusão (`GET / PUT / DELETE`):** Valida o ciclo de vida completo do registro criado durante a execução.

---

## ⚙️ Ajustes Realizados na API para Suporte aos Testes E2E

Para permitir a execução determinística da suíte de testes sem falhas de ordenação ou conflitos de chave primária:
1. **`GET /api/books`:** Adicionado suporte ao parâmetro `orderBy=id` na lista de ordenação permitida (`validOrderBy`).
2. **`POST /api/books`:** Habilitado o envio opcional de `id` no payload e ajustada a query SQL para `INSERT OR REPLACE`, garantindo que o livro de teste seja sempre criado/atualizado no **ID 5**.
