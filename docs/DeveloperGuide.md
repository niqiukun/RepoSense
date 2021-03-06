<frontmatter>
  title: "Developer Guide"
  header: header.md
  footer: footer.md
  siteNav: mainNav.md
  pageNav: 3
</frontmatter>

# RepoSense - Developer Guide
Thank you for your interest in contributing to RepoSense!

## Setting up

### Prerequisites
1. **JDK `1.8.0_60`** or later. You may download the JDK [here](https://www.oracle.com/technetwork/java/javase/downloads/index.html).
1. **git `2.14`** or later on the command line. You may download git [here](https://git-scm.com/downloads).
 > Type `git --version` on your OS terminal and ensure that you have the correct version of **git**.

### Setting up the project in your computer using IntelliJ
1. Fork this repo, and clone the fork to your computer.
1. Open *IntelliJ* (if you are not in the welcome screen, click `File` > `Close Project` to close the existing project dialog first).
1. Set up the correct *JDK* version for *Gradle*.
    1. Click `Configure` > `Project Defaults` > `Project Structure`.
    1. Click `New…​` and find the directory of the *JDK*.
1. Click `Import Project`.
1. Locate the `build.gradle` file and select it. Click `OK`.
1. Ensure that the selected version of `Gradle JVM` matches our prerequisite.
1. Click `OK` to accept the all the other default settings.

### Verifying the setup
1. Ensure that *Gradle* builds without error by running the command `gradlew clean build`, and ensure that it finishs with a `BUILD SUCCESSFUL` message.
1. Run the tests to ensure that they all pass by running the command `gradlew test systemtest`, and ensure that it finishs with a `BUILD SUCCESSFUL` message.
  > Ensure that you are on the project root directory when using the `gradlew` commands.

### Configuring the Java coding style
This project follows [oss-generic coding standards](https://oss-generic.github.io/process/docs/CodingStandards.html). *IntelliJ’s* default style is mostly compliant with our *Java* coding convention but it uses a different import order from ours. To rectify,

1. Go to `File` > `Settings…`​ (*Windows/Linux*), or `IntelliJ IDEA` > `Preferences…`​ (*macOS*).
1. Select `Editor` > `Code Style` > `Java`.
1. Click on the `Imports` tab to set the order
   * For `Class count to use import with '*'` and `Names count to use static import with '*'`: Set to `999` to prevent IntelliJ from contracting the import statements
   * For `Import Layout`, follow this image below:
   ![import-order](images/import-order.png)

Optionally, you can follow the [Using Checkstyle]({{baseUrl}}/UsingCheckstyle.html) document to configure *Intellij* to check style-compliance as you write code.

### Configuring the JavaScript and CSS coding style
Our project follows the [Airbnb Javascript Style Guide](https://github.com/airbnb/javascript) and [OSS CSS Coding Standard](https://oss-generic.github.io/process/codingStandards/CodingStandard-Css.html), which is governed by the Eslint and Stylelint respectively. We have our own customized style checker for the Pug files, which is governed by pug-lint. Their configuration files can be found at the root of the project. Please run a `npm run lint` from the project root directory and fix all of the lint errors before committing your code for final review.  You can also use the `npm run lintfix` script to automatically fix some of the javascript and css lint errors!

Eslint, Stylelint and their accompanying modules can be installed through NPM, so do ensure that you got it [installed](https://www.npmjs.com/get-npm) if you are working on the report.

### Configuring Cypress for automated front-end testing
We use [Cypress](https://www.cypress.io/) for automated end-to-end front-end testing. <br/>

#### To write tests
1. Create a new test file in `frontend/cypress/tests`
1. At project root start *Cypress Test Runner* by running `gradlew cypress`
1. On the top right hand corner, set `Chrome` as the default browser
1. Under **Integration Tests**, click on the newly created test file to run it
![Cypress Test Runner](images/cypress-test-runner.jpg "Cypress Test Runner")

> Read [Cypress's Documentation](https://docs.cypress.io/api/commands/document.html#Syntax) to familiarize yourself with its syntax and [Cypress's debugging guide](https://docs.cypress.io/guides/guides/debugging.html#Log-Cypress-events) to tackle problems with your tests.

#### To run all tests locally
1.  At project root, run `gradlew frontendTest`
> If you encountered an invalid browser error, please ensure that you have `Chrome` installed in the default installation directory. Otherwise, follow the instructions [here](https://docs.cypress.io/guides/guides/debugging.html#Launching-browsers) to create symbolic links so Cypress can locate `Chrome` in your system.

### (Optional) Using Vue.js devtools for frontend debugging on Chrome
1. On your Chrome, visit the website of [Vue.js devtools](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd) and add the extension.
1. Go the detail page of this extension in Chrome's extension management panel and select `Allow access to file URLs`. If you are unable to locate it, copy the link: `chrome://extensions/?id=nhdogjmejiglipccpnnnanhbledajbpd` and visit it on your Chrome.
1. Open any report generated by RepoSense.
1. Press `F12` or right click and choose `inspect` at the report page.
1. Choose `Vue` at the navigation bar.
![Choose Vue](images/choose-vue.png)
1. Debug using the tool.
![Use Vue](images/use-vue.png)
> See its [Github](https://github.com/vuejs/vue-devtools) page for more details.

### Before writing code
1. Do check out our [process guide]({{baseUrl}}/Process.html) before submitting any PR with your changes.

### Building and running RepoSense from code

1. Execute the following command on the OS terminal inside the project directory. <br/>
Usage: `gradlew run -Dargs="([--config CONFIG_FOLDER] | [--repos REPO_PATH_OR_URL...]) [--view [REPORT_FOLDER]] [--output OUTPUT_DIRECTORY] [--since DD/MM/YYYY] [--until DD/MM/YYYY] [--formats FORMAT...] [--ignore-standalone-config] [--timezone ZONE_ID[±hh[mm]]]"` <br/>
Named Arguments:
``` {.no-line-numbers}
--help, -h           Show help message.
--version, -V        Show the version of RepoSense.
--view [PATH], -v [PATH]
                     Starts a server to display the report in the
                     provided directory. If used as a flag (with no
                     argument), generates a report and automatically
                     displays the report.
--output PATH, -o PATH
                     The directory to output the report folder,
                     reposense-report. If not provided, the report
                     folder will be created in the current working
                     directory.
--since dd/MM/yyyy, -s dd/MM/yyyy
                     The date to start filtering.
--until dd/MM/yyyy, -u dd/MM/yyyy
                     The date to stop filtering.
--formats [FORMAT [FORMAT ...]], -f [FORMAT [FORMAT ...]]
                     The alphanumeric file formats to process.
                     If not provided, all file formats will be
                     used.
                     Please refer to userguide for more information.
--ignore-standalone-config, -i
                     A flag to ignore the standalone config file in
                     the repo.
--timezone ZONE_ID[±hh[mm]], -t ZONE_ID[±hh[mm]]
                     The timezone to use for the generated report.
                     One kind of valid timezones is relative to UTC.
                     E.g. UTC, UTC+08, UTC-1030.
                     If not provided, system default timezone will be used.
--config PATH, -c PATH
                     The directory containing the config files. If not
                     provided, the config files will be obtained from
                     the current working directory.
--repo LOCATION [LOCATION ...], --repos LOCATION [LOCATION ...], -r LOCATION [LOCATION ...]
                     The GitHub URL or disk locations to clone repository.
```

Sample usage to generate the report with no specify arguments: (find and use config files in current working directory)
``` {.no-line-numbers}
gradlew run
```

Sample usage to generate the report with config files and automatically open the report:
``` {.no-line-numbers}
gradlew run -Dargs="--config ./config/ --output output_path/ --since 21/10/2017 --until 21/11/2019 --formats java adoc js --view"
```

Sample usage to generate the report with config files and choose the timezone used to be UTC+8:
``` {.no-line-numbers}
gradlew run -Dargs="--config ./config/ --output output_path/ --timezone UTC+08"
```

Sample usage to generate the report with repository locations and automatically open the report:
``` {.no-line-numbers}
gradlew run -Dargs="--repos https://github.com/reposense/RepoSense.git https://github.com/se-edu/collate.git --output output_path/ --since 21/10/2017 --until 21/11/2017 --formats java adoc js --view"
```

Sample usage to generate the report with repository locations but ignore the standalone config file:
``` {.no-line-numbers}
gradlew run -Dargs="--repos https://github.com/reposense/RepoSense.git https://github.com/se-edu/collate.git --ignore-standalone-config"
```

Sample usage to view the report:
``` {.no-line-numbers}
gradlew run -Dargs="--view output_path/reposense-report"
```

Sample usage to generate the report with config files using the alias of argument:
``` {.no-line-numbers}
gradlew run -Dargs="-c ./config/ -o output_path/ -s 21/10/2017 -u 21/11/2017 -f java adoc js"
```

`-Dargs="..."` uses the same argument format as mentioned above.

## Documentation

Our documentation is powered by [MarkBind](https://markbind.org/).

### Downloading MarkBind

Run the following command to install MarkBind.
``` {.no-line-numbers}
$ npm install -g markbind-cli
```

### Previewing the documentation site

Run the following command while in the `docs` directory. It will generate a website from your documentation files, start a web server, and open a live preview of your site in your default Browser.
``` {.no-line-numbers}
$ markbind serve
```

### MarkBind features

MarkBind's list of comprehensive features is available [here](https://markbind.org/userGuide/index.html).

## Architecture

 ![architecture](images/architecture.png)
*Figure 1. Overall architecture of RepoSense*

### Parser(ConfigParser)
[`Parser`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/parser) contains three components:
 * [`ArgsParser`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/parser/ArgsParser.java): Parses the user-supplied command line arguments into a `CliArguments` object.
 * [`CsvParser`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/parser/CsvParser.java): Abstract generic class for CSV parsing functionality. The following three classes extend `CsvParser`.
   * [`AuthorConfigCsvParser`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/parser/AuthorConfigCsvParser.java): Parses the `author-config.csv` config file into a list of `AuthorConfiguration` for each repository to analyze.
   * [`GroupConfigCsvParser`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/parser/GroupConfigCsvParser.java) Parses the `group-config.csv` config file into a list of `GroupConfiguration` for each repository to analyze.
   * [`RepoConfigCsvParser`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/parser/RepoConfigCsvParser.java): Parses the `repo-config.csv` config file into a list of `RepoConfiguration` for each repository to analyze.
 * [`JsonParser`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/parser/JsonParser.java): Abstract generic class for JSON parsing functionality. The following class extends `JsonParser` class:
   * [`StandaloneConfigJsonParser`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/parser/StandaloneConfigJsonParser.java): Parses the `_reposense/config.json` config file into a `StandaloneConfig`.



### Git
[`Git`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/git) package contains the wrapper classes for respective *git* commands.
 * [`GitBlame`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/git/GitBlame.java): Wrapper class for `git blame` functionality. Traces the revision and author last modified each line of a file.
 * [`GitBranch`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/git/GitBranch.java): Wrapper class for `git branch` functionality. Gets the name of the working branch of the target repo.
 * [`GitCheckout`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/git/GitCheckout.java): Wrapper class for `git checkout` functionality. Checks out the repository by branch name or commit hash.
 * [`GitClone`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/git/GitClone.java): Wrapper class for `git clone` functionality. Clones the repository from *GitHub* into a temporary folder in order to run the analysis.
 * [`GitDiff`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/git/GitDiff.java): Wrapper class for `git diff` functionality. Obtains the changes between commits.
 * [`GitLog`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/git/GitLog.java): Wrapper class for `git log` functionality. Obtains the commit logs and the authors' info.
 * [`GitLsTree`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/git/GitLsTree.java): Wrapper class for `git ls-tree` functionality. Ensures that the tracked files do not contain any paths with illegal characters for Windows users.
 * [`GitRevList`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/git/GitRevList.java): Wrapper class for `git rev-list` functionality. Retrieves the commit objects in reverse chronological order.
 * [`GitRevParse`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/git/GitRevParse.java): Wrapper class for `git rev-parse` functionality. Ensures that the branch of the repo is to be analyzed exists.
 * [`GitShortlog`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/git/GitShortlog.java): Wrapper class for `git shortlog` functionality. Obtains the list of authors who have contributed to the target repo.
 * [`GitUtil`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/git/GitUtil.java): Contains helper functions used by the other Git classes above.


### CommitsReporter
[`CommitsReporter`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/commits/CommitsReporter.java) is responsible for analyzing the **commit** history and generating a [`CommitContributionSummary`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/commits/model/CommitContributionSummary.java) for each repository. `CommitContributionSummary` contains information such as each author's daily and weekly contribution and the variance of their contribution. `CommitsReporter`,
 1. uses [`CommitInfoExtractor`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/commits/CommitInfoExtractor.java) to run the `git log` command, which generates the statistics of each commit made within date range.
 1. generates a [`CommitInfo`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/commits/model/CommitInfo.java) for each commit, which contains the `infoLine` and `statLine`.
 1. uses [`CommitInfoAnalyzer`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/commits/CommitInfoAnalyzer.java) to extract the relevant data from `CommitInfo` into a [`CommitResult`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/commits/model/CommitResult.java), such as the number of line insertions and deletions in the commit and the author of the commit.
 1. uses [`CommitResultAggregator`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/commits/CommitResultAggregator.java) to aggregate all `CommitResult` into a [`CommitContributionSummary`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/commits/model/CommitContributionSummary.java).


### AuthorshipReporter
[`AuthorshipReporter`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/authorship/AuthorshipReporter.java) is responsible for analyzing the white listed **files**, traces the original author for each line of text/code, and generating an [`AuthorshipSummary`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/authorship/model/AuthorshipSummary.java) for each repository. `AuthorshipSummary` contains the analysis results of the white listed files and the amount of line contributions each author made. `AuthorshipReporter`,
 1. uses [`FileInfoExtractor`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/authorship/FileInfoExtractor.java) to traverse the repository to find all relevant files.
 1. generates a [`FileInfo`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/authorship/model/FileInfo.java) for each relevant file, which contains the path to the file and a list of [`LineInfo`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/authorship/model/LineInfo.java) representing each line of the file.
 1. uses [`FileInfoAnalyzer`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/authorship/FileInfoAnalyzer.java) to analyze each file, using `git blame` or annotations, and finds the `Author` for each `LineInfo`.
 1. generates a [`FileResult`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/authorship/model/FileResult.java) for each file, which consolidates the authorship results into a *Map* of each author's line contribution to the file.
 1. uses [`FileResultAggregator`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/authorship/FileResultAggregator.java) to aggregate all `FileResult` into an `AuthorshipSummary`.


### ReportGenerator(Main)
[`ReportGenerator`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/report/ReportGenerator.java),
 1. uses `GitClone` API to clone the repository from *GitHub*.
 1. copies the template files into the designated output directory.
 1. uses `CommitReporter` and `AuthorshipReporter` to produce the commit and authorship summary respectively.
 1. generates the `JSON` files needed to generate the `HTML` report.


### System
[`System`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/system) contains the classes that interact with the Operating System and external processes.
 * [`CommandRunner`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/system/CommandRunner.java) creates processes that executes commands on the terminal. It consists of many *git* commands.
 * [`LogsManager`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/system/LogsManager.java) uses the `java.util.logging` package for logging. The `LogsManager` class is used to manage the logging levels and logging destinations. Log messages are output through: `Console` and to a `.log` file.
 * [`ReportServer`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/system/ReportServer.java) starts a server to display the report on the browser. It depends on the `net.freeutils.httpserver` package.


### Model
[`Model`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/model) holds the data structures that are commonly used by the different aspects of *RepoSense*.
 * [`Author`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/model/Author.java) stores the `GitHub ID` of an author. Any contributions or commits made by the author, using his/her `GitHub ID` or aliases, will be attributed to the same `Author` object. It is used by `AuthorshipReporter` and `CommitsReporter` to attribute the commit and file contributions to the respective authors.
 * [`CliArguments`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/model/CliArguments.java) stores the parsed command line arguments supplied by the user. It contains the configuration settings such as the CSV config file to read from, the directory to output the report to, and date range of commits to analyze. These configuration settings are passed into `RepoConfiguration`.
 * [`FileTypeManager`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/model/FileTypeManager.java) stores the file format to be analyzed and the custom groups specified by the user for any repository.
 * [`RepoConfiguration`](https://github.com/reposense/RepoSense/blob/master/src/main/java/reposense/model/RepoConfiguration.java) stores the configuration information from the CSV config file for a single repository, which are the repository's orgarization, name, branch, list of authors to analyse, date range to analyze commits and files from `CliArguments`.
 These configuration information are used by:
    - `GitClone` to determine the location to clone the repository from and which branch to check out to.
    - `AuthorshipReporter` and `CommitsReporter` to determine the range of commits and files to analyze.
    - `ReportGenerator` to determine the directory to output the report.


## HTML Report
The source files for the report is located in [`frontend/src`](https://github.com/reposense/RepoSense/blob/master/frontend/src) and is built by [spuild](https://github.com/ongspxm/spuild2) before being packaged into the JAR file to be extracted as part of the report.

The main HTML file is generated from [`frontend/src/index.pug`](https://github.com/reposense/RepoSense/blob/master/frontend/src/index.pug).

[Vue](https://vuejs.org/v2/api/) (pronounced /vjuː/, like view) is a progressive framework for building user interfaces. It is heavily utilized in the report to dynamically update the information in the various views. (Style guide available [here](https://vuejs.org/v2/style-guide/), Developer tool available [here](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd)). Vue lifecycle hooks are the defined methods which gets executed in a certain stage of the Vue object lifespan. The following is the Vue lifecycle diagram taken from [here](https://vuejs.org/v2/guide/instance.html#Lifecycle-Diagram) indicating the hook sequence:
![vue lifecycle diagram](images/vue-lifecycle-diagram.png)

The following is a snapshot of the report:
![report screenshot](images/report-summary.png)

### Report Architecture
![report architecture](images/report-architecture.png)

The main Vue object (`window.app`) is responsible for the loading of the report (through `summary.json`). Its `repos` attribute is tied to the global `window.REPOS`, and is passed into the various other modules when the information is needed.

`window.app` is broken down into two main parts
- the summary view
- and the tabbed interface

The summary view acts as the main report which shows the various calculations. </br>
The tabbed interface is responsible for loading various modules such as authorship and zoom to display additional information.

### Javascript Files
- [**main.js**](#main-main-js) - main controller that pushes content into different modules
- [**api.js**](#data-loader-api-js) - loading and parsing of the report content
- [**v_summary.js**](#summary-view-v-summary-js) - module that supports the summary view
- [**v_authorship.js**](#authorship-view-v-authorship-js) - module that supports the authorship tab view
- [**v_zoom.js**](#zoom-view-v-zoom-js) - module that supports the zoom tab view
- [**v_ramp.js**](#ramp-view-v-ramp-js) - module that supports the ramp chart view
- [**v_segment.js**](#segment-view-v-segment-js) - module that supports the code segment view

### JSON Report Files
- **summary.json** - a list of all the repositories and their respective details
- **projName/commits.json** - contains information of the users' commits information (e.g. line deletion, insertion, etc), grouped by date
- **projName/authorship.json** - contains information from git blame, detailing the author of each line for all the processed files

### Main ([main.js](https://github.com/reposense/RepoSense/blob/master/frontend/src/static/js/main.js))
This contains the logic for main VueJS object, `window.app`, which is responsible for passing the necessary data into the relevant modules to be loaded.

`v_summary`, `v_authorship`, `v_zoom`, `v_segment` and `v_ramp` are components which will be embedded into report and will render the corresponding content based on the data passed into it from the main `window.app`.

#### Loading of report information
The main Vue object depends on the `summary.json` data to determine the right `commits.json` files to load into memory. This is handled by `api.js` which loads the relevant file information from the network files if it is available, otherwise a report archive, `archive.zip`, have to be used.

Once the relevant `commit.json` files are loaded, all the repo information will be passed into `v_summary` to be loaded in the summary view as the relevant ramp charts.

#### Activating additional view modules
Most activity or actions should happen within the module itself, but in the case where there is a need to spawn or alter the view of another module, an event is emitted from the first module to the main Vue object (`window.app`), which then handles the data received and passes it along to the relevant modules.

#### Hash link
Other than the global main Vue object, another global variable we have is the `window.hashParams`. This object is reponsible for generating the relevant permalink for a specific view of the summary module for the report.

### Data loader ([api.js](https://github.com/reposense/RepoSense/blob/master/frontend/src/static/js/api.js))
This is the module that is in charge of loading and parsing the data files generated as part of the report.

#### Loading from ZIP file
Due to security design, most modern browsers (e.g. Chrome) do not allow web pages to obtain local files using the directory alone. As such, a ZIP archive of the report information will be produced alongside the report generation.

This archive will be used in place of the network files to load information into the report, in the case when the network files are unavailable.

The API module will be handling all request for all the JSON data files. If the network file is not available, the files will be obtained from the zip archive provided.

#### Retrieving and parsing information
After the JSON files are loaded from their respective sources, the data will be parsed as objects and included inside the global storage object, `window.REPOS`,  in the right format.

For the basic skeleton of `window.REPOS`, refer to the generated `summary.json` file in the report for more details.

### Summary View ([v_summary.js](https://github.com/reposense/RepoSense/blob/master/frontend/src/static/js/v_summary.js))
The `v_summary` module is in charge of loading the ramp charts from the corresponding `commits.json`.

![summary architecture](images/report-architecture-summary.png)

#### Initializing the data for the ramp charts
The summary module is activated after the information is loaded from the main Vue.JS object. At creation, the `repo` attribute is populated with the `window.REPOS` object, which contains information loaded from `summary.json`.

#### Filtering users and repositories
The commits information is retrieved from the corresponding project folders for each repository. These information will be filtered and sorted before passed into the template to be displayed as ramp charts.

### Authorship View ([v_authorship.js](https://github.com/reposense/RepoSense/blob/master/frontend/src/static/js/v_authorship.js))
The authorship module retrieves the relevant information from the corresponding `authorship.json` file if it is not yet loaded. If it has been loaded, the data will be written into `window.REPOS` and be read from there instead.

![authorship architecture](images/report-architecture-authorship.png)

#### Showing relevant information by authors
The files will be filtered, picking only files the selected author has written in. The lines are then split into chunks of "touched" and "untouched" code segments to be displayed in the tab view which will be popped up on the right side of the screen.

### Zoom View ([v_zoom.js](https://github.com/reposense/RepoSense/blob/master/frontend/src/static/js/v_zoom.js))
The `v_zoom` module is in charge of filtering and displaying the commits from selected sub-range of a ramp chart.

### Ramp View ([v_ramp.js](https://github.com/reposense/RepoSense/blob/master/frontend/src/static/js/v_ramp.js))
The `v_ramp` module is responsible for receiving the relevant information from `v_summary` and generating ramp charts that contain ramp slices.

#### Padding for dates
For ramps between the date ranges, the slices will be selected and it will be pre and post padded with empty slices to align the ramp slice between the `sinceDate` and `untilDate`. The ramps will then be rendered with the slices in the right position.

### Segment View ([v_segment.js](https://github.com/reposense/RepoSense/blob/master/frontend/src/static/js/v_segment.js))
The `v-segment` module is used as a component in `v_authorship`. It separates the code in terms of "touched" and "untouched" segments and only loads each "untouched" segment when it is toggled.
