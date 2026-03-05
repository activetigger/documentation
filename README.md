# ActiveTigger Documentation

This repository contains the documentation for [ActiveTigger](https://github.com/activetigger/activetigger), a collaborative text annotation web tool designed for computational social sciences. ActiveTigger assists researchers in exploring, annotating, and classifying text datasets using active learning and BERT model fine-tuning — without writing a single line of code.

The documentation is built with [MkDocs](https://www.mkdocs.org/) and available at: https://activetigger.github.io/documentation/


## Documentation structure

- **First steps** — Quickstart guide, use cases, access, environmental impact
- **Functionalities** — Detailed pages for each feature (annotation, codebook, models, export, generative AI, etc.)
- **Theoretical concepts** — Key concepts and glossary
- **Showcase** — Real-world use cases
- **Software** — Architecture and contributors
- **FAQ** — Common questions

## Building the documentation locally

Make sure you have Python and MkDocs installed:

```bash
pip install mkdocs
```

Then serve the documentation locally:

```bash
mkdocs serve
```

The site will be available at `http://127.0.0.1:8000`.

## Contributing

Contributions are welcome! Here's how you can help:

### Reporting issues

If you spot an error, a typo, or missing information, please [open an issue](../../issues) describing the problem.

### Proposing changes

1. **Fork** this repository
2. **Create a branch** for your changes (`git checkout -b my-contribution`)
3. **Edit or add** Markdown files in the `docs/` directory
4. **Preview** your changes locally with `mkdocs serve`
5. **Submit a pull request** with a clear description of what you changed and why

### Writing guidelines

- Keep language clear and accessible — the audience is social science researchers, not developers
- Use [admonitions](https://squidfunk.github.io/mkdocs-material/reference/admonitions/) (`!!! info`, `!!! warning`) to highlight tips and important notes
- Add screenshots or diagrams when they help illustrate a workflow
- If you add a new page, register it in `mkdocs.yml` under the appropriate section

### Other ways to contribute

- Suggest new use cases or tutorials based on your experience with ActiveTigger
- Improve existing pages with clearer explanations or updated screenshots
- Translate documentation into other languages
- Join the Discord community to help answer questions from other users
