# ses-react-deploy-instructions

Instructions on how to deploy a react app:


React provides this [link](https://cra.link/deployment) that leads you to a lot of resources
- Highly recommend using [github pages](https://create-react-app.dev/docs/deployment/#github-pages). See github-pages section below
- Using AWS. Recommended especially if you already have an account. See instructions [here](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html).
Add this Bucket policy below. Make sure you're only uploading files that you want to make public to your bucket. **Also replace `<YOUR_BUCKET_NAME>` with the name of your bucket.**
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::<YOUR_BUCKET_NAME>/*"
            ]
        }
    ]
}
```
- Heroku is another common way of deploying. I think it's a little more complicated. Here's how you should go about it
    - Get an [Heroku Account](https://github.com/mars/create-react-app-buildpack#user-content-requires) account and install the cli
    - Go into your react project and at the root of your project, run below. Make sure to rename `$APP_NAME` to your project folder name

        ```heroku create $APP_NAME --buildpack mars/create-react-app```
    - If the "homepage" key exists in your package.json, delete that whole line.
    - This assumes you already have your code on github.
    - Run this to have heroku as a remote repository `heroku git:remote -a $APP_NAME`
    - Once you've made all your changes, run `git add .` and `git commit -m "describe changes you made here"`
    - Push it to heroku `git push heroku main`
    - You can also follow this [tutorial](https://www.geeksforgeeks.org/how-to-deploy-react-app-to-heroku/).


## github-pages
Things to Note
- Make sure to change the "deploy" script to this in your package.json `"deploy": "gh-pages -b gh-pages -d build",`.  Any changes made will be deployed if you run `npm run deploy` just give it a minute or so for the changes to take effect.
- Note gh-pages won't work well with react-router using `browserHistory`.