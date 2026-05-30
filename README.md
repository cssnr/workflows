[![GitHub Last Commit](https://img.shields.io/github/last-commit/cssnr/workflows?logo=listenhub&label=updated)](https://github.com/cssnr/workflows/pulse)
[![GitHub Repo Size](https://img.shields.io/github/repo-size/cssnr/workflows?logo=buffer&label=repo%20size)](https://github.com/cssnr/workflows?tab=readme-ov-file#readme)
[![GitHub Top Language](https://img.shields.io/github/languages/top/cssnr/workflows?logo=devbox)](https://github.com/cssnr/workflows?tab=readme-ov-file#readme)
[![GitHub Contributors](https://img.shields.io/github/contributors-anon/cssnr/workflows?logo=southwestairlines)](https://github.com/cssnr/workflows/graphs/contributors)
[![GitHub Issues](https://img.shields.io/github/issues/cssnr/workflows?logo=codeforces&logoColor=white)](https://github.com/cssnr/workflows/issues)
[![GitHub Discussions](https://img.shields.io/github/discussions/cssnr/workflows?logo=theconversation)](https://github.com/cssnr/workflows/discussions)
[![GitHub Forks](https://img.shields.io/github/forks/cssnr/workflows?style=flat&logo=forgejo&logoColor=white)](https://github.com/cssnr/workflows/forks)
[![GitHub Repo Stars](https://img.shields.io/github/stars/cssnr/workflows?style=flat&logo=gleam&logoColor=white)](https://github.com/cssnr/workflows/stargazers)
[![GitHub Org Stars](https://img.shields.io/github/stars/cssnr?style=flat&logo=apachespark&logoColor=white&label=org%20stars)](https://cssnr.github.io/)
[![Discord](https://img.shields.io/discord/899171661457293343?logo=discord&logoColor=white&label=discord&color=7289da)](https://discord.gg/wXy6m2X8wY)
[![Ko-fi](https://img.shields.io/badge/Ko--fi-72a5f2?logo=kofi&label=support)](https://ko-fi.com/cssnr)

# Workflows

~~Reusable~~ Workflows.

- https://docs.github.com/en/actions/how-tos/reuse-automations/reuse-workflows

Coming soon...

| Workflow File                                              | Uses Line                                              |
| :--------------------------------------------------------- | :----------------------------------------------------- |
| [npm-build.yaml](.github/workflows/npm-build.yaml)         | `cssnr/workflows/.github/workflows/npm-build.yaml`     |
| [deploy-static.yaml](.github/workflows/deploy-static.yaml) | `cssnr/workflows/.github/workflows/deploy-static.yaml` |

Example using both workflows: [django-files/django-files.github.io/dev.yaml](https://github.com/django-files/django-files.github.io/blob/master/.github/workflows/dev.yaml)

### npm-build.yaml

```yaml
jobs:
  build:
    name: 'Build'
    if: ${{ !contains(github.event.head_commit.message, '#nodev') }}
    uses: cssnr/workflows/.github/workflows/npm-build.yaml@master
    permissions:
      contents: read
    with:
      install: 'npm ci' # install command
      build: 'npm run build' # build command
      path: 'dist' # directory of artifacts
      name: 'artifact' # artifact name
      pages: false # create a pages artifact
    secrets:
      webhook: ${{ secrets.webhook }} # failure notification

  # Example Usage
  deploy:
    name: 'Deploy'
    needs: build
    runs-on: ubuntu
    steps:
      - name: 'Download Artifact'
        uses: actions/download-artifact@v5
        with:
          name: 'artifact'
      - name: 'Debug'
        run: ls -lAh .
```

### deploy-static.yaml

```yaml
jobs:
  build:
    # Example Usage
    - name: 'Upload Artifact'
      uses: actions/upload-artifact@v4
      with:
        path: dist
        name: 'artifact'

  deploy:
    name: 'Deploy'
    uses: cssnr/workflows/github/workflows/deploy-static.yaml
    needs: build
    permissions:
      contents: read
    with:
      name: 'dev' # Environment name and url
      url: 'https://dev-static.cssnr.com/github-projects'
      path: 'github-projects' # Optional path/subdirectory
      robots: true # Add robots.txt to block robots
      artifact: 'artifact' # Custom artifact name
      dest: '/static' # Target rsync destination
    secrets:
      host: ${{ secrets.DEV_DEPLOY_HOST }}
      port: ${{ secrets.DEV_DEPLOY_PORT }}
      user: ${{ secrets.DEV_DEPLOY_USER }}
      pass: ${{ secrets.DEV_DEPLOY_PASS }}
      webhook: ${{ secrets.DISCORD_WEBHOOK }} # Optional discord notification
```

# Contributing

For instructions on modifying the documentation see the [CONTRIBUTING.md](#contributing-ov-file).

Please consider making a donation to support the development of this project
and [additional](https://cssnr.com/) open source projects.

[![Ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/cssnr)

For a full list of current projects visit: [https://cssnr.github.io/](https://cssnr.github.io/)
