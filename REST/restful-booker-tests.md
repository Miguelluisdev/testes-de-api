# Relatório de Testes – API Restful Booker

## 1. Visão Geral

Este relatório descreve os testes realizados na **API Restful Booker**, com foco na validação funcional, contrato, integração e integridade de dados. Os testes foram executados manualmente e com suporte à automação utilizando **Postman**.

* **API:** Restful Booker
* **Objetivo:** Validar o correto funcionamento dos principais endpoints da API
* **Testador:** Miguel Luis
* **Ferramenta:** Postman

---

## 2. Escopo dos Testes

### Testes Realizados

* ✅ Testes funcionais (requisições válidas)
* ✅ Testes de contrato
* ✅ Testes de integração
* ✅ Testes de integridade de dados

### Testes Não Realizados

* ❌ Testes de performance
* ❌ Testes de PATCH

---

## 3. Ambiente de Testes

* **Ferramenta de testes:** Postman
* **Tipo de API:** REST
* **Formato de dados:** JSON
* **Ambiente:** Público (Heroku)

### Documentação da API

* [https://restful-booker.herokuapp.com/apidoc/index.html](https://restful-booker.herokuapp.com/apidoc/index.html)

### Collections e Environments utilizados

* Collection:

  * [https://github.com/Miguelluisdev/testes-de-api/blob/main/REST/RestFul-booker.postman_collection.json](https://github.com/Miguelluisdev/testes-de-api/blob/main/REST/RestFul-booker.postman_collection.json)
* Environment:

  * [https://github.com/Miguelluisdev/testes-de-api/blob/main/REST/Restful-booker.postman_environment.json](https://github.com/Miguelluisdev/testes-de-api/blob/main/REST/Restful-booker.postman_environment.json)

---

## 4. Resultados dos Testes

### 4.1 Testes Funcionais

* A API aceita corretamente dados válidos nos endpoints testados.
* Respostas retornam os status HTTP esperados para cenários positivos.

**Status:** ✅ Aprovado

---

### 4.2 Testes de Contrato

* Estrutura das respostas (campos, tipos e obrigatoriedade) está de acordo com a documentação.
* Não foram identificadas quebras de contrato.

**Status:** ✅ Aprovado

---

### 4.3 Testes de Integração

* Comunicação entre endpoints ocorre conforme esperado.
* Fluxos dependentes (ex: autenticação → criação → consulta) funcionam corretamente.

**Status:** ✅ Aprovado

---

### 4.4 Testes de Integridade de Dados

* Dados criados, consultados e validados mantêm consistência.
* Não foram identificadas corrupções ou inconsistências nos dados retornados.

**Status:** ✅ Aprovado

---

## 5. Problemas Encontrados

### 5.1 Problemas nos Endpoints PUT e DELETE

* Os endpoints **PUT** e **DELETE** retornam **erro 403 – Forbidden** durante os testes.
* O problema ocorre mesmo após a atualização correta do token de autenticação.
* O erro está relacionado à **autenticação do usuário**.

### Observação Importante

* Quando são utilizados exatamente os dados e exemplos fornecidos na **documentação oficial da API**, as rotas **PUT** e **DELETE** funcionam corretamente.
* Entretanto, durante a execução de testes e automações (Postman), o comportamento se torna **instável**.

### Impacto

* Dificulta a automação confiável dos testes.
* Compromete a previsibilidade dos testes de atualização e remoção de dados.

---

### 5.2 Endpoint PATCH

* O endpoint **PATCH** não foi testado.

**Status:** ⚠️ Pendente

---

## 6. Testes de Performance

* Testes de performance **não foram realizados**.

**Status:** ❌ Não executado

---

## 7. Conclusão

De forma geral, a **API Restful Booker apresenta bom funcionamento** nos cenários testados, especialmente nos testes funcionais, de contrato, integração e integridade de dados.

No entanto, foram identificados **problemas críticos de autenticação** nos endpoints **PUT** e **DELETE**, que resultam em erro 403 durante testes e automações, apesar de funcionarem corretamente quando utilizados exatamente conforme a documentação.

Esses problemas tornam a automação instável e indicam possíveis inconsistências no mecanismo de autenticação ou validação de token da API.

---

## 8. Recomendações

* Investigar e corrigir o fluxo de autenticação para PUT e DELETE.
* Realizar testes no endpoint PATCH.
* Implementar testes de performance.
* Melhorar a estabilidade da API para uso em testes automatizados.

---

**Relatório elaborado por:** Miguel Luis
**Ferramenta:** Postman

