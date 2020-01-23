FROM ubuntu:16.04

#installation des dependances
RUN apt-get update -y && apt-get upgrade -y && \
	apt-get install curl openssh-server ca-certificates git tzdata -y && \
	curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | bash && \
	apt-get install -y gitlab-ce

RUN echo "external_url 'https://10.11.10.11'" >> /etc/gitlab/gitlab.rb && \
	echo "nginx['redirect_http_to_https'] = true" >> /etc/gitlab/gitlab.rb && \ 
	echo "(/opt/gitlab/embedded/bin/runsvdir-start &) && service ssh start && gitlab-ctl reconfigure" >> script.sh && \
	echo "bash" >> script.sh
EXPOSE 22 443 80
ENTRYPOINT ["sh", "script.sh"] 
#gcl https://10.11.6.12:8443/root/b3wida.git  https
#gcl ssh://git@10.11.6.12:8022/root/b3wida.git ssh
## 
