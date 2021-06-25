# Docker Terraform
Containerised Terraform CLI with Pythyon3, GCP, AWS sdks and GOSU installed.

## Usage
The below example are using the `terraform` user inside the container.
This is explained below in [Configuration](#configuration).

### Docker
Run as a command:

```bash
docker run --rm -v ~/.aws:/home/terraform/.aws -v $(pwd):/opt/terraform sivakumarvunnam/terraform --version
```

