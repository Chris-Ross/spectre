<p align=center>
  <br>
  <a href="https://github.com/Chris-Ross/spectre" target="_blank"><img src="https://i.imgur.com/gJzXIuX.png"/></a>
  <br>
  <span> Detect username accounts across a plethora of <a href="https://github.com/chris-ross/spectre/blob/master/sites.md">social networks</a></span>
  <br>
</p>

<p align=center>
  <br>
  <a href="https://github.com/sherlock-project/sherlock">This is a fork of the Sherlock Project</a>
</p>

<p align="center">
  <a href="#installation">Installation</a>
  &nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#usage">Usage</a>
  &nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#docker-notes">Docker Notes</a>
  &nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#contributing">Contributing</a>
</p>

<p align="center">
<img width="70%" height="70%" src="https://i.imgur.com/21TYWm4.png"/>
</a>
</p>


## Installation

```console
# clone the repo
$ git clone https://github.com/Chris-Ross/spectre.git
# change the working directory to spectre
$ cd spectre

# install the requirements
$ python3 -m pip install -r requirements.txt
```

## Usage

```console
$ python3 spectre --help
usage: spectre [-h] [--version] [--verbose] [--folderoutput FOLDEROUTPUT]
                [--output OUTPUT] [--tor] [--unique-tor] [--csv]
                [--site SITE_NAME] [--proxy PROXY_URL] [--json JSON_FILE]
                [--timeout TIMEOUT] [--print-all] [--print-found] [--no-color]
                [--browse] [--local] [--nsfw]
                USERNAMES [USERNAMES ...]

spectre: Find Usernames Across Social Networks (Version 0.14.3)

positional arguments:
  USERNAMES             One or more usernames to check with social networks.
                        Check similar usernames using {?} (replace to '_', '-', '.').

optional arguments:
  -h, --help            show this help message and exit
  --version             Display version information and dependencies.
  --verbose, -v, -d, --debug
                        Display extra debugging information and metrics.
  --folderoutput FOLDEROUTPUT, -fo FOLDEROUTPUT
                        If using multiple usernames, the output of the results will be
                        saved to this folder.
  --output OUTPUT, -o OUTPUT
                        If using single username, the output of the result will be saved
                        to this file.
  --tor, -t             Make requests over Tor; increases runtime; requires Tor to be
                        installed and in system path.
  --unique-tor, -u      Make requests over Tor with new Tor circuit after each request;
                        increases runtime; requires Tor to be installed and in system
                        path.
  --csv                 Create Comma-Separated Values (CSV) File.
  --xlsx                Create the standard file for the modern Microsoft Excel
                        spreadsheet (xslx).
  --site SITE_NAME      Limit analysis to just the listed sites. Add multiple options to
                        specify more than one site.
  --proxy PROXY_URL, -p PROXY_URL
                        Make requests over a proxy. e.g. socks5://127.0.0.1:1080
  --json JSON_FILE, -j JSON_FILE
                        Load data from a JSON file or an online, valid, JSON file.
  --timeout TIMEOUT     Time (in seconds) to wait for response to requests (Default: 60)
  --print-all           Output sites where the username was not found.
  --print-found         Output sites where the username was found.
  --no-color            Don't color terminal output
  --browse, -b          Browse to all results on default browser.
  --local, -l           Force the use of the local data.json file.
  --nsfw                Include checking of NSFW sites from default list.
```

To search for only one user:
```
python3 spectre user123
```

To search for more than one user:
```
python3 spectre user1 user2 user3
```

Accounts found will be stored in an individual text file with the corresponding username (e.g ```user123.txt```).

## Anaconda (Windows) Notes

If you are using Anaconda in Windows, using `python3` might not work. Use `python` instead.

## Docker Notes

If docker is installed you can build an image and run this as a container.

```
docker build -t myspectre-image .
```

Once the image is built, spectre can be invoked by running the following:

```
docker run --rm -t myspectre-image user123
```

Use the following command to access the saved results:

```
docker run --rm -t -v "$PWD/results:/opt/spectre/results" myspectre-image -o /opt/spectre/results/text.txt user123
```

Docker is instructed to create (or use) the folder `results` in the current working directory and to mount it at `/opt/spectre/results` on the docker container by using the ```-v "$PWD/results:/opt/spectre/results"``` options. `spectre` is instructed to export the result using the `-o /opt/spectre/results/text.txt` option.


### Using `docker-compose`

You can use the `docker-compose.yml` file from the repository and use this command:

```
docker-compose run spectre -o /opt/spectre/results/text.txt user123
```

## Tests

The following is an example of the command line to run all the tests for
spectre.  This invocation hides the progress text that spectre normally
outputs, and instead shows the verbose output of the tests.

```console
$ cd spectre/spectre
$ python3 -m unittest tests.all --verbose
```

Note that we do currently have 100% test coverage.  Unfortunately, some of
the sites that spectre checks are not always reliable, so it is common
to get response problems.  Any problems in connection will show up as
warnings in the tests instead of true errors.

If some sites are failing due to connection problems (site is down, in maintenance, etc)
you can exclude them from tests by creating a `tests/.excluded_sites` file with a
list of sites to ignore (one site name per line).

