# Production

### Things Out Watch Out For
* Bind Mounts shouldnt' be used in Production
* Containerized apps might need a build step (i.e. React apps)
* Multi-Container projetcs might need to be split (or should be split) across multiple hosts/remote machines
* Trade-offs between control and responsibility might be worth it

### Hosting

AWS EC2 is a service that allows you to spin up and manage your own remote machines

1. Create and launch EC2 instance, VPC (virtual public cloud) and security group
2. Configure security group to expose all required ports to WWW
3. Connect to instance (SSH), install Docker and run container

### Bind Mounts, Volumes & COPY

Development | Production
--- | ---
Containers should encapsulate the runtime environment but not necessarily the code | A container should really work standalone, you should NOT have source code on your remote machine
Use Bind Mounts to provide your local host project files to the running container | Use COPY to copy a code snapshot into the image
Allows for instant updates without restarting the container | Ensures that every images runs without any extra surrounding configuration or code

### Deploy Source Code vs Image

Source Code | Built Image
--- | ---
Build image on remote machine | Build image before deployment (i.e. on local machine)
Push source code to remote machine, run docker build then docker run | Just execute docker run
**Unnecessary complexity** | **Avoid unnecessary remote sever work**

### Managed vs Automated

Your Own Remote Machine | Managed Remote Machine
--- | ---
AWS EC2 | AWS ECS
You need to create them, manage them, keep them updated, monitor them, scale them, etc. | Creation, management, updating is handled automatically, monitoring and scaling is simplified
*Great if you're an experienced admin/cloud expert* | *Great if you simply want to deploy your app/containers*
