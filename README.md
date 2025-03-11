# Raspberry Pi Pico Deployment Demo
Example of continuous delivery/deployment for the Raspberry Pi Pico (RP2040).

## Build Project with Docker Locally
You can run the Docker image locally to produce a .uf2 file, which can then be copied directly to your Pico board. Make sure you have Docker Desktop installed and run the following from this directory:
```
docker build -t pico-builder-image .
docker create --name pico-builder-container pico-builder-image
docker cp pico-builder-container:/project/src/build/blink.uf2 ./blink.uf2
```

Note that the binary is named based on the project name set in src/CMakeLists.txt: project(blink C CXX ASM). If you change blink in that line to something else (e.g. app), then you will need to update the final line above to copy out the newly named binary (e.g. app.uf2).

To remove the container and image when you're done, run the following:

```
docker rm pico-builder-container
docker rmi pico-builder-image
```