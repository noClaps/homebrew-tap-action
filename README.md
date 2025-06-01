# homebrew-tap-action
A GitHub Action to push updates to a Homebrew tap

## Usage

Create a fine-grained token for your Homebrew tap repository, with read and write permssions for Content. Set it as `HOMEBREW_TAP_TOKEN` in your repository's actions secrets.

In your build workflow, put your output binary files into `tar.gz` archives, with the following structure:

```
my-tool-macos-arm64.tar.gz
└── my-tool-macos-arm64

my-tool-linux.tar.gz
└── my-tool-linux
```

You can then use the workflow with:

```yaml
- name: Update Homebrew Tap
  uses: noClaps/homebrew-tap-action@v1
  with:
    tap_repo: 'your-username/homebrew-tap'
    formula_name: 'my-tool'
    version: ${{ github.event.release.tag_name }}
    tap_token: ${{ secrets.HOMEBREW_TAP_TOKEN }}
    macos_file: 'my-tool-macos-arm64.tar.gz'
    linux_file: 'my-tool-linux.tar.gz'
```

When the workflow finishes running, you should have an updated file in your `homebrew-tap/Formula/my-tool.rb` file.
