# Project Pythia Cookbook Contributor's Guide

Project Pythia Cookbooks are collections of more advanced and domain-specific example
workflows building on top of [Pythia Foundations](https://foundations.projectpythia.org/landing-page.html).
They are [geoscience](https://en.wikipedia.org/wiki/Earth_science)-focused
and should direct the reader towards the Foundations material for any required
background knowledge.

The following is a step-by-step guide to getting your cookbook idea
hosted on the [Project Pythia Cookbooks Gallery](https://cookbooks.projectpythia.org).

Before you begin, ask yourself if the content you are developing for a cookbook would be better suited as an addition to an existing cookbook. The best place to discuss cookbook ideas is the [Project Pythia category of the Pangeo Discourse](https://discourse.pangeo.io/c/education/project-pythia/60).

## Data access

Before developing your cookbook, you should consider how it will access the data you plan to use. In loose order of preference, we recommend the following:
1. Rely on data that is already freely available and accessible with tools in the ecosystem. Point to Foundations or other cookbooks for tool how-to guides if needed. Examples include the [CMIP6 Cookbook](https://projectpythia.org/cmip6-cookbook/) and the [CESM LENS on AWS Cookbook](https://projectpythia.org/cesm-lens-aws-cookbook/)
1. Focus on representative subsets of data that can be packaged alongside the cookbook in-repo. An example is the [Landsat ML Cookbook](https://projectpythia.org/landsat-ml-cookbook/README.html)
1. Wait for the Pythia team to explore cloud storage support via NSF JetStream or adjacent efforts
1. Provide the tools and/or clear documentation for accessing the data that you have stored somewhere else

## Use the template

1. If you don't already have a GitHub account, create one by following the [Getting Started with GitHub guide](https://foundations.projectpythia.org/foundations/getting-started-github.html)
1. On https://github.com/ProjectPythia/cookbook-template, click "Use this template&rarr;Create a new repository"
1. Give your repository a descriptive name followed by `-cookbook` (e.g., `hydrology-cookbook`, `hpc-cookbook`, `cesm-cookbook`) and a description
1. Choose "Include all branches" and create the repository. Your browser will be directed to the newly created repository under your GitHub account
1. Under Settings&rarr;Pages, ensure that GitHub Pages is enabled. If it is not, change the Branch from "None" to "gh-pages/(root)" and click "Save"
1. Under Settings&rarr;Actions&rarr;General, allow Github Actions to **push** to the repository <img width="901" alt="Screenshot 2023-01-13 at 3 12 47 PM" src="https://user-images.githubusercontent.com/26660300/212428991-cd0ae2f0-73ca-40d8-b983-f122359463aa.png">

Your cookbook is now ready to have content added. In the rest of this guide, we will mostly assume that you are familiar with git/GitHub. If not, we recommend reading through our [GitHub tutorials in Foundations](https://foundations.projectpythia.org/foundations/getting-started-github.html).

## Set up the environment

1. [Clone the repository](https://foundations.projectpythia.org/foundations/github/github-cloning-forking.html) in your local workspace
1. Within `environment.yml`, change `name` from `cookbook-dev` to `<your-cookbook-name>-dev` (e.g. `cesm-cookbook-dev`) and add all required libraries and other dependencies under `dependencies:`. Commit the changes
1. Create the Conda environment with `conda env create -f environment.yml`. If it crashes, try running `conda config --set channel_priority strict`
1. Activate your environment with `conda activate <env-name>`
1. In `.github/workflows/nightly-build.yaml`, `.github/workflows/publish-book.yaml`, and `.github/workflows/trigger-book-build.yaml`, change the `environment_name` to the name of your environment (ex. `cesm-cookbook-dev`)

## Develop your cookbook

To add content, you should edit (and duplicate as necessary) the notebook template `notebooks/notebook-template.ipynb`. You can add folders to organize notebooks into sections if applicable.
Once you have a set of notebooks that you are ready to share, there are various edits that need to be made so that your cookbook is functional and polished. Here is a checklist to go through before moving on to the next step:

- [ ] Add the notebooks to `_toc.yml` (the table of contents). See [`radar-cookbook/_toc.yml`](https://github.com/ProjectPythia/radar-cookbook/blob/main/_toc.yml) for syntax
- [ ] Edit `README.md` as described in that file. This is the homepage of your cookbook, so it should be descriptive
- [ ] In the badge links in `README.md`, change `cookbook-template` to your cookbook repo name
- [ ] Edit `_config.yml`. These will show up on your [card in the gallery](https://cookbooks.projectpythia.org/)
  - [ ] title
  - [ ] author
  - [ ] description
  - [ ] thumbnail (not logo). You may simply replace the default `thumbnail.png` with your own image
  - [ ] tags
- [ ] Under the `execute` section of `_config.yml`, change `execute_notebooks` from `cache` to either `binder` to run on the Pythia Binder or `force` to run with GitHub Actions. Cookbooks that are expected to use a lot of resources should use the Pythia Binder
- [ ] Clear all notebook outputs, since the Pythia infrastructure will execute the notebooks
- [ ] Ensure that your cookbook successfully builds and shows the executed code

## Transfer cookbook to the [ProjectPythia](https://github.com/ProjectPythia) organization

1. [Contact Project Pythia via the Pangeo Discourse](https://discourse.pangeo.io/c/education/project-pythia/60) (or otherwise) to let us know about your cookbook
1. Someone from the Pythia team will add you as a member of the ProjectPythia organization
1. Once you have accepted the invitation, navigate to the settings of your cookbook repository, scroll down to the Danger Zone, and click "Transfer"
1. Select or type "ProjectPythia", confirm, and transfer
1. Replace the `repository_url` in the `sphinx/config/html_theme_options` of the `_config.yml` file to point to your cookbook's new GitHub repository within the [ProjectPythia](https://github.com/ProjectPythia) organization

You will automatically retain write access to your cookbook, but if you would like to add outside collaborators to the repository, contact a member of the Pythia team to be given the Admin role on your cookbook repository.

You can open issues, PRs, and continue making edits as necessary.

## Add your cookbook to the Cookbooks Gallery!

1. Navigate to the [Cookbooks Gallery](https://cookbooks.projectpythia.org/)
1. Click the "Submit a New Cookbook" button, which will redirect you to a [new cookbook PR template](https://github.com/ProjectPythia/cookbook-gallery/issues/new?assignees=ProjectPythia%2Feducation&labels=content%2Ccookbook-gallery-submission&template=update-cookbook-gallery.yaml&title=Update+Gallery+with+new+Cookbook)
1. Add the root name of your cookbook repository (e.g., just "cesm-cookbook", not the whole URL) and any other information you'd like the team to know
1. Your request will be reviewed, and you will be notified once your content has been accepted or if changes are requested
