# How FAIR is your software? Introduction and Tutorial

## `howfairis`

## fair-software GitHub action

## `fairtally`

## Additional materials

### Citation File Format and its tooling

Tools and format together with Stephan Druskat (DLR, UBerlin, SSI), Arfon Smith (GitHub), Rob Haines (UManchester), and contributors.

- cffinit
- cffconvert

### Draft and publish depositions on Zenodo with `zenodraft` CLI

**This section in brief**

1. download and install Node and NPM
1. download and install `zenodraft` from https://npmjs.com
1. get access tokens for Zenodo Sandbox
1. use `zenodraft` to publish a local file to Zenodo Sandbox
1. use `zenodraft` to attach metadata to the new deposition on Zenodo Sandbox

Since we're only exploring at the moment, this tutorial uses the Zenodo Sandbox environment instead of regular Zenodo. The `zenodraft` commands work the same for either target platform, just make sure to leave out the `--sandbox` flag, and don't forget you need separate tokens for each platform.

Also note that some of the commands used in this section, specifically how environment variables are handled, are for Linux or Mac terminal emulator programs. If you're on Windows, "Git Bash" from the "Git for Windows" package is probably your best bet. You can download it from here: https://gitforwindows.org/.

Before we get started, make sure you have the required programs:

```shell
# assert you have node and npm and zenodraft (after prerequisite sections)
node --version       # I'm on v16.15.0
npm --version        # I'm on 8.5.5
zenodraft --version  # I'm on 0.12.0
```

In order to use Zenodo Sandbox, you are required to identify yourself using a token. Get the token here https://sandbox.zenodo.org/account/settings/applications/. `zenodraft` will look for an environment variable by the name of `ZENODO_SANDBOX_ACCESS_TOKEN` whose value you should set to the value of your token.

```shell
# add tokens to terminal
export ZENODO_SANDBOX_ACCESS_TOKEN=<your-zenodo-sandbox-token>
```

Let's create an empty draft deposition in a new collection. If successful, it will return the identifier for the first version in the new collection, which is empty at the moment and still a draft / unpublished.

```shell
VERSION_ID=$(zenodraft deposition create concept --sandbox)
```

Now point your browser to https://sandbox.zenodo.org and click "Upload" (button at the center top of the page; may ask you to provide credentials). After the jump, you should see a list of your depositions on Zenodo Sandbox. If everything worked, the top one is the one you just made. It should still be in unpublished/draft mode.

Let's add a file to the draft deposition. Just use some dummy file, but make sure it has some content otherwise Zenodo doesn't play nice.

```shell
# make some fake data
echo 'some data' > thefile.txt
```

Now upload the file to the newly created deposition

```shell
zenodraft file add --sandbox $VERSION_ID thefile.txt
```

Next, let's add some metadata to the deposition. We can store this metadata in a local file, typically named `.zenodo.json`. 

```shell
# add the metadata using data from a metadata file
zenodraft metadata update --sandbox $VERSION_ID .zenodo.json
```

Zenodo supports a lot of metadata, but documentation is a bit sparse at the moment. The unofficial JSONschema for Zenodo depositions is available here: https://github.com/zenodraft/metadata-schema-zenodo. You can use tools such as JSONlint (https://jsonlint.com) to make sure the file you're writing is valid JSON, and tools like JSONSchemaValidator (https://www.jsonschemavalidator.net/) to make sure the JSON follows the layout that Zenodo expects.

For a glimpse of what is possible, have a look at https://sandbox.zenodo.org/record/1049232, a dummy deposition where we tried to use all the supported properties.

OK, we're almost near the end of this section. We just need to use `zenodraft` to finalize the deposition. Note that once you finalize a deposition, you can no longer update the files in the deposition themselves (but the metadata can still be updated afterwards). Also note that finalizing can also be done by navigating to the Zenodo Sandox interface and clicking the button there.

```shell
# Optionally finalize the deposition from this command line, or via Zenodo interface
zenodraft deposition publish --sandbox $VERSION_ID
```

### Recommended workflow to publish on Zenodo with maximum metadata

Prerequisites:

- section above on Citation File Format
- section above on `zenodraft`
- GitHub Actions

**This section in brief**

1. Take a GitHub repo
1. Add a `CITATION.cff` file
1. Add the `zenodraft` GitHub action
1. Configure the workflow such that it will create a new version in an existing collection on Zenodo Sandbox each time a new release is published on GitHub.
1. Update the workflow file with a step to convert data from CITATION.cff to equivalent Zenodo JSON
1. Update the workflow file with a step to merge metadata from different sources into one file, which is then used when pushing the deposition to Zenodo Sandbox.

Problems with Zenodo-GitHub integration:

- when using CITATION.cff in your repo, minor ingestion errors (e.g. `name-particle`)
- CITATION.cff ingestion supports only small subset of what Zenodo metadata can do

In the current situation, one is forced to choose between good metadata rendering on GitHub citation widget, or good and extensive metadata on Zenodo. However, by combining `cffconvert`, `zenodraft`, GitHub actions, and `jq` (a command line JSON processor program), it's possible to have the best of both worlds. The rest of this section is dedicated to outlining the required workflow.

### Checklist for FAIR research software

This checklist is a collaboration between Australian Research Data Council and Netherlands eScience Center. The questions in the checklist are based on discussions from the FAIR4RS initiative. Although the checklist is already in a usable state, be aware that it is still a work in progress. In particular, the checklist is hosted at GitHub pages at the moment. Because GitHub Pages URLs are a bit unwieldy, it's likely that the URL will change. Be aware that this may break hyperlinks, which may mean that you have to redo any previous self assessments (which isn't a lot of work if you have no more than a handful of projects, but still).

The checklist is designed to be interactive, and yields a "FAIRness" badge that developers can put in their project's README file:

```MarkDown
[![FAIRness badge image](https://ardc-fair-checklist.github.io/ardc-fair-checklist/badge.svg)](https://ardc-fair-checklist.github.io/ardc-fair-checklist/#/software?v=0.1&f=000000&a=0000&i=00&r=000000)
```

The snippet above renders like this:

[![FAIRness badge image](https://ardc-fair-checklist.github.io/ardc-fair-checklist/badge.svg)](https://ardc-fair-checklist.github.io/ardc-fair-checklist/#/software?v=0.1&f=000000&a=0000&i=00&r=000000)

The advantage of this approach is that when visitors come to the project's README, they can restore the FAIRness self assessment state by clicking on the badge. This helps both with transparency and with metrics collection, while nudging researchers toward FAIRer practices.

Go to https://ardc-fair-checklist.github.io/ardc-fair-checklist and see for yourself!
