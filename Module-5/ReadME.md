# Explanation of TASK

When I build single build then the size of image had become almost 1 GB
with unnecessary codes. but we just need the compiled binary file to run and get the out put. 
so then when we use multi stage build . we coppied the compiled build version of application 
generated binary file into new work directory then just set the entry point of the application.
when container will run our application will start running from there. And when we used multi stage build then the images size came to 14.8 mb only!

# Build image

```
sudo docker build -t go-app .
```

# RUN
```
sudo docker run -p 8080:8080 go-app
```