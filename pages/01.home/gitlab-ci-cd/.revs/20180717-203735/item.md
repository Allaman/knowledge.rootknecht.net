---
title: 'Gitlab CI-CD'
taxonomy:
    category:
        - DevOps
        - CI/CD
    author:
        - Knecht
---

## Install gitlab-runner

```bash
docker run -d --name gitlab-runner --restart always \
  -v /srv/gitlab-runner/config:/etc/gitlab-runner \
  -v /var/run/docker.sock:/var/run/docker.sock \
  gitlab/gitlab-runner:latest
```
More install options are [available](https://docs.gitlab.com/runner/install/)

## Register gitlab-runner

Run in your runner host (here in the docker container)
```
sudo gitlab-runner register
```
- Get your token from `/admin/runners` of your Gitlab instance
- Set your [executioner](https://docs.gitlab.com/runner/executors/README.html) (here docker)
- No tags, allow untagged jobs, no shared runner (without those settings the runner stuck)

## Basic maven build
add and push `.gitlab-ci.yml` in your project root
```yml
image: maven:latest

verify:
  stage: build
  script:
    - mvn verify

build:
  stage: build
  script:
    - mvn compile
```

## Gitlab Pages

Recommended: wildcard domain and corresponding SSL certificate

1. Assign a runner to a group of projects in Gitlab [runner](https://docs.gitlab.com/ee/ci/runners/)
2. Start runner `docker run -d --name gitlab-runner-public --restart always   -v /srv/gitlab-runner/config:/etc/gitlab-runner   -v /var/run/docker.sock:/var/run/docker.sock   gitlab/gitlab-runner:latest`
3. [Register runner](https://docs.gitlab.com/runner/register/index.html) 
	1. docker exec -it gitlab-runner-public bash
		- gitlab-runner register
		- docker as default executioner
		- alpine as default image (depends on your tools to build pages e.g. Jekyll)
	1. non interactive register
		```bash
        docker run --rm -t -i -v /path/to/config:/etc/gitlab-runner --name gitlab-runner gitlab/gitlab-runner register \
  							--non-interactive \
							--executor "docker" \
                          	--docker-image alpine:3 \
                          	--url "https://gitlab.com/" \
                          	--registration-token "PROJECT_REGISTRATION_TOKEN" \
                          	--description "docker-runner" \
                          	--tag-list "docker,aws" \
                          	--run-untagged \
                          	--locked="false"
  ```
4. Setup [Pages](https://gitlab.com/pages) (wildcard domain with TLS support)
	gitlab.rb
    ```ruby
            pages_external_url "https://pages.rootknecht.net/"
            gitlab_pages['enable'] = true
            gitlab_pages['inplace_chroot'] = true # in case of gitlab-pages daemon not starting due to bind mount permission error
            pages_nginx['redirect_http_to_https'] = true
            pages_nginx['ssl_certificate'] = "/etc/gitlab/ssl/pages-nginx.crt"
            pages_nginx['ssl_certificate_key'] = "/etc/gitlab/ssl/pages-nginx.key"
    ```
	Reconfigure and restart
    ```bash
        gitlab-ctl reconfigure
        gitlab-ctl restart gitlab-pages
    ```
    Debugging
    ```bash
    	# get logs (run in container)
		gitlab-ctl tail gitlab-pages
        # path of your pages (in container)
        ls /var/opt/gitlab/gitlab-rails/shared/pages
        # error log of bundled nginx
        /var/log/gitlab/nginx/gitlab_pages_error.log
	```