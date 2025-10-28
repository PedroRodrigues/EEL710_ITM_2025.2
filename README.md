# 🧠 Simulador de Circuitos Elétricos — UFRJ / Electronic Brazil Devices

## 📘 Visão Geral

Este repositório contém o desenvolvimento do **Protótipo de Simulador de Circuitos Elétricos**, fruto da parceria entre o **Departamento de Eletrônica (DEL)** da **Universidade Federal do Rio de Janeiro (UFRJ)** e a **Electronic Brazil Devices**, no contexto da disciplina **Instrumentação e Técnicas de Medidas (EEL710)**, ministrada pelo professor **João Victor da Fonseca Pinto**.

O objetivo é criar um simulador modular e extensível em **Python**, utilizando:

* **Análise Nodal Modificada (MNA)**;
* **Integração numérica (Backward Euler)**;
* **Método de Newton–Raphson** para elementos não lineares;
* **Leitura de netlists SPICE-like** e **API programática Python**;
* **CI/CD com GitHub Actions** e testes automatizados com Pytest.

---

## 👨‍🔬 Equipe de Desenvolvimento

| Aluno               | Função                                    | Principais Responsabilidades                                                                                                             |
| ------------------- | ----------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| **Pedro Rodrigues** | Infraestrutura, Integração e Documentação | Gerenciamento do repositório, configuração do CI/CD, integração dos módulos, revisão de PRs e documentação geral do projeto.             |
| **Anderson Sandes** | Desenvolvedor do Motor de Simulação       | Implementação da análise transiente, integração temporal (Backward Euler) e método de Newton–Raphson com controle de tolerâncias.        |
| **Lucas Duque**     | Desenvolvedor de Elementos                | Implementação e validação das classes de componentes elétricos (R, L, C, fontes, diodo, MOSFET, op-amp).                                 |
| **Vinícius Falcão** | Testes, Documentação e Suporte            | Implementação de testes automatizados (Pytest), manutenção da documentação técnica (Sphinx/Doxygen) e suporte em módulos complementares. |

---

## 🧭 Estrutura do Repositório

```
simulador-circuitos/
├── README.md                    # Visão geral e índice do projeto
├── requirements.txt             # Dependências do Python
├── pyproject.toml               # Configuração de build e metadados
├── .editorconfig                # Sincroniza as configurações do VSCode
├── .github/
│   └── workflows/
│       ├── ci.yml               # Pipeline de integração contínua
│       └── README.md            # Detalhes do CI/CD
├── src/
│   └── simulador/
│       ├── README.md            # Estrutura e organização do código
│       ├── elements/            # Classes de componentes elétricos
│       ├── integrator/          # Métodos numéricos de integração
│       ├── solver/              # Solvers lineares e não lineares
│       ├── netlist/             # Parser e writer de netlists
│       └── io/                  # Exportação de resultados e gráficos
├── tests/
│   ├── README.md                # Organização e execução dos testes
│   ├── fixtures/                # Netlists e saídas de referência
│   └── test_*.py                # Testes automatizados com Pytest
└── docs/
    ├── README.md                # Introdução à documentação técnica
    ├── architecture.md          # Estrutura do software
    ├── elements.md              # Detalhamento dos elementos suportados
    ├── solver.md                # Método de Newton–Raphson e solvers
    ├── integrator.md            # Métodos de integração temporal
    ├── netlist.md               # Sintaxe e parsing de netlists
    ├── api.md                   # Interface Python (classe Circuito)
    └── ci_cd.md                 # Detalhamento do pipeline CI/CD
```

> 📘 Para explicações detalhadas sobre cada parte do projeto, acesse os arquivos de documentação localizados em `/docs`.

---

## 🚀 Entregáveis Principais

1. **Simulador funcional em Python** com arquitetura orientada a objetos.
2. **Repositório público no GitHub** com controle de versão, issues e PRs.
3. **Suporte completo a netlists** e **API Python**.
4. **Análise transiente** com método Backward Euler.
5. **Suporte a elementos lineares e não lineares** (incluindo Diodo e MOSFET).
6. **CI/CD automatizado** com GitHub Actions e testes via Pytest.
7. **Documentação completa** em Markdown e Sphinx.
8. **Apresentação final** com demonstração de casos de teste do Anexo II.

---

## 🌿 Fluxo de Desenvolvimento (GitFlow)

* **main** → versão estável e pronta para entrega.
* **dev** → integração das novas funcionalidades.
* **feature/** → desenvolvimento de módulos específicos.
* **fix/** → correções e ajustes menores.

**Fluxo:**

1. Criar branch `feature/nome-funcionalidade` a partir de `dev`.
2. Desenvolver e abrir Pull Request para `dev`.
3. Revisão obrigatória por outro integrante.
4. Merge aprovado dispara o pipeline CI.
5. Release final é feita de `dev` → `main`.

> 🔖 Utilizar versionamento semântico (`v1.0.0`, `v1.1.0`, etc.).

---

## 🧪 Execução de Testes

```bash
pytest -v
pytest --cov=src --cov-report=term-missing
```

Os testes são executados automaticamente pela pipeline do GitHub Actions em cada Pull Request.

Mais detalhes em [`tests/README.md`](tests/README.md).

---

## 🧩 Documentação Técnica

A documentação técnica completa está localizada em [`/docs`](docs/README.md) e inclui:

* **Arquitetura e hierarquia de classes**;
* **Detalhes sobre cada elemento elétrico**;
* **Implementação dos integradores e solvers**;
* **Exemplos de uso via API e netlists**;
* **Descrição do pipeline CI/CD**.

Para gerar a documentação localmente:

```bash
cd docs
make html
```

A documentação será gerada em `docs/_build/html/index.html`.

---

## 📩 Contatos

**Instituição:** Universidade Federal do Rio de Janeiro
**Curso:** Engenharia Eletrônica e da Computação
**Disciplina:** EEL710 — Instrumentação e Técnicas de Medidas
**Professor:** [[joaovictor@poli.ufrj.br](mailto:joaovictor@poli.ufrj.br)]
**Integrantes:**
* Pedro Rodrigues: [[rodriguespedro@poli.ufrj.br](mailto:rodriguespedro@poli.ufrj.br)]
* Anderson Sandes: [[anderson.sandes@me.com](mailto:anderson.sandes@me.com)]
* Lucas Duque: [[lucasduque.ma@gmail.com](mailto:lucasduque.ma@gmail.com)]
* Vinícius Falcão: [[viniciusfalcaodeassis@gmail.com](mailto:viniciusfalcaodeassis@gmail.com )]

---

## 🧾 Licença e Aviso

Este projeto é **acadêmico e fictício**, regido pelo contrato educacional da disciplina **EEL710 - Instrumentação e Técnicas de Medidas (UFRJ)**. Nenhum uso comercial é permitido sem autorização do orientador.

---