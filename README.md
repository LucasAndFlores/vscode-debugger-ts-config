# How to configure your VSCode debugger for a typescript environment

This is a quick reminder for me on how to configure my debugger for my projects. But this can help you too.
I already spent some huge time trying to configure vscode debugger and the debugger helps you to develop fast and understand better the problem that you have it.

The thing is: With Node js and Javascript was easier, we don't need to compile the code and map so many things. But things got a little bit complicated when we tried to do using Typescript. Since we need to compile from Typescript to Javascript, and we want to know the exact part where our Typescript code is not working (not the compiled one), we need the debugger.

We have some tricks and I'll try to explain.

First things first: For the dev environment, now, I'm liking more to use `ts-node` and `nodemon`. So, for every project that I start and I'll configure a dev environment (with hot reload, for example), I choose these two. Because we can easily integrate ts-node with nodemon and nodemon gives you the option to pass the flag `--inspect` to the node process. Without this, the node interpreter could have some issues connecting. So, make sure that you are using these two for dev environment and you can find an example of `nodemon.json` file to connect the debugger.

After these two, you probably will find two scenarios: local development or using a container (my preferred one).

## Docker env

In case you are using a container, you need to pay attention to some details. You will find a file called `launch.json` that is configured for this type of environment. You need to take a look and understand some fields.

The field `remoteRoot` refers to the docker environment and the common `WORKDIR`that we use to configure. Make sure that you are pointing to `/src` directory correctly.

The field `localRoot` will map the files in your local directory, not the docker one. Also, make sure that you are correctly pointing to `/src`.

The last one is `sourceMaps`, which enables you to map your files. Make sure that you activated this on the `launch.json` but also in your `tscofing.json`.

After this, also, do not forget to open port `9229` inside your container.

## Local environment

For this one, you only need to copy the file `launch.local.json` and enable the `sourceMap` configuration in your `tsconfig.json`.

### Contributions

If you know some solutions to other libraries for the dev environment, such as `ts-node-dev` or any other, feel free to open a PR and contribute. Let's share the usage of the debugger
