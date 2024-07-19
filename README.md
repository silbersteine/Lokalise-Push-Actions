GitHub Actions for Lokalise: Manual upload and download files

## About

This repository contains two GitHub Actions, `ManualPull.yml` and `ManualPush.yml`, designed to streamline the process of managing localization files with Lokalise. The actions allow for manual triggering of pulling and pushing translation files between your GitHub repository and Lokalise, ensuring your localization data is always up-to-date.

## ManualPush.yml

### Overview

The `ManualPush.yml` action pushes your source lnguage localization files from your GitHub repository to Lokalise. This action can be manually triggered to upload the latest translations from your project to Lokalise, ensuring your translation management is always current. It can be triggered from any branch in your repository and tags the keys in Lokalise with the branch name.

### Usage

To use `ManualPush.yml`, ensure you have set up the necessary environment variables and secrets. Trigger the action manually in GitHub to push the latest localization files from your repository to Lokalise.

### Current Parameters and Options

The `ManualPush.yml` action is currently configured with several parameters, including `--replace-modified`, `--include-path`, `--use-automations=true`, and tagging options for inserted, skipped, and updated keys. These settings ensure that the file path is included in the file name for a smooth download process and keys with similar names can coexist in case they are assigned to different filenames.

Please note that additional options are available with the Lokalise CLI. Review the [Lokalise CLI documentation](https://github.com/lokalise/lokalise-cli-2-go/tree/main) for more details on how to customize these parameters further to fit your specific needs.


## ManualPull.yml

### Overview

The `ManualPull.yml` action pulls localization files from Lokalise and commits them to your branch in GitHub. This action fetches the latest translations from Lokalise, ensuring your project always has the most recent localization updates.

### Usage

To use `ManualPull.yml`, make sure you have configured the required environment variables and secrets. Trigger the action manually to pull the latest localization files into your repository. Only files and keys tagged with your repository's branch name will be included in the pull. To avoid missing any keys or files, start your tryanslation workflow by pushing from your branch to ensure that all translation keys in your branch are tagged in Lokalise with your branch's name. This step is crucial for including all relevant translations during the download.

### Current Parameters and Options

The `ManualPull.yml` action is configured with parameters such as `--format json`, `--original-filenames=true`, and `--include-tags`. These settings ensure that localization files are downloaded in JSON format, with original filenames and filepaths, and filtered by branch in your repo using the tags filter. 

Remember that additional options are available with the Lokalise CLI. For further customization and to explore all available parameters, consult the [Lokalise CLI documentation](https://github.com/lokalise/lokalise-cli-2-go/tree/main?tab=readme-ov-file).

## Setup Instructions

1. **Add Secrets and Variables**: Ensure the necessary secrets (`API_TOKEN`) and variables (`PROJECT_ID`, `SOURCE_LANG`, `FOLDER_PATH`) are set in your repository settings.
2. **Manual Trigger**: Both actions are manually triggered using `workflow_dispatch`, allowing you to pull from or push to Lokalise whenever needed.
3. **Important Note**: The folder path specified in the actions may differ from your project's folder structure. Pay close attention to your folder structure and adjust the path in line 42 of the `ManualPull.yml` commit step to match your specific setup. This ensures that files are correctly located and processed according to your repository's organization. The current setup is designed to omit the committing of source language resource files. Remember that Lokalise will substitute hardcoded language ISO codes found in your filenames and folder structure with the %LANG_ISO% placeholder, allowing for dynamic switching of ISO codes for your target languages during download.


## Contributing

Feel free to contribute by opening issues or submitting pull requests. Ensure your code follows the repository's coding standards and includes relevant tests.
