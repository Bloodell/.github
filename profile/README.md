# Bloodell

> Plataforma para gestão, distribuição e monitoramento de hemocomponentes na rede de sangue.

## Sobre o projeto

O Bloodell é uma aplicação web desenvolvida para apoiar a gestão e distribuição de hemocomponentes na rede de sangue.

O sistema busca integrar diferentes etapas do processo, desde o gerenciamento de estoque e recebimento de requisições hospitalares até a alocação de bolsas compatíveis, priorização por validade (FEFO), roteirização de entregas e monitoramento da cadeia fria.

A solução é inspirada no fluxo da Hemorrede/SUS, contemplando centros de coleta e doação, hemocentros de processamento e controle, estoques e hospitais.

Todos os dados utilizados no projeto são sintéticos, não envolvendo informações reais de doadores ou pacientes.

> **Aviso:** a compatibilidade ABO/Rh implementada no projeto possui finalidade exclusivamente didática e não substitui protocolos clínicos ou sistemas oficiais da Hemorrede/SUS.

---

## Problema

A rede de sangue precisa garantir que o componente correto seja disponibilizado:

* para o paciente adequado;
* no hospital correto;
* dentro do tempo necessário;
* mantendo as condições adequadas de armazenamento e transporte.

Falhas nesse processo podem contribuir para desabastecimento, descarte de hemocomponentes por vencimento e dificuldades na distribuição.

O Bloodell busca centralizar essas informações e auxiliar na tomada de decisões relacionadas ao estoque, compatibilidade e distribuição.

---

## Solução

A plataforma será responsável por integrar:

* gestão de estoque de hemocomponentes;
* requisições hospitalares;
* compatibilidade ABO/Rh;
* priorização por validade utilizando FEFO (First Expired, First Out);
* roteirização de entregas;
* monitoramento da cadeia fria;
* simulação de localização e telemetria;
* indicadores de estoque e demanda.

---

## Arquitetura

O projeto está dividido em dois repositórios independentes:

```text
                    Bloodell
                       │
             ┌─────────┴─────────┐
             │                   │
             ▼                   ▼
          Front-end           Back-end
             │                   │
             │                   │
             └─────── API ───────┘
                         │
                         ▼
                   Banco de Dados
```

### Back-end

Desenvolvido em Java com Spring Boot, responsável pela API REST, regras de negócio, processamento dos dados e comunicação com o banco de dados.

Repositório: [Bloodell Backend](#)

### Front-end

Interface responsável pela interação dos usuários com o sistema e consumo da API disponibilizada pelo back-end.

Repositório: [Bloodell Frontend](#)

---

## Tecnologias

### Back-end

* Java
* Spring Boot
* API REST (padrão `/api/v1`)
* Maven
* Spring Data JPA

### Front-end

* React
* Vite
* TypeScript

### Banco de dados

* PostgreSQL

### Infraestrutura

* Docker e Docker Compose
* GitHub Actions (CI/CD)
* Nginx (proxy reverso com TLS na borda pública)

### Ferramentas

* Git
* GitHub

---

## Entregas

### Entrega 01

**Data:** 31/08
**Status:** Concluído

**Descrição:** levantamento das histórias de usuário do projeto, claras, concisas e completas, com detalhes de negócio na descrição e cenários de validação em BDD.

**Artefatos**

* Documentação: [Histórias de Usuário](https://github.com/gabrielgandrade/Bloodell_Historias_De_Usuario)
* Documentação: [Personas](https://github.com/gabrielgandrade/Bloodell_Personas)
* Protótipo Lo-Fi: [Figma](https://www.figma.com/make/LA6ILypFBbqo9QBfuR6eeG/High-Fidelity-Web-App-Prototype?code-node-id=0-6&fullscreen=1)

### Entrega 02

**Data prevista:** 21/09
**Status:** A definir

**Descrição:** a definir.

**Artefatos**

* [Documentação](#)
* [Apresentação](#)
* [Screenshots](#)
* [Outros artefatos](#)

### Entrega 03

**Status:** A definir

**Descrição:** a definir.

**Artefatos**

* [Documentação](#)
* [Apresentação](#)
* [Screenshots](#)
* [Outros artefatos](#)

---

## Contexto acadêmico

O Bloodell é um projeto interdisciplinar que integra conhecimentos de diferentes áreas do curso.

Entre as principais competências trabalhadas estão:

* programação orientada a objetos;
* desenvolvimento de APIs REST;
* estruturas de dados;
* grafos e caminhos mínimos;
* filas de prioridade;
* hash;
* compatibilidade e matching;
* estatística descritiva;
* probabilidade;
* concorrência;
* CI/CD;
* computação em nuvem;
* arquitetura de redes;
* telemetria;
* trabalho em equipe e integração entre áreas.

---

## Limitações e cuidados

* O projeto utiliza exclusivamente dados sintéticos.
* Não serão utilizadas informações reais de pacientes ou doadores.
* A telemetria de temperatura e GPS será simulada.
* A compatibilidade ABO/Rh possui finalidade exclusivamente didática.
* O sistema não substitui protocolos médicos ou sistemas oficiais.
* Não haverá integração com sistemas oficiais da Hemorrede/SUS.
* O grafo utilizado para roteirização terá tamanho limitado.
* As condições da cadeia fria serão simuladas para fins acadêmicos.

---

## Equipe

| Nome             | E-mail CESAR School                           |
| ---------------- | --------------------------------------------- |
| Alisson Santana  | [ass6@cesar.school](mailto:ass6@cesar.school) |
| Arthur Abelardo  | [aacc@cesar.school](mailto:aacc@cesar.school) |
| Carlos Henrique  | [chcf@cesar.school](mailto:chcf@cesar.school) |
| Danilo Diniz     | [dgds@cesar.school](mailto:dgds@cesar.school) |
| Gabriel Andrade  | [gga3@cesar.school](mailto:gga3@cesar.school) |
| Roberto Henrique | [rhcf@cesar.school](mailto:rhcf@cesar.school) |

---

## Repositórios

| Repositório           | Descrição                                    |
| ---------------------- | --------------------------------------------- |
| Bloodell               | Página principal e documentação do projeto    |
| Bloodell Backend       | API e regras de negócio em Java/Spring Boot   |
| Bloodell Frontend      | Interface web da aplicação                    |

---

## Licença

A definir.
