# Royal Stay — Hotel Website UI

Responsive hotel landing page for Docker, Amazon ECR and Amazon ECS practice.

## Files

```text
royal-stay-hotel/
├── index.html
├── Dockerfile
├── README.md
├── .dockerignore
└── static/
    ├── style.css
    └── script.js
```

## Build and run

```bash
docker build -t royal-stay-hotel .
docker run -d --name royal-stay -p 8080:80 royal-stay-hotel
```

Open `http://localhost:8080`. Remove the test container with `docker rm -f royal-stay`.

## Push to GitHub

Create an empty GitHub repository and run these commands in this folder:

```bash
git init
git add .
git commit -m "Add Royal Stay hotel website"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
git push -u origin main
```

## Clone on EC2

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
cd YOUR_REPOSITORY
docker build -t royal-stay-hotel .
docker run -d --name royal-stay -p 8080:80 royal-stay-hotel
```

Allow TCP 8080 in the EC2 security group for your test and browse to `http://EC2_PUBLIC_IP:8080`.

## Push to Amazon ECR

Replace the placeholders with your AWS account ID and region. Your AWS CLI identity needs ECR permissions.

```bash
aws ecr create-repository --repository-name royal-stay-hotel --region YOUR_REGION
aws ecr get-login-password --region YOUR_REGION | docker login --username AWS --password-stdin YOUR_ACCOUNT_ID.dkr.ecr.YOUR_REGION.amazonaws.com
docker tag royal-stay-hotel:latest YOUR_ACCOUNT_ID.dkr.ecr.YOUR_REGION.amazonaws.com/royal-stay-hotel:latest
docker push YOUR_ACCOUNT_ID.dkr.ecr.YOUR_REGION.amazonaws.com/royal-stay-hotel:latest
```

## Deploy to ECS

Create an ECS cluster and a Fargate task definition using the ECR image URI above. Set container port to **80**, then create a service. Configure task networking and its security group to allow HTTP traffic from your test client, or use an Application Load Balancer. Ensure the ECS task execution role can pull from ECR and write logs.

## Included UI features

- Responsive hotel home page, navigation and room cards
- Check-in/check-out date validation and guest selector
- Demo booking modal with name and email fields
- Nginx container serving static HTML/CSS/JavaScript

**Important:** This is a front-end practice project only. It has no backend, database, real room inventory, payment processing or real reservation handling. Room prices and contact details are sample values. Room photos and fonts load from external services, so a browser internet connection is needed for them. Remove unused AWS resources after practice to avoid charges.
