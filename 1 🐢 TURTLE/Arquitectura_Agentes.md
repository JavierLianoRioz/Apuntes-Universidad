# Arquitectura de Agentes: Ecosistema Modular Vault-Crew (v2 - Diseño en Curso)

Este documento define la infraestructura modular y los flujos de inteligencia para la gestión de la Bóveda.

## 1. Mapa de Capacidades (Pool de Expertos)

```mermaid
graph TD
    subgraph "Capas de Inteligencia"
        direction TB
        C1["<b>Capa de Percepción:</b><br/>Investigación y RAG"]
        C2["<b>Capa Estructural:</b><br/>Arquitectura y Relaciones"]
        C3["<b>Capa de Síntesis:</b><br/>Redacción y Narrativa"]
        C4["<b>Capa de Ejecución:</b><br/>Escritura y Registro"]
    end

    subgraph "Expertos Disponibles"
        direction LR
        E1["Structural Analyst"]
        E2["Web Researcher"]
        E3["Concept Mapper"]
        E4["Senior Software Engineer"]
        E5["Learning Strategist"]
        E6["Asesor Financiero"]
        E7["Note Architect"]
        E8["Quality Auditor"]
    end

    C1 --- E1 & E2 & E6
    C2 --- E3 & E4
    C3 --- E5 & E7
    C4 --- E7 & E8
```

---

## 2. Flujo de Trabajo Maestro (The Value Pipeline)

```mermaid
graph TD
    User((Usuario)) --> Master["<b>Orquestador Maestro</b><br/>(Antigravity CLI)"]
    
    subgraph "Fase 1: Estrategia (The Brain)"
        Master --> |"Mission Briefing"| Strategist["<b>Expert Strategist</b>"]
        Strategist --> |"Consulta RAG"| VaultDB[(Vault RAG)]
        VaultDB --> |"Hechos y Teoría"| Strategist
        Strategist --> |"Raw Insights"| Pipe{<b>Value Pipe</b>}
    end

    subgraph "Fase 2: Producción y Enrutado"
        Pipe --> Architect["<b>Note Architect</b>"]
        Architect --> Routing{<b>Routing Logic</b>}
        
        Routing --> |"Concepto Técnico"| Public[(Bóveda Pública)]
        Routing --> |"Dato Personal"| Private[(Base de Datos Privada)]
        
        %% Lógica Dinámica de Diario
        Private -.-> |"Búsqueda Proactiva"| Weaver[[get_predecessor_daily_note]]
        Weaver -.-> |"Auto-Link"| Private
    end

    subgraph "Fase 3: Control"
        Public & Private --> Auditor["<b>Quality Auditor</b>"]
        Auditor -.-> |"Aprendizajes"| Memory[[Memoria del Sistema]]
    end

    style Private fill:#fdd,stroke:#a33
    style Public fill:#dfd,stroke:#3a3
    style Weaver fill:#e1f5fe,stroke:#01579b
```

---

## 3. Estrategia de Almacenamiento Atómico

| Tipo de Info | Destino | Formato | Conectividad Temporal |
| :--- | :--- | :--- | :--- |
| **Conocimiento** | Raíz `/` | Nota Atómica (.md) | Wikilinks conceptuales |
| **Hechos personales**| `/Private` | Registro Maestro | Categorización por dominio |
| **Diario** | `/Private/Diario`| YYYY-MM-DD.md | **Auto-link al último día** |

---

## 4. Matriz de Herramientas (Skills)

| Agente | Herramienta | Función |
| :--- | :--- | :--- |
| **Strategist** | `VaultRAGTool` | Búsqueda semántica en PDFs y Notas. |
| **Architect** | `FileWriterTool`| Escritura física forzada (Raíz/Private). |

---

## 5. Estado de Implementación
- [x] Motor RAG Atómico (Ollama).
- [x] Fábrica Modular de Crews.
- [x] Skill de Escritura Directa (FileWriterTool).
- [x] Enrutado de Privacidad (Public vs Private).
