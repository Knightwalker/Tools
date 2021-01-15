# I. Github Deployments Tool
There is no UI for this yet, but you can do it using the GitHub API.<br>
Documentation: https://docs.github.com/en/free-pro-team@latest/rest/reference/repos#deployments<br>

## I.1. Delete a deployment
1. Go to your GitHub account settings, then developer settings, then personal access tokens. Create a new token that has repo_deployments allowed. After it's generated, save the hexadecimal token, you'll need it for the upcoming API requests.<br>

2. First, list all the deployments on your repo:<br>
`curl https://api.github.com/repos/${username}/${repo}/deployments`<br>

   Each deployment has an id integer. Note it, and replace ${deployment_id} in the upcoming code blocks with that ID. Or create another shell variable for it.<br>

3. Now you have to create an "inactive" status for that deployment:<br>
`curl https://api.github.com/repos/${username}/${repo}/deployments/${deployment_id}/statuses -X POST -d '{"state":"inactive"}' -H 'accept: application/vnd.github.ant-man-preview+json' -H "authorization: token ${personal_access_token}"`

4. Delete deployment<br>
`curl https://api.github.com/repos/${username}/${repo}/deployments/${deployment_id} -X DELETE -H "authorization: token ${personal_access_token}"`