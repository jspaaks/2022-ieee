# IEEE

- first slide: 
    - create a github account if you don't have one
    - make sure your internet connection works
- TODO check wifi situation at the conference
- TODO get colored sticky notes
- explain connection readme and howfairis score side by side
- test installation instructions on clean ubuntu
- test installation instructions on clean fedora
- test installation instructions on windows with git bash
- test `which` command on windows git bash
- installing jq on windows
- after adding a cff, check you have the widget
- validating a JSON file with JSONlint, with JSON schema validator .zenodo.extras.json
- zenodo mention cant upload empty file
- zenodo mention cant upload file (deposition?) with the same hash, easy workaround is echoing datetime to the upload file
- update tentative schedule
- looks like there may be a bug with ignoring remote howfairis config files, im getting an assertionerror

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
