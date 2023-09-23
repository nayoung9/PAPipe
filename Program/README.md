# Markdown for running PAPipe (Program directory)

**Programs/**

- contains programs required to run PAPipe
- In this directory, PAPipe has been configured to automatically set up and incorporate programs that would otherwise pose difficulties for users due to legacy or environment-related requirements, making them easily accessible and usable.
- Do not change the name or the path of this directory.

### Prepare running PAPipe in two ways

### Local

- You can prepare all the requirements via set_local_env.sh
    
    ```
    # in current directory
    bash build_Docker_image.sh
    ```
    

### Docker

- You can run PAPipe on docker without having to prepare all the requirements (*recommended!*)
    
    ```
    # in current directory
    bash build_Docker_image.sh
    ```