## Gitea redirection bug

When Gitea is hosted with a subUrl (e.g., studio.localhost/repos), there seems to be a problem with redirection. 

If you provide the redirect parameter as “/”, Gitea should redirect to the root (“/”). However, it currently redirects to “/repos”, which is a gitea home page. Similarly, if you pass any other parameter (e.g., “/redirected”) as the redirect_to parameter, Gitea redirects to the Gitea homepage rather than the specified page.
The same issue exists with the OIDC (OpenID Connect) flow.


## Steps to Reproduce
1. Add the following line to your `/etc/hosts` file:
```text
127.0.0.1 studio.localhost
```
2. Run the following command to start the Docker containers:
```sh
docker-compose up -d
```
3. Create an admin user using the following command:
```sh
docker exec gitea gitea admin user create --username adminUser --password test1234$ --email admin@localhost --admin
```
4. Open the link [http://studio.localhost](http:/studio.localhost) in your browser.
5. Click the "Login with Redirect" button.
6. Enter the credentials for the `adminUser` account (username: `adminUser`, password: `test1234$`).
7. Observe that redirection occurs to the Gitea home page.

## Notes
If redirection is successful, the page with the content "Redirected after Gitea login" should be displayed.
To verify the expected redirection behavior, use `1.21.10-rootless` image in `compose.yaml` file. The bug is introduced after version 1.21.10