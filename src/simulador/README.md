# ⚙️ Módulo Principal — Simulador de Circuitos Elétricos

## 🧩 Objetivo
Este módulo é o **núcleo funcional** do simulador de circuitos elétricos.  
Ele implementa toda a lógica necessária para:
- Montar e resolver circuitos elétricos descritos por netlists;
- Calcular tensões e correntes ao longo do tempo;
- Gerenciar os elementos lineares e não lineares;
- Oferecer uma API Python clara e extensível para análise de circuitos.

O desenvolvimento deve priorizar **modularidade, precisão numérica e clareza de código**, garantindo fácil manutenção e expansão futura.

---

## 🧠 Estrutura do Módulo
 
 ```
 src/simulador/
├── circuit.py                  # Classe principal Circuito — coordena a simulação
├── element_base.py             # Classe base Elemento — interface para todos os componentes
├── elements/                   # Componentes elétricos (R, L, C, fontes, diodo, MOSFET, etc.)
├── solver/                     # Solvers lineares e Newton–Raphson
├── integrator/                 # Métodos de integração (Backward Euler)
├── netlist/                    # Parser e writer de netlists
└── io/                         # Funções de exportação e visualização de resultados
 ```

 Cada subpacote possui um `README.md` próprio com explicações detalhadas.

 ---

## 🚀 Expectativas de Implementação

### 1. Núcleo (`Circuito`)
- Deve ser responsável por armazenar todos os elementos e nós do circuito.  
- Montar as matrizes de condutância (G), fontes (I) e variáveis de estado (x).  
- Executar o loop de simulação, chamando o integrador e o solver conforme necessário.  
- Manter interface clara: `adicionar_elemento()`, `simular()`, `obter_resultados()`.

### 2. Elementos (`Elemento` e `elements/`)
- Cada elemento deve herdar de `ElementoBase`.
- Implementar métodos padrão:
  - `stamp(G, I, x)` → adiciona contribuições nas matrizes;
  - `update_state()` → atualiza variáveis internas no tempo.
- A modelagem deve seguir o **Anexo I** do contrato (matrizes e equações).

### 3. Solver (`solver/`)
- Resolver sistemas lineares via `numpy.linalg.solve`.
- Implementar método Newton–Raphson para componentes não lineares.
- Garantir convergência e tratamento de falhas numéricas.

### 4. Integrador (`integrator/`)
- Implementar **Backward Euler** para análise transiente.
- Permitir futura extensão para Trapezoidal e Forward Euler.
- Controlar passo de tempo (`Δt`) e estabilidade numérica.

### 5. Netlist (`netlist/`)
- Ler netlists estilo SPICE.
- Criar instâncias de elementos automaticamente.
- Fornecer utilitários de exportação e importação para diferentes formatos.

### 6. IO (`io/`)
- Gerar gráficos de tensão e corrente (via `matplotlib`).
- Exportar resultados em CSV e Pandas DataFrame.

---

## 🧱 Diretrizes de Desenvolvimento
- Seguir **PEP8** e manter **tipagem estática (type hints)**.
- Todos os módulos devem ter **testes unitários** (`pytest`).
- Evitar dependências externas além de:
  - `numpy`, `scipy`, `matplotlib`, `pandas`.
- Comentários e docstrings devem seguir o padrão **Google Style**.
- Utilizar **orientação a objetos** e **princípio de responsabilidade única**.

---

## 🧩 Exemplo de Uso (prototípico)
```python
from simulador.circuit import Circuito
from simulador.elements import Resistor, Capacitor, FonteDC

# Criar circuito
c = Circuito("RC simples")
c.adicionar_elemento(Resistor("R1", "n1", "n0", 1e3))
c.adicionar_elemento(Capacitor("C1", "n1", "n0", 1e-6))
c.adicionar_elemento(FonteDC("V1", "n1", "n0", 5))

# Executar análise transiente
resultado = c.simular(tempo_final=0.01, passo=1e-5)

# Visualizar resultados
resultado.plotar()