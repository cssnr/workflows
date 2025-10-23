[![GitHub Last Commit](https://img.shields.io/github/last-commit/smashedr/github-projects?logo=vitepress&logoColor=white&label=updated)](https://github.com/smashedr/github-projects/pulse)
[![GitHub Contributors](https://img.shields.io/github/contributors-anon/smashedr/github-projects?logo=github)](https://github.com/smashedr/github-projects/graphs/contributors)
[![GitHub Repo Size](https://img.shields.io/github/repo-size/smashedr/github-projects?logo=bookstack&logoColor=white&label=repo%20size)](https://github.com/smashedr/github-projects)
[![GitHub Discussions](https://img.shields.io/github/discussions/smashedr/github-projects?logo=github)](https://github.com/smashedr/github-projects/discussions)
[![GitHub Repo Stars](https://img.shields.io/github/stars/smashedr/github-projects?style=flat&logo=github)](https://github.com/smashedr/github-projects/stargazers)
[![GitHub Org Stars](https://img.shields.io/github/stars/cssnr?style=flat&logo=github&label=org%20stars)](https://cssnr.github.io/)
[![Discord](https://img.shields.io/discord/899171661457293343?logo=discord&logoColor=white&label=discord&color=7289da)](https://discord.gg/wXy6m2X8wY)
[![Ko-fi](https://img.shields.io/badge/Ko--fi-72a5f2?logo=kofi&label=support)](https://ko-fi.com/cssnr)

# Workflows

~~Reusable~~ Workflows.

- https://docs.github.com/en/actions/how-tos/reuse-automations/reuse-workflows#passing-inputs-and-secrets-to-a-reusable-workflow

Coming soon...

| Workflow File                                              | Uses Line                                              |
| :--------------------------------------------------------- | :----------------------------------------------------- |
| [deploy-static.yaml](.github/workflows/deploy-static.yaml) | `cssnr/workflows/.github/workflows/deploy-static.yaml` |

### deploy-static.yaml

```yaml
jobs:
  build:
    name: "Build"
    ## Build and upload an "artifact"

  deploy:
    name: "Deploy"
    uses: cssnr/workflows/github/workflows/deploy-static.yaml
    needs: build
    permissions:
      contents: read
    with:
      name: "dev" # Environment name and url
      url: "https://dev-static.cssnr.com/github-projects"
      path: "github-projects" # Optional path/subdirectory
      robots: true # Add robots.txt to block robots
      artifact: "artifact" # Custom artifact name
      dest: "/static" # Target rsync destination
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
