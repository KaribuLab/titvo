# Proyecto Titvo - Índice de Repositorios
https://www.titvo.com
Proyecto Open Source que contiene un sistema que analiza automáticamente commits de GitHub, Bitbucket o archivos enviados por CLI en busca de vulnerabilidades de seguridad utilizando modelos avanzados de LLM.

Este repositorio sirve como punto de entrada para navegar por los diferentes componentes del ecosistema Titvo.

## Componentes Principales

### Seguridad y Escaneo

| Repositorio | Descripción |
|-------------|-------------|
| [titvo-security-scan-pipe](https://bitbucket.org/karibu-cl/titvo-security-scan-pipe/src/main/) | Pipeline de Bitbucket para escaneos de seguridad |
| [titvo-security-scan-action](https://github.com/KaribuLab/titvo-security-scan-action) | GitHub Action para escaneos de seguridad |
| [titvo-security-scan](https://github.com/KaribuLab/titvo-security-scan) | Motor principal de escaneo de seguridad |
| [titvo-security-scan-infra-aws](https://github.com/KaribuLab/titvo-security-scan-infra-aws) | Infraestructura AWS para el escaneo de seguridad |

### Autenticación y Configuración

| Repositorio | Descripción |
|-------------|-------------|
| [titvo-auth](https://github.com/KaribuLab/titvo-auth) | Servicio de autenticación |
| [titvo-auth-setup](https://github.com/KaribuLab/titvo-auth-setup) | Configuración del servicio de autenticación |
| [titvo-setup](https://github.com/KaribuLab/titvo-setup) | Herramientas de configuración general |

### Gestión de Tareas

| Repositorio | Descripción |
|-------------|-------------|
| [titvo-trigger](https://github.com/KaribuLab/titvo-trigger) | Servicio para iniciar procesos |
| [titvo-task-trigger](https://github.com/KaribuLab/titvo-task-trigger) | Disparador específico de tareas |
| [titvo-task-status](https://github.com/KaribuLab/titvo-task-status) | Seguimiento del estado de tareas |
| [titvo-task-cli-files](https://github.com/KaribuLab/titvo-task-cli-files) | Archivos CLI para gestión de tareas |

## Arquitectura General

La arquitectura de Titvo está dividida en los siguientes componentes principales:

1. **Seguridad**: Herramientas para análisis y escaneo de seguridad
2. **Autenticación**: Servicios para manejo de identidad y acceso
3. **Gestión de Tareas**: Componentes para la ejecución y seguimiento de procesos

## Contribuciones

Para contribuir a cualquiera de los proyectos:

1. Crear un fork del repositorio específico
2. Crear una rama para tu funcionalidad (`git checkout -b feature/amazing-feature`)
3. Hacer commit de tus cambios (`git commit -m 'feat: agregar nueva funcionalidad'`)
4. Enviar la rama (`git push origin feature/amazing-feature`)
5. Abrir un Pull Request

## Licencia

Los proyectos Titvo se distribuyen bajo la licencia Apache 2.0. Consulta el archivo `LICENSE` en cada repositorio para más detalles.
