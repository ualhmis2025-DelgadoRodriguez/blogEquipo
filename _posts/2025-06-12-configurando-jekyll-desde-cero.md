---
layout: post
title: "Configurando Jekyll desde cero: Mi experiencia con el blog del equipo 03"
date: 2025-06-12 15:30:00 +0200
categories: jekyll hmis tutorial
author: Abel Rodríguez
---

**Fecha:** 12 de junio de 2025  
**Autor:** Abel Rodríguez - Equipo 03  

En este post documento mi experiencia configurando Jekyll para nuestro blog del equipo 03 en la asignatura HMIS. Ha sido un proceso de aprendizaje interesante que quiero compartir paso a paso.

## Índice

1. [Contexto inicial](#contexto-inicial)
2. [Verificación del entorno](#verificación-del-entorno)
3. [Creación del proyecto Jekyll](#creación-del-proyecto-jekyll)
4. [Configuración del sitio](#configuración-del-sitio)
5. [Configuración para GitHub Pages](#configuración-para-github-pages)
6. [Primera ejecución](#primera-ejecución)
7. [Reflexiones y próximos pasos](#reflexiones-y-próximos-pasos)

## Contexto inicial

Nuestro equipo tenía un blog básico con HTML estático que funcionaba, pero queríamos migrar a Jekyll para cumplir con la práctica y aprovechar sus ventajas: sistema de posts, templates reutilizables, y mejor integración con GitHub Pages.



## Verificación del entorno

Lo primero fue verificar que tuviera las herramientas necesarias instaladas. En mi caso ya tenía Ruby instalado previamente a través de VS Code, pero fue importante verificarlo:

```bash
ruby -v
jekyll -v
```

Ruby estaba funcionando correctamente, y Jekyll también estaba disponible. Este paso es crucial porque evita problemas posteriores.

## Creación del proyecto Jekyll

En lugar de empezar desde cero, decidí aprovechar la estructura existente de nuestro repositorio. Después de hacer backup del contenido original, limpié el repositorio dejando solo las carpetas `.git/` y `.vscode/`.

El comando clave fue:

```bash
jekyll new --skip-bundle .
```

Este comando es especial porque:
- `jekyll new` crea un nuevo proyecto Jekyll
- `--skip-bundle` evita ejecutar bundle automáticamente (útil para configurar GitHub Pages después)
- `.` indica que se cree en el directorio actual

Inmediatamente se generó toda la estructura base: `_config.yml`, `Gemfile`, `_posts/`, `index.markdown`, etc.

## Configuración del sitio

El archivo `_config.yml` es el núcleo de Jekyll. Aquí he personalizado toda la información de nuestro equipo:

```yaml
title: "Blog del equipo 03"
email: equipo03@ejemplo.com
description: >-
  Blog del equipo 03 de la asignatura HMIS (Herramientas y Métodos de
  Ingeniería del Software).
baseurl: "/blogEquipo"  
url: "https://ualhmis2025-DelgadoRodriguez.github.io"
github_username: ualhmis2025-DelgadoRodriguez  
```

Un punto importante es que nuestro repositorio está en una **organización** GitHub (`ualhmis2025-DelgadoRodriguez`), no en una cuenta personal. Esto afecta la configuración del `url` y `github_username`.

## Configuración para GitHub Pages

Para que el blog funcione en GitHub Pages, hay que modificar el `Gemfile`:

**1. Comentar la línea de Jekyll:**
```ruby
# gem "jekyll", "~> 4.4.1"
```

**2. Descomentar la línea de GitHub Pages:**
```ruby
gem "github-pages", group: :jekyll_plugins
```

**3. Instalar y actualizar dependencias:**
```bash
bundle install
bundle update github-pages
```

El comando `bundle install` fue necesario porque era la primera vez que se configuraban las dependencias. Luego `bundle update github-pages` aseguró la compatibilidad con GitHub Pages.

## Primera ejecución

El despliegue del blog se realizó con:

```bash
bundle exec jekyll serve
```

Aquí la correspondiente salida por consola

```
Configuration file: C:/Users/Abel/source/repos/blogEquipo/_config.yml
            Source: C:/Users/Abel/source/repos/blogEquipo
       Destination: C:/Users/Abel/source/repos/blogEquipo/_site
      Generating...
       Jekyll Feed: Generating feed for posts
                    done in 0.504 seconds.
    Server address: http://127.0.0.1:4000/blogEquipo/
  Server running... press ctrl-c to stop.
```

El blog estaba corriendo en `http://127.0.0.1:4000/blogEquipo/` y se veía perfectamente.

## Reflexiones y próximos pasos

### Lo que aprendí

1. **La importancia del entorno:** Verificar Ruby y Jekyll desde el principio ahorra muchos problemas.

2. **GitHub Organizations vs Personal:** Configurar correctamente la URL cuando el repo está en una organización es crucial.

3. **Bundle vs Jekyll directo:** Usar `bundle exec` asegura que se usen las versiones correctas de las dependencias.

4. **GitHub Pages tiene sus peculiaridades:** Necesita configuración específica en el Gemfile.

### Próximos pasos

1. **Migrar contenido:** Convertir nuestras páginas HTML existentes (Abel y Pablo) a formato Jekyll.

2. **Crear más posts:** Documentar nuestro progreso en HMIS.

3. **Personalización:** Customizar CSS y layouts según nuestras necesidades.

4. **Deploy:** Subir todo a GitHub y verificar que funciona en GitHub Pages.

### Recursos útiles


- [Documentación oficial de Jekyll](https://jekyllrb.com/)
- [GitHub Pages + Jekyll](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll)

---

Ha sido una experiencia muy enriquecedora. Jekyll demuestra ser una herramienta potente para blogs técnicos, y el proceso de configuración, aunque tiene sus particularidades, es bastante directo cuando se siguen los pasos correctos.
