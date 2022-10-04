# IEEE

- first slide: 
    - create a github account if you don't have one
    - make sure your internet connection works
- TODO check wifi situation at the conference
- TODO get colored sticky notes
- explain connection readme and howfairis score side by side
- test installation instructions on clean ubuntu
- test installation instructions on windows with git bash
- validating a JSON file JSON schema validator
- zenodo mention cant upload file (deposition?) with the same hash, easy workaround is echoing datetime to the upload file
- looks like there may be a bug with ignoring remote howfairis config files, im getting an assertionerror
- TODO add installation instructions for node, npm

on fedora>=35,
  - `python3` installed by default
  - `pip` can be installed with `sudo dnf install python3-pip`
  - `venv` is installed
  - `cffconvert` installable with `sudo dnf install cffconvert`
  - `jq` installed by default
  - `sudo dnf install nodejs`, includes `npm`
  - `sudo npm install -g zenodraft`

on ubuntu 22,
  - `python3` installed by default
  - `pip` can be installed with `sudo apt install python3-pip`
  - `venv` can be installed with `sudo apt install python3-venv`
  - jq can be installed with `sudo apt install jq`
  - `cffconvert` installable from pypi
  - `nodejs==12.22` installable with `sudo apt install nodejs`, looks like that works though
  - `npm==8.5` installable with `sudo apt install npm`
  - `curl` installable with `sudo apt install curl`

on windows,
  - test `which` command on windows git bash (alternative `where`)
  - installing jq on windows

json schema lint
```json
{
  "$ref": "https://zenodraft.github.io/metadata-schema-zenodo/0.2.0/schema.json"
}
```

minimal accepted document:

```json
{
  "access_right": "open",
  "upload_type": "other",
  "title": "the title",
  "license": "Apache-2.0",
  "description": "The description"
}
```

## interest poll

1. making your code citable with CITATION.cff & cffinit
1. GitHub-Zenodo integration
1. zenodraft, zenodo metadata schema
1. ARDC checklist?

## introduction

_(presentation, 20 minutes)_

1. hello and welcome
1. layout of the session / set expectations. Typical structure:
    1. I demo, you watch
    1. hands on trying it out yourself, exploring
1. my goals
    1. make you aware of tools, resources, workflows out there
    1. gather feedback
1. introduce fair-software.nl
    1. provides context for rest of the tutorial
    1. consider adding your organization as an endorser mailto:fair-software@esciencecenter.nl
1. fair principles / fair principles paper
