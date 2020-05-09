### FIX RUNNERS IF YOU MESSED UP /etc/gitlab/gitlab-secrets.json
inside gitlab container
```
gitlab-rails c
```
```
settings = ApplicationSetting.last
settings.update_column(:runners_registration_token_encrypted, nil)
Ci::Runner.all.update_all(token_encrypted: nil)
exit
```
```
gitlab-rails dbconsole
```
```
UPDATE projects SET runners_token = null, runners_token_encrypted = null;
UPDATE namespaces SET runners_token = null, runners_token_encrypted = null;
UPDATE application_settings SET runners_registration_token_encrypted = null;
UPDATE ci_builds SET token_encrypted = NULL;
\q
```

for debuggering...
```
#docker exec -it runner-docker /usr/bin/gitlab-runner  register  --non-interactive  --executor "docker"  --docker-image alpine:latest  --docker-privileged="False"  --run-untagged="true"  --tag-list "default"  --locked="false"  --url "https://server.name.tld"  --registration-token TOKEN  --description "runner-docker"
```