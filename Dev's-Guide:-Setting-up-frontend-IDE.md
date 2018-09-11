This sections explains how to set up IDE for local frontend development.

- [Prerequisites](#prerequisites)
- [Setting up IDEA project](#setting-up-idea-project)

## Prerequisites

Any IDE, but we highly recommend using IntelliJ IDEA. This section will only cover setup on IDEA.

## Setting up IDEA project

1. Open IDEA.
1. Click **Open**, and then select `judgels-frontends/raphael` directory. The project should now be ready.
1. Configure linters:
   1. Open **Preferences**.
   1. Go to **Tools** -> **File Watchers**.
   1. Add the following two entries: Prettier TS and Prettier TSX as depicted below.

     [[images/prettier-ts.png]]
     [[images/prettier-tsx.png]]
   
   Now, whenever you edit and save files, Prettier will be run to format the files.

1. Configure Jest for testing:
   1. Open **Run** -> **Edit configurations...**
   1. Select **Jest** under **Defaults** on the left.
   1. Edit the options and environment variables as depicted below.

      [[images/jest-configuration.png]]

   Now, you can run tests from IDEA.