# docker-whale

Run me : `docker run -p80:80 ushamandya/whale-example`

Build me: `docker build -t ushamandya/whale-example .`

# Some notes

Experienced issues with:
* Building GitHub cache — it seems the cache is expected to exist first
* Tagging — in VS Code tags are pushed through the command palette: `Git: Push Tags`
* GitHub repo casing — could not build to the GitHub repository using a dynamic variable name (see below)
## GitHub Container Repo Casing

The following instruction resulted in an error:

```
# Include builder and cache properties
- name: Build and push
  id: docker_build
  uses: docker/build-push-action@v2
  with:
    context: ./
    file: ./Dockerfile
    builder: ${{ steps.buildx.outputs.name }}
    push: true
    tags: ghcr.io/${{ github.repository_owner }}/simplewhale:latest
```

```
buildx failed with: error: invalid tag "ghcr.io/JessicaOPRD/simplewhale:latest": repository name must be lowercase
```

This is an issue with casing. I could not quickly determine a way to solve this in the context of this tutorial. One way is to use an additional step in the process that applies lowercase to the variable. There are numerous solutions. Here I hard-coded as proof-of-concept.