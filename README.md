# Promnesia-101
[Promnesia](https://github.com/karlicoss/promnesia) set-up and instructions for windows

## Set-up
### Installation

To install Promnesia you need to 
- type `pip3 install --user promnesia` or `pip install --user promnesia` whichever works for you. 
    I faced some issues while instaling with optional dependencies. Solved it by installing these: `pip3 install --user bs4 lxml mistletoe logzero`
- Install the respective "Promnesia" browser extension
    - Chrome/Edge: https://chrome.google.com/webstore/detail/promnesia/kdmegllpofldcpaclldkopnnjjljoiio
    - Firefox: https://addons.mozilla.org/en-US/firefox/addon/promnesia/

### Extra dependencies
Some sources require [additional dependencies](https://github.com/karlicoss/promnesia/blob/master/doc/SOURCES.org#extra-dependencies) which you can install if needed.

- `pip3 install --user promnesia[optional]`

   dependencies that bring some bells & whistles: logzero, python-magic
- `pip3 install --user promnesia[HPI]`

   dependencies for [[https://github.com/karlicoss/HPI][HPI]]: HPI
- `pip3 install --user promnesia[html]`

   dependencies for sources.html: beautifulsoup4, lxml
- `pip3 install --user promnesia[markdown]`

   dependencies for sources.markdown: mistletoe
- `pip3 install --user promnesia[org]`

   dependencies for sources.org: orgparse
- `pip3 install --user promnesia[telegram]`

   dependencies for sources.telegram: dataset
:end:

Alternatively, you can just install all of them in bulk: `pip3 install --user promnesia[all]`.

### Demo

to verify that promnesia has installed successfully, you can run the following command: `python -m promnesia  demo https://github.com/karlicoss/exobrain`

### Custom Set-up

Follow the belo steps to use promnesia for a custom database:

- create the config: 
    ```
    python -m promnesia config create
    ```

    This will create a `config.py` file in your local directory at the following location: `%LocalAppData%\promnesia\promnesia`
- edit the config and add some sources

    Add/Update the source location in the config.py file to the folder where you notes are. Below is my example config:

    <details>
    <summary>My example config</summary>
    
    ```python
    from promnesia.common import Source
    from promnesia.sources import auto

    SOURCES = [
        Source(
            auto.index,
            'C:/Users/AnweshG/AppData/Local/promnesia/promnesia/Local_Promnesia',
            name='My Notes',
        )
    ]

    ```
    </details>

- Indexing in windows with UTF-8. When running `python -m promnesia  index` in windows, you might see an error `character maps to <undefined>`. To solve this, you need to rung the following command before indexing:

    ```
    set PYTHONUTF8=1
    ```
- Indexing all the files

    this command reads all the content in the text documents in the folder mentioned in the config.py & adds them into a database (promnesia.sqlite) for the browser plugin to use
    ```
    python -m promnesia  index
    ```
- run the server: `python -m promnesia serve`
