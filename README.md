<!-- start title -->

# GitHub Action:Upload a released helm chart to a git helm charts repository

<!-- end title -->
<!-- start description -->

Extracts a helm chart from a release, adds it to a git helm repository, then reindexes the repository. This action is designed to be run on a release trigger, and to extract a packaged chart in .tgz format from a .tgz file such as chart.tgz.

<!-- end description -->
<!-- start contents -->
<!-- end contents -->
<!-- start usage -->

```yaml
- uses: swarm-io/action-upload-chart-git@undefined
  with:
    # Github token to use, must specify a PAT so that the action can clone the charts
    # repo and push changes to it
    token: ""

    # Release tag to fetch chart from
    # Default: ${{ github.event.release.tag_name }}
    tag: ""

    # the asset name containing the chart, must be a tar file
    # Default: chart.tgz
    release-asset-name: ""

    # The git repository to upload the chart to
    # Default: ${{ github.repository_owner }}/charts
    chart-repository: ""

    # The git repository ref to push the chart to
    # Default: main
    chart-repository-ref: ""
```

<!-- end usage -->
<!-- start inputs -->

| **Input**                  | **Description**                                                                                             |               **Default**               | **Required** |
| :------------------------- | :---------------------------------------------------------------------------------------------------------- | :-------------------------------------: | :----------: |
| **`token`**                | Github token to use, must specify a PAT so that the action can clone the charts repo and push changes to it |                                         |   **true**   |
| **`tag`**                  | Release tag to fetch chart from                                                                             | `${{ github.event.release.tag_name }}`  |  **false**   |
| **`release-asset-name`**   | the asset name containing the chart, must be a tar file                                                     |               `chart.tgz`               |  **false**   |
| **`chart-repository`**     | The git repository to upload the chart to                                                                   | `${{ github.repository_owner }}/charts` |  **false**   |
| **`chart-repository-ref`** | The git repository ref to push the chart to                                                                 |                 `main`                  |  **false**   |

<!-- end inputs -->
<!-- start outputs -->
<!-- end outputs -->
<!-- start examples -->

### Example usage

```yaml
name: Upload Released Chart
on:
  release:
    types:
      - published
jobs:
  upload-chart-gar:
    runs-on: ubuntu-latest
    steps:
      - name: Dump Context
        uses: crazy-max/ghaction-dump-context@v1
      - name: Push Chart
        uses: swarm-io/action-upload-chart-git@v1
        with:
          token: ${{ secrets.GIT_RUNNER_TOKEN }}
```

<!-- end examples -->
<!-- start [.github/ghdocs/examples/] -->
<!-- end [.github/ghdocs/examples/] -->
