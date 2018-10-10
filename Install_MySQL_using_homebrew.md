Install MySQL using homebrew 
======

mac OS High Sierra 10.13.6

***


```
 $ brew install mysql
Updating Homebrew...
==> Auto-updated Homebrew!
Updated 3 taps (homebrew/core, homebrew/cask and homebrew/cask-fonts).
==> New Formulae
bundletool          i2pd                objfw               rke
c-blosc             libcerf             opensubdiv          stanford-corenlp
geant4              mallet              opentracing-cpp     tdlib
==> Updated Formulae
pandoc ✔                                 kubernetes-helm
abcde                                    kubernetes-service-catalog-client
aircrack-ng                              landscaper
alexjs                                   languagetool
ammonite-repl                            ldc
ansible                                  libepoxy
apache-geode                             libgda
apache-spark                             libheif
app-engine-java                          libopkele
arangodb                                 libphonenumber
ark                                      librealsense
aws-elasticbeanstalk                     libssh
aws-okta                                 libvirt
babel                                    links
ballerina                                logstash
bazel                                    mame
bcal                                     mariadb
bettercap                                meson
bitcoin                                  metabase
black                                    micronaut
blink1                                   mkdocs
caffe                                    mkvtoolnix
carthage                                 mosquitto
cern-ndiff                               mpv
cgal                                     mscgen
checkbashisms                            mujs
circleci                                 mupdf
clamav                                   mupdf-tools
clipper                                  ne
cloc                                     nginx
cmake                                    nifi-registry
cmocka                                   nim
commandbox                               node-build
conan                                    nodebrew
container-diff                           nomad
convox                                   numpy
cpprestsdk                               openapi-generator
cromwell                                 opencv
darksky-weather                          orc-tools
dita-ot                                  pandoc-citeproc
dnscrypt-proxy                           pass
doctl                                    pegtl
elasticsearch                            phoronix-test-suite
elm-format                               php-code-sniffer
eslint                                   phpunit
evince                                   picat
exercism                                 pipenv
exiftool                                 pixz
faas-cli                                 poppler
fail2ban                                 presto
ffmbc                                    prometheus
flatbuffers                              pulumi
fn                                       puzzles
folly                                    quicktype
fpc                                      rabbitmq
futhark                                  rakudo-star
fzf                                      rom-tools
geckodriver                              roswell
git                                      rtags
git-annex                                rustup-init
git-archive-all                          safe
git-standup                              saxon
glances                                  sbcl
glide                                    sbt
go                                       scala
godep                                    serverless
goenv                                    shpotify
golang-migrate                           skaffold
grakn                                    skafos
grv                                      smlnj
gst-editing-services                     softhsm
gst-libav                                solr
gst-plugins-bad                          sops
gst-plugins-base                         strongswan
gst-plugins-good                         suricata
gst-plugins-ugly                         swiftformat
gst-python                               swiftgen
gst-rtsp-server                          telegraf
gst-validate                             teleport
gstreamer                                terraform-docs
haproxy                                  terragrunt
highlight                                texmath
hledger                                  tinc
hyperfine                                topgrade
i2p                                      typescript
iamy                                     unrar
ipv6calc                                 vert.x
ipython                                  vice
jbake                                    vim
jenkins                                  webpack
jetty                                    wireguard-go
jetty-runner                             wireguard-tools
jfrog-cli-go                             wtf
jhipster                                 x265
jmeter                                   yamllint
joplin                                   ykman
juju                                     youtube-dl
kibana                                   yubico-piv-tool
kotlin                                   zenity
krakend                                  zig
kubernetes-cli                           zstd
==> Deleted Formulae
asciinema2gif   casperjs        qt@5.5          redis@2.8       sonarlint

Error: Cannot install mysql because conflicting formulae are installed.
  mysql-connector-c: because both install MySQL client libraries
  mariadb-connector-c: because both install plugins

Please `brew unlink mysql-connector-c mariadb-connector-c` before continuing.

Unlinking removes a formula's symlinks from /usr/local. You can
link the formula again after the install finishes. You can --force this
install, but the build may fail or cause obscure side-effects in the
resulting software.
```

I chose to `brew unlink` these connectors.

```
$ brew unlink mysql-connector-c mariadb-connector-c
Unlinking /usr/local/Cellar/mysql-connector-c/6.1.11... 57 symlinks removed
Unlinking /usr/local/Cellar/mariadb-connector-c/3.0.3... 3 symlinks removed
```

Then try `mysql` install again.

```
 $ brew install mysql
==> Downloading https://homebrew.bintray.com/bottles/mysql-8.0.12.high_sierra.bo
==> Downloading from https://akamai.bintray.com/96/963bbfbd11282a5dee036f5dafe93
######################################################################## 100.0%
==> Pouring mysql-8.0.12.high_sierra.bottle.tar.gz
==> /usr/local/Cellar/mysql/8.0.12/bin/mysqld --initialize-insecure --user=marti
==> Caveats
We've installed your MySQL database without a root password. To secure it run:
    mysql_secure_installation

MySQL is configured to only allow connections from localhost by default

To connect run:
    mysql -uroot

A "/etc/my.cnf" from another install may interfere with a Homebrew-built
server starting up correctly.

To have launchd start mysql now and restart at login:
  brew services start mysql
Or, if you don't want/need a background service you can just run:
  mysql.server start
==> Summary
🍺  /usr/local/Cellar/mysql/8.0.12: 255 files, 233.0MB
```

Now reinstall the `mysql-connector-c`

```
$ brew install mysql-connector-c
Warning: mysql-connector-c 6.1.11 is already installed, it's just not linked
You can use `brew link mysql-connector-c` to link this version.
```

Attempt to link `link mysql-connector-c`

```
$ brew link mysql-connector-c
Linking /usr/local/Cellar/mysql-connector-c/6.1.11... 
Error: Could not symlink bin/my_print_defaults
Target /usr/local/bin/my_print_defaults
is a symlink belonging to mysql. You can unlink it:
  brew unlink mysql

To force the link and overwrite all conflicting files:
  brew link --overwrite mysql-connector-c

To list all files that would be deleted:
  brew link --overwrite --dry-run mysql-connector-c
```

Force the link

```
$ brew link --overwrite mysql-connector-c
Linking /usr/local/Cellar/mysql-connector-c/6.1.11... 73 symlinks created
```

Install `mariadb-connector-c`

```
$ brew install mariadb-connector-c
Warning: mariadb-connector-c 3.0.3 is already installed, it's just not linked
You can use `brew link mariadb-connector-c` to link this version.
````

Link `mariadb-connector-c`

```
$ brew link mariadb-connector-c
Linking /usr/local/Cellar/mariadb-connector-c/3.0.3... 3 symlinks created
```
