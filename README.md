# pyro-template
Example of using a base docker container on DockerHub to work in Jupyter with Python or R.
- Uses `vanilla` pyro container from [zachbogart/pyro](https://github.com/zachbogart/pyro)
- Containers available on [DockerHub](https://hub.docker.com/r/zachbogart/pyro)

## Workflow (TL;DR)
``` 
    # build pyro container
    docker build --force-rm . -t pyro_template:latest
    
    # run project
    docker run -p 8899:8888 -v $PWD:/project pyro_template:latest
    
    # get codin'
    http://localhost:8899/
```

***

# Use this repo as a template 
- If you want to get started with your own thing, just make a new repo using this one as a template (the big "Use this template" button will get you going).
- If you want more explanation about the setup, see the walkthrough below.

### Notes
- For the template peeps, you should: 
    - update the workflow section above with your new docker tag

# Give pyro a try! (Walkthrough)
- This setup uses a base docker container that has Python and R wrapped in with Jupyter. Work in jupyter notebooks with your favorite language!
- **Note**: Docker builds will use ~1-2 GB disk space

## 01 Build Project
1. First, clone this repo. `cd` inside to the project's root directory.

2. Execute this at the project's root directory:
```
    docker build --force-rm . -t pyro_example:latest
```
- It will go get the base container from DockerHub and build it for you (won't take long).
- Using `<PROJECT_NAME>:latest` as an example image naming convention.

## 02 Run Project
1. Execute this at the project's root directory:
```
    docker run -p 8899:8888 -v $PWD:/project pyro_example:latest
```
- This command will run this project using its [Dockerfile](Dockerfile), which uses a command to start a jupyter notebook.

## 03 Accessing Jupyter Environment 
1. After executing the above command, there will be some links in the output, which will include a long token string (`token=<LONG_STRING>`). Copy the token string.
2. Navigate to `http://localhost:8899` in your browser. You should see a prompt at the top for a "password or token". Paste the token string you copied above.
2. You should now be inside a jupyter environment. You can now execute code, running notebooks in Python or R! As an example, there are some notebooks working with the [palmerpenguins](https://github.com/allisonhorst/palmerpenguins) dataset.

### Notes
- Local host port (left of the colon) is set to `8899`. Can be changed if desired. Docker-level port (right of the colon) must be set to `8888` according to Dockerfile.
- Connects local instance of project as a volume to the docker image (`-v $PWD:/project`). Anything you do while in jupyter will update your local files.

## 04 Play!
- You are now running a jupyter notebook inside a docker image! Feel free to run the code or make your own notebooks. All work will be reproducible across different users (thanks docker) and since we defined a volume, your work will affect your local files rather than just being ephemeral. 
- This should help other people to go through your code, allowing them to execute it in the same environment you built it. Or it could just allow people to run your scripts without the hassle of installing a bunch of stuff.

### Extensions are your friend
- There are a bunch of nbextensions that the community has created and they are super useful. Check them out in the `Nbextensions` tab when running jupyter (when you open up jupyter you'll see `Files`, `Running`, `Clusters`, and then `Nbextensions`). Here are some good ones:
    - `Table of Contents (2)`: automatically creates ToC tools
    - `ScrollDown`: long outputs are automatically scrolled down as they execute
    - `Variable Inspector`: Get a table of variables created in the notebook
    - `Hinterland`: autocomplete as you type without hitting TAB
    - `spellchecker`: highlights misspelled words as you type a markdown cell
    - `Initialization cells`: Mark cells that can be run all at once with the push of a button or on startup
- You can manually enable these extensions every time you `docker run ...` or [enable them through commands](https://jupyter-contrib-nbextensions.readthedocs.io/en/latest/install.html#enabling-disabling-extensions) in the project Dockerfile once you have a set you prefer (see [`vanilla_swirl` Dockerfile](https://github.com/zachbogart/pyro/blob/main/vanilla_swirl/Dockerfile) for an example).
    - *Note: the nbextension tab is present because it is installed in the pyro container.*
    
## Troubleshooting
- The `docker image list` command in Terminal is helpful to see what containers/images you have installed. Or open up Docker Desktop.
- If you run into port conflicts, consider changing the host port (left of the colon in `docker run`)

***

Hope you enjoy coding with [pyro](https://github.com/zachbogart/pyro)!

![Homer Simpson Overwhelmed by Ice Cream](https://media.giphy.com/media/nxscd2YGVf6xi/giphy.gif)

Made with 💖
