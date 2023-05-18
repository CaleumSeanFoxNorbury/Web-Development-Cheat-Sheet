# Gitlabs / Gitaly Configuration 

## Configure Gitaly for Linux

-	Install Gitlabs. 
-	Install Gitaly.
-	Configure authentication.
  o	 Gitaly and Gitlab use two aspects of authentication secrets, a Gitaly token and a Gitlab shell token. Configure Gitaly token  by editing file `/etc/gitlab/gitlab.rb`.
```
   # Gitaly Token
  	 	gitaly['configuration'] = {
      			# ...
      		auth: {
        		# ...
        		token: 'abc123secret',
      		},
   	}

```
and configure Gitlab secret token by coping file `/etc/gitlab/gitlab-secrets.json` to the same path on Gitaly servers and any other client.
-	Configure Gitaly servers. 
o	Edit `/etc/gitlab/gitlab.rb`:
```
# Avoid running unnecessary services on the Gitaly server
postgresql['enable'] = false
redis['enable'] = false
nginx['enable'] = false
puma['enable'] = false
sidekiq['enable'] = false
gitlab_workhorse['enable'] = false
grafana['enable'] = false
gitlab_exporter['enable'] = false
gitlab_kas['enable'] = false

# If you run a separate monitoring node you can disable these services
prometheus['enable'] = false
alertmanager['enable'] = false

# If you don't run a separate monitoring node you can
# enable Prometheus access & disable these extra services.
# This makes Prometheus listen on all interfaces. You must use firewalls to restrict access to this address/port.
# prometheus['listen_address'] = '0.0.0.0:9090'
# prometheus['monitor_kubernetes'] = false

# If you don't want to run monitoring services uncomment the following (not recommended)
# node_exporter['enable'] = false

# Prevent database connections during 'gitlab-ctl reconfigure'
gitlab_rails['auto_migrate'] = false

# Configure the gitlab-shell API callback URL. Without this, `git push` will
# fail. This can be your 'front door' GitLab URL or an internal load
# balancer.
# Don't forget to copy `/etc/gitlab/gitlab-secrets.json` from Gitaly client to Gitaly server.
gitlab_rails['internal_api_url'] = 'https://gitlab.example.com'

gitaly['configuration'] = {
   # ...
   #
   # Make Gitaly accept connections on all network interfaces. You must use
   # firewalls to restrict access to this address/port.
   # Comment out following line if you only want to support TLS connections
   listen_addr: '0.0.0.0:8075',
   auth: {
     # ...
     #
     # Authentication token to ensure only authorized servers can communicate with
     # Gitaly server
     token: 'AUTH_TOKEN',
   },
}
```

o	Append to the above document the following for each server Gitaly will be using/stored on: 
First server:
```
gitaly['configuration'] = {
   # ...
   storage: [
      {
         name: 'default',
         path: '/var/opt/gitlab/git-data',
      },
      {
         name: 'storage1',
         path: '/mnt/gitlab/git-data',
      },
   ],
}
```
Every server after:
```
gitaly['configuration'] = {
   # ...
   storage: [
      {
         name: 'storage2',
         path: '/srv/gitlab/git-data',
      },
   ],
}

```
o	Save file and reconfigure Gitlab. Lastly, confirm that Gitaly can perform call-backs to gitlabs API by running ` sudo /opt/gitlab/embedded/bin/gitaly check /var/opt/gitlab/gitaly/config.toml`.
-	Configure Gitaly clients.
o	Tell Gitaly to use the servers we have just configured, this can be done by adding Gitaly addresses to GitLab’s main config file. Edit ` /etc/gitlab/gitlab.rb`:
```
	# use different tokens per server!
git_data_dirs({
  'default'  => { 'gitaly_address' => 'tcp://gitaly1.internal:8075', 'gitaly_token' => '<AUTH_TOKEN_1>' },
  'storage1' => { 'gitaly_address' => 'tcp://gitaly1.internal:8075', 'gitaly_token' => '<AUTH_TOKEN_1>' },
  'storage2' => { 'gitaly_address' => 'tcp://gitaly2.internal:8075', 'gitaly_token' => '<AUTH_TOKEN_2>' },
})
```
o	Save and reconfigure gitlabs, run ` sudo gitlab-rake gitlab:gitaly:check` to make sure we can connect to Gitaly servers, the watch the logs! 
	    ` sudo gitlab-ctl tail gitaly`

## References 

-	(Gitaly)https://docs.gitlab.com/ee/administration/gitaly/configure_gitaly.html [2023]




