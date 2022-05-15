# clean-workflows-logs-runs V1

Acción de Github que permite la limpieza de los logs de los jobs.

Por defecto usará el token asociado al workflow **${{ secrets.GITHUB_TOKEN }}**

## Usage

```yaml


uses: jmmirand/clean-workflows-logs-runs@main
with:
  # PAT Personal Access Token utilizado para eliminar las ejecuciones
  # Token Temporal de las Actions tiene permisos suficiente.
  myToken: ${{ github.GITHUB_TOKEN }}

  # Numero de ejecuciones que dejamos sin borrar
  # Default: 10
  num_runs: 10

```

## Referencias

* [Plantilla Oficial Accion Github en JavaScript](https://github.com/actions/javascript-action)
* [Referencia del cliente octokit](https://octokit.github.io/rest.js/v18#actions-delete-workflow-run-logs) manera facil de acceder a las APIS de Github
* [Variables de entornos disponibles en una acción](https://docs.github.com/es/actions/learn-github-actions/environment-variables#default-environment-variables)
* Primer contacto [Crear Github Actions Adictos Trabajo](https://www.adictosaltrabajo.com/2020/10/30/como-crear-acciones-utilizando-github-actions/)
* [Librerías JavaScritp para Construccion de Github Actions](https://github.com/actions/toolkit)
* [Gestionar GITHUB_TOKEN](https://dev.to/github/the-githubtoken-in-github-actions-how-it-works-change-permissions-customizations-3cgp)

## Usage

La versión v1 limpia logs de las ejecuciones de workflows del repo actual, borrando
de más antiguo a más nuevo.

* **num_runs** : Numero de ejecuciones que deamos.
* **myToken** : Token Personal con permiso en Repo

```yaml
      - name: JavaScript repeat action
        uses: jmmirand/clean-workflows-logs-runs@v1
        with:
         myToken: ${{ secrets.MY_REPO_TOKEN }}
         num_runs: 12
```

## Create a release branch

Users shouldn't consume the action from master since that would be latest code and actions can break compatibility between major versions.

Checkin to the v1 release branch

```bash
git checkout -b v1
git commit -a -m "v1 release"
```

```bash
git push origin v1
```

Note: We recommend using the `--license` option for ncc, which will create a license file for all of the production node modules used in your project.

Your action is now published! :rocket:

See the [versioning documentation](https://github.com/actions/toolkit/blob/master/docs/action-versioning.md)

## Package for distribution

GitHub Actions will run the entry point from the action.yml. Packaging assembles the code into one file that can be checked in to Git, enabling fast and reliable execution and preventing the need to check in node_modules.

Actions are run from GitHub repos.  Packaging the action will create a packaged action in the dist folder.

Run prepare

```bash
npm run prepare
```

Since the packaged index.js is run from the dist folder.

```bash
git add dist
```

See the [actions tab](https://github.com/actions/javascript-action/actions) for runs of this action! :rocket:
