# Docker Terraform
Containerised Terraform CLI with Pythyon3, GCP, AWS sdks and GOSU installed.

## Usage
The example using the `terraform` user inside the container.
This is explained below in [Configuration](#configuration).

### Docker
Run as a command:

```bash
docker run --rm -v ~/.aws:/home/terraform/.aws -v $(pwd):/opt/terraform sivakumarvunnam/terraform:0.15.5 --version
```

### Bash
Can also set as a bash function and placed in your `~/.bashrc` or equivalent
for quick access, with correct mounting points:

```bash
function terraform() {
  docker run --rm -it -v ~/.aws:/home/terraform/.aws -v $(pwd):/opt/terraform sivakumarvunnam/terraform:0.15.5 "$@";
}
```

Then run `terraform {params} {action}` just like you are using your local
`terraform` executable.

## Configuration
There are some custom configurations that can be applied to prevent the
container from running as root and owning all your files.
[gosu](https://github.com/tianon/gosu) is utilised to set the UID and GID of
the custom user inside the container to whatever `/opt/terraform` is mounted as from
the host.

### Environment Variables
Here are some quick `optional` environment variables to get you started:

- `TERRAFORM_UID` - Custom UID to run terraform process as. Default will try to determine from host mount permissions (i.e. your user ID).
- `TERRAFORM_GID` - Custom GID to run terraform process as. Default will try to determine from host mount permissions (i.e. your group ID).
- `TERRAFORM_USER` - Custom user name to run terraform process as. Defaults to `terraform`
- `TERRAFORM_GROUP` - Custom group name to run terraform process as. Defaults to `terraform`

Remember that these variables are completely optional and that the `entrypoint.sh`
will do its best to determine UID and GID of the user that invokes the container
from the host machine by whatever the mount point is.

## Build
Update the `TERRAFORM_VERSION` in both `Makefile` and `DockerFile`. Then run:

```
make build
```

