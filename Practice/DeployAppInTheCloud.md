### TASK
- Install Docker on EC2 Create a simple FastAPI or Flask app locally 
- Create a Dockerfile Build + run locally Push code to EC2 and run: docker build -t myapp . docker run -d -p 80:8000 myapp 
- You should now see your app at: http://<EC2-public-ip>

### How to do this

You already have an Ubuntu server running, to deploy an app you can run Docker over that server.

- Step 1 Install docker on EC2

In EC2 terminal (In SSH window):

#Update package list
sudo apt-get update

#Install Docker
sudo apt-get install -y docker.io

#Start Docker service
sudo systemctl start docker

#Enable Docker to start on reboot
sudo systemctl enable docker

#Check Docker is running
sudo docker ps

- STEP 2 Create a simple FastAPI app on EC2

Still on the EC2 machine: Create a fastAPI app

mkdir fastapi-app
cd fastapi-app

Create the app file:
nano main.py

from fastapi import FastAPI
app = FastAPI()
@app.get("/")
def read_root():
    return {"message": "Hello from FastAPI on EC2 with Docker!"}

Save & exit in nano:
Ctrl + O, Enter
Ctrl + X

Now create requirements.txt:
nano requirements.txt

fastapi
uvicorn[standard]

Save & exit again.

- Step 3 Create the dockerfile
Still in fastapi-app/:
nano Dockerfile

Write this
#Use official Python image
FROM python:3.11-slim

#Set work directory inside the container
WORKDIR /app

#Copy dependency file
COPY requirements.txt .

#Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

#Copy app code
COPY . .

#Expose the port FastAPI will run on
EXPOSE 8000

#Command to run the app
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]

Save & exit.

- Step 4 Build the docker image (on EC2)

From inside fastapi-app/:
sudo docker build -t myapp .

This may take a minute the first time (downloads Python image, installs packages).
When it finishes, run:
sudo docker images

You should see myapp listed.

- Step 5 Run the container and map it to port 80
Now run your app in the background and expose it to the world:
sudo docker run -d -p 80:8000 --name myapp-container myapp

Explanation:
-> Inside container → app listens on 8000
-> EC2 instance → listens on 80
-> -p 80:8000 maps EC2:80 → container:8000

Check it’s running:
sudo docker ps

You should see myapp-container with 0.0.0.0:80->8000/tcp.

- Step 6 Test in browser

On your laptop:
Go to the AWS EC2 Console → copy the Public IPv4 address
In your browser, visit: http://<your-ec2-public-ip>

Example: http://3.XXX.XXX.XX

You should see JSON: {"message":"Hello from FastAPI on EC2 with Docker!"}

That means:
EC2 is working
Docker is working
FastAPI is running in a container
Port mapping & security groups are correct

- How to stop/remove the container when done
#stop the container
sudo docker stop myapp-container

#remove the contiainer
sudo docker rm myapp-container