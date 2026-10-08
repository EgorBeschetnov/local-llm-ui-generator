Local LLM UI Generator

Dashboard
Analytics
Game Menu

A Python desktop app that turns a natural language description into a working user interface, generated entirely on your own machine.

Describe the interface you want, and the app produces an interactive HTML page you can open in your browser. The generated UI is functional: sliders drag, checkboxes toggle, dropdowns open, sidebar navigation works.

How it works

1. You enter a description in the app window.
2. The description is injected into a large prompt stored in the app's Python code.
3. The prompt is sent to a local LLM served by Ollama.
4. The model returns a JSON description of the interface: title, items, background and text colors, hover states, font, layout, border radius, text transforms.
5. A second module renders that JSON into an HTML file.
6. The result opens automatically in your browser.

Nothing leaves your machine. No API keys, no cloud calls, no cost per generation.

Features

- Natural language input (Russian supported)
- Runs fully offline on a local model via Ollama (llama3.2:3b)
- Optional visual reference: attach up to 3 screenshots of a UI you like
- Screenshots are interpreted by LLaVA (multimodal) and folded into the prompt, so the output borrows layout and style from your references
- Automatic styling: colors, layout and components chosen by the model
- Interactive output: generated sliders, toggles, dropdowns and navigation actually work
- Covers many interface types: game menus, dashboards, settings panels, calculators, file managers, media players
- Full session logging for analysis and debugging

Stack

- Python 3.11+
- Ollama (llama3.2:3b, LLaVA for image input)
- Local inference

Install

pip install -r requirements.txt

ollama pull llama3.2:3b

Run

python main.py

Performance

Measured on a laptop with Ryzen 5 and a GTX 1650 Ti:

- Text-only description: ~15 to 20 seconds
- With image references (up to 3 screenshots): 1 to 2 minutes

Project structure

- main.py: entry point and app window
- generator.py: builds the prompt and calls the local model
- parser.py: parses the model's JSON response
- templates/: HTML templates used to render the interface
- inspiration/: reference screenshots used as visual input
- output/: generated HTML pages
- sessions/: generation logs (JSON)
- logger.py: logging

Known limitations

The bundled llama3.2:3b model is small, so distinct prompts often converge on similar layouts and styling. Output quality is sensitive to prompt detail: more specific descriptions produce more varied results. These are known tradeoffs of running a compact model locally rather than a large hosted one.

Notes

Built as a diploma project for a Computer Science degree.
