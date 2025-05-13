# Proyecto Titvo - Índice de Repositorios
https://www.titvo.com

Proyecto Open Source que contiene un sistema que analiza automáticamente commits de GitHub, Bitbucket o archivos enviados por CLI en busca de vulnerabilidades de seguridad utilizando modelos avanzados de LLM.

Este repositorio sirve como punto de entrada para navegar por los diferentes componentes del ecosistema Titvo.

## Arquitectura General

Titvo está construido siguiendo principios de arquitectura limpia, con diferentes componentes que cumplen roles específicos en el sistema.

## Componentes del Sistema

### Módulos de Dominio (Node.js)

Repositorios que contienen la lógica de negocio pura siguiendo principios de Clean Architecture:

| Repositorio | Descripción |
|-------------|-------------|
| [titvo-auth](https://github.com/KaribuLab/titvo-auth) | Lógica de dominio del servicio de autenticación |
| [titvo-trigger](https://github.com/KaribuLab/titvo-trigger) | Lógica de dominio para iniciar procesos de análisis |

### Implementaciones de Infraestructura (AWS)

Repositorios que implementan la infraestructura específica acoplada a AWS:

| Repositorio | Descripción |
|-------------|-------------|
| [titvo-auth-setup](https://github.com/KaribuLab/titvo-auth-setup) | Infraestructura AWS para el servicio de autenticación |
| [titvo-setup](https://github.com/KaribuLab/titvo-setup) | Infraestructura AWS para configuración general |
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
graph TD
    %% Definición de estilos
    classDef interfaces fill:#f9f9f9,stroke:#333,stroke-width:1px;
    classDef dominio fill:#d4f4fa,stroke:#333,stroke-width:1px;
    classDef seguridad fill:#d5f5d5,stroke:#333,stroke-width:1px;
    classDef securityInternals fill:#bdeabd,stroke:#333,stroke-width:1px;
    classDef infraestructura fill:#fae5d5,stroke:#333,stroke-width:1px;

    %% Interfaces de Usuario
    subgraph Interfaces["Interfaces de Usuario"]
        CLI[fa:fa-terminal tli]
        GH[fa:fa-github GitHub Action]
        BB[fa:fa-git Bitbucket Pipeline]
    end
    class Interfaces interfaces;
    class CLI interfaces;
    class GH interfaces;
    class BB interfaces;

    %% Módulos de Dominio
    subgraph Dominio["Módulos de Dominio (Node.js)"]
        Auth[titvo-auth]
        Trigger[titvo-trigger]
    end
    class Dominio dominio;
    class Auth dominio;
    class Trigger dominio;

    %% Componente de Seguridad
    subgraph Security["Componente de Seguridad"]
        Scan[titvo-security-scan]
        
        subgraph ScanInternals["Clean Architecture Interna"]
            Domain[Dominio]
            UseCases[Casos de Uso]
            API[API]
            Adapters[Adaptadores]
        end
    end
    class Security seguridad;
    class Scan seguridad;
    class ScanInternals securityInternals;
    class Domain securityInternals;
    class UseCases securityInternals;
    class API securityInternals;
    class Adapters securityInternals;

    %% Infraestructura AWS
    subgraph Infra["Infraestructura AWS"]
        AuthSetup[titvo-auth-setup]
        Setup[titvo-setup]
        TaskTrigger[titvo-task-trigger]
        TaskStatus[titvo-task-status]
        TaskCliFiles[titvo-task-cli-files]
        ScanInfra[titvo-security-scan-infra-aws]
    end
    class Infra infraestructura;
    class AuthSetup infraestructura;
    class Setup infraestructura;
    class TaskTrigger infraestructura;
    class TaskStatus infraestructura;
    class TaskCliFiles infraestructura;
    class ScanInfra infraestructura;

    %% Conexiones
    CLI --> Auth
    CLI --> Scan
    GH --> Scan
    BB --> Scan
    
    Auth --> AuthSetup
    Trigger --> TaskTrigger
    Trigger --> TaskStatus
    
    Scan --> ScanInfra
    
    Domain --> UseCases
    UseCases --> API
    UseCases --> Adapters
    Adapters --> ScanInfra
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
