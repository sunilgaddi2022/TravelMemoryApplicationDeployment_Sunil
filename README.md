# TravelMemoryApplicationDeployment_Sunil

The above assignment was completed by me in the class itself,
Below are the Instances name,
sunil-tm-be
sunil-tm-fe


Below are the steps:
1. Backend Configuration:
Clone the repository and navigate to the backend directory:

git clone https://github.com/UnpredictablePrashant/TravelMemory
cd TravelMemory/backend

Set up a reverse proxy using nginx:
Install nginx and create a configuration file for your backend. Replace your_backend_domain with your domain and update the port if necessary.

sudo apt-get update
sudo apt-get install nginx
sudo nano /etc/nginx/sites-available/your_backend_domain


Add the following configuration:

server {
    listen 80;

    server_name your_backend_domain;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}

sudo ln -s /etc/nginx/sites-available/your_backend_domain /etc/nginx/sites-enabled
sudo nginx -t
sudo systemctl restart nginx


Update the .env file:
Navigate to the backend directory and update the .env file with your database connection details and port information.

nano .env


2. Frontend and Backend Connection:
Update urls.js in the frontend directory:
Navigate to the frontend directory and update urls.js with the backend URL.

cd ../frontend
nano src/utils/urls.js

Replace the backendURL with your backend URL.

3. Scaling the Application:
Create multiple instances and set up load balancing:
Launch multiple EC2 instances for both frontend and backend.
Set up Node.js on each instance.
Deploy the TravelMemory application on each instance.
Use a load balancer (e.g., AWS Elastic Load Balancer) to distribute traffic.


4. Domain Setup with Cloudflare:
Connect custom domain to the application:
Sign up for Cloudflare and add your domain.
Update your domain's nameservers to Cloudflare's nameservers.
Create a CNAME record pointing to the load balancer endpoint.
Set up an A record with the IP address of the EC2 instance hosting the frontend.



