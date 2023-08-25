# action-translate-readme

[English version](README.md) | 
[Chinese version README.md](README.zh-TW.md)

# What's changed for action-translate-readme?

With the emergence of ChatGPT, the author thought that the translation task of this project could be handed over to GPT for implementation. Through the open source project [`gpt4free`](https://github.com/xtekky/gpt4free), we were able to achieve a free GPT API and hope to enhance the translation ability of this project!

* Translation method for version 1: implemented through a third-party package for Linux (`translation.sh`)
  * Translation effect: poor, similar to Google translation effect
  * Translation speed: slow
  * Stability: high, ensuring correct translation every time

* Translation method for version 2: translation task implemented through GPT (`translation.py`)
  * Translation effect: good
  * Translation speed: fast or slow
  * Stability: low
  
  Because `gpt4free` uses reverse engineering to realize the free invocation of API, abnormal situations may occur during the invocation process. The author added a `retry` technique (if an exception occurs, it will be executed again) to the API function invocation to avoid translation failure. As a result, translation speed will increase with the increase of retry times.

  Please note that `gpt4free` has different Providers, which provide the source for API invocation. If the automatic translation tool of this project cannot be used normally, the problem usually comes from the fact that the Provider currently in use has become **Inactive**. Therefore, in your `translate-readme.yml` file, you can set this [parameter](.github\workflows\translate-readme.yml) yourself (default is `g4f.Provider.DeepAi`).

# Introduction

* We all know that writing documentations takes a lot of time, but now there is a solution that can save you half of the time. This is our `action-translate-readme`.

* With this tool, you can automatically translate the `README.md` file, and not only can translate, but also translate various elements such as **inline code, emoticons, code blocks, HTML tags, and links**.

* Its working principle is automated through `Github Actions`. Just push the updated README file, and the translated README (zh or en) file will be automatically updated.

* Continuous Integration (CI)

* **Automatically translate the language of README through Github Action**

* Update `README.md` and push it. This action will automatically update `README.zh-TW.md`.
  (Update `README.zh-TW.md` to automatically update `README.md`)

* Save half the time of writing documentation.

# Features

* Not translated:
    * Inline code (`inline_code`)
    * Emoticons
    * Code blocks
    * HTML tags
    * Links

# How to use ?

1. Click the :star: icon to add this project to your Github repository.

2. Set your `Github Token`:

    * Create a new **`Github Secret Token`**
        * Settings
        * Developer settings
        * Personal access tokens - `Tokens (classic)`
        * Generate new token
        * Select scope: `repo` and `workflow`
        * **Keep** your secret token (do not discard it, you will need to paste it later)
        <img src="https://github.com/Lin-jun-xiang/action-translate-readme/assets/63782903/b7487b49-817c-4925-b94a-bdb7b025a0c2" width=" 60%" />

    * Create a new **`repository secret`**
        * In your repository - `settings`
        * `Securits and variables`
        * `Actions`
        * `New repository secret`
        * Fill in the tag and name it as `token` (e.g. `Action_Bot`)
        <img src="https://github.com/Lin-jun-xiang/action-translate-readme/assets/63782903/27dc7bcd-633f-431e-98e8-387b97ecd47c" width=" 60%" />

4. Create the language of README you want: `README.md`, `READM.zh-TW.md`, etc.

5. Create your action example in `your_action.yml` directory `.github/workflows/`:

    ```
    # .github/workflows/translate.yml
    name: Translate Readme

    on:
        push:
            branches: ['**']

    jobs:
        translate:
            runs-on: ubuntu-latest
            steps:
                - name: Checkout
                  uses: actions/checkout@v3
                  with:
                    fetch-depth: 3

                - name: Auto Translate
                  uses: Lin-jun-xiang/action-translate-readme@v1 # Based on the tag
                  with:
                    token: ${{ secrets.Action_Bot }} # Based on step2 name
    ```

6. Now you can update `README.md`, and an automatically generated translated version will be available!

![](./img/auto-translation.gif)

---

# Results of Test Document

* View [test document](https://github.com/Lin-jun-xiang/vscode-extensions-best/tree/main)
* Update the test document with our tool

<a href="#top">Back to top</a>