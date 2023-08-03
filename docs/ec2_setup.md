# EC2 Setup

Generally I have one EC2 instance hosting all of my projects, but occasionally I need to upgrade, or test a migration to some new architecture and I always forget how I go about setting up these instances. This doc will hopefully keep track of that process to reduce this setup pain!

## Steps

1. Launch a new instance
    1. Image - Whatever the current recommended flavour of Amazon Linux is, should be fine
    1. Instance type - Should be fairly obvious depending on what you need
    1. Key Pair - `ec2_key_pair` if you want to re-use
    1. Security Group - `launch-wizard-12` if you want to re-use
1. (Optional) Create an Elastic IP Address
    1. Head to `Elastic IPs` under `Network & Security`, on the EC2 home page
    1. Click `Allocate Elastic IP Address`
    1. Keep all of the defaults and hit `Allocate`
    1. Click on `Actions`, and then `Associate Elastic IP Address` from the dropdown
    1. Pick your instance in the dropdown and click `Associate`
1. Either ssh on to the box, or connect via the AWS console, and do the following:
    1. Install Git. Run:
        1. `sudo yum install git`
    1. Install NVM. Run:
        1. `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash`
    1. Install Node. Run:
        1. `nvm install 16`
    1. Install PM2. Run:
        1. `npm install pm2 -g`
    1. Install and configure NGINX. Run:
        1. `sudo yum install nginx`
        1. `sudo systemctl enable nginx && sudo systemctl start nginx`
        1. (Optional, configure your server) `sudo nano /etc/nginx/nginx.conf`
1. (Optional) Configure Route53
    1. Head to the Route53 dashboard
    1. Go into `Hosted Zones`
    1. Go into the website you'd like to configure
    1. Click on your A Record
    1. Click `Edit Record` on the right panel
    1. Change the value to your new static IP Address
