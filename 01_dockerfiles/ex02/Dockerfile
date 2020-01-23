FROM ruby

#installation du gestionnaire de version ruby.
RUN apt update -y && apt upgrade -y && \
	apt install curl git nodejs gcc make libssl-dev libreadline-dev zlib1g-dev libsqlite3-dev -y && \
	git clone https://github.com/rbenv/rbenv.git ~/.rbenv && \
	echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc && \
	echo 'eval "$(rbenv init -)"' >> ~/.bashrc
SHELL ["/bin/bash", "-l", "-c"]
RUN mkdir -p "$(rbenv root)"/plugins && \
	git clone https://github.com/rbenv/ruby-build.git "$(rbenv root)"/plugins/ruby-build

ONBUILD SHELL ["/bin/bash", "-l", "-c"]
ONBUILD COPY app /opt/app
ONBUILD WORKDIR /opt/app
ONBUILD RUN rm Gemfile.lock
ONBUILD RUN bundle platform --ruby | sed "s/^ruby //" > .ruby-version && \
			rbenv install $(cat .ruby-version) && \
			rbenv global $(cat .ruby-version) && \
			gem install bundler && \
			rbenv rehash

ONBUILD RUN	bundle install && \
			rake db:migrate && \
			rake db:seed
ONBUILD ENTRYPOINT ["bundle", "exec"]
