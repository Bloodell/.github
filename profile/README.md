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

Repositório: [Bloodell Backend](https://github.com/Bloodell/bloodell-backend)

### Front-end

Interface responsável pela interação dos usuários com o sistema e consumo da API disponibilizada pelo back-end.

Repositório: [Bloodell Frontend](https://github.com/Bloodell/bloodell-frontend)

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

**Data:** 19/10 (prorrogada para 23/10)
**Status:** Concluída

**Descrição:** implementação de ponta a ponta de duas histórias de usuário da Entrega 01, a **US05** e a **US06**: API REST com PostgreSQL, telas na interface web e testes automatizados (unitários, de integração e de aceitação em Gherkin). Tudo roda em container e é publicado automaticamente na AWS a cada merge na `main`.

**Sistema no ar:** [https://34.235.158.105](https://34.235.158.105) · [saúde da API](https://34.235.158.105/actuator/health)

#### Histórias implementadas

<p align="center">
  <img src="assets/postit-us05.svg" width="380" alt="Post-it US05: Como Técnico de Hemoterapia, quero ver as bolsas organizadas por tipo sanguíneo e hemocomponente, para acompanhar o estoque e identificar reposição e risco de vencimento.">
  <img src="assets/postit-us06.svg" width="380" alt="Post-it US06: Como responsável pelas solicitações do hospital, quero registrar uma requisição com hemocomponente, quantidade e prioridade, para que o hemocentro organize o atendimento.">
</p>

##### US05 · Visualizar e controlar o estoque

> **Como** Técnico de Hemoterapia, **quero** visualizar as bolsas disponíveis organizadas por tipo sanguíneo e hemocomponente **para** acompanhar a situação do estoque e identificar necessidades de reposição ou riscos de vencimento.
>
> 🔴 Must Have · Persona: Técnico de Hemoterapia

| Cenário BDD (Entrega 01) | Como foi atendido | Onde ver |
| --- | --- | --- |
| Visualização do estoque | A doação registrada gera as bolsas, com validade calculada por componente, e elas entram no estoque. As bolsas podem ser consultadas com filtro por status, componente e unidade | Telas **Doações** e **Estoque** · `POST /api/v1/doacoes` · `GET /api/v1/bolsas` |
| Agrupamento por tipo sanguíneo e hemocomponente | O resumo do estoque soma as bolsas por unidade, tipo sanguíneo e hemocomponente | Tela **Estoque** · `GET /api/v1/estoques` |
| Bolsas próximas do vencimento | Cada bolsa mostra quantos dias faltam para vencer, ou há quantos dias venceu | Tela **Estoque** (“vence em X dia(s)”) |

**Testes:** [`FabricaDeBolsasTest`](https://github.com/Bloodell/bloodell-backend/blob/main/src/test/java/br/edu/cesar/bloodell/bolsa/FabricaDeBolsasTest.java) e `BolsaTest` (unitários), `CadastrosIT` (integração com PostgreSQL) e [3 cenários Gherkin](https://github.com/Bloodell/bloodell-backend/blob/main/src/test/resources/aceitacao/us-r1-01-registrar-doacao.feature) executados contra a API real.

##### US06 · Criar e acompanhar requisições

> **Como** profissional responsável pelas solicitações hospitalares, **quero** registrar uma requisição de hemocomponentes informando quantidade e prioridade **para** que o hemocentro possa organizar o atendimento da necessidade do hospital.
>
> 🔴 Must Have · Persona: Profissional Responsável pelas Solicitações Hospitalares

| Cenário BDD (Entrega 01) | Como foi atendido | Onde ver |
| --- | --- | --- |
| Criação da requisição | A requisição é registrada com hospital, tipo sanguíneo, hemocomponente, quantidade e prioridade, e entra na fila com status `NA_FILA` (pendente) | Tela **Requisições** · `POST /api/v1/requisicoes` |
| Organização por prioridade | A fila atende EMERGÊNCIA, depois URGENTE, depois ELETIVA; na mesma prioridade, vale a ordem de chegada. A fila é uma estrutura de dados feita à mão (AED), espelhada em C | Tela **Requisições** · `GET /api/v1/requisicoes/fila` |
| Acompanhamento da requisição | A consulta mostra o status atual (`NA_FILA` → `ALOCADA` → `EM_ROTA` → `ATENDIDA`). Enquanto está na fila, a prioridade pode ser alterada e o pedido pode ser cancelado | `GET · PUT · DELETE /api/v1/requisicoes/{id}` |

**Testes:** `FilaRequisicoesTest` e `AlocacaoProvisoriaU1Test` (unitários), `FluxoDaUnidadeUmIT` (integração com PostgreSQL) e [8 cenários Gherkin](https://github.com/Bloodell/bloodell-backend/tree/main/src/test/resources/aceitacao) de requisição e alocação.

**Fora desta entrega:** o prazo/janela de entrega da requisição e a autenticação dos perfis ([ADR-004](https://github.com/Bloodell/bloodell-backend/blob/main/docs/adr/ADR-004-autenticacao-fora-do-mvp.md)) ficam para as próximas entregas.

#### Screencasts

| Vídeo | Link |
| --- | --- |
| 🎬 Sistema funcionando: as novas histórias na interface | _[adicionar link do YouTube]_ |
| 🎬 Explicação do código das histórias implementadas | _[adicionar link do YouTube]_ |

#### Versionamento

* Fluxo de trabalho: uma branch por tarefa → pull request → `dev` → `main`, com `dev` e `main` protegidas (CI verde e 1 aprovação para o merge).
* Histórico: [commits do backend](https://github.com/Bloodell/bloodell-backend/commits/main) · [pull requests](https://github.com/Bloodell/bloodell-backend/pulls?q=is%3Apr+is%3Amerged) · [execuções da esteira](https://github.com/Bloodell/bloodell-backend/actions).
* Cada merge na `main` testa, empacota e publica o sistema na AWS ([primeiro deploy automático](https://github.com/Bloodell/bloodell-backend/actions/runs/39865307872), em 22/10).

#### Issue tracker

As tarefas e os bugs em aberto ficam nas [issues do backend](https://github.com/Bloodell/bloodell-backend/issues).

<p align="center">
  <img src="assets/issues-entrega-03.png" width="760" alt="Print da tela de issues do repositório bloodell-backend">
</p>

**Artefatos**

* [Story map da Release 1](https://github.com/Bloodell/bloodell-backend/blob/main/docs/story-map-release-1.md)
* [Rastreabilidade: tarefas × testes](https://github.com/Bloodell/bloodell-backend/blob/main/docs/rastreabilidade-release-1.md)
* [Documentação da API (Swagger)](https://34.235.158.105/swagger-ui.html)
* [Evidências de execução](https://github.com/Bloodell/bloodell-backend/tree/main/docs/evidencias/e1)

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
| [Bloodell Backend](https://github.com/Bloodell/bloodell-backend)   | API e regras de negócio em Java/Spring Boot   |
| [Bloodell Frontend](https://github.com/Bloodell/bloodell-frontend) | Interface web da aplicação                    |

---

## Licença

A definir.
