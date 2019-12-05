# install Java

ref:
<https://stackoverflow.com/questions/24342886/how-to-install-java-8-on-mac>

Note: Oracle Java 8/9/10 is no longer available for public download (license change).
First install and update brew from Terminal:

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap homebrew/cask-versions
brew update
```

NEW as of June 2019
To install the JDKs from AdoptOpenJDK:

> brew tap adoptopenjdk/openjdk

choose a version

```bash
brew cask install adoptopenjdk8
brew cask install adoptopenjdk9
brew cask install adoptopenjdk10
brew cask install adoptopenjdk11
```

Existing users of Homebrew may encounter Error: Cask adoptopenjdk8 exists in multiple taps due to prior workarounds with different instructions. This can be solved by fully specifying the location with `brew cask install adoptopenjdk/openjdk/adoptopenjdk8`.
