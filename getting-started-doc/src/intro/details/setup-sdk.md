# Setup the DevRock-SDK

**Preconditions**: 
- Java must be installed. 
We currently advice Java v17 or later. Type `java --version` to see if you are set up properly. [Read more....](install-java.md).
- Be prepared to work on the command line / terminal (on Windows, Mac, or Linux). The initial setup and understanding of important tools require this. 

### The DevRock-SDK developer package
  - Download the package from here: [Download SDK](https://academy.modularmind.eu/services/download-sdk) 
  - Unpack the `devrock-sdk` root folder from the zip file to a directory of your choice. We recommend this directory being close to a root to keep paths as short as possible. For example: `/dir-of-your-choice/devrock-sdk/`
  - Add `devrock-sdk/tools/jinni/bin` to your **PATH** environment variable
  - Important for Windows users: Add the `devrock-sdk` folder to the exception list in Windows Virus & threat protection settings. Otherwise, Windows will scan all downloaded files one-by-one, causing performance problems.  
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

__Further reading:__
  - [What is the "devrock-sdk"?](devrock-sdk.md)
  - [What is an "dev-environment, aka devenv"?](dev-environment.md)
  - [Introduction to jinni](intro-jinni.md)
  
***

## Tutorials

It is highly advised to learn the content of this documentation by going through a series of practical exercises. 

[Exercises...](../practice/jinni.md).


## More detailed information

[Read more...](configuration.md).
