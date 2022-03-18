# CustomGento Mage Marketplace Package Converter Action

CustomGento Mage Marketplace Package Converter Action is a GitHub Action, which creates Marketplace-compatible packages from GitHub releases.

Usually, code in PHP repositories is split into two directories `src` and `tests`. Unfortunately, Magento Marketplace does not support this structure. It expects you to put all your extension code into the root directory. To ease your release process, this action takes care of the conversion, so that you can directly upload a package in the right format to Magento Marketplace.

_If you do not use a `src` directory in your repository, you do not need this action._

Each time you tag a new release, the action will convert your package to a Magento-Marketplace-compatible version. The following steps will be executed:

1. All contents from the `src` directory will be moved to the root directory.
2. In the `composer.json`, all references to the `src` directory will be removed.
3. A zip-package will be created with the updated contents and added to your release.


## Usage

1. Create a personal access token under User Settings > Developer Settings > Personal access tokens with the scope `repo` and copy its value.
2. In the repository settings under Secrets > Actions, create a new repository secret with the name `ACCESS_TOKEN` and the value from (1).
3. In your repository, create a file `.github/workflows/magento-marketplace.yml` with the following contents:

        name: Publish

        on:
          push:
            tags:
              - '*'

        jobs:
          build:
            name: Publish Magento Marketplace Package
            runs-on: ubuntu-latest

            steps:
            - name: Create Marketplace Package
              uses: customgento/mage-marketplace-package-converter-action@main
              with:
                access_token: ${{ secrets.ACCESS_TOKEN }}

Feel free to adapt this default workflow to your needs.


## Credits

Thanks to [@svenstaro](https://github.com/svenstaro) for his [action to upload files to GitHub releases](https://github.com/svenstaro/upload-release-action).


## License

[MIT License](https://github.com/customgento/mage-marketplace-package-converter-action/blob/main/LICENSE)


## Copyright
&copy; 2022 - present CustomGento GmbH
