# Proyecto Titvo - Índice de Repositorios

<img src="./images/logo.png" alt="Logo Titvo" height="40px">

https://www.titvo.com

Proyecto Open Source que contiene un sistema que analiza automáticamente commits de GitHub, Bitbucket o archivos enviados por CLI en busca de vulnerabilidades de seguridad utilizando modelos avanzados de LLM.

Este repositorio sirve como punto de entrada para navegar por los diferentes componentes del ecosistema Titvo.

## Arquitectura General

Titvo está construido siguiendo principios de arquitectura limpia, con diferentes componentes que cumplen roles específicos en el sistema.

## Componentes del Sistema

### Módulos de Dominio

Repositorios que contienen la lógica de negocio pura siguiendo principios de Clean Architecture:

| Repositorio | Descripción |
|-------------|-------------|
| [titvo-auth](https://github.com/KaribuLab/titvo-auth) | Lógica de dominio del servicio de autenticación |
| [titvo-trigger](https://github.com/KaribuLab/titvo-trigger) | Lógica de dominio para iniciar procesos de análisis |
| [titvo-shared](https://github.com/KaribuLab/titvo-shared) | Biblioteca compartida con servicios comunes y utilidades reutilizables |

### Implementaciones de Infraestructura (AWS)

Repositorios que implementan la infraestructura específica acoplada a AWS:

| Repositorio | Descripción |
|-------------|-------------|
| [titvo-auth-setup](https://github.com/KaribuLab/titvo-auth-setup) | Infraestructura AWS para el servicio de autenticación |
| [titvo-task-cli-files](https://github.com/KaribuLab/titvo-task-cli-files) | Infraestructura AWS para archivos CLI |
| [titvo-task-trigger](https://github.com/KaribuLab/titvo-task-trigger) | Infraestructura AWS para disparadores específicos de tareas |
| [titvo-task-status](https://github.com/KaribuLab/titvo-task-status) | Infraestructura AWS para seguimiento del estado de tareas |
| [titvo-security-scan-infra-aws](https://github.com/KaribuLab/titvo-security-scan-infra-aws) | Infraestructura AWS para el motor de escaneo |

### Componente de Seguridad

| Repositorio | Descripción |
|-------------|-------------|
| [titvo-security-scan](https://github.com/KaribuLab/titvo-security-scan) | Motor de escaneo de seguridad con implementación interna de Clean Architecture |

### Interfaces de Usuario

Puntos de entrada al sistema desde diferentes plataformas:

| Repositorio | Descripción |
|-------------|-------------|
| [tli](https://github.com/KaribuLab/tli) | CLI de seguridad para desarrollo (Go) |
| [titvo-security-scan-action](https://github.com/KaribuLab/titvo-security-scan-action) | GitHub Action para escaneos de seguridad |
| [titvo-security-scan-pipe](https://bitbucket.org/karibu-cl/titvo-security-scan-pipe/src/main/) | Pipeline de Bitbucket para escaneos de seguridad |

## Diagrama de Arquitectura

```mermaid
flowchart TD
    %% Definimos los nodos con colores que funcionen en modo claro y oscuro
    style CLI fill:#d4f4fa,stroke:#000000,stroke-width:2px,color:#000000
    style GH fill:#d4f4fa,stroke:#000000,stroke-width:2px,color:#000000
    style BB fill:#d4f4fa,stroke:#000000,stroke-width:2px,color:#000000
    
    style Auth fill:#d4f4fa,stroke:#000000,stroke-width:2px,color:#000000
    style Trigger fill:#d4f4fa,stroke:#000000,stroke-width:2px,color:#000000
    style Shared fill:#d4f4fa,stroke:#000000,stroke-width:2px,color:#000000
    
    style Scan fill:#d5f5d5,stroke:#000000,stroke-width:2px,color:#000000
    
    style AuthSetup fill:#fae5d5,stroke:#000000,stroke-width:2px,color:#000000
    style TaskTrigger fill:#fae5d5,stroke:#000000,stroke-width:2px,color:#000000
    style TaskStatus fill:#fae5d5,stroke:#000000,stroke-width:2px,color:#000000
    style TaskCliFiles fill:#fae5d5,stroke:#000000,stroke-width:2px,color:#000000
    style ScanInfra fill:#fae5d5,stroke:#000000,stroke-width:2px,color:#000000
    
    %% Interfaces
    CLI["tli (CLI)"]
    GH["GitHub Action"]
    BB["Bitbucket Pipeline"]
    
    %% Módulos de Dominio
    Auth["titvo-auth"]
    Trigger["titvo-trigger"]
    Shared["titvo-shared"]
    
    %% Seguridad
    Scan["titvo-security-scan"]
    
    %% Infraestructura
    AuthSetup["titvo-auth-setup"]
    TaskTrigger["titvo-task-trigger"]
    TaskStatus["titvo-task-status"]
    TaskCliFiles["titvo-task-cli-files"]
    ScanInfra["titvo-security-scan-infra-aws"]
    
    %% Conexiones con color rojo brillante para alta visibilidad
    CLI -- "utiliza" --> Auth
    CLI -- "escanea" --> Scan
    GH -- "usa" --> Scan
    BB -- "usa" --> Scan
    
    Auth -- "implementado en" --> AuthSetup
    Trigger -- "implementado en" --> TaskTrigger
    Trigger -- "implementado en" --> TaskStatus
    
    Scan -- "implementado en" --> ScanInfra
    
    %% Conexiones con titvo-shared
    Auth -- "utiliza" --> Shared
    Trigger -- "utiliza" --> Shared
    Scan -- "utiliza" --> Shared
    
    %% Etiquetas para los grupos
    subgraph Interfaces[" Interfaces de Usuario "]
        CLI
        GH
        BB
    end
    
    subgraph Domain[" Módulos de Dominio "]
        Auth
        Trigger
        Shared
    end
    
    subgraph Security[" Componente de Seguridad "]
        Scan
    end
    
    subgraph Infra[" Infraestructura AWS "]
        AuthSetup
        TaskTrigger
        TaskStatus
        TaskCliFiles
        ScanInfra
    end
    
    style Interfaces fill:#d4f4fa,stroke:#000000,stroke-width:3px,color:#000000
    style Domain fill:#d4f4fa,stroke:#000000,stroke-width:3px,color:#000000
    style Security fill:#d5f5d5,stroke:#000000,stroke-width:3px,color:#000000
    style Infra fill:#fae5d5,stroke:#000000,stroke-width:3px,color:#000000
    
    %% Estilo de enlaces con color rojo para alta visibilidad
    linkStyle 0 stroke:#FF0000,stroke-width:2px;
    linkStyle 1 stroke:#FF0000,stroke-width:2px;
    linkStyle 2 stroke:#FF0000,stroke-width:2px;
    linkStyle 3 stroke:#FF0000,stroke-width:2px;
    linkStyle 4 stroke:#FF0000,stroke-width:2px;
    linkStyle 5 stroke:#FF0000,stroke-width:2px;
    linkStyle 6 stroke:#FF0000,stroke-width:2px;
    linkStyle 7 stroke:#FF0000,stroke-width:2px;
    linkStyle 8 stroke:#FF0000,stroke-width:2px;
    linkStyle 9 stroke:#FF0000,stroke-width:2px;
    linkStyle 10 stroke:#FF0000,stroke-width:2px;
```

## Uso de la Herramienta CLI (tli)

[tli](https://github.com/KaribuLab/tli) es una herramienta de línea de comandos para escanear código fuente en busca de problemas de seguridad.

Para más detalles sobre el uso y funcionalidades de tli, consulta el [repositorio oficial](https://github.com/KaribuLab/tli).

## Contribuciones

Para contribuir a cualquiera de los proyectos:

1. Crear un fork del repositorio específico
2. Crear una rama para tu funcionalidad (`git checkout -b feature/amazing-feature`)
3. Hacer commit de tus cambios (`git commit -m 'feat: agregar nueva funcionalidad'`)
4. Enviar la rama (`git push origin feature/amazing-feature`)
5. Abrir un Pull Request

## Licencia

Los proyectos Titvo se distribuyen bajo la licencia Apache 2.0. Consulta el archivo `LICENSE` en cada repositorio para más detalles.
