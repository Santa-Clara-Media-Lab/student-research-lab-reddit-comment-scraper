# Reddit Comment Scraper
 
<p align="center">
  <img src="https://github.com/Santa-Clara-Media-Lab/student-research-lab-reddit-comment-scraper/blob/main/assets/educord.png?raw=true">
</p>

- Using mixed-method approach in Dr. David Jeong's lab to study social media interactions as well as ethical implications of emerging media technology.
- Developed Reddit comment scraper for sentiment analysis on behalf of the SCU Media Research Lab - Data Science Team.

# Installing and setting up the Node.js environment

1. Installing **Node** and **NPM** on **Windows** and **macOS** is straightforward because you can just use the provided installer:

- Download the required installer:
  - Go to https://nodejs.org/en/
  - Select the button to download the **LTS** build that is `"Recommended for most users"`.

2. Install **Node** by double-clicking on the downloaded file and following the installation prompts.

# Testing your Node.js and NPM installation

- The easiest way to test that **Node** is installed is to run the "version" command in your terminal/command prompt and check that a version string is returned:

```
> node -v
v16.15.1
```

- The **Node.js** package manager **NPM** should also have been installed, and can be tested in the same way:

```
> npm -v 
v8.13.1
```

# Using NPM

- Like **Python** is to **pip**, **NPM** is used to fetch any packages (**JavaScript libraries**) that an application needs for **Node** development, testing, and/or production, and may also be used to run tests and tools used in the development process.
- You can manually use **NPM** to separately fetch each needed package. Typically we instead manage dependencies using a plain-text definition file named `package.json`. The `package.json` file should contain everything **NPM** needs to fetch and run your application.

# Adding Dependencies

- The following steps show how you can use **NPM** to download a package, save it into the project dependencies, and then require it in a **Node** application.

1. First create a directory named `reddit-scraper-bot` for your new application and navigate into it:

```
mkdir reddit-scraper-bot
cd reddit-scraper-bot
```

2. Use the `npm init` command to create a `package.json` file for your application. This command prompts you for a number of things, including the name and version of your application and the name of the initial entry point file (by default this is `index.js`. For now, just accept the defaults:

```
npm init
```

3. Now do `npm install [insert package name]` for each of the following dependencies we will need for the sake of this project:

   - `entities`: Decodes HTML entities (e.g. &amp; becomes &, &quot; becomes ", &lt becomes <, &gt; becomes >).
   - `json2csv`: Convert **JSON** to **CSV**.
   - `path`: **Node.js** "path" module published to the **NPM** registry.
   - `snoowrap`: Fully-featured **JavaScript** wrapper that provides a simple interface to access every **Reddit API** endpoint.
   - `vader-sentiment`: **Javascript** port of the VADER sentiment analysis tool. Sentiment from text can be determined in a **Node.js** app.
   - `fs`: Provides a lot of very useful functionality to access and interact with the file system.
   - `dayjs`: **JavaScript** date library for parsing, validating, manipulating, and formatting date.
   - `prompt-sync`: A sync prompt for **Node.js**. very simple. no C++ bindings and no bash scripts.
   - `pm2`: Production process manager for **Node.js** applications that allows you to keep applications alive for however long you want without downtime and to facilitate common system admin tasks.

# Obtain Reddit Credentials

1. Go to this [website](https://www.reddit.com/prefs/apps), make a new **Reddit** account (or use pre-existing one), and uou will see a box at the bottom that reads: "are you a developer, create an app."

<p align="center">
  <img src="https://user-images.githubusercontent.com/42426861/127065682-39207003-91d0-44e4-98a6-c37581960731.png">
</p>

2. Click "create app" and obtain the following credentials from the portal to properly calibrate your **Reddit API** instance.

<p align="center">
  <img src="https://user-images.githubusercontent.com/42426861/127066287-6f9d89c1-1e47-447e-b181-5b7cc1d05eb4.png">
</p>

3. To properly secure your new Reddit credentials, make a file called `.env` and copy the format structure below while filing in the variables for the **Reddit API** instance:

```
CLIENT_ID=[insert-client-id]
CLIENT_SECRET=[insert-reddit-client-secret]
USER_AGENT='Student Research Lab Robot by /u/anon-username' 'https://github.com/Santa-Clara-Media-Lab/student-research-lab-robot'
USER_NAME=[your-reddit-username]
PASS_WORD=[your-reddit-password]
```

# Deploy Scripts

1. [Holistic Method](https://github.com/Santa-Clara-Media-Lab/student-research-lab-reddit-comment-scraper/blob/main/modules/holisticRedditMethod.js):
   - Scrapes across various subreddits with set post and comment amount limits to avoid overloading requests to the **Reddit** server.
   - To properly utilize this method, we would do the following:
     - 1. Copy the code linked above and name it `holisticMethodReddit.js` and save it in your current coding folder - `reddit-scraper-bot`
     - 2. Go to the command line and type then hit enter: `pm2 start holisticMethodReddit.js`
     - 3. Wait because this method takes a long amount of time but over a couple hours it will output large amounts of metadata into the `holisticRedditComments.csv` in your coding folder.
     - 4. Check the `redditComments` folder for your outputted `holisticRedditComments.csv` file!

<p align="center"> 
  <img src="https://user-images.githubusercontent.com/42426861/127064469-62a95cdd-c1d9-41ed-9192-89478ff7c72a.png">
</p>

<p align="center"> 
  <img src="https://user-images.githubusercontent.com/42426861/127064502-4af7b6b1-0055-4cd6-b718-9f9be7f9a9df.png">
</p>

2. [Quality Method](https://github.com/Santa-Clara-Media-Lab/student-research-lab-reddit-comment-scraper/blob/main/modules/qualityRedditMethod.js):
   - Recursively scrapes all comments and their children replies from a specific post ID
   - Say we wanted to scrape all the comments from this thread, we would do the following:
     - 1. Copy the code linked above and name it `qualityMethodReddit.js` and save it in your current coding folder - `reddit-scraper-bot`
     - 2. Go to the post comment url => https://www.reddit.com/r/virtualreality/comments/obdzm5 => and get `obdzm5`, which would be the post ID.
     - 3. Go to the command line and type then hit enter: `pm2 start qualityMethodReddit.js`
     - 4. It will ask you to input a post id, so enter in `obdzm5`
     - 5. Check the `redditComments` folder for your outputted `qualityRedditComments.csv` file!

<p align="center">
  <img src="https://user-images.githubusercontent.com/42426861/127062838-ac4e0dfb-b36c-4541-a34a-4ead3325b1cd.png">
</p>

<p align="center">
  <img src="https://user-images.githubusercontent.com/42426861/127065044-3485a336-6fdb-4014-85f1-67e929a10d37.png">
</p>

# Common Issues (But Not Limited To These) To Be Addressed

- Updating outdated **Node.js** and **NPM** versions.
- Fixing the **Node.js** environment path variables for Windows/Mac per this [website&#39;s instructions](https://newbedev.com/fixing-npm-path-in-windows-8-and-10).
- Identifying and installing packages for dependencies not found.
- **Reddit** status codes 429 and/or 503 when using the **Reddit API** via my scripts.
- Having **Reddit API** credentials that don’t match what you have on the developer portal and/or inputting the inaccurate information.
