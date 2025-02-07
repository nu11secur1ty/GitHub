# ghcr (GitHub Container Registry) quickstart

## CLI 

To push container images to ghcr, you need peronal access token (PAT) - see [how to create PAT](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)

1. Get PAT (personal access token)

Personal Settings > Developer settings > [Personal access tokens](https://github.com/settings/tokens)

2. ghcr login test
```bash
# echo $PAT | docker login ghcr.io -u <github_user> --password-stdin
echo $PAT | docker login ghcr.io -u your_user --password-stdin

Login Succeeded
```

3. push
```bash
docker tag mycontainer ghcr.io/your_user/myrepo/mycontainer:0.0.1
docker push ghcr.io/yokawasa/myrepo/mycontainer:0.0.1
```
4. inspect

```bash
docker inspect ghcr.io/your_user/myrepo/mycontainer:0.0.1
```

## GitHub Actions 

you can do seamless access to containers from Actions workflows via the `GITHUB_TOKEN`

> The Container registry supports the GITHUB_TOKEN for easy and secure authentication in your workflows. If your workflow is using a personal access token (PAT) to authenticate to ghcr.io, then we highly recommend you update your workflow to use the GITHUB_TOKEN.


```yaml
     - name: Log in to registry
        # This is where you will update the PAT to GITHUB_TOKEN
        run: echo "${{ secrets.GITHUB_TOKEN }}" | docker login ghcr.io -u ${{ github.actor }} --password-stdin
```

See [Upgrading a workflow that accesses ghcr.io](https://docs.github.com/en/packages/managing-github-packages-using-github-actions-workflows/publishing-and-installing-a-package-with-github-actions#upgrading-a-workflow-that-accesses-ghcrio) for more detail 


## Associate a certain package to a repository

- [Connecting a repository to a package](https://docs.github.com/en/packages/learn-github-packages/connecting-a-repository-to-a-package)

## REFERENCES
- https://github.com/features/packages
- [Upgrading a workflow that accesses ghcr.io](https://docs.github.com/en/packages/managing-github-packages-using-github-actions-workflows/publishing-and-installing-a-package-with-github-actions#upgrading-a-workflow-that-accesses-ghcrio)
