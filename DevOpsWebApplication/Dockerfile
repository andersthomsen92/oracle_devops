# Log in to GitHub Container Registry (GHCR)
- name: Log in to GHCR
  uses: docker/login-action@v2
  with:
    registry: ghcr.io
    username: ${{ github.actor }}
    password: ${{ secrets.GITHUB_TOKEN }}

# Build the Docker image
- name: Build and Push Docker image
  run: |
    docker build \
      -t ghcr.io/${{ github.repository }}:staging \
      -t ghcr.io/${{ github.repository }}:${{ steps.semver-app.outputs.version }} \
      -f DevOpsWebApplication/Dockerfile \
      .

    docker push ghcr.io/${{ github.repository }} --all-tags

# Register a release in the GitHub repository
- name: Create release notes
  uses: ncipollo/release-action@v1
  with:
    tag: ${{ steps.semver-app.outputs.version }}
    generateReleaseNotes: true
    body: |
      This release includes the following container image:
      http://ghcr.io/${{ github.repository }}:${{ steps.semver-app.outputs.version }}
