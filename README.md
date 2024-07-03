## Gitea redirection bug

When gitea is hosted to url with subUrl, for example studio.localhost/repos, there is an problem with redirection.

Lets assume that desired redirection after log in is "/"

If we provide redirect parameter as "/" instead of redirecting to "/" gitea redirects to "/repos".
The same happens if any other parameter is provided, for example if "/redirected" is passed as redirect_to parameter, gitea redirects to gitea home page instead of "/redirected" page.



## Steps to reproduce
1. add `127.0.0.1   studio.localhost` line in /etc/hosts file
2. run  
3. run docker exec gitea gitea admin user create --username adminUser --password test1234$ --email admin@localhost --admin
4. open http://studio.localhost linke in browser
5. click login with redirect button
6. type adminUser and test1234$ as credentials
7. If redirection is ok page with `Redirected after gitea login` content should be shown

## Notes currently compose contains last version of gitea that doesn't contain a bug. For checking current behaviour change to version .21.10-rootless in the compose file.