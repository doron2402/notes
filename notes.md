# OS X 10.11 (El Capitan) / Node.js and io.js Developer Environment

Custom recipe to get OS X 10.11 El Capitan running from scratch with useful applications and Node.js Developer environment. I use this gist to keep track of the important software and steps required to have a functioning system after fresh install.

## Content

* [Appearance](#appearance)
* [WebStorm](#webstorm)
* [Xcode & Command Line Tools](#xcode--command-line-tools)
* [Git & GitHub](#git)
* [Homebrew](#homebrew)
* [Node.js and io.js Environment](#nodejs-and-iojs-environment)
* [Electron](#electron)
* [Database & Stores](#database)
* [Tools](#tools)
* [Applications](#applications)
* [Other Installation Tracks](#other-installation-tracks)

## Appearance

The best fonts to code:
* Menlo (OS X built-in)
* [Mensch coding font](http://robey.lag.net/2010/06/21/mensch-font.html)

## WebStorm

* [Download WebStorm](https://www.jetbrains.com/webstorm/) by using second link "Get WebStorm 10 with JDK 1.8" and install it.
* [Twilight 2 Theme](https://github.com/DenisIzmaylov/webstorm-twilight2-theme)
* [GitHub Markdown Plugin](https://plugins.jetbrains.com/plugin/7701)

## XCode & Command Line Tools

* [Download](https://developer.apple.com/xcode/downloads/) XCode 7.0 Beta or latest. Install it.
* Then open `Xcode > Preferences > Downloads > Command Line Tools` or execute in Terminal:
```sh
xcode-select --install
```
* Select `Xcode > Preferences > Locations > Command Line Tools` (to avoid `ld: library not found for -lgcc_s.10.5` error in  working with `npm`).

## Git

### Setup
```sh
git config --global user.name "Denis Izmaylov"
git config --global user.email "example@izmy.lv"
```

### Configure GitHub

There is 2 ways to configure keys. The first is:
* Create new key:
```sh
ssh-keygen -t rsa -C "example@izmy.lv"
```
* Copy public key:
```sh
cat ~/.ssh/id_rsa.pub
```
* Add it to `github.com`

The second way was just to backup your `~/.ssh` before re-install and restore it now. Be aware - private keys should have `0400` access.

#### Test connection
```sh
ssh -T git@github.com
```

## Homebrew

```sh
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

## Node.js and io.js Environment

If you are not sure which platform to use Node.js or io.js - [see compatibility table](http://kangax.github.io/compat-table/es6/). The good reason to choice *io.js* is [React Native](https://facebook.github.io/react-native/docs/getting-started.html#content).

* To install [Node.js](https://nodejs.org/):
```sh
brew install node
```
* To install [io.js](https://iojs.org/en/index.html):
```sh
brew install iojs
## to prevent node-gyp errors (https://github.com/strongloop/fsevents/issues/49)
sudo npm install -g node-gyp-install
node-gyp-install
```
* Install development tools:
```sh
npm install gulp eslint webpack node-inspector -g
```

* To get installed Phantom.js and use it:
```sh
npm install phantom phantomjs -g
```

## Electron

Build cross platform desktop apps with web technologies. Formerly known as Atom Shell.
```sh
npm install electron-prebuilt -g
```

## Database

### Redis

* Install
```sh
brew install redis
```
* Launch:
```sh
launchctl load /usr/local/opt/redis/homebrew.mxcl.redis.plist
```
* To have launchd start redis at login:
```sh
mkdir -p ~/Library/LaunchAgents
ln -sfv /usr/local/opt/redis/*.plist ~/Library/LaunchAgents
```
* Test:
```sh
redis-cli
```

### MongoDB

* Try to install with Homebrew:
```sh
brew install mongodb
```
* If you could not install with Homebrew try to do it manually:
```sh
curl -O https://fastdl.mongodb.org/osx/mongodb-osx-x86_64-3.0.4.tgz
tar -zxvf mongodb-osx-x86_64-3.0.4.tgz
mv mongodb-osx-x86_64-3.0.4/ /usr/local/opt/mongodb
export PATH=/usr/local/opt/mongodb/bin:$PATH
echo export PATH=/usr/local/opt/mongodb/bin:\$PATH>~/.bash_profile
chmod +x ~/.bash_profile
mkdir -p ~/data/mongodb
```
* Then execute in Terminal:
```sh
sudo mongod --dbpath=$HOME/data/mongodb 
```

### PostgreSQL

* Install:
```sh
brew install postgres
```

* Launch:
```sh
launchctl load /usr/local/opt/postgresql/homebrew.mxcl.postgresql.plist
```

* To have launchd start postgres at login:
```sh
mkdir -p ~/Library/LaunchAgents
ln -sfv /usr/local/opt/postgresql/*.plist ~/Library/LaunchAgents
```

## Tools
One of easiest ways to install apps is using Cask.
So let's install it before:
```sh
brew install caskroom/cask/brew-cask
```
Now we can install tools by single command. Let's use it.

### webp-quicklook
Open-source QuickLook plugin to generate thumbnails and previews for [WebP images](http://code.google.com/speed/webp/). Requires Mac OS X 10.7 or later.
```sh
brew cask install webpquicklook
```

### Midnight Commander
Just install:
```sh
brew install mc
```
And start:
```
mc
```

## Applications
 * Editor: [Sublime 3](http://www.sublimetext.com/3)
 * Browser: [Chrome](https://www.google.ru/chrome/browser/desktop/)
 * Passwords Store: [LastPass](https://lastpass.com/) or [1Password](https://agilebits.com/onepassword/mac)
 * Cloud Drive:
  - [Dropbox](https://www.dropbox.com/downloading?src=index)
  - [Yandex.Disk](https://disk.yandex.ru/download/#desktop)
 * Communication:
   - [Skype](http://www.skype.com/ru/download-skype/skype-for-mac/downloading/)
      - Use `~/Library/Application Support/Skype` directory to create/restore your chat history backup
      - Disable sound notifications (`Skype > Preferences > Notifications`)
   - [Telegram](https://desktop.telegram.org/)
   - [Gitter](https://update.gitter.im/osx/latest)
   - [Slack](https://itunes.apple.com/app/slack/id803453959?ls=1&mt=12)
 * [Twitter](https://itunes.apple.com/ru/app/twitter/id409789998?mt=12) to stay turned with the best developers.
 * Productive:
   - [Activity Timer](https://itunes.apple.com/ru/app/activity-timer-productivity/id808647808?mt=12) provides a plain and smoothly integrated timer for your OS X status bar. Choose between time presets (3, 5, 25 or 30 minutes or custom defined intevals) which proved to be perfect intervals for all kind of activities.
  - [RescueTime](https://www.rescuetime.com/) helps you understand your daily habits so you can focus and be more productive. Runs securely in the background. Tracks time spent on applications and websites, giving you an accurate picture of your day.
  - [Wakatime](https://wakatime.com/) Quantify your coding. Metrics and insights about your programming using open source text editor plugins.

