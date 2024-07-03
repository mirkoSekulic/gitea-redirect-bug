## Gitea redirection bug

When Gitea is hosted with a subUrl (e.g., studio.localhost/repos), there seems to be a problem with redirection. 

If you provide the redirect parameter as “/”, Gitea should redirect to the root (“/”). However, it currently redirects to “/repos”, which is a gitea home page. Similarly, if you pass any other parameter (e.g., “/redirected”) as the redirect_to parameter, Gitea redirects to the Gitea homepage rather than the specified page.
The same issue exists with the OIDC (OpenID Connect) flow.


## Steps to reproduce
1. add `127.0.0.1   studio.localhost` line in /etc/hosts file
2. run  
3. run docker exec gitea gitea admin user create --username adminUser --password test1234$ --email admin@localhost --admin
4. open http://studio.localhost linke in browser
5. click login with redirect button
6. type adminUser and test1234$ as credentials
7. If redirection is ok page with `Redirected after gitea login` content should be shown, which doesn't happen with 1.22.0 version

## Notes 

To check the expected redirection behaviour use the 1.21.10-rootless image in the compose.yaml file.