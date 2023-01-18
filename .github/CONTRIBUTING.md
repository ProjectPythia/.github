# Project Pythia Cookbook Contributor's Guide

Project Pythia Cookbooks are collections of more advanced and domain-specific example
workflows building on top of [Pythia Foundations](https://foundations.projectpythia.org/landing-page.html).
They are [geoscience](https://en.wikipedia.org/wiki/Earth_science)-focused
and should direct the reader towards the [Foundations material](https://foundations.projectpythia.org/landing-page.html) for any required
background knowledge.

The following is a step-by-step guide to getting your cookbook idea
hosted on the [Project Pythia Cookbooks gallery](https://cookbooks.projectpythia.org).

Before you begin, ask yourself if the content you are developing for a cookbook would be better suited as an addition to an existing cookbook.

1. Use the template
   1. If you don't already have a GitHub account, create one by following the [Getting Started with GitHub guide](https://foundations.projectpythia.org/foundations/getting-started-github.html)
   1. On https://github.com/ProjectPythia/cookbook-template, click "Use this template"
   1. Choose "Include all branches"
   1. Create the repo under your account with a descriptive name, followed by `-cookbook` (e.g. `hydrology-cookbook`, `hpc-cookbook`, `cesm-cookbook`, etc.) by entering a name into the "Repository name" field and clicking on "Create repository from template"
   1. Your browser should be directed to the newly created repository under your GitHub account. Under Settings, enable GitHub Pages by changing the Source from "None" to `gh-pages` and clicking on "Save"
   1. [Clone the repo](https://foundations.projectpythia.org/foundations/github/github-cloning-forking.html) in your local workspace and `cd` into your cookbook directory
1. Create the environment
   1. Within `environment.yml`, change `name:` from `cookbook-dev` to `<your-cookbook-name>-dev` (e.g. `cesm-cookbook-dev`) and add all required libraries and other dependencies under `dependencies:`. Commit the changes
   1. Create the Conda environment with `conda env create -f environment.yml`. If it crashes, try running `conda config --set channel_priority strict`
   1. Activate your environment with `conda activate <env-name>`
   1. Update the `.github/workflows/nightly-build.yaml` and `.github/workflows/publish-book.yaml` files to include the new name of the environment (ex. `cesm-cookbook-dev`)
1. Add content
   1. After [creating a new git branch](https://foundations.projectpythia.org/foundations/github/git-branches.html), edit (and duplicate as necessary) the notebook template `notebooks/notebook-template.ipynb` to add your content. Add folders to organize notebooks into sections if applicable
   1. Add the notebooks to `_toc.yml`. See [`radar-cookbook/_toc.yml`](https://github.com/ProjectPythia/radar-cookbook/blob/main/_toc.yml) for syntax
   1. Replace the `thumbnail.svg` with a thumbnail image relevant to your cookbook
   1. Change `README.md` to include your cookbook title, a sentence or two describing the cookbook, and if desired embed your thumbnail image. See the [Radar Cookbook](https://github.com/ProjectPythia/radar-cookbook/blob/main/README.md) for an example
   1. In the badge links in `README.md`, change `cookbook-template` to your cookbook repo name
   1. Replace the `title`, `author`, `description`, `thumbnail`, and the domain and package `tags` fields in the `_config.yml` file with values relevant to your cookbook. These values will affect how information about your cookbook is displayed in the gallery.
   1. Commit your changes with git, and [open a Pull Request](https://foundations.projectpythia.org/foundations/github/github-pull-request.html) on your cookbook repo. When you open a PR there, the github-actions bot will comment a link to a preview of your cookbook
1. Transfer cookbook to the [ProjectPythia](https://github.com/ProjectPythia) organization

   1. Navigate to the settings of your repo, scroll down to the Danger Zone, and click "Transfer"
      1. For ProjectPythia owners or members: type "ProjectPythia", confirm, and transfer
      1. For outside contributors:
         1. Contact an owner of ProjectPythia to be added as an outside collaborator. Then transfer to ProjectPythia; or
         1. Type the username of an owner or member. They will then tranfer it to ProjectPythia and add you as an outside collaborator on that repo
   1. Replace the `repository_url` in the `sphinx/config/html_theme_options` of the `_config.yml` file to point to your cookbook's GitHub repository within the [ProjectPythia](https://github.com/ProjectPythia) organization
   1. Make sure the workflow settings under Settings-->Actions-->General are set to allow Github Actions to **push** to the repository <img width="901" alt="Screenshot 2023-01-13 at 3 12 47 PM" src="https://user-images.githubusercontent.com/26660300/212428991-cd0ae2f0-73ca-40d8-b983-f122359463aa.png"> (Please reach out if you are not able to access the Settings for your repository by tagging @ProjectPythia/core)

   1. Open issues, PRs, and continue making edits as necessary

1. Add your Cookbook to the Cookbook gallery!
   1. Navigate to the [Cookbooks Gallery](https://cookbooks.projectpythia.org/)
   1. Click the "Submit a New Cookbook" button, which will redirect you to a [new cookbook PR template](https://github.com/ProjectPythia/cookbook-gallery/issues/new?assignees=ProjectPythia%2Feducation&labels=content%2Ccookbook-gallery-submission&template=update-cookbook-gallery.yaml&title=Update+Gallery+with+new+Cookbook)
   1. Add the root name of your cookbook repository in the relevant field and any other information you'd like the team to know
   1. Your request will be reviewed, and you will be notified once your content has been accepted or if changes are requested
