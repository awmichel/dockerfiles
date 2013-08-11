# gitlab-ci-runner
from        ubuntu:13.04
maintainer  amichel "adam@amichel.me"

# apt-get deps
run         apt-get update -y
run         apt-get install -y -q sudo
run         apt-get install -y -q wget
run         apt-get install -y -q git
run         apt-get install -y -q build-essential
run         apt-get install -y -q libicu-dev

# install rbenv and Ruby 2.0.0-p247
run         git clone https://github.com/sstephenson/rbenv.git ~/.rbenv
run         git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
run         echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.profile
run         echo 'eval "$(rbenv init -)"' >> ~/.profile
run         exec $SHELL -l
run         rbenv install 2.0.0-p247
run         rbenv global 2.0.0-p247
run         gem install bundler

## install gitlab-ci-runner into /gcr
run         git clone https://github.com/gitlabhq/gitlab-ci-runner.git ~/gitlab-ci-runner
run         cd ~/gitlab-ci-runner && bundle install

# setup ssh
## sub-optimal... it seems that ssh-keygen doesn't honor $HOME
## mkdir for .ssh keys in the base director
run         mkdir /.ssh
## modify ssh config to use the appropriate key
run         echo "\nIdentityFile /.ssh/id_rsa" >> /etc/ssh/ssh_config

## the default command to be run when this docker image is started
cmd         /gcr/bin/runner
