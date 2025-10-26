# 🧪 Relatório de Testes — GraphQL Countries API

## 🔗 Coleção no Postman
[🔗 Acessar no Postman](https://www.postman.com/darir0/workspace/teste-de-api/collection/37063479-aa82ae3b-2b6c-4087-a1dc-a16c607e1cc0?action=share&creator=37063479&active-environment=37063479-e7294626-e190-41f4-92a4-9ff6d2356a7b)

---

## 🧭 Visão Geral

A **GraphQL Countries API** é uma API pública hospedada em:
> **https://countries.trevorblades.com/**

Ela fornece informações sobre países, continentes e idiomas, permitindo explorar relações entre esses dados através de queries GraphQL.

Os testes foram realizados utilizando o **Postman**, cobrindo tanto **consultas simples** (unitárias) quanto **consultas compostas** com variáveis dinâmicas.  
Foram aplicados **testes manuais e automatizados (Postman Tests Scripts)** para validar o comportamento da API e a integridade das respostas.

---

## ⚙️ Configuração da Requisição

**Método:** `POST`  
**Endpoint:** `https://countries.trevorblades.com/`  
**Header:**  
```
Content-Type: application/json
```

**Formato GraphQL usado nos testes:**
```graphql
query getCountry($code: ID!) {
  country(code: $code) {
    name
    native
    emoji
    currency
    languages {
      code
      name
    }
  }
}
```

**Variables:**
```json
{
  "code": "BR"
}
```

---

## ✅ Cenários de Teste Executados

| ID | Cenário | Objetivo | Resultado |
|----|----------|-----------|-----------|
| TC01 | Consulta país por código (`getCountry`) | Validar se a API retorna corretamente os dados de um país específico (BR) | ✅ Sucesso |
| TC02 | Consulta países por continente (`getCountriesByContinent`) | Verificar se países da América do Sul são retornados corretamente | ✅ Sucesso |

---

## 🧩 Testes Automatizados (Scripts Postman)

Os seguintes testes foram implementados no Postman, utilizando a aba **Tests**:

```javascript
pm.test("Status code is 200", () => {
  pm.response.to.have.status(200);
});

const json = pm.response.json();

pm.test("Country object exists", () => {
  pm.expect(json.data.country).to.be.an("object");
});

pm.test("Country name matches 'Brazil'", () => {
  pm.expect(json.data.country.name).to.eql("Brazil");
});

pm.test("Currency field is a non-empty string", () => {
  pm.expect(json.data.country.currency).to.be.a("string").and.not.be.empty;
});

pm.test("Languages list is an array and not empty", () => {
  pm.expect(json.data.country.languages).to.be.an("array").and.have.lengthOf.above(0);
});
```

---

## 📋 Validações realizadas

| Tipo de Validação | Descrição | Resultado |
|-------------------|------------|------------|
| **Status HTTP** | Retorno `200 OK` em todas as queries | ✅ |
| **Tempo de resposta** | Abaixo de 500ms em todas as requisições | ✅ |
| **Headers** | `Content-Type: application/json` validado | ✅ |
| **Corpo da resposta** | Estrutura conforme schema GraphQL esperado | ✅ |
| **Campos obrigatórios** | `name`, `native`, `emoji`, `currency`, `languages` presentes | ✅ |

---

## 🧱 Estrutura dos Dados

Exemplo de resposta obtida para o código `"BR"`:

```json
{
  "data": {
    "country": {
      "name": "Brazil",
      "native": "Brasil",
      "emoji": "🇧🇷",
      "currency": "BRL",
      "languages": [
        {
          "code": "pt",
          "name": "Portuguese"
        }
      ]
    }
  }
}
```

---

## 🧪 Conclusão

Os testes mostraram que a **Countries GraphQL API**:
- Retorna dados consistentes e bem estruturados.
- É estável e responde rapidamente (< 500 ms).
- Possui schema padronizado, ideal para estudos e automação de testes GraphQL.

✅ **Resultado Final:** Todos os cenários passaram com sucesso.

---

**Autor:** Miguel Luis  
**Data de execução:** 26/10/2025  
**Ferramentas:** Postman, GraphQL, JavaScript (test scripts)
