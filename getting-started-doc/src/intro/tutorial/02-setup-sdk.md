# Setup SDK - Tutorial Introduction

## Install the Devrock-SDK
  - Download the package: [Download SDK](https://api.hiconic-os.org/download-sdk.php)
  - Unpack the `devrock-sdk` root folder from the zip file to a directory of your choice. We recommend this directory being close to your file system root to keep the paths short.<br/>
  **Example:** `/dir-of-your-choice/devrock-sdk/`
  - Add `devrock-sdk/tools/jinni/bin` to your **PATH** environment variable
  - [Generate a Personal Access Token (classic)](https://github.com/settings/tokens) with `read:packages` scope and copy its value (`ghp_AbcD3FGh1jK....`) in the environment variable `GITHUB_READ_PACKAGES_TOKEN`.
  - Important for _Windows_ users: Add the `devrock-sdk` folder to the exception list in _Windows_ `Virus & threat protection` settings. Otherwise, _Windows_ will scan all downloaded files one-by-one, causing performance problems. 
  - verify installation by running `jinni version`. Expected output:
  
  ```plain
            °  ┌────┐
    ┌    ┌──┴───────┘
    └────┘        °
      °°
  Jinni - version: 2.1.<revision>
  get help with: jinni help
  
  DONE
  ```
