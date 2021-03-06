Goal: Install everything needed for the workshop

We advise using the native command line tools for your OS.
> **_NOTE: Nordstrom Technology!_**
>
> If you are a _Nordstrom_ engineer, please ignore this step and instead see the page titled _`Serverless Workshop - Nordstrom Technology Setup`_ in **Confluence** and follow the instructions there.
Install the [AWS-CLI](http://docs.aws.amazon.com/cli/latest/userguide/installing.html) and use the `aws configure` command to setup your credentials.

Your credentials are located in the AWS Console under:

IAM --> users --> select your user ID --> security credentials tab


### Step 1: Creating an AWS account
Go to https://aws.amazon.com/console/ and click `Sign In to the Console` in the upper right hand corner. When the sign in page loads, enter your email and click `Sign in using our secure server`.

Enter your information on the next page and click `Create account`.

Next comes standard sign up information. fill out the following as you normally would:
    Contact info
    Payment info
    Indentity verification
    
When you reach support plan, select the basic plan if you are simply testing out serverless-artillery. All the plans have descriptions, so if you know you want something more, go for it. Otherwise, stick to basic. You should receive an email confirming your sign up. 


### Step 2: Setting up AWS user
Setting up credentials requires you create a user aside from the root account. In general, root credentials should be set aside and heavily protected, as anyone with these credentials has access and control over the entire AWS account. Scary things happen when someone has unlimited access to something you pay for..!

Generally, it's best to create a user with the least amount of permissions possible to do what you need to do. In this case, that's a bit complicated, so this documentation provides a lazy way and a best practice way to setup a user for this workshop. 

Either way, start by logging in to the console (https://aws.amazon.com/), search `IAM` into the search bar, and click on the result. Click Users -> Add user. Enter the username and give the user `Programmatic access`. On the next page, click `Attach existing policies directly`. This is where the lazy and best practice methods depart.

#### The Best Way
Due to it's somewhat extensive nature, the [Best Way](LEAST-PERMISSIONS-USER.md) is stored in a different file.

#### The Lazy Way
Check the box next to `AdministratorAccess`. Now, your user has access to all AWS services and resources. This is lazy (in a bad, irresponsible way, not in the cool programmer way) and dangerous, and if you have any security concerns this method should be avoided. 


### Step 3: Setting up AWS credentials
If you use any AWS profile other than the default, you'll need to provide that profile name to the environment via the `AWS_PROFILE` variable. For those who did things the Best Way, use the profile name associated with the credentials you just made that allow the user to assume the role you created.

#### OS X
```sh
export AWS_PROFILE=<your-profile>
```

#### Windows
```bat
set AWS_PROFILE=<your-profile>
```

#### Powershell
```
$env:AWS_PROFILE='nordstrom-federated'
```

### Step 4: install serverless node package on your machine.

Install the serverless.com deployment framework - this will make it easy to deploy serverless components to AWS.

#### OS X or Windows
```sh
npm install -g serverless@1.11.0
```

If you are on OS X and have used sudo to install libraries (and are thereby hitting permissions issues running the above, execute the following): 
`sudo chown -R $(whoami) $(npm config get prefix)/{lib/node_modules,bin,share}`
