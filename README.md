<center>

![waka-readme](https://socialify.git.ci/athul/waka-readme/png?description=1&forks=1&issues=0&pulls=0)

</center>

# Dev Metrics in Readme [![Build Status](https://travis-ci.com/athul/waka-readme.svg?branch=master)](https://travis-ci.com/athul/waka-readme)

![Project Preview](https://user-images.githubusercontent.com/8397274/87243943-e6b45c00-c457-11ea-94c9-2aa0bf241be8.png)

[WakaTime](https://wakatime.com) Weekly Metrics on your Profile Readme:

**Forum**: [GitHub Discussions](https://github.com/athul/waka-readme/discussions)

## Prep Work

1. You need to update the markdown file(.md) with 2 comments. You can refer [here](#update-your-readme) for updating it.
2. You'll need a WakaTime API Key. You can get that from your WakaTime Account Settings
   - You can refer [here](#new-to-wakatime), if you're new to WakaTime
3. **Optional** You'll need a GitHub API Token with `repo` scope from [here](https://github.com/settings/tokens) if you're running the action not in your Profile Repository
   - You can use [this](#other-repository-not-profile) example to work it out
4. You need to save the WakaTime API Key (and the GitHub API Token, if you need it) in the repository secrets. You can find that in the Settings of your Repository.Be sure to save those as the following.
   - WakaTime-api-key as `WAKATIME_API_KEY = <your wakatime API Key>`and
   - The GitHub Access Token as `GH_TOKEN=<your github access token>`
5. You can follow either of the Two Examples according to your needs to get started with.

> I strongly suggest you to run the Action in your Profile Repo since you won't be needing a GitHub Access Token

This Action will run everyday at 00.00 UTC

## Update your Readme

Add a comment to your `README.md` like this:

```md
<!--START_SECTION:waka-->

```txt
Python             10 hrs 38 mins  ███████████▒░░░░░░░░░░░░░   45.14 %
HTML               4 hrs 58 mins   █████▒░░░░░░░░░░░░░░░░░░░   21.13 %
YAML               3 hrs 23 mins   ███▓░░░░░░░░░░░░░░░░░░░░░   14.39 %
Markdown           1 hr 45 mins    ██░░░░░░░░░░░░░░░░░░░░░░░   07.45 %
Text               40 mins         ▓░░░░░░░░░░░░░░░░░░░░░░░░   02.87 %
```

<!--END_SECTION:waka-->
```

6. Go to Workflows menu (mentioned in step 1), click `Waka Readme`, click `Run workflow`.
7. Go to your profile page. you will be able to see it.

### Other Repository (not Profile)

_If you're executing the workflow on another repo other than `<username>/<username>`_

You'll need to get a [GitHub Access Token](https://docs.github.com/en/actions/configuring-and-managing-workflows/authenticating-with-the-github_token) with a `repo` scope and save it in the Repo Secrets `GH_TOKEN = <Your GitHub Access Token>`

Here is Sample Workflow File for running it:

```yml
name: Waka Readme

on:
  schedule:
    # Runs at 12am UTC
    - cron: "0 0 * * *"

jobs:
  update-readme:
    name: Update Readme with Metrics
    runs-on: ubuntu-latest
    steps:
      - uses: athul/waka-readme@master
        with:
          WAKATIME_API_KEY: ${{ secrets.WAKATIME_API_KEY }}
          GH_TOKEN: ${{ secrets.GH_TOKEN }}
          REPOSITORY: <username/username> # optional, By default, it will automatically use the repository who's executing the workflow.
```

## Tests

### Running Tests

To run tests simply execute the following in the directory containing main.py:

```python
python -m unittest discover
```

### Contributing Tests

These tests uses the python Unit testing framework, [unittest](https://docs.python.org/3/library/unittest.html)

Since this project is contained all within one file, 'main.py'. You can simply add a function to the TestMain class in tests/test_main.py, similar to the test_graph function.

## Extras

1. If you want to add the week in the Header of your stats, you can add `SHOW_TITLE: true` in your workflow file like this

```yml
- uses: athul/waka-readme@master
        with:
          WAKATIME_API_KEY: ${{ secrets.WAKATIME_API_KEY }}
          GH_TOKEN: ${{ secrets.GH_TOKEN }}
          SHOW_TITLE: true
```

`SHOW_TITLE` flag can be set to true if you want to display the week number and days in the readme, by default it will be false. Here is an example output with `SHOW_TITLE` set to true.

```text
Week: 10 July, 2020 - 17 July, 2020
Python      8 hrs 52 mins       ███████████████████░░░░░░   75.87 %
Go          1 hr 15 mins        ██░░░░░░░░░░░░░░░░░░░░░░░   10.79 %
Markdown    52 mins             █░░░░░░░░░░░░░░░░░░░░░░░░   07.43 %
Docker      16 mins             ░░░░░░░░░░░░░░░░░░░░░░░░░   02.32 %
YAML        7 mins              ░░░░░░░░░░░░░░░░░░░░░░░░░   01.07 %
```

2. You can specify a commit message to override the default _"Updated the Graph with new Metrics"_. Here is how you do it

```yml
- uses: athul/waka-readme@master
        with:
          WAKATIME_API_KEY: ${{ secrets.WAKATIME_API_KEY }}
          GH_TOKEN: ${{ secrets.GH_TOKEN }}
          COMMIT_MESSAGE: Updated the Readme
```

If no commit message is specified in the `yml` file, it defaults to _"Updated the Graph with new Metrics"_

3. You can change the block characters to match with the style of your readme. By default the one show in the graphs before is used. Here is how you do it

```yml
- uses: athul/waka-readme@master
        with:
          WAKATIME_API_KEY: ${{ secrets.WAKATIME_API_KEY }}
          BLOCKS: ⣀⣄⣤⣦⣶⣷⣿
```

This will change the graphs to something like this:

```text
Python      8 hrs 52 mins       ⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣀⣀⣀⣀⣀⣀   75.87 %
Go          1 hr 15 mins        ⣿⣿⣦⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀   10.79 %
Markdown    52 mins             ⣿⣿⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀   07.43 %
Docker      16 mins             ⣤⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀   02.32 %
YAML        7 mins              ⣄⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀   01.07 %
```

4. As an alternative to official WakaTime, _waka-readme_ also integrates with WakaTime-compatible services like [Wakapi](https://wakapi.dev) and [Hakatime](https://github.com/mujx/hakatime). To use one of these, **adapt the API URL accordingly and use the respective service's API key** instead:

```yml
- uses: athul/waka-readme@master
        with:
          WAKATIME_API_KEY: ${{ secrets.WAKATIME_API_KEY }}
          API_BASE_URL: https://wakapi.dev/api
```

## Why only the language stats and not other data from the API?

I am a fan of minimal designs and the profile readme is a great way to show off your skills and interests. The WakaTime API, gets us a **lot of data** about a person's **coding activity including the editors and Operating Systems you used and the projects you worked on**. Some of these projects maybe secretive and should not be shown out to the public. Using up more data via the Wakatime API will clutter the profile readme and hinder your chances on displaying what you provide **value to the community** like the pinned Repositories. I believe that **Coding Stats is nerdiest of all** since you can tell the community that you are _**exercising these languages or learning a new language**_, this will also show that you spend some amount of time to learn and exercise your development skills. That's what matters in the end :heart:
