# Vagrant + Docker + Ansible = Datacenter in a box

I wanted an efficient way to emulate my companies production infrastructure locally. It's composed on many applications across many servers in a datacenter. Vagrant allows me to boot up multiple servers but after a couple of servers, I quickly began to run out of system resource on my machine. I needed something that was more light weight.

Vagrant has recently added support for Docker. I first started off with the Vagrant Docker provider but ran into a number issues (mostly around hanging for 5mins or more when has_ssh is defined and other networking issues). I ended up settling on this configuration you see here. I make use of the Vagrant Docker provisioner to handle running the docker containers at the provisioning step. Using this setup I treat each docker container as an individual server. Now I can run a small cluster of servers that looks like the companies production environment on my laptop.

Why are you SSHing into docker containers? Why not do it the docker way and push those to production?

I don't use docker containers in production yet. I'm pretty sure I will eventually, but for now I'm much more interested in locally being able to iterate on the companies Ansible playbooks, be able to verify they work before pushing them to production, and be able to recreate the companies infrastructure on my machine on a laptop with finite resources. Plus I have been looking for a good reason to try out docker.
