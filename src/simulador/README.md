# ⚙️ Módulo `simulador/`

Este diretório contém o núcleo do **Simulador de Circuitos Elétricos**, desenvolvido em Python e estruturado segundo o paradigma de **Programação Orientada a Objetos (POO)**.  
O objetivo deste módulo é fornecer a infraestrutura para simulação transiente de circuitos, conforme a **Análise Nodal Modificada (MNA)**, seguindo os requisitos do contrato UFRJ–Electronic Brazil Devices.

---

## 🧠 Estrutura Interna

```
simulador/
├── elements/           # Classes que representam componentes elétricos (R, L, C, Diodo, MOSFET, etc.)
├── integrator/         # Métodos numéricos de integração no tempo (Backward Euler, Forward Euler, Trapezoidal)
├── solver/             # Solvers lineares e não lineares (Newton–Raphson)
├── netlist/            # Leitura e escrita de netlists SPICE-like
└── io/                 # Saída de resultados, exportação e visualização
```

---

## 🧩 Descrição dos Submódulos

### `elements/`
Define as classes de cada **elemento de circuito**, todas herdando de uma classe base `ElementoCircuito`.  
O uso de **herança e polimorfismo** é obrigatório — cada classe implementa o método `stamp()` para adicionar suas contribuições à matriz de condutâncias `G` e vetor `b`.

**Elementos implementados:**
- Resistor, Capacitor, Indutor  
- Fontes independentes (tensão e corrente)  
- Fontes controladas (E, F, G, H)  
- Diodo, MOSFET e resistor não linear  
- Amplificador operacional ideal  

---

### `integrator/`
Contém as rotinas de integração no domínio do tempo (análise transiente).

**Métodos suportados:**
- `Backward Euler` (obrigatório)  
- `Forward Euler` e `Trapezoidal` (estruturas previstas)

O motor de simulação (`time_analysis.py`) gerencia:
- Controle de passo (`Δt`)
- Iterações internas
- Testes de convergência (`tolerância ≤ 0.001`)
- Reiteração com novos valores de `x(t)` até convergir (máx. 100 tentativas)

---

### `solver/`
Implementa os algoritmos numéricos para resolver o sistema `A·x = b` e o **método de Newton–Raphson** para elementos não lineares.

**Principais funções:**
- `solve_linear(A, b)` — solução direta via `numpy.linalg.solve`
- `newton_raphson(circuito, N=50, M=100, tol=1e-3)` — controle de iteração e convergência

---

### `netlist/`
Responsável pelo **parsing e escrita de netlists** compatíveis com SPICE.  
Permite a criação de circuitos a partir de arquivos `.net` ou diretamente via API Python.

**Principais arquivos:**
- `parser.py` — leitura e tokenização de netlists  
- `writer.py` — exportação de circuitos para `.net`  
- `models/` — definições de formato por tipo de componente  

---

### `io/`
Gerencia as **saídas da simulação**, armazenando resultados em estruturas acessíveis como `dict` ou `pandas.DataFrame`.

**Funções principais:**
- `export_results()` — salva dados em `.csv`
- `plot_results()` — gera gráficos de tensão e corrente em função do tempo  

---

## 🧮 Fluxo de Execução

1. **Leitura ou construção** do circuito (via netlist ou API Python);
2. **Instanciação dos elementos** e montagem das matrizes do sistema;
3. **Simulação temporal** com o método Backward Euler;
4. **Iteração de Newton–Raphson** para elementos não lineares;
5. **Armazenamento e plotagem** dos resultados.

---

## 📚 Exemplo de Uso

### Construção via código:
```python
from simulador.netlist import parser
from simulador.integrator.time_analysis import simulate

circuito = parser.load_netlist("tests/fixtures/lc.net")
resultados = simulate(circuito, metodo="BE", tmax=3e-3, dt=1e-5)
resultados.plot()
```

### Construção via código:

```python
from simulador.elements import Resistor, Capacitor, FonteTensao
from simulador.circuito import Circuito

c = Circuito()
c.adicionar(Resistor("R1", "1", "0", 1000))
c.adicionar(Capacitor("C1", "1", "0", 1e-6))
c.adicionar(FonteTensao("V1", "1", "0", tipo="DC", valor=5))
res = c.simular(metodo="BE", tmax=1e-3, dt=1e-5)
res.plot()
```

---

## 🧪 Testes Automatizados

Os testes são implementados com Pytest e executados automaticamente pelo GitHub Actions.

### Exemplos de testes:

* Validação de leitura de netlists (test_netlist_parser.py)
* Teste de simulação LC e Chua (test_time_analysis.py)
* Teste de convergência de Newton–Raphson (test_solver.py)
* Comparação com saídas de referência do Anexo II

Para executar manualmente:

```
pytest -v --maxfail=1 --disable-warnings
```

---
