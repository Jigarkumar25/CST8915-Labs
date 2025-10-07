# Lab 4 (CST8915) <br> pate1595

### Youtube Video link: <br>

https://youtu.be/7cEQzn7wabo

---

### Reflection Questions:

1) What are the main differences between a Docker image and a Docker container?<br>
→ An image is a read-only blueprint; a container is a running instance of that image with its own writable layer.

2) Explain how Docker's layered architecture improves efficiency.<br>
→ Layers let Docker reuse unchanged parts when rebuilding or sharing images, saving time and space.

3) Why does each container get its own writable layer?<br>
→ It isolates changes so one container’s edits don’t affect others or the base image.

4) What are the benefits of using Docker Compose over running containers individually?<br>
→ Compose manages multiple containers with one YAML file—handling networks, volumes, scaling, and startup order automatically.