# Discussion Category Templates

Discussion category forms collect structured information when someone starts a discussion in your repository.

## About discussion category forms

Define forms in YAML using [GitHub's form schema](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/syntax-for-githubs-form-schema). The schema supports configurable input fields and validation.

Store each form in the repository's `.github/DISCUSSION_TEMPLATE/` directory.

Organization-wide forms can be supplied through a public `.github` repository. See [Creating a default community health file](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file).

Polls do not support discussion category forms. See [About discussions](https://docs.github.com/en/discussions/collaborating-with-your-community-using-discussions/about-discussions).

The following screenshot illustrates a rendered discussion form:

![Example discussion form rendered on GitHub.](https://docs.github.com/assets/cb-83694/images/help/discussions/discussion-category-form-sample.png)

## How to create discussion category forms

You need repository write access to create a form.

1. Open the target repository.
2. Create `.github/DISCUSSION_TEMPLATE/FORM-NAME.yml`. Replace `FORM-NAME` with the discussion category's slug. For example, use `announcements.yml` for an "Announcements" category. See [Creating new files](https://docs.github.com/en/repositories/working-with-files/managing-files/creating-new-files).
3. Add the YAML form definition. See [Syntax for discussion category forms](https://docs.github.com/en/discussions/managing-discussions-for-your-community/syntax-for-discussion-category-forms).
4. Commit the completed file to the repository's default branch.

For the complete procedure, see [Creating discussion category forms](https://docs.github.com/en/discussions/managing-discussions-for-your-community/creating-discussion-category-forms).
