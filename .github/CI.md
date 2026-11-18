# Integración continua y ramas protegidas

`develop` integra cambios y `master` representa producción. Abrir pull requests de las ramas de trabajo hacia `develop` y de `develop` hacia `master` para una promoción. El [workflow](workflows/ci.yml) valida cada push y pull request hacia ambas ramas.

## Contrato del proyecto Node.js

- Versionar `package.json` y `package-lock.json` en la raíz. El workflow usa Node.js 24 y `npm ci`.
- Definir `npm run lint` para ejecutar el análisis estático.
- Configurar `npm test` para ejecutar Jest y descubrir pruebas unitarias y de integración en una sola corrida. Las pruebas de integración deben usar servicios de prueba o emuladores accesibles desde CI sin credenciales de producción.
- Configurar `collectCoverageFrom` en Jest para incluir todo el código de aplicación relevante, incluidos los archivos que las pruebas todavía no importan. El workflow requiere al menos 70 % en cada métrica global, líneas, sentencias, funciones y ramas. Un informe ausente, inválido o sin elementos medibles en una métrica produce un fallo.
- El repositorio actualmente contiene documentación. El workflow dará un error explícito hasta incorporar el proyecto Node.js con sus dependencias, linter y pruebas. [Configuración de Jest](https://jestjs.io/docs/configuration).

## Protección de master en GitHub

1. Publicar el workflow y ejecutar al menos un pull request hacia `master` para que GitHub registre el chequeo.
2. Ir a **Settings → Branches → Branch protection rules → Add rule**. Usar el patrón exacto `master`.
3. Activar **Require a pull request before merging**. Para revisión, se recomienda requerir al menos una aprobación y descartar aprobaciones obsoletas cuando se suban cambios.
4. Activar **Require status checks to pass before merging**. Seleccionar **CI - lint, tests and coverage** como chequeo obligatorio. Si la interfaz permite seleccionar su origen, elegir **GitHub Actions**.
5. Activar **Require branches to be up to date before merging** y **Do not allow bypassing the above settings**. Mantener deshabilitados los force pushes y el borrado de la rama.
6. Verificar con un pull request de prueba que una cobertura inferior al 70 % marca el chequeo como fallido y bloquea el merge. Restablecer el umbral de cobertura con pruebas y comprobar que el chequeo pasa.

Para mantener el control durante cambios en el propio pipeline, considerar revisión obligatoria por CODEOWNERS para el workflow, la configuración de Jest y los scripts de prueba. Si se habilita una cola de merges más adelante, agregar el evento `merge_group` antes de usarla con este chequeo. [Protección de ramas de GitHub](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches).

La copia local se inicializó en `main`. Al publicar la estrategia de ramas, crear `master` y `develop` en el repositorio remoto y seleccionar `master` como rama predeterminada.
