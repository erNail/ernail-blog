# ernail-blog

My personal [blog](https://blog.nailforge.dev/blog) written completely in Markdown

## Contributing

Please check the [`CONTRIBUTING.md`](./CONTRIBUTING.md) to learn how to contribute.

## Development

### Install dependencies

You can install all required dependencies via `Task` and `Homebrew`

```shell
brew install go-task
task install
```

If you'd like to use other tools,
you can find all dependencies and relevant commands in the [`taskfile.yaml`](./taskfile.yaml).

### Run Linting

```shell
task lint
```

### Render Blog

```shell
task serve
```

### Build Blog

```shell
task build
```
